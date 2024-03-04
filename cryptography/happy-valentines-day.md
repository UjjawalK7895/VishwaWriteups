### Happy Valentine's Day
#### Description
```txt
My girlfriend and I captured our best moments of Valentine's Day in a portable graphics network. But unfortunately I am not able to open it as I accidentally ended up encrypting it. Can you help me get my memories back?
```

#### Writeup
We got two files, enc.txt and source.txt with the following python code:
```py
from PIL import Image
from itertools import cycle

def xor(a, b):
    return [i^j for i, j in zip(a, cycle(b))]

f = open("original.png", "rb").read()
key = [f[0], f[1], f[2], f[3], f[4], f[5], f[6], f[7]]

enc = bytearray(xor(f,key))

open('enc.txt', 'wb').write(enc)
```

It appears to be taking the XOR of each byte with corresponding byte of the key. We can reverse the process to get the original image, as we know A^B = C, so C^B = A. We can use the following python code to get the original image:

```py
from itertools import cycle

def xor(a, b):
    return [i^j for i, j in zip(a, cycle(b))]

enc = open("enc.txt", "rb").read()
key = [0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A]

dec = bytearray(xor(enc,key))

open('dec.png', 'wb').write(dec)
```

from with we obtain the image, which contains the flag.

#### FLAG : `vishwaCTF{h34d3r5_f0r_w1nn3r5}`