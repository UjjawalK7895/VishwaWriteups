### Wired Secrets

#### Description
```txt
You are an intern at the Cyber Security Department of India and you have been assigned your first case.
The Department has finally caught a notorious Hacker who communicates online in a Secretive manner.
It is suspected that this file might contain clues to unlock critical information.
Your task is to analyse the file and decipher any hidden messages or patterns to progress further in the investigation,

PS: Zero is Hero, and dont forget to treat brackets neatly.

Note : Flag has upper case letter and numbers only
```

#### Writeup
We are given a pcapng file `okay10.pcapng` which we can open in Wireshark. We observe that it contains USB traffic. Extracting the hid data from the pcapng file, we use the following script to plot the data:
```py
import sys
import matplotlib.pyplot as plt

plt.xlim(-1000, 1000)
plt.ylim(-300, 300)

filename = "keystrock.txt"

def to_signed(h):
    i = int(h, 16)
    return i - ((0x80 & i) << 1)

coordinate_x = 0
coordinate_y = 0

for line in open(filename).readlines():
    if len(line) > 1:
        status, raw_x, raw_y, junk = line.split(":")
        coordinate_x += to_signed(raw_x)
        coordinate_y += to_signed(raw_y)

        if status != "00":
            # print("%d %d" % (coordinate_x, coordinate_y))
            plt.plot(coordinate_x, coordinate_y, color="red", marker=".")

plt.show()
```

We get the following plot:
![plot](https://media.discordapp.net/attachments/1203376160348708951/1213755780512096256/Screenshot_from_2024-03-03_13-21-44.png?ex=65f6a128&is=65e42c28&hm=b4c289748ed5626ba9ee34ace154c67d7d9152d3b3274112550b1838e801214b&=&width=1408&height=968)

As the data is not clear, we make first change the graph scale, and then we add a condition to print only specific data points. We get the following graphs:
![plot1](https://media.discordapp.net/attachments/1203376160348708951/1213766687015567391/Screenshot_2024-03-03_at_2.05.15_PM.png?ex=65f6ab50&is=65e43650&hm=798c8b6c5e6a61d0efefc438ef0048497b06cb9361f3a74715bfc2f44883e692&=&width=1202&height=968)
![plot2](https://media.discordapp.net/attachments/1203376160348708951/1213766972811116574/Screenshot_2024-03-03_at_2.06.23_PM.png?ex=65f6ab95&is=65e43695&hm=362e825eda24bdbaa0954a1e8862957399e7d76f2278e7665fe30e7589c421b2&=&width=1072&height=968)

Thus after mirroring the graph vertically we get the flag.

#### FLAG : `VishwaCTF{KUD0SD3T3CTIVE}`