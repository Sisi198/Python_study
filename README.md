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


# Data types 

## Int

Code EX: 

      participant_id = 205
      trial_number = 12
      n_trials = 40

## float

Code EX:

   reaction_time = 0.452
   accuracy = 0.87
   mean_rt = 452.0

## string, str

Code EX: 

   participant_name = "Sisi"
   group = "experimental"
   condition = "congruent"

## boolean, bool (TRUE or FALSE)

Code EX: 

   is_correct = True
   is_timeout = False


## Checking the types of data

: type()

Code EX: 

   reaction_time = 0.452
   print(type(reaction_time))    # <class 'float'>
   
   participant_name = "Jimin"
   print(type(participant_name)) # <class 'str'>


### Scenario: Organising a single participant's experimental results.

      1. Store the integer `314` inside a variable named **`participant_id`**.
      2. Store the string `"incongruent"` inside a variable named **`condition`**.
      3. Store the float `0.673` inside a variable named **`rt`**.
      4. Store the boolean `True` inside a variable named **`is_correct`**.
      5. Output each variable using **`print(type(...))`** to verify that the 4 variables correctly display as **int**, **str**, **float**, and **bool**.


# Mixing Data Types: What Happens Next?

## Run This Code and Predict the Outcome

Create a temporary script or use your interactive window to run the following block. Don't worry about whether it throws an error or runs successfully—simply observe the outcome and share what you see:

      participant_id = 314
      message = "Participant " + participant_id


<img width="1202" height="178" alt="Screenshot 2026-07-06 at 6 00 24 pm" src="https://github.com/user-attachments/assets/e3ee3590-3680-48e9-bc26-110e1dca9682" />

## Why Did This Error Occur?

"+" concatenates strings together, but string + integer isn't automatic — Python refuses because it doesn't know how to combine two different types.

    5 + 3                    # ✅ 8  (int + int)
   "a" + "b"                 # ✅ "ab"  (str + str)
   "participant" + 314       # ❌ TypeError (str + int, mixed)


### Solution 1: Explicit Type Casting using str()

Code EX:   
      participant_id = 314
      message = "Participant " + str(participant_id)
      print(message)    # Output: Participant 314

### Solution 2 (Much Cleaner): Embracing f-strings

Code EX:
      participant_id = 314
      message = f"Participant {participant_id}"
      print(message)    # Output: Participant 314


## Scenario: Combining a participant's group designation and baseline accuracy score into a single unified log string.

      group = "control"
      accuracy = 0.91
      
      1. Using str(): Construct and output the string "Group: control, Accuracy: 0.91" by combining the + operator and the explicit str() function.
      
      2. Using an f-string: Recreate the exact same output sentence using a single f-string.
      
      3. Verify that both methods yield identical text blocks in your console.

### Checking the codes:

1. Using str():

<img width="1194" height="134" alt="Screenshot 2026-07-06 at 6 11 29 pm" src="https://github.com/user-attachments/assets/0a685ec5-b507-483e-ba4f-4cf2d2dad912" />

Grammatically correct, but no space was inserted between "control" and "accuracy" — with + concatenation, Python just glues strings together; you have to manually add spaces.)

 2. Using an f-string:

<img width="1200" height="78" alt="Screenshot 2026-07-06 at 6 12 29 pm" src="https://github.com/user-attachments/assets/f5db2746-b55f-4708-8772-86274c03d77c" />

Key point: the + inside the quotes is just a literal character being printed, not an addition operator. Anything outside { } in an f-string prints exactly as typed.


<img width="1216" height="100" alt="Screenshot 2026-07-06 at 6 13 15 pm" src="https://github.com/user-attachments/assets/3eba59ea-4709-49d4-a68f-50ea6695bfac" />


# Operators

# Arithmetic Operators

   * `+`  **Addition**
   * `-`  **Subtraction**
   * `*`  **Multiplication**
   * `/`  **Division** (Always returns a float/decimal result)
   * `//` **Floor Division** (Discards the decimal part, returns the quotient only)
   * `%`  **Modulo** (Returns the remainder only)


Code EX: 

n_correct = 15
n_total = 20

accuracy = n_correct / n_total
print(accuracy)     # 0.75

## Scenario: Calculating the mean of 3 reaction times (in seconds).

      rt1 = 0.45
      rt2 = 0.52
      rt3 = 0.61
      
      1. Add the three values together and store the result inside a variable named total_rt.
      
      2. Divide total_rt by 3 and store the result inside a variable named mean_rt.
      
      3. Output the result using an f-string in the following format: "Mean RT: 0.527s" (rounded to 3 decimal places).


