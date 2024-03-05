### Lets Smother the King  

#### DESCRIPTION
```txt
In my friend circle, Mr. Olmstead and Mr. Ben always communicate with each other through a secret code language that they created, which we never understand. Here is one of the messages Mr. Ben sent to Mr. Olmstead, which I somehow managed to hack and extract it from Ben's PC. However, it's encrypted, and I don't comprehend their programming language. Besides being proficient programmers, they are also professional chess players. It appears that this is a forced mate in a 4-move chess puzzle, but the information needs to be decrypted to solve it. Help me out here to solve the chess puzzle and get the flag.

Flag format: VishwaCTF{move1ofWhite_move1ofBlack_move2ofWhite_move2ofBlack_move3ofWhite_move3ofBlack_move4ofWhite}.

Note: Please use proper chess notations while writing any move.

# Author : Naman Chordia

FLAG FORMAT:
VishwaCTF{write the chess moves}
```

#### Writeup
the name Mr. Olmstead and Mr. Ben  is not 2 names it's Ben Olmstead 

Ben Olmstead is best known as the creator of Malbolge (1998), an early esolang which remains the most difficult language to code.(reference is also given as they are proficient programmers)

In given File we have code of Malbolge language which can be run [here](https://malbolge.doleczek.pl/)

By runing code we get 

```txt
White- Ke1,Qe5,Rc1,Rh1,Ne6,a2,b3,d2,f2,h2 Black- Ka8,Qh3,Rg8,Rh8,Bg7,a7,b7,e4,g2,g6,h7
```

Actually these are the positions of the chess pieces. So I put the position on lichess and then solved the puzzle to eventually smother mate the black king.

#### FLAG : VishwaCTF{Nc7+_Kb8_Na6+_Ka8_Qb8+_Rxb8_Nc7#}
