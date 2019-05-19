##### 欧几里得算法 (python don`t like recursion)

```python
def gcd(m, n):
    if n == 0:
        return m
    r = m % n
    return(gcd(n, r))
```

