### Poly Fun
#### Description
```
Its a simple symmetric key encryption, I am sure you will be able to solve it (what do you mean the key looks weird)
```
#### Writeup
Attached to the challenge are three files: `encoded_flag.txt`, `encoded_key.txt`, and `challenge.py`.

`encoded_key.txt`: ```☞➭⥄⫣Ⲋ⸹⿰ㆯ㍶☞⒗☞☞☞➭☞⥄☞⫣☞Ⲋ☞⸹☞⿰☞ㆯ☞㍶➭⒗➭```
`encoded_flag.txt`: ```u5FUKxDUxH9y8yxvfaaU+GSXDwvJS6QxlN/3udOEzpU6fIVUExjDLsB3LKqUTz/x```
The `challenge.py` has below content:
```py
import numpy as np
import random

polyc = [4,3,7]
poly = np.poly1d(polyc)


def generate_random_number():
    while True:
        num = random.randint(100, 999)
        first_digit = num // 100
        last_digit = num % 10
        if abs(first_digit - last_digit) > 1:
            return num


def generate_random_number_again():
    while True:
        num = random.randint(1000, 9999)
        if num % 1111 != 0:
            return num


def transform(num):
    number = random.randint(1, 100000)
    org = number
    number *= 2
    number += 15
    number *= 3
    number += 33
    number /= 6
    number -= org
    if number == 13:
        num1 = random.randint(1, 6)
        num2 = random.randint(1, 6)
        number = num1 * 2
        number += 5
        number *= 5
        number += num2
        number -= 25
        if int(number / 10) == num1 and number % 10 == num2:
            number = generate_random_number()
            num1 = int(''.join(sorted(str(number), reverse=True)))
            num2 = int(''.join(sorted(str(number))))
            diff = abs(num1 - num2)
            rev_diff = int(str(diff)[::-1])
            number = diff + rev_diff
            if number == 1088:
                org = num
                num *= 2
                num /= 3
                num += 5
                num *= 4
                num -= 9
                num -= org
                return num
            else:
                number = generate_random_number_again()
                i = 0
                while number != 6174:
                    digits = [int(d) for d in str(number)]
                    digits.sort()
                    smallest = int(''.join(map(str, digits)))
                    digits.reverse()
                    largest = int(''.join(map(str, digits)))
                    number = largest - smallest
                    i += 1

                if i <= 7:
                    org = num
                    num *= 2
                    num += 7
                    num += 5
                    num -= 12
                    num -= org
                    num += 4
                    num *= 2
                    num -= 8
                    num -= org
                    return num
                else:
                    org = num
                    num **= 4
                    num /= 9
                    num += 55
                    num *= 6
                    num += 5
                    num -= 23
                    num -= org
                    return num
        else:
            org = num
            num *= 10
            num += 12
            num **= 3
            num -= 6
            num += 5
            num -= org
            return num
    else:
        org = num
        num += 5
        num -= 10
        num *= 2
        num += 12
        num -= 20
        num -= org
        return num


def encrypt(p,key):
    return ''.join(chr(p(transform(i))) for i in key)


key = open('key.txt', 'rb').read()
enc = encrypt(poly,key)
print(enc)
```
The bulk of the above code defines an encoding, seemingly based on random values. However, looking at the first few lines of the transform function closely:
```py
    number = random.randint(1, 100000)
    org = number
    number *= 2
    number += 15
    number *= 3
    number += 33
    number /= 6
    number -= org
    if number == 13:
```
reveals that `number` evaluates to $$\frac{3(2x+15)+33}{6}-x$$ where `x` is the random number. The above expression simplifies to 13, regardless of the value of generated, thus implying that the else block is never executed. 
The other if-checks are evaluated in the same predetermined fashion:
```py
def transform(num):
    number = random.randint(1, 100000)
    org = number
    number *= 2
    number += 15
    number *= 3
    number += 33
    number /= 6
    number -= org
    if number == 13:
        num1 = random.randint(1, 6)
        num2 = random.randint(1, 6)
        number = num1 * 2
        number += 5
        number *= 5
        number += num2
        number -= 25
        if int(number / 10) == num1 and number % 10 == num2:
            number = generate_random_number()
            num1 = int(''.join(sorted(str(number), reverse=True)))
            num2 = int(''.join(sorted(str(number))))
            diff = abs(num1 - num2)
            rev_diff = int(str(diff)[::-1])
            number = diff + rev_diff
            if number == 1088:
                print("UNREACHABLE")
            else:
                number = generate_random_number_again()
                i = 0
                while number != 6174:
                    digits = [int(d) for d in str(number)]
                    digits.sort()
                    smallest = int(''.join(map(str, digits)))
                    digits.reverse()
                    largest = int(''.join(map(str, digits)))
                    number = largest - smallest
                    i += 1

                if i <= 7:
                    org = num
                    num *= 2
                    num += 7
                    num += 5
                    num -= 12
                    num -= org
                    num += 4
                    num *= 2
                    num -= 8
                    num -= org
                    return num
                else:
                    print("UNREACHABLE")
        else:
            print("UNREACHABLE")
```
The lines inside the only if block ever executed end up doing nothing to num, and so the transform function reduces to simply:
```py
def transform(num):
    return num
```
And the entire `challenge.py` reduces to:
```py
import numpy as np

polyc = [4,3,7]
poly = np.poly1d(polyc)

def encrypt(p,key):
    return ''.join(chr(p(i)) for i in key)

key = open('key.txt', 'rb').read()
enc = encrypt(poly,key)
print(enc)
```
The `key.txt` needs to be recovered from the `encoded_key.txt`, so the above code needs to be reversed. My python code for it:
```py
polyvalues = list(open('encoded_key.txt','rb').read().decode('utf-8'))
polyvalues = list(map(lambda x: ord(x), polyvalues))
import numpy as np
result = [np.roots([4,3, 7-v]) for v in polyvalues] # [array([-49.75, 49. ]), array([-50.75, 50. ]), array([-51.75, 51. ]), ....
result = list(map(lambda roots: int(roots[1]) , result)) # [49, 50, 51, 52, 53, 54, 55, 56, 57, 49, ...
key = ''.join([chr(i) for i in result])  # '12345678910111213141516171819202'
```
The challenge description ("symmetric") and the key we just recovered (32 characters, 256 bits) suggests that the base64 encoded_flag is AES-ECB encrypted. Decrypting using the same, we get `VishwaCTF{s33_1_t0ld_y0u_1t_w45_345y}`

#### FLAG : `VishwaCTF{s33_1_t0ld_y0u_1t_w45_345y}`
