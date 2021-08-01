---
layout:     post
title:      aptenodytes-forsteri
date:       2014-06-08 11:21:29

categories: jekyll pixyll
---




![Challenge](/images/2021-06-22-aptenodytes-forsteri/Untitled.png)

![aptenodytes-forsteri%20%5BDone%5D%2033a4326170294e6486fecade35504a0b/Untitled%201.png](/images/2021-06-22-aptenodytes-forsteri/Untitled_1.png)

![aptenodytes-forsteri%20%5BDone%5D%2033a4326170294e6486fecade35504a0b/Untitled%202.png](/images/2021-06-22-aptenodytes-forsteri/Untitled_2.png)

This challenge seems more like reverse engineering.

Here is my take on what the Python file does:

1. Open the flag text
2. Ensure flag must follow the standard flag format
3. As for encrypting the flag itself:
    1. Find the index of `A` in letters. Plus 18 to that. Mod 26 to everything
    2. Find the index of `B` in letters

Let me pause here and try a little playful experimentation before cracking my brain. Let me test this python script out:

![aptenodytes-forsteri%20%5BDone%5D%2033a4326170294e6486fecade35504a0b/Untitled%203.png](/images/2021-06-22-aptenodytes-forsteri/Untitled_3.png)

![aptenodytes-forsteri%20%5BDone%5D%2033a4326170294e6486fecade35504a0b/Untitled%204.png](/images/2021-06-22-aptenodytes-forsteri/Untitled_4.png)

Excellent! Without even needing to reverse engineer the code, I can kinda figure out how this script works intuitively: 

- The alphabetical order of whatever string is passed through the encryption it is shifted by 8
- Alphabets that "exceed" the 26 alphabets are "looped" back

![aptenodytes-forsteri%20%5BDone%5D%2033a4326170294e6486fecade35504a0b/Untitled%205.png](/images/2021-06-22-aptenodytes-forsteri/Untitled_5.png)

In the spirit of trial and error, let me try to reverse engineer this by taking the scrambled alphabets, passing it through the script, and modifying variables within the script until I get unscrambled alphabets back.

![aptenodytes-forsteri%20%5BDone%5D%2033a4326170294e6486fecade35504a0b/Untitled%206.png](/images/2021-06-22-aptenodytes-forsteri/Untitled_6.png)

And my intuition is right: `18` is the variable that is scrambling the flag. All I need to do is to change `18` to `8` since `26 - 18 = 8` where 26 is the number of alphabets. 

![aptenodytes-forsteri%20%5BDone%5D%2033a4326170294e6486fecade35504a0b/Untitled%207.png](/images/2021-06-22-aptenodytes-forsteri/Untitled_7.png)

Got the flag!