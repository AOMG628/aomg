import random

countries = ["Canada", "United States", "Brazil", "India", "China", "Australia", "France", "Germany", "Italy", "Russia"]

secret_word = random.choice(countries).upper()

def display_word(secret_word, guessed_letters):
    display = "".join(letter if letter in guessed_letters else "_ " for letter in secret_word)
    return display

chances = len(secret_word) + 2

def process_guess(secret_word, guessed_letters, guess):
    guessed_letters.add(guess.upper())
    return guess.upper() in secret_word

def check_win(secret_word, guessed_letters):
    return all(letter in guessed_letters for letter in secret_word)

guessed_letters = set()
print("Welcome to Country Hangman!")
print("You have", chances, "chances to guess the country name.")
print(display_word(secret_word, guessed_letters))

while chances > 0:
    guess = input("Enter your guess (a letter): ").upper()
    if len(guess) != 1 or not guess.isalpha():
        print("Please enter a single letter.")
        continue
    if guess in guessed_letters:
        print("You've already guessed that letter.")
        continue
    if process_guess(secret_word, guessed_letters, guess):
        print("Correct!")
    else:
        print("Incorrect!")
        chances -= 1
    print("Chances left:", chances)
    print(display_word(secret_word, guessed_letters))
    if check_win(secret_word, guessed_letters):
        print("Congratulations! You've guessed the country correctly:", secret_word)
        break

if chances == 0:
    print("Sorry, you've run out of chances. The country was:", secret_word)
