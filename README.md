Chloe Tang - Project manager: chloetang1122@gmail.com
ZANDER - Backend developer: Zander.xuzan@gmail.com
Bowen Whaleman - Technical writer: insert_email_here --> _____________________

The Lost Ruins: A Text-Based Adventure

Welcome to The Lost Ruins, an interactive text-based adventure where you explore an ancient jungle, uncover forgotten secrets, and navigate dangerous challenges in search of a legendary treasure.

About the Game

You play as an archaeologist who stumbles upon an ancient map detailing the location of a lost temple deep in the uncharted jungles of South America. Along the way, you’ll encounter treacherous terrain, solve cryptic puzzles, and decide who to trust as you race against time—and rival treasure hunters—to uncover the secrets hidden within the ruins.

Your choices shape the story, and every decision can lead to fortune, danger, or even doom. Will you claim the treasure, or will the jungle claim you?

Features
	•	Branching Storyline – Every choice impacts the outcome, leading to multiple endings.
	•	Challenging Puzzles – Solve ancient riddles and unlock hidden passages.
	•	Inventory System – Collect and use items to aid in your adventure.
	•	Dynamic Characters – Encounter allies and foes with their own motives.
	•	Replayability – Discover different story paths and endings.




How to Play
	•	The game presents you with text descriptions and choices.
	•	Type the number of your chosen option and press Enter.
	•	Manage your inventory and use items wisely.
	•	Unravel the mysteries of the lost ruins to uncover the treasure!

Contributing

We welcome contributions! If you’d like to improve the game, please:
	1.	Fork the repository.
	2.	Create a new branch for your changes.
	3.	Submit a pull request with a detailed description of your changes.

License

This project is licensed under the MIT License.

Are you ready to brave the jungle, unlock ancient mysteries, and claim the lost treasure? Play The Lost Ruins now and see if you have what it takes!



import sys
import time

inventory = []

def print_pause(message, delay=1):
    print(message)
    time.sleep(delay)

def game_over():
    print_pause("GAME OVER")
    play_again()

def game_won():
    print_pause("YOU WIN")
    play_again()

def play_again():
    choice = input("Do you want to play again? (yes/no) > ").lower()
    if choice == "yes":
        start_game()
    elif choice == "no":
        print_pause("Thank you for playing! Goodbye!")
        sys.exit()
    else:
        print_pause("Invalid choice. Please choose 'yes' or 'no'.")
        play_again()

def intro():
    print_pause("You find yourself at the edge of an ancient jungle.")
    print_pause("Legends speak of a legendary treasure hidden deep within.")
    print_pause("With a map in hand and a sense of adventure, you step into the jungle.")

def first_choice():
    print_pause("You come across a fork in the path.")
    print_pause("To the left, you hear the sound of rushing water.")
    print_pause("To the right, the path leads deeper into the dense jungle.")
    choice = input("Do you want to go left or right? (left/right) ").lower()
    if choice == "left":
        waterfall()
    elif choice == "right":
        dense_jungle()
    else:
        print_pause("Invalid choice. Please choose 'left' or 'right'.")
        first_choice()

def waterfall():
    print_pause("You follow the sound of water and find a beautiful waterfall.")
    print_pause("Behind the waterfall, you notice a hidden cave.")
    choice = input("Do you want to enter the cave or go back? (enter/back) ").lower()
    if choice == "enter":
        hidden_cave()
    elif choice == "back":
        first_choice()
    else:
        print_pause("Invalid choice. Please choose 'enter' or 'back'.")
        waterfall()

def hidden_cave():
    print_pause("You enter the cave and find ancient carvings on the walls.")
    print_pause("The carvings tell the story of the legendary treasure.")
    print_pause("You find a clue that points you further into the jungle.")
    print_pause("You decide to head back to the fork in the path.")
    first_choice()

def dense_jungle():
    print_pause("You venture deeper into the dense jungle.")
    print_pause("The path becomes more difficult to navigate.")
    print_pause("You come across a clearing with three paths.")
    choice = input("Do you want to take the left, middle, or right path? (left/middle/right) ").lower()
    if choice == "left":
        snake_pit()
    elif choice == "middle":
        ancient_temple()
    elif choice == "right":
        quicksand()
    else:
        print_pause("Invalid choice. Please choose 'left', 'middle', or 'right'.")
        dense_jungle()

def snake_pit():
    print_pause("You take the left path and suddenly fall into a pit of snakes!")
    print_pause("You manage to escape, but decide to head back to the clearing.")
    dense_jungle()

def ancient_temple():
    print_pause("You take the middle path and find an ancient temple.")
    print_pause("Inside the temple, you find the legendary treasure!")
    print_pause("Congratulations! You have found the legendary treasure and completed your adventure.")
    game_won()

def quicksand():
    print_pause("You take the right path and find yourself sinking into quicksand!")
    print_pause("You manage to escape, but decide to head back to the clearing.")
    dense_jungle()

def start_game():
    intro()
    first_choice()

if __name__ == "__main__":
    start_game()
