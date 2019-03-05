# crypto: RSAaaay
difficulty: easy

## Description
This challenge is pretty much the basics of RSA, and uses the vulnerability of the "weak exponent".
We are given:
  - A ciphertext : "906851 991083 1780304 2380434 438490 
                    356019 921472 822283 817856 556932 2102538 
                    2501908 2211404 991083 1562919 38268"
  - A key : (2531257, 43)
      - e = 43
      - n = 2531257
 
First off, we see that the modulus (2531257) is very weak, so we go to factordb.com and retrieve p, q and phi(N):
  - p = 509
  - q = 4973
  - phi(n) = (p-1)*(q-1) = 2525776
We must then find the private exponent d by finding the modular inverse of e modulo phi(n).
You can either use a script to bruteforce the modular inverse, or you can use an online too like dcode (https://www.dcode.fr/modular-inverse)

We get d = 58739

We have all the information we need, now we just have to decrypt the message with this simple python3 script:
```
result = []
n = 2531257
d = 58739
for i in "906851 991083 1780304 2380434 438490 356019 921472 822283 817856 556932 2102538 2501908 2211404 991083 1562919 38268".split(' '):
  result.append( int(i) ** d % n)
print(result)
```
we get result = [103, 105103, 101109, 12383, 97118, 97103, 10195, 83105, 12095, 70108, 121105, 110103, 9584, 105103, 101114, 115125]
splitting these values and converting to characters with chr() will give us the following flag:

gigem{Savage_Six_Flying_Tigers}
