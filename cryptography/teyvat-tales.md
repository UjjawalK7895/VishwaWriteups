### Teyvat Tales

#### DESCRIPTION
```txt
All tavern owners in Mondstadt are really worried because of the frequent thefts in the Dawn Winery cellars.
The Adventurers’ Guild has decided to secure the cellar door passwords using a special cipher device.
But the cipher device itself requires various specifications….which the guild decided to find out by touring the entire Teyvat.

PS: The Guild started from the sands of Deshret then travelled through the forests of Sumeru and finally to the cherry blossoms of Inazuma
```

#### Writeup
We get 4 passwords in the website after searching in the script.js which reveals a cipher text. The passwords were :

- enigma m3
- ukw c
- rotor1 i p m rotor2 iv a o rotor3 vi i n
- vi sh wa ct fx

And the cipher text is : CYNIPJ_RE_LSKR-YAZN_MBSJ

I then randomly searched about enigma m3 and it revealed that it was a type of cipher. On [this](https://cryptii.com/pipes/enigma-machine) site i got a decrypter which required rotor 1, 2, 3 and plugboard. I just plugged in the values and the flag finally came.

#### FLAG : VishwaCTF{beware_of_tone-deaf_bard}
