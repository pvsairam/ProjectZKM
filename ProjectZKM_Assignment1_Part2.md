# ProjectZKM Assignment 1 - Part 2

```
def algorithm_3_60(alpha, beta, n, k=383):
    x_0, a_0, b_0 = 1, 0, 0

    def f(x, a, b):
        if x % 3 == 1:
            return beta * x % k, a, (b + 1) % n
        elif x % 3 == 0:
            return x * x % k, (2 * a) % n, (2 * b) % n
        else:
            return alpha * x % k, (a + 1) % n, b

    x_i_1, a_i_1, b_i_1 = x_0, a_0, b_0
    x_2i_2, a_2i_2, b_2i_2 = x_0, a_0, b_0

    while True:
        x_i, a_i, b_i = f(x_i_1, a_i_1, b_i_1)
        x_2i, a_2i, b_2i = f(*f(x_2i_2, a_2i_2, b_2i_2))

        x_i_1, a_i_1, b_i_1 = x_i, a_i, b_i
        x_2i_2, a_2i_2, b_2i_2 = x_2i, a_2i, b_2i

        if x_i == x_2i:
            r = (b_i - b_2i) % n
            if r == 0:
                return 'Error'
            else:
                return (pow(r, -1, n) * (a_2i - a_i)) % n

# Test Pollard's Rho for Discrete Logarithms
alpha, beta, n = 2, 228, 191
result = algorithm_3_60(alpha, beta, n)
print(f"The discrete logarithm is {result}")

```

## Output:

### The discrete logarithm is 110
