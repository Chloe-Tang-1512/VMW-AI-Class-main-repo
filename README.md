Chloe Tang - Project manager: chloetang1122@gmail.com
Zander - Backend developer: Zander.xuzan@gmail.com
Albert Tu - Backend developer: alberttu96@gmail.com
Kevin 
Bowen Whaleman - Technical writer: Whaleswhales507@gmail.com

import sys
import time
import random

inventory = []
health = 100

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
    random_event()
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
    global health
    print_pause("You take the left path and suddenly fall into a pit of snakes!")
    print_pause("You manage to escape, but you are bitten by a snake and lose 20 health points.")
    health -= 20
    if health <= 0:
        game_over()
    else:
        print_pause(f"Your current health is: {health}")
        dense_jungle()

def ancient_temple():
    print_pause("You take the middle path and find an ancient temple.")
    print_pause("Inside the temple, you find the legendary treasure!")
    print_pause("Congratulations! You have found the legendary treasure and completed your adventure.")
    game_won()

def quicksand():
    global health
    print_pause("You take the right path and find yourself sinking into quicksand!")
    print_pause("You manage to escape, but you are exhausted and lose 10 health points.")
    health -= 10
    if health <= 0:
        game_over()
    else:
        print_pause(f"Your current health is: {health}")
        dense_jungle()

def random_event():
    events = [
        "You find a healing herb and regain 10 health points.",
        "You encounter a wild animal and lose 15 health points.",
        "You find a hidden stash of supplies and add a rope to your inventory.",
        "You step on a trap and lose 20 health points."
    ]
    event = random.choice(events)
    print_pause(event)
    if "regain" in event:
        global health
        health += 10
    elif "lose" in event:
        health -= int(event.split("lose ")[1].split(" ")[0])
    elif "add" in event:
        inventory.append("rope")
    print_pause(f"Your current health is: {health}")
    if health <= 0:
        game_over()

def inventory_management():
    print_pause("Your current inventory: " + ", ".join(inventory))
    choice = input("Do you want to use an item? (yes/no) > ").lower()
    if choice == "yes":
        if "rope" in inventory:
            print_pause("You use the rope to climb out of a pit.")
            inventory.remove("rope")
        else:
            print_pause("You have no items to use.")
    elif choice == "no":
        print_pause("You decide not to use any items.")
    else:
        print_pause("Invalid choice. Please choose 'yes' or 'no'.")
        inventory_management()

def character_interaction():
    print_pause("You meet a mysterious stranger in the jungle.")
    print_pause("The stranger offers to help you in exchange for an item from your inventory.")
    choice = input("Do you want to trade an item? (yes/no) > ").lower()
    if choice == "yes":
        if inventory:
            item = input("Which item do you want to trade? > ").lower()
            if item in inventory:
                print_pause(f"You trade your {item} with the stranger.")
                inventory.remove(item)
                print_pause("The stranger gives you a map to the treasure.")
                inventory.append("map")
            else:
                print_pause("You don't have that item.")
        else:
            print_pause("You have no items to trade.")
    elif choice == "no":
        print_pause("You decide not to trade with the stranger.")
    else:
        print_pause("Invalid choice. Please choose 'yes' or 'no'.")
        character_interaction()

def puzzle_challenge():
    print_pause("You come across a locked door with a puzzle.")
    print_pause("Solve the puzzle to open the door.")
    puzzle = input("What is 5 + 3? > ")
    if puzzle == "8":
        print_pause("You solved the puzzle and the door opens.")
        ancient_temple()
    else:
        print_pause("Incorrect answer. Try again.")
        puzzle_challenge()

def combat():
    global health
    enemy_health = 30
    print_pause("You encounter a wild animal!")
    while enemy_health > 0 and health > 0:
        action = input("Do you want to fight or run? (fight/run) > ").lower()
        if action == "fight":
            damage = random.randint(5, 15)
            enemy_damage = random.randint(5, 15)
            print_pause(f"You attack the animal and deal {damage} damage.")
            enemy_health -= damage
            if enemy_health <= 0:
                print_pause("You defeated the animal!")
                break
            print_pause(f"The animal attacks you and deals {enemy_damage} damage.")
            health -= enemy_damage
            if health <= 0:
                game_over()
                return
            print_pause(f"Your current health is: {health}")
        elif action == "run":
            print_pause("You run away from the animal.")
            dense_jungle()
            return
        else:
            print_pause("Invalid choice. Please choose 'fight' or 'run'.")
    if health > 0:
        print_pause("You continue your journey.")

def save_game():
    with open("savegame.txt", "w") as file:
        file.write(f"{health}\n")
        file.write(",".join(inventory))
    print_pause("Game saved.")

def load_game():
    global health
    try:
        with open("savegame.txt", "r") as file:
            health = int(file.readline().strip())
            inventory.extend(file.readline().strip().split(","))
        print_pause("Game loaded.")
    except FileNotFoundError:
        print_pause("No saved game found.")

def start_game():
    global health
    health = 100
    inventory.clear()
    intro()
    first_choice()

if __name__ == "__main__":
    start_game()
