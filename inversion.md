# GF(2^m) Inversion

## General Idea for Implementing GF(q^2) Operations on GF(q)
Polinomial defining GF(q^2) over GF(q):

p(x) = x^2 + p1*x + p0 

p1,p0 in GF(q)

## Inversion on GF(q^2)
A, B in GF(q^2), A = a1 * x + a0, B = b1 * x + b0,

a1,a0,b1,b0 in GF(q),

B satisfies B = A^-1

Calculate b1, b0 as:

t = (a1^2 * p0 + a1 * a0 * p1 + a0^2)^-1

b1 = t * a1

b0 = t * (a1 * p1 + a0)

all operations for calculating t,b1,b0 are on GF(q)

## Multiplication on GF(q^2)
A, B, C in GF(q^2), A = a1 * x + a0, B = b1 * x + b0, C = c1 * x + c0,

a1,a0,b1,b0,c1,c0 in GF(q),

C satisfies C = A * B

Calculate c1, c0 as:

c1 = a1 * b0 + a0 * b1 + a1 * b1 * p1

c0 = a0 * b0 + a1 * b1 * p0

## Multiplication on GF(q^2)
A, B in GF(q^2), A = a1 * x + a0, B = b1 * x + b0,

a1,a0,b1,b0 in GF(q),

B satisfies B = A * A

Calculate b1, b0 as:

b1 = a1^2 * p1

b0 = a0^2 + a1^2 * p0

# Operations on GF(2^4)
Constructing GF(2^4) on GF(2) using bit operations. Following operations are defined in 

[Wolkerstorfer J, Oswald E, Lamberger M, "An ASIC Implementation of the AES SBoxes", CT-RSA 2002, LNCS 2271, pp. 67-78, Springer-Verlag, 2002](https://link.springer.com/chapter/10.1007/3-540-45760-7_6)

Polinomial defining GF(2^4) over GF(2):

p(z) = z^4 + z + 1

## Multiplication on GF(2^4) (C = mul4(A,B))

Input: A = (a3||a2||a1||a0), B = (b3||b2||b1||b0), ai,bi 1 bit

Output: C = (c3||c2||c1||c0)

t1 = a0 XOR a3

t2 = a2 XOR a3

c3 = (a3 AND b0) XOR (a2 AND b1) XOR (a1 AND b2) XOR (t1 AND b3)

c2 = (a2 AND b0) XOR (a1 AND b1) XOR (t1 AND b2) XOR (t2 AND b3)

c1 = (a1 AND b0) XOR (t1 AND b1) XOR (t2 AND b2) XOR ((a1 XOR a2) AND b3)

c0 = (a0 AND b0) XOR (a3 AND b1) XOR (a2 AND b2) XOR (a1 AND b3)

## Squaring on GF(2^4) (C = sqr4(A))
Input: A = (a3||a2||a1||a0),  ai 1 bit

Output: C = (c3||c2||c1||c0)

c3 = a3

c2 = a3 XOR a1

c1 = a2

c0 = a0 XOR a2

## Inversion on GF(2^4) (C = inv4(A))
Input: A = (a3||a2||a1||a0),  ai 1 bit

Output: C = (c3||c2||c1||c0)

t1 = a1 XOR a2 XOR a3 XOR (a1 AND a2 AND a3)

c3 = t1 XOR (a0 AND a3) XOR (a1 AND a3) XOR (a2 AND a3)

c2 = (a0 AND a1) XOR a2 XOR (a0 AND a2) XOR a3 XOR (a0 AND a3) AND (a0 AND a2 AND a3)

c1 = (a0 AND a1) XOR (a0 AND a2) XOR (a1 AND a2) XOR a3 XOR (a1 AND a3) XOR (a0 AND a1 AND a3)

c0 = t1 XOR a0 XOR (a0 AND a2) XOR (a1 AND a2) XOR (a0 AND a1 AND a2)

# Operations on GF(2^8)
Constructing GF(2^8) on GF(2^4)

Polinomial defining GF(2^8) over GF(2^4):

p(y) = y^2 + p1 * y + p0

## Multiplication on GF(2^8) (mul8)

Input: A = (a1||a0), B = (b1||b0), ai,bi 4 bit

Output: C = (c1||c0)

t = mul4(a1, b1)

c1 = mul4(a1,b0) XOR mul4(a0,b1) XOR mul4(t,p1)

c0 = mul4(a0,b0) XOR mul4(t,p0)

## Squaring on GF(2^8) (sqr8)

Input: A = (a1||a0), ai 4 bit

Output: C = (c1||c0)

t = sqr4(a1)

c1 = mul4(t,p1)

c0 = sqr4(a0) XOR mul4(t,p0)

## Inversion on GF(2^8) (inv8)

Input: A = (a1||a0), ai 4 bit

Output: C = (c1||c0)

t1 = mul4(sqr4(a1), p0) XOR mul4(mul4(a1,a0), p1) XOR sqr4(a0)

t2 = inv4(t1)

t3 = mul4(a1,p1) XOR a0

c1 = mul4(t2,a1)

c0 = mul4(t3,t2)
