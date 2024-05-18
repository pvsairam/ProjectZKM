# Part 1: Constructing a Prime Number with Your Name

```
# Import necessary libraries
import random
from sympy import isprime
import string

# Convert phrase to number
def phrase_to_number(phrase):
    char_map = {char: f"{i:02d}" for i, char in enumerate(string.ascii_uppercase, start=1)}
    char_map[' '] = "27"
    number_str = ''.join(char_map[char] for char in phrase.upper() if char in char_map)
    return number_str

# Generate a random odd number
def generate_random_odd_number(base_number, length=100):
    while True:
        random_part = ''.join(random.choices(string.digits, k=length - len(base_number) - 1))
        odd_digit = random.choice('13579')
        candidate = int(base_number + random_part + odd_digit)
        if len(str(candidate)) == length and candidate % 2 != 0:
            return candidate

# Find a prime number with the given suffix
def find_prime_with_suffix(base_number):
    while True:
        candidate = generate_random_odd_number(base_number)
        if isprime(candidate):
            return candidate

# Your custom phrase
phrase = 'SAIRAM IS BULLISH ON METIS AND HYBRID ROLLUP'
number_phrase = phrase_to_number(phrase)

# Find the prime number
prime_candidate = find_prime_with_suffix(number_phrase)
print(f"Prime number: {prime_candidate}")
```

## Output:

```
Prime number: 2701030809200127091927022112120919082715142713052009192701140427082502180904271815121221166481104813
```

# Part 2: Implementing the Miller-Rabin Algorithm

```
# Decompose n-1 as 2^s * d
def decompose(n):
    s, d = 0, n - 1
    while d % 2 == 0:
        s += 1
        d //= 2
    return s, d

# Modular exponentiation
def mod_exp(base, exp, mod):
    result = 1
    base = base % mod
    while exp > 0:
        if exp % 2 == 1:
            result = (result * base) % mod
        exp = exp >> 1
        base = (base * base) % mod
    return result

# Miller-Rabin Primality Test
def miller_rabin_test(n, k):
    if n in (2, 3):
        return True
    if n % 2 == 0:
        return False
    
    s, d = decompose(n)
    for _ in range(k):
        a = random.randint(2, n - 2)
        x = mod_exp(a, d, n)
        if x in (1, n - 1):
            continue
        for _ in range(s - 1):
            x = mod_exp(x, 2, n)
            if x == n - 1:
                break
        else:
            return False
    return True

# Testing the prime number
security_param = 10
is_probably_prime = miller_rabin_test(prime_candidate, security_param)
print("The number is prime" if is_probably_prime else "The number is composite")

```

## Output:

```
The number is prime
```
