# CSAW2022-OSINT

Here is my solution for the one OSINT question in CSAW 2022 (categorised as forensics).

## PROBLEM
We are provided the following question:

Two things of note:
1. Find the twitter account
2. Answer the questions in the terminal:

```
Welcome agent! We have reason to believe a user with the twitter handle Darkroom8109 is working with The Enemy! Can you help us determine what The Enemy is planning?

1. When did the enemy agent join twitter? Please use the format MM/YYYY
Please enter your answer:
```

## SOLUTION
### A. Twitter
We can find the user's twitter account: www.twitter.com/Darkroom8109

Where it states he joined in August 2022.

```
1. When did the enemy agent join twitter? Please use the format MM/YYYY
Please enter your answer:
08/2022
That's right!
```

I then proceeded to conduct a quick scan of the twitter page. Looked through his tweets, followers (in case 'The Enemy' was following), lists, media, likes, etc. The only thing of note was this one tweet

This suggests looking at his deleted tweets may be of use to us. To WayBackMachine we go! Viewing the page archived on August 20, and we've found the deleted tweet in question.

### B. GitHub
The user's github account: https://github.com/spyduhman

```
2. What is the spy's github username?
Please enter your answer:
spyduhman
That's right!
```
The github has one repository for a Chat App. A brief look through the files provides no result, so the next step is always to check the commit history. There we find a log.txt file was deleted from the repository.

```
3. What is the full name of the file that contains communications between The Enemy and the Evil Spy?
Please enter your answer:
log.txt
That's right!
```

### C. Bankers' reMorse
Accessing the link in log.txt leads to an Assignment.wav file, which contains intermittent beeping noise. Morse code. Put it through an audio to text morse code decoder (https://morsecode.world/international/decoder/audio-decoder-adaptive.html).

```
HELLO EVIL AGENT YOUR NEXT TARGET IS A BANK THE BANK'S BIN NUMBER IS 452234 THE TARGETS SWIFT CODE IS YOUR PASSWORD FOR MORE INSTRUCTIONS VISIT BIT.LY SLASH OSINTSEC GOOD LUCK
```

The first part of the message gives us a bank BIN number, while the second leads us to a link (bit.ly/osintsec), which is a password-protected pdf file. The message clue suggests the 'Swift code' for the target is the password we need to unlock this pdf file. 

#### C-1. trash BIN
First, find the bank via its BIN number. ```BIN```, or Bank Identification Number, is a 4-6 digit bank code that identifies the credit/debit card issuer (i.e. the bank). 

With the provided BIN Number ```452234```, we find the bank ```TD Canada Trust``` (https://binlist.net/). From the message clue, we know this is our "target".

```
4. Which country is the target based in?
Please enter your answer:
canada
That's right!
```

#### C-2. taller SWIFT
Next, find the swift code to unlock the pdf. A ```SWIFT code```, is an 8-11 character code that is another form of a bank identification code.

The bank's SWIFT code is ```TDOMCATTTOR``` (https://wise.com/gb/swift-codes/countries/canada/td-toronto-dominion-bank-swift-code).

```
5. What is the target's international Swift code?
Please enter your answer:
TDOMCATTTOR
That's right!
```

### D. is for pDf
We can now successfully unlock the pdf. It's an image of a flood. At this point, I was rather perplexed. The next question on the terminal was:

```
6. What is a crime?
What is the answer? Hint: it is two words
```

Starting floods? Natural disasters? What could this be? And then I noticed the title of the document, which was revealed now that it had been unlocked. 

<em>Wow, I really am blind.</em>

```
Copyright Infringement
That's right!
Congrats! Thanks to you, we now have more information about The Enemy's upcoming attack!
Here's a little reward for your trouble: flag{C0N6r475463N7600DW0rKN3X771M3N0PU811C53rV3r}
```

The flag is ```flag{C0N6r475463N7600DW0rKN3X771M3N0PU811C53rV3r}```

