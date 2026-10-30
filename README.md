import random 

MIN_NUMBER = 1
MAX_NUMBER = 100
MAX_ATTEMPTS = 5
CLOSE_LIMIT = 5 
MEDIUM_LIMIT = 15


def get_valid_guess():
    while True: 
        text = input("Enter your guess (1 to 100): ")
        try:
            guess = int(text)
        except ValueError:
            print("Invalid input! Please enter only an integer.")
            continue
        
        if guess < MIN_NUMBER or guess > MAX_NUMBER:
            print("The number must be between 1 and 100!")
            continue
        
        return guess
    
def show_hint(guess, secret_number):
    if guess < secret_number:
        print("The secret number is bigger!")
    else:
        print("The secret number is smaller!")
        
    difference = abs(guess - secret_number)
    if difference <= CLOSE_LIMIT:
        print("So Close!")
    elif difference <= MEDIUM_LIMIT:
        print("You’re close, yet there’s still a distance!")
    else:
        print("You are very far away!")
        
def get_rank(attempts):
    if attempts == 1:
        return "ٍExcellent"
    elif attempts == 2:
        return "Very good"
    elif attempts == 3:
        return "Good"
    elif attempts == 4:
        return "Accepted"
    else:
        return "You won by luck!"
        
def play_round():
    secret_number = random.randint(MIN_NUMBER, MAX_NUMBER)
    attempts = 0
    won = False
            
    print("\n A number between 1 and 100 has been chosen. Guess it!")
            
    while attempts < MAX_ATTEMPTS and not won:
        remaining = MAX_ATTEMPTS - attempts
        print(f"\n attempts {attempts + 1} to {MAX_ATTEMPTS}")
        print(f"Remaining Life: {remaining}")
            
        guess = get_valid_guess()
        attempts += 1
            
        if guess == secret_number:
            won = True
        else:
            show_hint(guess, secret_number)
                
    if won:
        print("\n Welldone! You guessed right.")
        print(f"Your score: {get_rank(attempts)}")
    else:
        print("\n Unfortunatly You lost.")
        print(f" Secret number was: {secret_number} ")
                
def ask_play_again():
    while True:
        answer = input("\n Do you want to play again? (y/n): ").strip().lower()
        if answer == "y":
            return True
        elif answer == "n":
            return False
        else:
            print("Please answer only with y(yes) or n(no).")
            
print("Welcome to Number Guessing Game!")
while True:
    play_round()
    if not ask_play_again():
        print("The game is over. Goodbye.")
        break
