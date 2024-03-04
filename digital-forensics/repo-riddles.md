### Repo Riddles

#### Description
```txt
We got a suspicious Linkedin post which got a description and also a zip file with it. It is suspected that a message is hidden in there. Can you find it?

LinkedIn Post Description:

Title: My First Project -The Journey Begins

Hello fellow developers and curious minds!

I'm thrilled to share with you my very first Git project - a labor of love, dedication, and countless late-night commits. 🚀

Explore the code, unearth its nuances, and let me know your thoughts. Your feedback is invaluable and will contribute to the ongoing evolution of this project.
```

#### Writeup
We recieved a zip file `My First Git Project.zip` which had two files `profile_card.html` and `croping (62).jpg`. None of which are of particular interest.

We then looked at the git history using `git log`

```log
* 9370bf5 (HEAD, master) last commit
* ebf9671 second last commit
| * 02adccb (2) Usefull data insertion
| * 41dca9f Something is not looking good
| | * 57f6653 (3) string[0] = G string[1] = 1 string[2] = t
| |/  
| * db01ffe Initail Commit on branch 2
|/  
* aa3306a Initial Commit
```

From commit `57f6653` we can see that the string `G1t` is the first three characters of the flag. 

Next checking out to the commit `ebf9671` we can see that the string `ger` is the 7th, 8th and 9th characters of the flag.

Checking out to the commit `db01ffe` we can see that the string `_2727` is the 10th, 11th, 12th and 13th characters of the flag.

And finally in commit `02adccb` we can see that the string `G1g` is the 4th, 5th and 6th characters of the flag, from the index.html file.

#### FLAG : `vishwaCTF{G1tG1gger_2727}`

