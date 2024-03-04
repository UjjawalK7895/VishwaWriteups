### Mysterious Old Case

#### Description
```txt
You as a FBI Agent, are working on a old case involving a ransom of $200,000. After some digging you recovered an audio recording.
```

#### Writeup
We are given a audio file `final.mp3` which has the some interesting exif data. We can use `exiftool` to extract the exif data from the audio file. 
```txt
Album                           : Cooper
Recording Time                  : 1971
Genre                           : the zip file is 100 MB not 7 GB
Original Release Time           : 0001
Band                            : DB Cooper
Comment                         : password for the zip is all lowecase with no spaces
User Defined URL                : https://drive.google.com/file/d/1bkuZRLKOGWB7tLNBseWL34BoyI379QbF/view?usp=drive_lin
User Defined Text               : (purl) https://drive.google.com/file/d/1bkuZRLKOGWB7tLNBseWL34BoyI379QbF/view?usp=drive_lin
```

Also opening the audio file, at around 1:06 mark, we find something other than the music. Playing the audio file in reverse we can hear the following:
```txt
I'm Dan Cooper.
It is 24th of November 1971.
Now I have left from Seattle and header towards Rena.
I have got all my demands Fulfilled. I have done some changes in the flight log and upload it into a remote server.
The file is encrypted, the handful description is the airliner that I was flying in most importantly.
The secret key is split and hidden in every element of the Fibonacci series starting from 2
```

From the Google Drive Link we can download a zip file `flight_logs.zip` which is password protected, from the previous hint, we know the password is `northwestairlines`. Extracting the zip file we get a lot of files, but looking at `Flight-305.og` (the flight Dan Cooper hijacked) we see that the file has the following data:
```txt
1971-11-24 06:22:08.531691 - ATT - Boeing 727
V
i
1971-11-24 07:31:08.531691 - HWR - Boeing 727
s
1971-11-24 06:22:08.531691 - ATT - Boeing 727
1971-11-24 07:31:08.531691 - HWR - Boeing 727
h
1971-11-24 06:22:08.531691 - ATT - Boeing 727
1971-11-24 06:22:08.531691 - ATT - Boeing 727
1971-11-24 06:22:08.531691 - ATT - Boeing 727
1971-11-24 07:31:08.531691 - HWR - Boeing 727
w
1971-11-24 07:31:08.531691 - HWR - Boeing 727
1971-11-24 06:22:08.531691 - ATT - Boeing 727
```

It after a gap of no of lines corresponding to the Fibonacci series, there are the characters of the flag. But simply we can just ignore all lines starting with 1971, and obtain the flag.

```py
open_file = open("Flight-305.log", "r")
flag = ''

for line in open_file:
    if not line.startswith("1971"):
        flag += line[0]

# strip newlines
flag = flag.strip()
print(flag)
```

#### FLAG : `VishwaCTF{1_W!LL_3E_B@CK}`
