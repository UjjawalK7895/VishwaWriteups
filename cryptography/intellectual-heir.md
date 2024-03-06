### Intellectual Heir
#### Description
```
You received a package, and you got to know that you are the descendant of RIADSH. There are four files and a safe in the package.

You should analyze the files, unlock the safe, and prove your worth. The safe has alphanumeric and character combinations.

PS: The safe has no lowercase buttons.
```
#### Writeup
Unzipping the attached package.zip leaves us with four files: `file.txt`, `file1.txt`, `file2.txt` and `'Intellectual Heir.py'`.

The python file has below purposefully disfigured 'code':
```py
# my secret to hide the combination of my safe in fornt of all without anyone getting a clue what it is ;)

#some boring python function for conversion nothing new
def str_to_ass(input_string):
    ass_values = []
    for char in input_string:
        ass_values.append(str(ord(char)))
    ass_str = ''.join(ass_values)
    return ass_str

input_string = input("Enter the Combination: ")
result = str_to_ass(input_string)
msg = int(result)

#not that easy, you figure out yourself what the freck is a & z
a = 
z = 

f = (? * ?) #cant remember what goes in the question mark
e = #what is usually used

#ohh yaa!! now you cant figure out $h!t
encrypted = pow(msg, e, f)
print(str(encrypted))

#bamm!! protection for primes
number = 
bin = bin(number)[2:]

#bamm!! bamm!! double protection for primes
bin_arr = np.array(list(bin), dtype=int)
result = np.sin(bin_arr)
result = np.cos(bin_arr)
np.savetxt("file1", result)
np.savetxt("file2", result)
```

The file1.txt contains newline separated values, and each value is either `5.403023058681397650e-01` (cos 1) or `1.000000000000000000e+00` (cos 0), suggesting it corresponds to the `np.savetxt(np.cos(bin_arr))` above.
Since just one file is sufficient to recover the original number, the presence of two files indicates we can recover two numbers this way:
```py
import numpy as np
nps = np.round(np.arcsin(np.loadtxt('file2.txt'))).astype(int)
npc = np.round(np.arccos(np.loadtxt('file1.txt'))).astype(int)
sval = int(''.join(map(lambda x: str(int(x)), nps)),2)
# 89992838080292432041749786501934273286234288253944531238372481458518903256335509625431026718322552331965908097158513049639942869
cval = int(''.join(map(lambda x: str(int(x)), npc)),2)
# 57357445697656305449852658985072306792176526325401427689338172257827853689473430283849367024117704513636066741450894144354439223
```
Both the recovered values turn out to be primes, as was hinted from the python file. It also says e is "what is usually used", meaning `e = 65537`
The only remaining file to be seen is `file.txt`, which is simply a rsa encrypted ciphertext:
```py
p = sval
q = cval
e = 65537
phi = (p - 1) * (q - 1)
d = pow(e, -1, phi)
cipher = int(open('file.txt', 'r').read()) # 4400037514278889258479265625258024039636437755883377709505596356049534358755375772484057042989024750972247184288820831886430459963472328358741858934783775986591400972020736548834642094922678189447202173710409868474198821576627330424767999152339702779346380
m = pow(cipher, d, p * q) # 8948859564825195843551958748828435899579709551
```
`m` looks like the kind of output the `str_to_ass` function would give, given ascii plaintext as input. Reversing the function:
```py
ass = str(m)
# reverse of str_to_ass:
nxt = 0
while nxt != len(ass):
    checkchar = ass[nxt]
    nnext = (nxt + 3) if checkchar=='1' else (nxt + 2)
    hole = ass[nxt:nnext]
    print(chr(int(hole)),end='')
    nxt = nnext
```
This prints out `Y0U_@R3_T#3_W0RT#Y_OF_3` to the console, which is what the challenge description refers to as the safe's combination.

#### FLAG : `vishwaCTF{Y0U_@R3_T#3_W0RT#Y_OF_3}`
