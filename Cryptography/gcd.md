# Greatest Commond Divisor
GCD is the larges divisor common to two integers.  Divisors are an integers factors.

e.g. gcd(12, 20)

12 =  [1, 2, 3, 4, 6, 12]
20 = [1, 2, 4, 5, 10, 20]

gcd = 4

Eucledian algorithm

gcd(a,b)

a = q(b) + r
a = largest of a and b
b = smallest of a and b
q = quotient
r = remainder

gcd(12,20)

20 = 1(12) + 8
a =  q(b) + r

repeate with b becomes a and r becomes b

12 = 1(8) + 4
8 = 2(4) + 0

GCD is the remainder of the last solution before the remainder is 0

$$\frac {1}{x}\\$$