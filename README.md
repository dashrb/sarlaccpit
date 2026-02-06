# sarlaccpit
Support script for SarlaccPit, a Hangman-type word game for Star Wars fans online.
This game is posted to a social network (e.g. mastodon), shows a hangman-style or Wheel of Fortune-style game board, with letters and words.

The game master posts the board and a Poll, with 4 possible letters. The poll would typically have a 24-hour duration, to support international players.
Strangers see the post, and vote for a letter.

After the poll closes, the winning letter is exposed on the board (or is indicated to be a "wrong letter" if it doesn't appear).
There are typically many polls before someone guesses the solution.

The game ends when a person guesses the correct solution.
I keep track of the number of games we have played (well it was estimated after it had been going for some time).

More comprehensive rules about playing (not so much about this script, per se) are at: https://c.im/@darth_hideout/113631196868456567

# Usage
I personally use a command line / terminal window where I run this script, and leave the window in place until tomorrow when I run it again.
Each day, I run the script again, passing the day's chosen letter, in addition to all of the prior arguments.

For example, I am going to start the game, assuming this is game number 75, and my solution is "Use the force Luke".
On day 1 I would run:
`$ echo Use the force Luke | ./sarlaccpit -n 75`

(note: you could just run `sarlaccpit -n 75` and it would prompt you for the solution, but typing the solution phrase every day would be tedious and error-prone. Hence the `echo`)

and it would display this output:
```
Enter your solution:
=============   INTERNAL TEXT FOR GAME MASTER    ==========
  C:  1
  E:  4
  F:  1
  H:  1
  K:  1
  L:  1
  O:  1
  R:  1
  S:  1
  T:  1
  U:  2

=============  EXTERNAL TEXT FOR POSTING ONLINE  ==========


Welcome to poll number 1 of #SarlaccPit, a Star Wars themed word-guessing game.
This is game number 75, making this #SarlaccPit75.

This is a phrase with 4 words of 3, 3, 5, & 4 letters, respectively.

Solution Board:
  _ _ _ / _ _ _ / _ _ _ _ _ /
  _ _ _ _

Rules: https://c.im/@darth_hideout/113631196868456567


#Games #Puzzles #StarWars

```

The top "half" gives me some letter statistics, and helps me choose which letters to offer in the poll of the day.
I still have to manually pick which 4 letters to offer. The lower half of the output I can paste into my social media post.
After the paste, I would click to add a Poll, and choose the 4 letters to allow the audience to vote. I typically choose
3 or 4 letters which are IN the puzzle, and 0 or 1 letters which are NOT in the puzzle.

Then, wait, and eventually tomorrow arrives. If for example, the audience selects the letter E, then I "up-arrow" and add `-l e` to the command:
```
$ echo Use the force Luke | ./sarlaccpit -n 75 -l e
Enter your solution:
=============   INTERNAL TEXT FOR GAME MASTER    ==========
  C:  1
  E:  4     GUESSED, poll 1
  F:  1
  H:  1
  K:  1
  L:  1
  O:  1
  R:  1
  S:  1
  T:  1
  U:  2

  Votes so far, by poll:
  1     E   CORRECT

=============  EXTERNAL TEXT FOR POSTING ONLINE  ==========


Welcome to poll number 2 of #SarlaccPit, a Star Wars themed word-guessing game.
This is game number 75, making this #SarlaccPit75.

This is a phrase with 4 words of 3, 3, 5, & 4 letters, respectively.

The chosen letter in poll 1 is the letter 'E'. There are 4 Es.

Solution Board:
  _ _ E / _ _ E / _ _ _ _ E /
  _ _ _ E

Wrong Votes so far: None


#Games #Puzzles #StarWars
```

You can see the changes to the output. Set up another poll for the next day.
If the chosen letters over the next 3 days are "S", "U", and then "F", I would run:
`echo Use the force Luke | ./sarlaccpit -n 75 -l e -l s`
`echo Use the force Luke | ./sarlaccpit -n 75 -l e -l s -l u`
and then:
```
$ echo Use the force Luke | ./sarlaccpit -n 75 -l e -l s -l u -l f
Enter your solution:
=============   INTERNAL TEXT FOR GAME MASTER    ==========
  C:  1
  E:  4     GUESSED, poll 1
  F:  1     GUESSED, poll 4
  H:  1
  K:  1
  L:  1
  O:  1
  R:  1
  S:  1     GUESSED, poll 2
  T:  1
  U:  2     GUESSED, poll 3

  Votes so far, by poll:
  1     E   CORRECT
  2     S   CORRECT
  3     U   CORRECT
  4     F   CORRECT

=============  EXTERNAL TEXT FOR POSTING ONLINE  ==========


Welcome to poll number 5 of #SarlaccPit, a Star Wars themed word-guessing game.
This is game number 75, making this #SarlaccPit75.

This is a phrase with 4 words of 3, 3, 5, & 4 letters, respectively.

The chosen letter in poll 4 is the letter 'F'. There is 1 F.

Solution Board:
  U S E / _ _ E / F _ _ _ E /
  _ U _ E

Wrong Votes so far: None


#Games #Puzzles #StarWars
```
And for completeness, if the next day the chosen letter is not in the solution, e.g. "B":
```
$ echo Use the force Luke | ./sarlaccpit -n 75 -l e -l s -l u -l f -l b
Enter your solution:
=============   INTERNAL TEXT FOR GAME MASTER    ==========
  C:  1
  E:  4     GUESSED, poll 1
  F:  1     GUESSED, poll 4
  H:  1
  K:  1
  L:  1
  O:  1
  R:  1
  S:  1     GUESSED, poll 2
  T:  1
  U:  2     GUESSED, poll 3

  Votes so far, by poll:
  1     E   CORRECT
  2     S   CORRECT
  3     U   CORRECT
  4     F   CORRECT
  5     B               INCORRECT

=============  EXTERNAL TEXT FOR POSTING ONLINE  ==========


Welcome to poll number 6 of #SarlaccPit, a Star Wars themed word-guessing game.
This is game number 75, making this #SarlaccPit75.

This is a phrase with 4 words of 3, 3, 5, & 4 letters, respectively.

The chosen letter in poll 5 is the letter 'B'. There are no Bs.

Solution Board:
  U S E / _ _ E / F _ _ _ E /
  _ U _ E

Wrong Votes so far: B


#Games #Puzzles #StarWars

```

