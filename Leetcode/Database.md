
# [175. Combine Two Tables](https://leetcode.com/problems/combine-two-tables/)

```postgresql
select p.firstName as FirstName, p.lastName as LastName, a.city, a.state
from Person as p left join Address as a on p.personId=a.personId
```

# [181. Employees Earning More Than Their Managers](https://leetcode.com/problems/employees-earning-more-than-their-managers/)

```postgreSQL
select e.name as Employee
from Employee as e join Employee as m on e.managerId=m.id
where e.salary > m.salary
```

# [182. Duplicate Emails](https://leetcode.com/problems/duplicate-emails/)

```postgreSQL
select email as Email
from Person
group by email
having  count(email)>1
```


```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

```postgreSQL

```

