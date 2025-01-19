# Rock-paper-scissor-game
import random
options = {'r': 'Rock 🪨', 'p': 'Paper 📄', 's': 'Scissors ✂️'}

def get_no_of_rounds():
    while True:
        rounds = int(input("Enter the number of rounds you want to play: "))
        if rounds > 0:
            return rounds
        else:
            print("Invalid input! Please enter a valid number.")

def get_user_choice():
    while True:
        user_choice = input("Enter your choice (r-Rock, p-Paper, s-Scissors): ")
        user_choice_lower = user_choice.lower()
        if user_choice_lower in options:
            return user_choice_lower
        print("Invalid choice. Please enter 'r', 'p', or 's'.")

def select_winner(computer_choice, user_choice_lower):
    if computer_choice == user_choice_lower:
        return 'draw'
    elif (computer_choice == 'r' and user_choice_lower == 's') or \
         (computer_choice == 'p' and user_choice_lower == 'r') or \
         (computer_choice == 's' and user_choice_lower == 'p'):
        return 'computer'
    else:
        return 'user'

def play_round():
    computer_choice = random.choice(list(options.keys()))
    user_choice = get_user_choice()

    print(f"Computer chose {options[computer_choice]} and you chose {options[user_choice]}.")
    
    winner = select_winner(computer_choice, user_choice)
    if winner == 'draw':
        print("It's a draw!")
    elif winner == 'computer':
        print("Computer wins this round!")
    else:
        print("You win this round!")
    return winner

def play_game():
    rounds = get_no_of_rounds()
    
    computer_score = user_score = 0
    
    for i in range(rounds):
        print(f"\n--- Round {i+1} ---")
        winner = play_round()
        if winner == 'computer':
            computer_score += 1
        elif winner == 'user':
            user_score += 1

    print("\n--- Final Scores ---")
    print(f"Computer: {computer_score}")
    print(f"You: {user_score}")

    if computer_score > user_score:
        print("Computer wins the game!")
    elif computer_score < user_score:
        print("Congratulations! You win the game!")
    else:
        print("It's a draw!")
    
    replay = input("\nDo you want to play again? (yes/no): ").lower()
    if replay == 'yes':
        play_game()
    else:
        print("Thank you for playing!")

print("Welcome to the Rock, Paper, Scissors Game!")
play_game()
