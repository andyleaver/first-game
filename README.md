# my first python text game
# room class
def __init__(self, location, description, exits):
    self.location = location
    self.description = description
    self.exits = exits


def get_location(self):
    return self.location


def get_description(self):
    return self.description


def get_exits(self):
    return self.exits

# what position is player in
def find_position(room_position, player_position):
    for position in room_position:
        if position.get_location() == player_position:
            return position

# is move allowed
def is_valid_move(new_location, current_position):
    return new_location in current_position.get_exits()


# game commands
exit_door = False
exit_locked_door = False
exit_unlocked_door = False
exit_window = False
exit_broken_window = False
look_chair = False
look_door = False
look_locked_door = False
look_unlocked_door = False
look_window = False
look_broken_window = False
look_rusty_key = False
get_rusty_key = False
move_chair = False
use_rusty_key = False
use_chair = False
open_door = False
open_locked_door = False
open_unlocked_door = False
open_window = False
open_broken_window = False

# game items
window = False
broken_window = False
door = False
locked_door = False
unlocked_door = False
key = False
rusty_key = False
chair = False
blood = False

# room layout [
##################################
# top      |   top    |      top #
# left     |  centre  |    right #
#          |          |          #
#__0,0_____|___0,1____|____0,2___#
#          |          |          #
# centre   | centre   |   centre #
# left     |          |    right #
#___1,0____|___1,1____|____1,2___#
#          |          |          #
#          |          |          #
# bottom   |  bottom  |   bottom #
# left     |  centre  |    right #
#  2,0     |   2,1    |    2,2   #
##################################

centre = room([1,1],"""
                 you start in the centre of the room
              you can move: north, south, east, west
""", [[0,1], [1,0], [2,1], [1,2]])

top_centre = room([0,1],"""
                       top centre
              you can move: east, south, west
""", [[0,2], [1,1], [0,0]])

top_left = room([0,0],"""
                        top left
               you can move: south and east
""", [[1,0], [0,1]])

top_right = room([0,2],"""
                       top_right
               you can move: south and west
""", [[1,2], [0,1]])

centre_left = room([1,0],"""
                       centre_left
               you can move: north, east, south
""", [[0,0], [1,1], [2,0]])

centre_right = room([1,2],"""
                       centre_right
               you can move: north, south, west
""", [[0,2], [1,1], [2,2]])

bottom_left = room([2,0],"""
                        bottom left
               you can move: north, east
""", [[1,0], [2,1]])

bottom_centre = room([2,1],"""
                         bottom centre
                you can move: north, east, west
""", [[1,1], [2,2], [2,0]])

bottom_right = room([2,2],"""
                          bottom right
                you can move: north, west
""", [[1,2], [2,1]])

player_location = room([1,1])
playing = True
while playing:
    check_location = player_location
    print("you are here > ", player_location)
    current_room = find_room(room_list, player_location)
    print(current_room.get_description())
    action = input("where would you like to move: ")
    if action == "north":
        check_location[0] += 1
        if is_valid_move(check_location, current_room):
            player_location = check_location
        else:
            print("sorry you can't move that way")
            check_location[1] -= 1
    elif action == "south":
        check_location[1] -= 1
        if is_valid_move(check_location, current_room):
            player_location = check_location
        else:
            print("sorry yoy can't move that way")
            check_location[1] += 1
    elif action == "east":
        check_location[0] += 1
        if is_valid_move(check_location, current_room):
            player_location = check_location
        else:
            print("sorry you can't move that way")
            check_location[0] -= 1
    elif action == "west":
        check_location[0] -= 1
        if is_valid_move(check_location, current_room):
            player_location = check_location
        else:
            print("sorry you can't move that way")
            check_location[0] += 1
    elif action == "help":
        print("""

       move_   example: move_north                            open_   example: open_door          
    north                                                   door              locked_door
    south                                                   window
    east                                                    unlocked_door
    west                                                    broken_window
    chair


       exit_    example: exit_broken_window                  look_   example: look_door
    broken_window         locked_door                      rusty_key        door
    door                                                   chair            locked_door
    window                                                 window           unlocked_door
    unlocked_door                                          broken_window


       get_     example: get_key                             use_      example: use_rusty_key
    rusty_key                                              rusty_key 
                                                           chair                         """)

    elif action == "look_chair":
        if look_chair:
            print("a wooden chair, maybe you can move/use it")
        else:
            look_chair = True
        print("a wooden chair")
    elif action == "look_rusty_key":
        if look_rusty_key:
            print("a rusty key, maybe you can use it!")
        else:
            look_rusty_key = True
        print("a rusty key")
    elif action == "look_door":
        if look_door:
            print("the door is locked, there is a keyhole")
        else:
            look_door = True
            print("a door")
    elif action == "look_locked_door":
        if look_locked_door:
            print("the door is locked, you need a key to unlock it")
        else:
            look_locked_door = True
            print("door is locked, ")
    elif action == "look_unlocked_door":
        if look_unlocked_door:
            print("you unlocked the door, now you can exit")
        else:
            look_unlocked_door = True
            print("")
    elif action == "look_window":
        if look_window:
            print("""
        the window is broken
                  maybe you can climb out!""")
        else:
            look_window = True
            print("the window looks like it is broken!")
    elif action == "look_broken_window":
        if look_broken_window:
            print("""
        a broken window, you might cut yourself if you try climbing out! 
                    example: use_broken_window """)
        else:
            look_broken_window = True
            print("a broken window")
    elif action == "open_unlocked_door":
        if open_unlocked_door:
            print("you opened the door, you can now finish the game")
        else:
            open_unlocked_door = True
            print("you opened the door")

    elif action == "open_door":
        if open_door:
            print("the door is locked, you need to unlock it")
        else:
            open_door = True
            print("its locked")
    elif action == "open_window":
        if open_window:
            print("the window is broken you cant open it")
        else:
            open_window = True
            print("its broken")
    elif action == "open_broken_window":
        if open_broken_window:
            print("you cant open the window, its broken!!!")
        else:
            open_broken_window = True
            print("")
    elif action == "unlock_door":
        print("you unlocked the door")

    elif action == "use_rusty_key":
        print("you used the rusty_key")
    elif action == "use_chair":
        print("a wooden chair")
    elif action == "exit_locked_door":
        if exit_locked_door:
            print("you cant exit through a locked door!!")
        else:
            exit_locked_door = True
            print("? its locked")
    elif action == "exit_door":
        if exit_door:
            print("the door is locked, you cant do that")
        else:
            exit_door = True
            print("its locked")
    elif action == "exit_broken_window":
        print("""
    You tried to climb out the broken window
         you cut your self!
           now you are bleeding!!""")
    elif action == "exit_window":
        print("the window is broken")
    elif action == "exit_unlocked_door":
        if exit_unlocked_door:
            print("""
                 Congratulations! 
        you have completed the game""")
        else:
            exit_unlocked_door = True
            print("""
        well done! 
            you found you way out""")
    elif action == "use_rusty_key":
        if use_rusty_key:
            print("""
        you tried the key in the door
    the rust seems to be stopping it from turning""")
        else:
            use_rusty_key = True
            print("it wont turn")
    elif action == "get_rusty_key":
        if get_rusty_key:
            print("already got the key!")
        else:
            get_rusty_key = True
            print("you got the key!")
    elif action == "move_chair":
        if move_chair:
            print("""
    already moved the chair!
      you see a rusty_key!""")
        else:
            move_chair = True
            print("you got the chair")
    elif action == "quit":
        print("you left the game")
        break
    else:
        print("sorry that doesnt work")
