# 🔐 Diffie-Hellmann

```
 ________  ___  ________ ________ ___  _______                  ___  ___  _______   ___       ___       _____ ______   ________  ________   ________      
|\   ___ \|\  \|\  _____\\  _____\\  \|\  ___ \                |\  \|\  \|\  ___ \ |\  \     |\  \     |\   _ \  _   \|\   __  \|\   ___  \|\   ___  \    
\ \  \_|\ \ \  \ \  \__/\ \  \__/\ \  \ \   __/|   ____________\ \  \\\  \ \   __/|\ \  \    \ \  \    \ \  \\\__\ \  \ \  \|\  \ \  \\ \  \ \  \\ \  \   
 \ \  \ \\ \ \  \ \   __\\ \   __\\ \  \ \  \_|/__|\____________\ \   __  \ \  \_|/_\ \  \    \ \  \    \ \  \\|__| \  \ \   __  \ \  \\ \  \ \  \\ \  \  
  \ \  \_\\ \ \  \ \  \_| \ \  \_| \ \  \ \  \_|\ \|____________|\ \  \ \  \ \  \_|\ \ \  \____\ \  \____\ \  \    \ \  \ \  \ \  \ \  \\ \  \ \  \\ \  \ 
   \ \_______\ \__\ \__\   \ \__\   \ \__\ \_______\              \ \__\ \__\ \_______\ \_______\ \_______\ \__\    \ \__\ \__\ \__\ \__\\ \__\ \__\\ \__\
    \|_______|\|__|\|__|    \|__|    \|__|\|_______|               \|__|\|__|\|_______|\|_______|\|_______|\|__|     \|__|\|__|\|__|\|__| \|__|\|__| \|__|
```

## General Information

A major problem with the usage of symmetric algorithms for cryptography is the secure exchange of PSKs (pre-shared-keys) over an unsecured channel. In order to solve this problem, there is the Diffie-Hellmann approach, which allows the exchange of PKSs over an unsecured channel.

## How it works 

The concept between Diffi-Hellmann is quite easy and can easily be explained with the use of colors:

![DH in colors](https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/Diffie-Hellman_Key_Exchange.svg/250px-Diffie-Hellman_Key_Exchange.svg.png)

source: https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/Diffie-Hellman_Key_Exchange.svg/250px-Diffie-Hellman_Key_Exchange.svg.png

However, in cryptography we want to use numbers instead of colors. This is the calculation we can use for this:

1. **A**lice and **B**ob publicly agree to use the value `p = 23` (which has to be an prime number) and a base `g = 5` (which is a primitive root modulo 23). 

2. Now Alice decides on a secret integer `a = 4` and calculates her public value `A = g ^ a mod p` and sends it to Bob. (in our case here: `A = 4`)

3. Now Bob also calculates his public value with a secret integer he chose `b = 3` and calculates it the same way: `B = g ^ b mod p`. He also sends this value to Alice (in our case: `B = 10`)

4. Alice can now calculate the secret key with the value she has received from Bob: `s = B ^ a mod p`. (in our case: `s = 18`) 


5. Bob does the same with the value he received: `s = A ^ b mod p`. (in our case this also results in: `s = 18`).

Now Alice and Bob have successfully exchanged a PSK which can be used as a key in symmetric encryption.


## Simple Implementation

In order to demonstrate this, I have implemented a little Python script that shows a successful implementation of Diffi-Hellmann:

```python
from Crypto.Util.number import getPrime, getRandomInteger
from sympy import primitive_root

# Decide on the public key
p = getPrime(512)
g = primitive_root(p)

# Generate the secret integers (a = Alice, b = Bob)
a = getRandomInteger(512)
b = getRandomInteger(512)

# Calculate the public values (A = Alice, B = Bob)
A = pow(g, a, p)
B = pow(g, b, p)

# Calculate the secret keys (s_a = Alice, s_b = Bob)
s_a = pow(B, a, p)
s_b = pow(A, b, p) 

print(f'Secret Key of Alice: {s_a}')
print(f'Secret Key of Bob: {s_b}')
print(f'Are the same: {s_a == s_b}')
```

An example run would create following result:

```
Secret Key of Alice: 4045644280500037609325014736290639878747799864426323658578720978761824541502391154321193888931265757618562397510001163610360090106818855152000394223765391
Secret Key of Bob: 4045644280500037609325014736290639878747799864426323658578720978761824541502391154321193888931265757618562397510001163610360090106818855152000394223765391
Are the same: True
```