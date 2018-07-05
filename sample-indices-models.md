Models:

n = length
m = amount
b1 = 7
b2 = 0.16
c1 = 33
d1=6
d2=1
e1=0.1
e2=1
f1=500000
f2=0.9

Floyd's alg:
    f(m) = (b1 + b2*m)*m = b1*m + b2*m^2
Cache/rejection method:
    c(m) = c1*m
Inplace:
    i(m,n) = if n < f1 { d1*m^d2 + e1*n^e2 } else { f2*n }
        = if n < f1 { d1*m + e1*n^e2 } else { f2*n }

Find the boundaries:
```
f(m) < c(m)
=>  b1*m + b2*m^2 < c1*m
=>  b1 + b2*m < c1
=>  m < (c1 - b1) / b2
~> m < 163

i(m,n) < c(m)
=>  if n < f1 { d1*m + e1*n^e2 } else { f2*n } < c1*m
=>  if n < f1 { d1*m + e1*n^e2 < c1*m } else { f2*n < c1*m }
=>  if n < f1 { e1*n^e2 < (c1 - d1)*m } else { f2*n < c1*m }
~>  if n < f1 { e1*n < (c1 - d1)*m } else { f2*n < c1*m }
~>  if n < 500'000 { 0.1*n < 27*m } else { 0.9*n < 33*m }
~>  if n < 500'000 { n < 270*m } else { n < 330/9*m }

i(m,n) < f(m)
=>  if n < f1 { d1*m + e1*n^e2 } else { f2*n } < b1*m + b2*m^2
=>  if n < f1 { d1*m + e1*n^e2 < b1*m + b2*m^2 } else { f2*n < b1*m + b2*m^2 }
=>  if n < f1 { e1*n^e2 < (b1 - d1)*m + b2*m^2 } else { f2*n < b1*m + b2*m^2 }
~>  if n < f1 { e1*n < (b1 - d1)*m + b2*m^2 } else { f2*n < b1*m + b2*m^2 }
~>  if n < 500'000 { 0.1*n < 1*m + 0.16*m^2 } else { 0.9*n < 7*m + 0.16*m^2 }
~>  if n < 500'000 { n < 10*m + 1.6*m^2 } else { n < 70/9*m + 8/45*m^2 }
```
