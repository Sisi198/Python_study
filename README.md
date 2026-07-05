# Variable :  "A labeled box that holds a value"

A variable is a labeled box that holds a value. If you measure a participant's reaction time of 0.452 seconds and want to use it later, you need to store it somewhere. You do it like this:

reaction_time = 0.452

reaction_time
   ┌─────────────┐
   │    0.452    │
   └─────────────┘
   (box name)    (value inside the box)

## The most important thing: = does NOT mean "equals"

In math, = means "both sides are equal." But in Python, = is a command that means "put the value on the right into the box on the left." It has a direction: right → left.

reaction_time = 0.452

Read this as "put 0.452 into the reaction_time box," not "reaction_time equals 0.452."


## The value in the box can be changed

This is why it's called a "variable" (a value that can vary). When you measure the next participant, you can swap the value out.

    reaction_time = 0.452
    print(reaction_time)      # prints 0.452
    
    reaction_time = 0.681     # overwrites the value in the box
    print(reaction_time)      # now prints 0.681

The box stays the same; only its contents change.


##  Boxes can hold more than just numbers

      participant_id = 107          # a number
      participant_name = "Jimin"    # text (wrapped in quotes)
      mean_rt = 0.452               # a decimal


### Scenario: You have measured a single participant.

    1. Store the value `205` inside a variable named **`participant_id`**.
    2. Store the value `0.87` inside a variable named **`accuracy`**.
    3. Output both variables using separate **`print()`** functions to verify that the values were stored correctly.
    

## Going a bit deeper into variables — changing what's inside the box)

### Scenario. A participant scored 0.87 accuracy in practice trials, then 0.93 in the main trials

    1. Put 0.87 into a box called accuracy, and print(accuracy).
    2. Below that, put 0.93 into the SAME accuracy box, and print(accuracy) again.
    3. Check how many lines print, and how the value changes.)

Key point: there's only ONE box called accuracy. You didn't create a second box — you overwrote the same box's contents from 0.87 to 0.93.

This matters later for loops — when a trial runs 20 times, one box called current_trial keeps getting overwritten: 1 → 2 → 3 → ... → 20. Not 20 separate boxes, just one box being updated repeatedly. What you just did is the exact same mechanism.

### Scenario.  Also want to see it in milliseconds (ms).

    1. Put 0.452 into a box called reaction_time_sec.
    2. Put reaction_time_sec multiplied by 1000 into a box called reaction_time_ms.
    3. Print both boxes.

[variable info.py](https://github.com/user-attachments/files/29670802/variable.info.py)
Python 3.14.5 (v3.14.5:5607950ef23, May 10 2026, 07:38:09) [Clang 21.0.0 (clang-2100.0.123.102)] on darwin
Enter "help" below or click "Help" above for more information.
>>> participant_id = 205
>>> pritn(particpant_id)
Traceback (most recent call last):
  File "<pyshell#1>", line 1, in <module>
    pritn(particpant_id)
NameError: name 'pritn' is not defined. Did you mean: 'print'?
>>> participant_id = 205
>>> print(participant_id)
205
>>> accuracy = 0.87
>>> print(accuracy)
0.87
>>> accuracy = 0.93
>>> print(accuracy)
0.93
>>> reaction_time_sec = 0.452
>>> print(reaction_time_sec)
0.452
>>> reaction_time_ms = reaction_time_sec * 1000
>>> print(reaction_time_ms)
452.0





