### DESCRIPTION
Aesthetic Looking army of 128 Robots with AGI Capabilities are coming to destroy our locality!

Author : Samarth Ghante

FLAG FORMAT:
VishwaCTF{}

### Writeup

I didn't know what to do at first but then i randomly entered robots.txt file it contained :-
```txt
User-agent: *
Disallow: /admin
L3NlY3JldC1sb2NhdGlvbg==
Decryption key: th1s_1s_n0t_t5e_f1a9
```
I decoded the weird looking text using decode.fr as base64 it revealed /secret-location then i visited the site and found encrypted flag in local storage and then i decrpted the flag using the key on [this](https://encode-decode.com/aes-256-cbc-encrypt-online/) site.

### FLAG : VishwaCTF{g0_Su88m1t_1t_Qu14kl7}