### How f-string Float Formatting Works

   1. f"{mean_rt}" $\rightarrow$ "0.5266666666666667" (No formatting applied; prints the raw, original value)
   2. f"{mean_rt:.3f}" $\rightarrow$ "0.527" (Rounds to 3 decimal places)
   3. f"{mean_rt:.1f}" $\rightarrow$ "0.5" (Rounds to 1 decimal place)
   4. f"{mean_rt:.0f}" $\rightarrow$ "1" (Rounds to 0 decimal places, behaving like an integer)

* The colon (:) acts as a separator indicating that formatting rules follow.

* The period (.) signals that you are specifying the precision for the fractional (decimal) part.

* Breaking it down: .3 means "how many decimal places", f means "format as a float". You'll use this constantly when presenting experiment results — nobody reports accuracy as 0.5266666666666667

Q. Is storing it in a message variable mandatory? 

* You can feed an f-string directly into a print() function, and it will execute identically:

  #### Approach A: Store in a variable first, then print
      message = f"Mean RT: {mean_rt:.3f}"
      print(message)
   
  #### Approach B: Print directly (Skip creating the intermediate variable)
      print(f"Mean RT: {mean_rt:.3f}")


Creating an intermediate variable like message only earns its keep when you intend to re-use that exact string elsewhere in your script—for instance, if you need to print the text to the terminal window and write it to an external .txt log file simultaneously. 

If your objective is simply to display it once and move on, printing it directly via print(f"...") is much more concise.


