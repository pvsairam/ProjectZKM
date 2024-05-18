# ProjectZKM Assignment 1 - Part 1

import math

def algorithm_3_9(n):
    a, b = 2, 2
    n = abs(n)
    f = lambda x: (x**2 + 1) % n

    while True:
        a = f(a)
        b = f(f(b))
        d = math.gcd(a - b, n)
        if d > 1 and d < n:
            return d
        if d == n:
            return None

# Test Pollard's Rho for Factoring

n = 455459
factor = algorithm_3_9(n)
print(f"A non-trivial factor of {n} is {factor}")

## A non-trivial factor of 455459 is 743
