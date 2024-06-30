# Swap without temp

## C++
```cpp
#include <iostream>

int main() {
    int a = 5;
    int b = 7;

    a = a ^ b;
    b = a ^ b;
    a = a ^ b;

    std::cout << a << ", " << b << std::endl;
}
```

## Python
```python
a = 5
b = 7

a = a ^ b;
b = a ^ b;
a = a ^ b;

print(a, b)
```