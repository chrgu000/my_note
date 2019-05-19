##### python don`t like recursion

- gcd递归,如果不用return返回gcd调用的时候， 走到if，就会返回none，因为返回的时第一次进入循环的m,但这时m没有进入到if，所以会返回none

```python
def gcd(m, n):
if n == 0:
    print(m)
    return m
r = m % n
return(gcd(n, r))


sx = gcd(10, 2)
print(sx)
```

