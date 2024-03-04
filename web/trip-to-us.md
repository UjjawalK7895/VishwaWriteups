### Trip to Us

#### Description
```txt
IIT kharakpur is organizing a US Industrial Visit. The cost of the registration is $1000.
But as always there is an opportunity for intelligent minds.
Find the hidden login and Get the flag to get yourself a free US trip ticket.
```

#### Writeup

On clicking the `Click Here` link on the website, we see and error saying, `YOU ARE NOT AN IITAIN , GO BACK!!!!!!!`

Checking the source code of this page we find `Change User agent to 'IITIAN'` in the alt text of the image.

After changing the user agent to `IITIAN` and refreshing the page, we get to a login page.

Analysing the directories on the website we find the `/db/` directory, we find a `users.sql` file containing:
```sql
INSERT INTO `users` (`id`, `user_name`, `password`, `name`) VALUES
(1, 'admin', 'unbre@k@BLE_24', 'admin');
```

Logging in using these credentials, we get the flag.

#### FLAG : `VishwaCTF{y0u_g0t_th3_7r1p_t0_u5}`