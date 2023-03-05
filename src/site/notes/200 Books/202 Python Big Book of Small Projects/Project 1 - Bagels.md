---
{"dg-publish":true,"permalink":"/200-books/202-python-big-book-of-small-projects/project-1-bagels/"}
---

- A deductive logic game that has you guess a secret three-digit number based on clues. The game offers one of the following answers in response to your guess as a hint:
	- Pico - When a correct digit is in the wrong place
	- Fermi - correct digit in cofrect pplace
	- Bagels - no correct digits
- You get 10 tries to get the number right
- ## Dev stuff
	- We must set the number as a '324' string to compare instead of an integer:
```python
"""Bagels was created by Al Sweigart in the big book of small python projects"""  
Project by Andrew Weisbeck - andrew@tarheeldevstudio.com  
  
import random  
  
NUM_DIGITS = 3  
MAX_GUESSES = 10  
  
def main():  
    print('''Bagels, a deductive logic game.  
by Al Sweigart, coded by Andrew Weisbeck andrew.weisbeck@gmail.com  
  
I am thinking of a {} - digit number with no repeated digits. Try to guess what it is. Here are some clues:  
When I say:          That means:  
  Pico                  One digit correct and in wrong position  Fermi                 One Digit correct and in right position  
  Bagels                No Digit is correct    For example, your secret number is 248 and you guess is 843,   
  the clues would be Fermi Pico'''.format(NUM_DIGITS))  
  
    while True:    # Main Game loop  
        # Stores the secret number the player needs to guess        secretNum = getSecretNum()  
        print('I have thought up a number.')  
        print('  You have {} guesses to get it.'.format(MAX_GUESSES))  
  
        numGuesses = 1  
        while numGuesses <= MAX_GUESSES:  
            guess = ''  
            # Loop contiues until they enter a valid guess  
            while len(guess) != NUM_DIGITS or not guess.isdecimal():  
                print('Guess #{}: '.format(numGuesses))  
                guess = input('> ')  
  
            clues = getClues(guess, secretNum)  
            print(clues)  
            numGuesses += 1  
  
            if guess == secretNum:  
                break # They're correct, so break out of loop  
            if numGuesses > MAX_GUESSES:  
                print('You ran out of guesses.')  
                print('The answer was {}.'.format(secretNum))  
  
        # Ask player if they want to play again  
        print('Do you want to play again? (yes or no)')  
        if not input('> ').lower().startswith('y'):  
            break  
    print('Thanks for playing!')  
  
def getSecretNum():  
    """returns a string made up of NUM_DIGITS unique random digits."""  
    numbers = list('0123456789') # create a list of digits 0 to 9.  
    random.shuffle(numbers) # Shuffle them in random order  
  
    # Get the first NUM_DIGITS digits in the list for the secret number;    secretNum = ''  
    for i in range(NUM_DIGITS):  
        secretNum += str(numbers[i])  
    return secretNum  
  
def getClues(guess, secretNum):  
    """Returns a string with the pico, fermi, bagels clues for a guess and secret number pair."""  
    if guess == secretNum:  
        return 'You got it!'  
  
    clues = []  
  
    for i in range(len(guess)):  
        if guess[i] == secretNum[i]:  
            # A correct digit is in the incorrect place.  
            clues.append('Fermi')  
        elif guess[i] in secretNum:  
            # A correct digit is in the incorrect place.  
            clues.append('Pico')  
    if len(clues) == 0:  
        return 'Bagels' # There are no correct digits at all.  
    else:  
        # Sort the clues into alphabetical order so their original order doesn't give info away  
        clues.sort()  
        # Make a single string from the list of string clues  
        return ' '.join(clues)  
  
# If the program is run (instead of imported), run the game:  
if __name__ == '__main__':  
    main()
```

- # Here is the result of my first game to test:

```bash
C:\Users\andre\PycharmProjects\big-book-small-projects\bagels\venv\Scripts\python.exe C:\Users\andre\PycharmProjects\big-book-small-projects\bagels\main.py 
Bagels, a deductive logic game.
by Al Sweigart, coded by Andrew Weisbeck andrew.weisbeck@gmail.com

I am thinking of a 3 - digit number with no repeated digits. 
Try to guess what it is. Here are some clues:
When I say:          That means:
  Pico                  One digit correct and in wrong position 
  Fermi                 One Digit correct and in right position
  Bagels                No Digit is correct
  
  For example, your secret number is 248 and you guess is 843, 
  the clues would be Fermi Pico
I have thought up a number.
  You have 10 guesses to get it.
Guess #1: 
> 486
Fermi Fermi
Guess #2: 
> 487
Fermi Fermi
Guess #3: 
> 489
Fermi Fermi
Guess #4: 
> 481
You got it!
Do you want to play again? (yes or no)

```
- ## Follow up questions:
	- 1. What happens when you change the NUM_DIGITS constant?
		- You have to guess more digits correctly to win the game and it becomes much harder
	- 2. What happens when you change the MAX_GUESSES constant?
		- You get more guesses
```
C:\Users\andre\PycharmProjects\big-book-small-projects\bagels\venv\Scripts\python.exe C:\Users\andre\PycharmProjects\big-book-small-projects\bagels\main.py 
Bagels, a deductive logic game.
by Al Sweigart, coded by Andrew Weisbeck andrew.weisbeck@gmail.com

I am thinking of a 3 - digit number with no repeated digits. 
Try to guess what it is. Here are some clues:
When I say:          That means:
  Pico                  One digit correct and in wrong position 
  Fermi                 One Digit correct and in right position
  Bagels                No Digit is correct
  
  For example, your secret number is 248 and you guess is 843, 
  the clues would be Fermi Pico
I have thought up a number.
  You have 10 guesses to get it.
Guess #1: 
> 486
Fermi Fermi
Guess #2: 
> 487
Fermi Fermi
Guess #3: 
> 489
Fermi Fermi
Guess #4: 
> 481
You got it!
Do you want to play again? (yes or no)

```

- 3. What happens if you set NUM_DIGITS to a number larger than 10?
	- A `list index out of range` error occurs because there are more digits than possible numbers
- 4. What happens set secretNum = '123'?
	- Easy to guess b/c answer = 123
- 5. What error message if you delete or comment out numGuesses = 1 on line 34?
	- Unbound local error
- 6. What happens if you delete or comment out `random.shuffle(numbers)` on line 62?
	- The answer is always 123
- 7. What happens if you delete out or comment out `if guess == secretNum:` on lne 74 and return `'You got it!'` on line 75?
	- Error
- 8. What happens if you comment out numGuesses += 1 on line 44?
	- You never get past the first guess
	- 