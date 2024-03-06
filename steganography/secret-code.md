### Secret Code

#### Description
```txt
Akshay has a letter for you and need your help
```

#### Writeup
On runnong binwalk on the image we get a zip file `5ecr37_c0de.zip` and a text file `helper.txt`.

We used John The Ripper to crack the password of the zip file and got two files `5ecr37_c0de.txt` and `info.txt`.

As the `5ecr37_c0de.txt` file appears to be a list of coordinates, we use matplotlib to plot the points.

```py
import matplotlib.pyplot as plt

with open("coordinates.txt", "r") as file:
    lines = file.readlines()
    coordinates = [(int(line.split(", ")[0][1:]), int(line.split(", ")[1][:-2])) for line in lines]


x_coords, y_coords = zip(*coordinates)


plt.figure(figsize=(8, 6))
plt.scatter(x_coords, y_coords, color='blue', marker='o', s= 5)
plt.title('Scatter Plot of Coordinates')
plt.xlabel('X Coordinate')
plt.ylabel('Y Coordinate')

plt.show()
```

![](https://media.discordapp.net/attachments/1203376160348708951/1213451703245086791/Figure_1.png?ex=65f585f6&is=65e310f6&hm=6aa1beccfdb32e7df03f91a5d780b46c54a5113d187f50771c7097e453d5f214&=&width=1714&height=968)

On mirroring the image we get the flag.

#### FLAG : `VishwaCTF{th15_15_4_5up3r_53cr3t_c0d3_u53_1t_w153ly_4nd_d0nt_5h4re_1t_w1th_4ny0ne}`