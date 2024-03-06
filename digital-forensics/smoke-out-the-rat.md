### Smoke out the Rat

#### Description
```txt
There was a major heist at the local bank.
Initial findings suggest that an intruder from within the bank,
specifically someone from the bank's database maintenance team, aided in the robbery.
This traitor granted access to an outsider,
who orchestrated the generation of fake transactions and the depletion of our valuable customers' accounts.
We have the phone number, '789-012-3456', from which the login was detected, which manipulated the bank's employee data.
Additionally, it's noteworthy that this intruder attempted to add gibberish to the binlog and ultimately dropped the entire database at the end of the heist.

Your task is to identify the
first name of the traitor,
the last name of the outsider,
and the time at which the outsider was added to the database.

Flag format : VishwaCTF{TraitorFirstName_OutsiderLastName_HH:MM:SS}
```

#### Writeup

We are given a `DBlog--bin.000007` file. It appears to a MySQL Replication log.

Using the `mysqlbinlog` tool, we can read the file. From the description we search the phone number `789-012-3456` and find that it belongs to `Matthew Miller`, who is our traitor.

From the description, we also know that the outsider manipulated the bank's employee data. 

We then search for the place where any changes were made to the employees table, and find out that `John Smith` was replaced by `John Darwin`, who is our outsider.

And the timestamp at which the outsider was added to the database is `15:31:29`.

#### FLAG : `VishwaCTF{Matthew_Darwin_15:31:29}`