## Scenario. The experiment consists of a total of 45 trials, and I plan to provide a short break every 10 trials.

      1. Check the result of dividing n_trials by 10 (/). → How many "complete sets of 10" will we get?
      
      2. Check the result of floor dividing (//) n_trials by 10. → What is the difference between the two?
      
      3. Check the result of the modulo operation (%) on n_trials by 10 (the remainder). → What does this signify?


<img width="1230" height="322" alt="Screenshot 2026-07-12 at 1 32 15 pm" src="https://github.com/user-attachments/assets/25e143aa-b6ff-4b3f-b5b4-9b32b9e88e35" />


/ → 4.5

This is the value that accurately calculates "how many sets of 10 there are," down to the decimal. It means there are 4 sets, with the remaining half (0.5 sets) left over.

// → 4

It calculates only the quotient as a whole integer. It is used when you want to say, "Discard the remainder; I only want to know the number of completely filled sets." // is commonly called integer division or floor division.

% → 5

It represents "5 actual leftover trials" based on the raw trial count. In other words, if you divide 45 trials by 10, you fill 4 sets (40 trials), and 5 trials are left over, unable to make a full set. (The 5 isn't "0.5 of a trial" — it's 5 actual leftover trials: 4 full sets of 10 = 40 trials, and 5 trials remain uncounted.)

### Why this is useful in experiment code

Code EX: 

current_trial = 20

if current_trial % 10 == 0:
    print("Take a break!")

* If the remainder when dividing current_trial by 10 is 0 (meaning the 10th, 20th, 30th... trial), the break message appears exactly at that moment.

# Comparison Operators

   == : equal
   
   != : Not equal
   
   < : smaller than 
   
   > : Bigger than
   
   <= : smaller than or equal to
   
   >= : bigger than or equal to

Always returns in True/False


## Scenario: Check whether the participant's response time exceeded the timeout limit (1.5 seconds) and whether they answered correctly.

      rt = 1.72
      timeout_limit = 1.5
      correct_answer = "space"
      participant_response = "space"

1. Compare whether `rt` is greater than (exceeded) `timeout_limit`, store the result in the `is_timeout` box, and `print()` it.
2. Compare whether `participant_response` is equal to `correct_answer`, store the result in the `is_correct` box, and `print()` it.
3. Predict whether each of the two results will be `True` or `False` first, and then run the code to verify if your prediction is correct.

<img width="1108" height="466" alt="Screenshot 2026-07-12 at 1 54 17 pm" src="https://github.com/user-attachments/assets/3421d254-dc2c-429d-ab1d-2dfc58c98f98" />

<img width="1108" height="466" alt="Screenshot 2026-07-12 at 1 54 17 pm" src="https://github.com/user-attachments/assets/ccfc579d-0222-4900-9bef-1e10059cf959" />

   1. variable name

      : Since this value stores whether a timeout occurred rather than correctness, a name like is_timeout would be more appropriate. Because the name is_correct was reused twice, the first is_correct was actually overwritten by the second line (remember the "overwriting values inside a box" concept from last time?). Consequently, the value storing the timeout status is not preserved in this code.

   2. The comparison itself differs from the request
      
      : The request asked whether rt was greater than (exceeded) timeout_limit, but the code uses the equality operator (==).

            timeout_limit == rt     # "Is 1.5 equal to 1.72?" → False (because they are not equal)
            rt > timeout_limit       # "Is 1.72 greater than 1.5?" → This is what needs to be asked
         While 1.72 == 1.5 is naturally False, this does not mean "a timeout did not occur"; it simply means "the two numbers are different." 
         In reality, since rt = 1.72 is greater than timeout_limit = 1.5, a timeout has indeed occurred. The current code does not reflect this fact.

<img width="1210" height="550" alt="Screenshot 2026-07-12 at 2 05 36 pm" src="https://github.com/user-attachments/assets/45c9fc14-8449-44d9-9629-9fee24ae4b5e" />

# Conditional Statements (if / elif / else)

Conditional statements allow us to create "actions that change based on conditions" using the True/False values we have built so far, such as is_correct and is_timeout.

* Basic Structure

  if condition:

  Code to execute when the condition is True

* Code EX:

        rt = 1.72
      timeout_limit = 1.5
      
      if rt > timeout_limit:
          print("Timeout! Trial skipped.")

: Since rt > timeout_limit is True, the print(...) line is executed, and "Timeout! Trial skipped." is printed. If rt had been 1.2, the condition would be False, and the print inside would be completely skipped without running.

if rt > timeout_limit:      # 1) A colon (:) is mandatory at the end of the condition
    print("Timeout!")        # 2) The next line must be indented (usually 4 spaces)

* else — When the Condition is False

        rt = 1.2
      timeout_limit = 1.5
      
      if rt > timeout_limit:
          print("Timeout! Trial skipped.")
      else:
          print("Response recorded in time.")

: Since rt is 1.2, the condition evaluates to False. The if block is skipped, and the else block executes, printing "Response recorded in time.". Either if or else will run—never both.

* elif — When There Are Multiple Conditions

  This is used when you need three or more branches of logic, like "If A, do this; else if B, do that; otherwise, do this":

        accuracy = 0.55
      
      if accuracy >= 0.9:
          print("Excellent performance")
      elif accuracy >= 0.7:
          print("Good performance")
      else:
          print("Needs improvement")

:  Since accuracy = 0.55: the first condition (>= 0.9) → False, the second condition (>= 0.7) → also False, so it ultimately drops down to the else block and prints "Needs improvement". Python checks conditions sequentially from top to bottom, stops exactly where it encounters the first True, and skips the rest.

### Scenario: Provide different feedback depending on whether the participant's response is correct or incorrect.

   correct_answer = "space"
   participant_response = "enter"

   1. If participant_response is equal to correct_answer, print "Correct!".
   
   2. If they are not equal, print "Incorrect.".
   (Use if / else to handle both cases)
   
   3. Predict which result will appear first, then run the code to verify.


<img width="1192" height="188" alt="Screenshot 2026-07-12 at 3 22 56 pm" src="https://github.com/user-attachments/assets/8306e7d2-3c4d-4b8f-887a-848c0e403df5" />


### Scenario: Provide a three-stage feedback based on the participant's accuracy.

      accuracy = 0.78
      
      1. If accuracy is 0.9 or higher, print "Excellent performance".
      
      2. Otherwise, if it is 0.7 or higher, print "Good performance".
      
      3. If neither condition is met, print "Needs improvement".
      
      (Use all three: if / elif / else)

<img width="1186" height="486" alt="Screenshot 2026-07-12 at 3 22 03 pm" src="https://github.com/user-attachments/assets/11eec6c3-9019-4733-ba49-1e8eaacd77d3" />

# Combining Multiple Conditions: and, or

In experiment code, situations often arise where "this condition AND that condition must both be met." For example, a trial might only be counted as a "success" if the participant answered correctly and responded within the time limit.

      and: Both conditions must be True for the whole expression to be True.
      
      or: The whole expression is True if at least one of the conditions is True.

   is_correct = True
   is_timeout = False
   
   if is_correct and not is_timeout:
       print("Success: correct and in time")
   else:
       print("Failed: either wrong or too slow")
   
is_correct is True. is_timeout is False, but adding not flips it, making not is_timeout evaluate to True. Ultimately, it becomes True and True, so the overall condition is True, and the "Success" message is printed.

### Scenario: Print "Valid trial: correct and fast" only if the participant answered correctly and their response time was within 1.5 seconds. Otherwise, print "Invalid trial".

      is_correct = True
      rt = 1.8
      timeout_limit = 1.5

      Compare whether rt is less than timeout_limit, and store the result in the is_in_time box.

      Combine is_correct and is_in_time using and to create your condition.
      
      If the condition is True, print "Valid trial: correct and fast". If it is False, print "Invalid trial".


<img width="1208" height="426" alt="Screenshot 2026-07-12 at 3 39 38 pm" src="https://github.com/user-attachments/assets/28c6d1ef-669d-4cf6-a35e-2ad381e9e833" />


