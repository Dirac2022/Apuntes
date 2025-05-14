
## 📖 1. What is GitHub Actions?

- **GitHub Actions** is GitHub’s built‑in CI/CD platform.
- It lets you **automate** testing, building, and deploying your code **in response to repository events** (pushes, PRs, schedules, etc.).
- Workflows are defined in YAML files under `.github/workflows/`.

### Continuous Integration vs. Continuous Deployment

|Term|Purpose|
|---|---|
|CI|Automatically **build** and **test** code on every change.|
|CD|Automatically **deploy** or **release** after successful CI.|

---

## ⚙️ 2. Workflow Syntax Overview

Every workflow file is a YAML document with these top‑level keys:

```yaml
# .github/workflows/ci.yml
name: <human‑readable name>       # Optional: shown in Actions UI
on: <events>                      # What triggers this workflow
jobs:                             # One or more "jobs" to run
  <job_id>:
    runs-on: <runner>             # Which VM/environment to use
    steps:                        # Series of "steps" in this job
      - uses: <action>@<version>  # Call a prebuilt action
      - run: <shell command>      # Or run arbitrary shell
```

### `name`

- Descriptive title for the workflow (e.g. `CI`, `Build & Deploy`).

### `on`

Defines **triggering events**. Can be a single event or a map for fine control:

```yaml
on:
  push:
    branches: [ main, develop ]
    paths-ignore: [ 'docs/**' ]
  pull_request:
    types: [ opened, synchronize ]
  schedule:                       # Cron trigger
    - cron: '0 0 * * MON'         # Every Monday at 00:00 UTC
  workflow_dispatch:              # Manual trigger via UI
```

---

## 🏗️ 3. Jobs, Runs‑On & Steps

###  `jobs`

A workflow can have **multiple jobs** that run in parallel by default:

```yaml
jobs:
  lint:
    runs-on: ubuntu-latest
    steps: ...
  test:
    runs-on: ubuntu-latest
    needs: lint          # Wait for "lint" job to complete
    steps: ...
```

###  `runs-on`

Specifies the **virtual environment**:

- `ubuntu-latest`, `windows-latest`, `macos-latest`
- Self‑hosted runners (e.g. your own server)

###  `steps`

A **step** is one unit of work. Two main types:

1. **`uses:`** — calls an **Action** from the Marketplace or repository
2. **`run:`** — executes **shell commands**
    

Each step can have:

```yaml
- name: <label>              # Optional description
  uses: <owner>/<repo>@<tag> # Prebuilt action
  with:                      # Inputs for that action
    foo: bar
  env:                       # Environment vars for this step
    FOO: bar
```

or

```yaml
- name: Install deps
  run: |
    python -m pip install -U pip
    pip install -r requirements.txt
```

---

## 🧱 4. A Simple Python CI Example

```yaml
name: Python CI

on: [ push, pull_request ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4        # 1. Checkout code
      - name: Set up Python 3.11        # 2. Install Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      - name: Install dependencies      # 3. Install deps
        run: pip install -r requirements.txt
      - name: Run lint                  # 4. Lint
        run: ruff .
      - name: Run tests                 # 5. Tests
        run: pytest --maxfail=1 --disable-warnings -q
```

1. **Checkout** your repository.
2. **Setup‑Python** installs the requested interpreter.
3. **Install dependencies** from your `requirements.txt`.
4. **Lint** your code.
5. **Test** your code.

---

## 🎲 5. Matrix Builds

Run the same job across multiple environments:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python: [3.9, 3.10, 3.11]
        os: [ubuntu-latest, windows-latest]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with: { python-version: ${{ matrix.python }} }
      - run: pip install -r requirements.txt
      - run: pytest
```

- **`strategy.matrix`** defines combinations.
- **`${{ matrix.python }}`** and **`${{ matrix.os }}`** expand per job.

---

## ⚡ 6. Caching Dependencies

Speed up builds by caching package installs:

```yaml
- name: Cache pip
  uses: actions/cache@v3
  with:
    path: ~/.cache/pip
    key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
    restore-keys: |
      ${{ runner.os }}-pip-
```

- **`actions/cache`** saves/loads directories between runs.
- **`key`** determines cache identity; use file hashes to bust when deps change.

---

## 🔐 7. Secrets & Environment Variables

- **Secrets** are stored in GitHub repo settings and exposed as `secrets.NAME`.
- **Environment variables** can be defined globally or per-step:

```yaml
env:
  GLOBAL_VAR: hello

steps:
  - run: echo "Repo is $GITHUB_REPOSITORY"
  - name: Deploy
    env:
      API_TOKEN: ${{ secrets.DEPLOY_TOKEN }}
    run: deploy-tool --token $API_TOKEN
```

---

## 📦 8. Artifacts & Uploads

Save build outputs or test results:

```yaml
- name: Run tests
  run: pytest --junitxml=report.xml

- name: Upload test report
  uses: actions/upload-artifact@v3
  with:
    name: junit-report
    path: report.xml
```

Later you can download them from the Actions UI or in another job with `download-artifact`.

---

## 🚀 9. Deployment Example

Example: Docker build & push to Docker Hub:

```yaml
name: Build & Push Docker

on:
  push:
    branches: [ main ]

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Log in to Docker
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USER }}
          password: ${{ secrets.DOCKER_PASS }}
      - name: Build and push
        uses: docker/build-push-action@v4
        with:
          context: .
          push: true
          tags: myrepo/myimage:latest
```

---

## 🛠️ 10. Advanced Features

- **`needs:`** to express dependencies between jobs.
- **`if:`** conditionally run steps/jobs.
    ```yaml
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    ```
    
- **`concurrency`** to cancel in‑flight runs on the same branch.
- **Service containers** for test databases:
    
    ```yaml
    services:
      postgres:
        image: postgres:15
        env: { POSTGRES_USER: test, POSTGRES_DB: db }
        ports: [5432:5432]
    ```
    

---

## 🎯 11. Putting It All Together

1. **Define triggers** (`on:`).
2. **Organize jobs** and set `runs-on`.
3. **Sequence steps**: checkout → setup → install → test → deploy.
4. **Use matrices** for cross‑environment testing.
5. **Cache** heavy dependencies.
6. **Use secrets** for sensitive data.
7. **Upload artifacts** for logs, coverage, etc.
8. **Leverage conditional logic** for flexible pipelines.

---

