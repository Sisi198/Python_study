# Python_study

# Data Types

: A type is how Python represents different types of data

EX:

* 11 : integers

* 21.213 : real number

* Hello Python 101 : words

integers, real numbers, and words cab be expressed as different data types

<img width="1668" height="2154" alt="image" src="https://github.com/user-attachments/assets/fdff80e0-f247-4146-a36e-e10a12c1f594" />

## Can see the actual data type in Python by using the type command

<img width="1212" height="336" alt="Screenshot 2026-05-13 at 5 45 38 pm" src="https://github.com/user-attachments/assets/dba26e0c-4414-4559-abc0-ffd4dacd5da9" />

# Data type: int / float / string 

<img width="1668" height="2154" alt="Python Basic-2" src="https://github.com/user-attachments/assets/e8fd3a85-22ae-4363-aac9-eb0590a20ed2" />

<img width="1668" height="2154" alt="Python Basic-3" src="https://github.com/user-attachments/assets/63af7c63-030c-4568-8f47-679c0001549c" />

# Changing expression type

<img width="1454" height="825" alt="image" src="https://github.com/user-attachments/assets/d6323091-114f-449b-9490-38fa86e5b1d7" />

<img width="1052" height="356" alt="Screenshot 2026-05-13 at 5 54 09 pm" src="https://github.com/user-attachments/assets/a2a45665-f786-4892-a557-9a63ad2ddeb2" />


# Converting int to string

<img width="1516" height="1070" alt="image" src="https://github.com/user-attachments/assets/7a34539b-ec36-4723-a349-905bed824030" />

<img width="444" height="158" alt="Screenshot 2026-05-13 at 5 57 11 pm" src="https://github.com/user-attachments/assets/084dc153-68ff-4c70-ad48-3dd6098d63ef" />

In Python, when you want to convert an integer (**int**) or a floating-point number (**float**) into a string (**string**), you use the `str()` function.

### 1. Converting an Integer to a String (int → string)

This corresponds to the `str(1)` example at the top of your reference.

* **Input:** `1` is an integer (int), a numeric format used for calculations.
* **Process:** You place the number inside the parentheses of the function: `str(1)`.
* **Result:** It becomes `"1"`, with quotation marks added. From this point on, Python treats it as text (string) rather than a number.

### 2. Converting a Float to a String (float → string)

This is shown in the `str(4.5)` example at the bottom.

* **Input:** `4.5` is a floating-point number (float) that includes a decimal point.
* **Process:** Pass it through the same `str(4.5)` function.
* **Result:** It is converted into the string `'4.5'`.

---

### Why do we perform this conversion?

The primary reason is that Python does not allow you to directly add (concatenate) a string and a number. For example, you cannot add the text `"My score is "` to the number `100` directly. You must first convert the number into a string so they can be combined or printed together as text.

```python
# Error Example
print("Score: " + 100) # This will cause a TypeError

# Correct Example
print("Score: " + str(100)) # Result: "Score: 100"

```
<img width="984" height="212" alt="Screenshot 2026-05-13 at 6 00 05 pm" src="https://github.com/user-attachments/assets/b503b54a-68cd-438f-96a9-de5d6a14c4ec" />

# Data types: Boolean

Boolean is a data type that can only have one of two values: True or False. You can think of it as the computer's most basic logic, representing "Yes/No" or "On/Off."

<img width="1668" height="2154" alt="Python Basic-5 2" src="https://github.com/user-attachments/assets/6782bcf1-9a39-409a-a414-0dedf12a1c77" />

<img width="382" height="274" alt="Screenshot 2026-05-13 at 6 06 19 pm" src="https://github.com/user-attachments/assets/e38c0545-12e2-4ce0-97b8-d22472a61d2c" />


## In Python, Booleans have the following characteristics:

### 1. Only Two Values Exist

 * True: Represents "Yes" or "Correct." (Note: In Python, the first letter must be capitalised!)

 * False: Represents "No" or "Incorrect."

### 2. When are they used?
Booleans are primarily generated as results when you compare values or check conditions. Unlike converting numbers, this belongs to the realm of logic.

### Example 1 (Comparison):

If you input 10 > 5, Python answers True.

If you ask 3 == 4 (Is 3 equal to 4?), it answers False.

### Example 2 (Conditional Statements):

Booleans play a critical role when building logic like: "If (if) the user is logged in (True), show the My Page."

#### 1. the Boolean (True/False) acts as a "Pass/Fail notice."

is_logged_in = True  # Assuming the user is logged in (Boolean)

if is_logged_in:
    print("Accessing My Page...")
else:
    print("Login required.")

#### 2. How it works
Condition Check: Python checks whether the value immediately following the if is True or False.

The Fork in the Road:

If the value is True: The code directly under the if is executed.

If the value is False: The code under the else (meaning "otherwise") is executed.

#### 3. Real-life Analogies

Sensor Light: "Is motion detected?" → If True, turn on the light; if False, keep it off.

Vending Machine: "Is the inserted amount greater than the drink price?" → If True, dispense the drink; if False, display "Insufficient funds."

# Practical challenge

<img width="1264" height="1442" alt="Screenshot 2026-05-13 at 6 19 01 pm" src="https://github.com/user-attachments/assets/6901f041-25d0-4a20-8288-441033c9749c" />

**Why does the error occur?**

You were still inside the if and else blocks (indicated by the ... prompt) when a single space was entered before the print command.

Python's Rule: Python is extremely sensitive to indentation. If there is a space at the beginning of a line that isn't part of an if or else block, Python will throw a SyntaxError because it doesn't understand why that space is there.

Current State: The red-highlighted area before the letter 'p' in the middle of the image shows exactly where that incorrect space is located.

<img width="1122" height="1076" alt="Screenshot 2026-05-13 at 6 22 38 pm" src="https://github.com/user-attachments/assets/a1d7ad48-fcba-4cec-a811-2289701da838" />


# Expression

: Describe a type of operation the computer performs.

## Mathematical Operation

1. Numbers: operands
2. Math symbols: operators

<img width="1436" height="560" alt="Screenshot 2026-05-14 at 2 34 50 pm" src="https://github.com/user-attachments/assets/e30ed68b-db16-4ab4-8546-145acbe1b91f" />

Note. Basic arithmetic operations like adding multiple numbers

<img width="204" height="286" alt="Screenshot 2026-05-14 at 2 36 07 pm" src="https://github.com/user-attachments/assets/aa3d836e-6487-4148-bc12-c1ea966b0417" />

<img width="1546" height="472" alt="Screenshot 2026-05-14 at 2 36 21 pm" src="https://github.com/user-attachments/assets/295bef47-9346-4147-8ca1-567e1831ef98" />

## Curiosity 1. Why are the results different? (Types of Division)

* Python clearly distinguishes between two ways of performing division:

1. / (Normal Division): Division we learned in math class. Even if a number divides perfectly, Python provides the exact value, including decimal places, resulting in a float. For example, while $25 / 5$ divides evenly, Python outputs it as 5.0.

2. // (Floor Division): This discards everything after the decimal point and leaves only the "integer part," or the quotient. This is why in your image, $25 // 6$ results in 4 rather than 4.166....

## Curiosity 2. Does it always work this way?

* Mostly yes, but there are a few extra rules: 

1. The / operator always returns a float, regardless of the numbers being divided.

2. The // operator generally tries to return an int. However, if even one of the numbers involved is a float (e.g., $25 // 6.0$), the result will be a float like 4.0 (though the decimal part is still discarded).


## Examples in Psychology Research

: In psychology research, these operators are used differently when organising data or assigning participants: 

1. Normal Division (/): Used when calculating average scores for questionnaire items (e.g., an average depression scale score of $3.42$).

2. Floor Division (//): Useful for assigning participants equally into groups or calculating the total number of pages needed by dividing the total number of items by the number of items shown per page.

# Practise Challenge:

<img width="1076" height="530" alt="Screenshot 2026-05-14 at 2 58 18 pm" src="https://github.com/user-attachments/assets/5f8e4009-a3b2-4a14-9ee4-0fe52a591ec8" />


Note. Extra Tip (Modulo operator %) : Number of items left on the last page


### Note. use / when the "exact value" is important, and use // when "how many groups/chunks" is what matters! Let me know if you have any other questions.

# Variables

* We can use the variables to store the values

* In this case, we assign a value of 1 to the variable "my_varaible" using the assignment operator, i.e. the equal sign

  <img width="1098" height="428" alt="Screenshot 2026-05-14 at 3 02 01 pm" src="https://github.com/user-attachments/assets/0c4ed824-bbd3-4b76-b5cd-9b163767fdf4" />

* We can then use the value somewhere else in the code by typing the exact name of the variable

* We will use the clown to denote the value of the variable

  <img width="1388" height="610" alt="Screenshot 2026-05-14 at 3 02 42 pm" src="https://github.com/user-attachments/assets/f42c7c9c-aa07-4edb-9af4-6c0dcb472e32" />

# Example: 

<img width="842" height="1236" alt="Screenshot 2026-05-14 at 3 03 38 pm" src="https://github.com/user-attachments/assets/9045d1a0-b051-40be-bf22-5301c884f0a0" />

<img width="1356" height="672" alt="Screenshot 2026-05-14 at 3 33 49 pm" src="https://github.com/user-attachments/assets/9fb8fa23-8a5e-429d-9186-0cd1850d7f6f" />


# String Operations

* Strings: 

1. A sequence of characters contained within 2 quotes: ex) "Michael Jackson"

2. Also use a single quote: ex) 'Michael Jackson'

3. Can be spaces or digits: ex) 123456

4. Can be special characters: ex) ?><$%#@


We can bind or assign a string to another variable. It is helpful to think of a string as an ordered sequence. 

Each element in the sequence can be accessed using an index represented by an array of numbers.


<img width="1042" height="904" alt="Screenshot 2026-05-14 at 3 38 08 pm" src="https://github.com/user-attachments/assets/89661e8f-a775-415b-b943-75bf2f53941d" />


By using, to merge, repeat, or extract specific parts of text data. In psychology research, these are frequently utilised for tasks such as generating participant identification codes or setting data file paths.


## 1. Main Types of Operations

* Addition (+): Connects two strings together (e.g., combining a first name and last name).

* Multiplication (*): Repeats a string a specified number of times (e.g., printing a divider line).

* Indexing/Slicing: Extracts specific characters from a string.

  
## 2. Applications in Psychology Research


* ID Generation: Creating unique IDs by combining participant initials and birth years.

* Stimulus Presentation: Essential for combining text, such as "Hello, [Participant Name]. The test will now begin".

* File Management: Useful for automatically generating filenames based on versions, like data_v1.csv or data_v2.csv.

# Practice challenges (1): ID Generation & f-strings

<img width="1206" height="524" alt="Screenshot 2026-05-14 at 4 00 53 pm" src="https://github.com/user-attachments/assets/af84dd46-a0c5-4822-bacf-a429d737ab21" />

# Practice challenges (2): To read an Excel file, process data, and save it back

1. Import pandas as pd: Import the library for Excel processing
   
<img width="1006" height="286" alt="Screenshot 2026-05-14 at 11 21 58 pm" src="https://github.com/user-attachments/assets/e37fbc90-7ea8-4af3-a398-3c37e0129c41" />


2. Loading the Excel file with Python: In actual research, this single line brings Excel data into Python.

<img width="812" height="42" alt="Screenshot 2026-05-14 at 11 22 48 pm" src="https://github.com/user-attachments/assets/a1637d23-a2f7-4f5a-9e9a-b2d954b8d33a" />

3. Generating participant codes using string operations: To create a new column in the format of 'name_age'.
   Within pandas, .astype(str) is used to convert numbers into strings

   <img width="1236" height="186" alt="Screenshot 2026-05-14 at 11 24 07 pm" src="https://github.com/user-attachments/assets/c61a3031-8201-4d93-b877-15dbfdb1cdee" />

4. Exporting processed data back to Excel

   <img width="1220" height="222" alt="Screenshot 2026-05-14 at 11 24 41 pm" src="https://github.com/user-attachments/assets/ca352bcb-f2b3-4680-b870-9e29cb3644f5" />

   <img width="782" height="590" alt="Screenshot 2026-05-14 at 11 26 18 pm" src="https://github.com/user-attachments/assets/f583f832-9cdf-472f-9952-2e5e1a5b36e1" />


# Key Explanations

1. **pd.read_excel()**: This command "attaches" (loads) an Excel file into Python. It can bring in data for thousands of participants into a table format instantly.

2. **df_study['name'] + "_" + ...**: This applies the String Operations (+) to the entire Excel dataset at once. There is no need to manually copy and paste formulas in Excel.

3. **to_excel()**: This command converts the results worked on in Python back into an Excel file.


#  Stimulus Presentation; practise challenges

## Simulated psychology experiment workflow

### 1. Participant Info (Usually loaded from Excel, but set as variables here for practice)

<img width="1198" height="60" alt="Screenshot 2026-05-19 at 2 17 00 pm" src="https://github.com/user-attachments/assets/ef117b70-a558-4bff-a54a-a2feb4e9554b" />

### 2. First Stimulus: Greeting & Instructions (Using String Operations)

### f-strings let us seamlessly insert variables directly into a sentence.

<img width="1214" height="170" alt="Screenshot 2026-05-19 at 2 17 44 pm" src="https://github.com/user-attachments/assets/f0e0f702-24ab-47b3-b875-06c09853f755" />

### 3. Second Stimulus: Presenting the question and capturing a response

<img width="1180" height="118" alt="Screenshot 2026-05-19 at 2 18 40 pm" src="https://github.com/user-attachments/assets/51e12892-ccd6-4dc7-8539-efa00563216c" />

### input() is a function that halts the script and waits for keyboard input from the user.

<img width="1228" height="366" alt="Screenshot 2026-05-19 at 2 19 33 pm" src="https://github.com/user-attachments/assets/b8f3b833-9257-47d2-a786-78182eeb722a" />


## * Error: The Mechanism Behind the Error
    
    * When response = input("Enter your choice (1-5): ") runs, Python pauses and waits for keyboard input.
    
    * If you press Enter without typing anything, the response variable captures an empty string: "".
    
    * In the very next line, you executed int(response), which translates to int("")—a command telling Python to "convert an empty text into an integer."
    
    * Since Python cannot translate absolute emptiness or blank space into a number, it raises a ValueError, essentially stating: "This is not a valid piece of text to turn into a base-10 integer."

### 4. Response Verification & Data Categorisation

### User input always enters Python as a 'string'. We must convert it to an int to use math/logic.

<img width="1192" height="184" alt="Screenshot 2026-05-19 at 2 20 38 pm" src="https://github.com/user-attachments/assets/167d2ec3-e504-411d-b472-38b3dfe7ccdd" />

### 5. Result Summary (This data can later be exported to Excel)

<img width="1194" height="212" alt="Screenshot 2026-05-19 at 2 21 09 pm" src="https://github.com/user-attachments/assets/272745e1-0800-4208-8b68-a1a0e1ea5484" />


# Slicing 

* It is helpful to think of a string as a list or tuple: we can treat the string as a sequence and perform sequence operations.

<img width="1418" height="594" alt="Screenshot 2026-05-19 at 1 54 59 pm" src="https://github.com/user-attachments/assets/59431976-4c06-43ee-8519-76b84cf08e40" />

# Stride

* We can also input a stride value as follows:

    * The two indicate, we'd select every second variable
 
<img width="1466" height="566" alt="Screenshot 2026-05-19 at 1 56 25 pm" src="https://github.com/user-attachments/assets/9527f970-b9a9-4302-a062-f36d549948df" />

<img width="1570" height="696" alt="Screenshot 2026-05-19 at 2 45 06 pm" src="https://github.com/user-attachments/assets/ad4c1e74-1adc-4bc1-a660-c2babdd491e1" />


## Applications in Psychology Research

* Extracting Sub-identifiers (Slicing): If a participant ID follows a strict notation like 2026SisiA, you can use slicing to isolate the 4-digit year, the name, or the group condition letter separately.

* Split-Half Reliability (Stride): When psychometrically validating a questionnaire, researchers often calculate split-half reliability by separating odd-numbered items from even-numbered items to correlate them. A stride of 2 allows you to split these items in a single line of code.

## Example 1: Extracting info from a participant code (Slicing)

<img width="1202" height="32" alt="Screenshot 2026-05-19 at 2 40 41 pm" src="https://github.com/user-attachments/assets/9c667ee5-e6ae-4f25-8eb2-c39a6d7f9662" />


### Slice the first 4 characters (indices 0, 1, 2, 3)

<img width="1216" height="82" alt="Screenshot 2026-05-19 at 2 41 06 pm" src="https://github.com/user-attachments/assets/79beac1b-5085-4a9f-a3fb-f139ee838a84" />


### Slice from index 4 up to (but excluding) index 8

<img width="1216" height="84" alt="Screenshot 2026-05-19 at 2 41 35 pm" src="https://github.com/user-attachments/assets/a3743420-cab8-47f5-aab7-c0afa3d03709" />


## Example 2: Splitting odd/even items for reliability checks (Stride)

### A participant's response scores for items 1 through 8

<img width="1216" height="32" alt="Screenshot 2026-05-19 at 2 42 19 pm" src="https://github.com/user-attachments/assets/bb789b82-860d-4fd8-af68-d6249f56a991" />

### [start at 0 :: step by 2] -> Extracts indices 0, 2, 4, 6 (Items 1, 3, 5, 7)

<img width="1202" height="30" alt="Screenshot 2026-05-19 at 2 42 56 pm" src="https://github.com/user-attachments/assets/7005feed-5863-4ce5-82e7-d7653c1f6038" />

### [start at 1 :: step by 2] -> Extracts indices 1, 3, 5, 7 (Items 2, 4, 6, 8)

<img width="1198" height="38" alt="Screenshot 2026-05-19 at 2 43 22 pm" src="https://github.com/user-attachments/assets/0b6607d6-ad5b-492c-9810-e7a49a84afa2" />

### Results:
<img width="1198" height="272" alt="Screenshot 2026-05-19 at 2 43 40 pm" src="https://github.com/user-attachments/assets/f0452301-90d6-4967-b16e-3e998c97963c" />


# Tuples: Slicing

* Use the len command to obtain the length of the string. - As there are 15 elements, the result is 15

  <img width="976" height="308" alt="Screenshot 2026-05-19 at 2 47 23 pm" src="https://github.com/user-attachments/assets/39f8fdae-3c70-4ae4-9cfa-cb890175bd18" />

## What exactly is a Tuple?

* A tuple is an "unalterable data bundle whose contents can never be changed."

  * Syntax: Unlike a List, which uses square brackets [ ], a Tuple is created using parentheses ( ). (e.g., my_tuple = (1, 2, 3))
 
  * Core Characteristic (Immutability): Once constructed, elements cannot be added, removed, or modified.

### Why use Tuples in psychology research?

* Tuples are used to safely lock away critical reference values or parameters that must never fluctuate during an experiment.

    * Fixed stimulus presentation intervals: (0.5, 1.0, 1.5, 2.0)
    
    * The baseline monitor resolution settings: (1920, 1080)
    
    * Fixed group criteria or demographic categories: ("Male", "Female")

* Even if you make a mistake in your script and accidentally try to alter these values, Python will instantly raise an error and halt the program, shielding your experimental design from accidental corruption.

## When do we use Tuple Slicing?

* Using Tuple Slicing when you want to safely copy out a specific segment of data from a fixed tuple:

    * Scenario: Extracting only the first 3 presentation times out of a 10-stimulus calibration sequence.
    
    * Scenario: Isolating a specific Region of Interest (ROI) from a fixed array of EEG channel names.
 
## Practise challenges; Tuple Slicing :

### 1. Defining fixed experimental stimulus intervals (seconds) as a Tuple

<img width="1202" height="36" alt="Screenshot 2026-05-19 at 2 59 35 pm" src="https://github.com/user-attachments/assets/4ee882cf-9e86-475a-b868-985eaa031727" />

### 2. Tuple Slicing (Extracting indices 1 up to, but excluding, 4)

### The raw data is left untouched; the snippet is copied into a 'new tuple'.

<img width="1192" height="184" alt="Screenshot 2026-05-19 at 3 00 10 pm" src="https://github.com/user-attachments/assets/bdce1909-ddc4-4364-b4fc-d0b000690135" />

### 3. Testing the absolute rule of Tuples (Error Test)

<img width="1230" height="838" alt="Screenshot 2026-05-19 at 3 00 47 pm" src="https://github.com/user-attachments/assets/d79922e6-04e2-46e3-936c-c495571b5542" />



### Curiosity: What if I would like to change the settings of the stimulus in the experiments?


### A: In situations like that, instead of modifying the tuple itself, you should either directly update the numbers in your Python script file or redesign your data container into a List configuration depending on your experimental needs.

### 1. Modifying the Experimental Design Itself (Script Editing)

* If you initially designed the stimulus presentation intervals to be (0.5, 1.0, 1.5) but decided to increase them to (1.0, 2.0, 3.0) after a research meeting, you simply open your Python file and rewrite the hard-coded values:

    Before: stimulus_intervals = (0.5, 1.0, 1.5)
    
    After: stimulus_intervals = (1.0, 2.0, 3.0)

* Modifying and saving the script file itself is completely fine. What a tuple strictly prevents is the running program from accidentally altering its own memory values mid-experiment.



### 2. When Values Must Dynamically Change Mid-Experiment (Using Lists)

* If you are designing an Adaptive Task—where stimulus presentation times must scale up or down in real-time based on the participant's performance or reaction speed—you should use a highly mutable List ([ ]) right from the start rather than a tuple.

### Practise challenges

### Scenario A: Fixed Baseline Configuration (Tuple)

### This display resolution standard must never drift during the task session.

<img width="1206" height="34" alt="Screenshot 2026-05-19 at 3 08 04 pm" src="https://github.com/user-attachments/assets/5b9d82fb-f15f-4008-afea-822d9d54f697" />

### Scenario B: Dynamic Real-time Adjustments (List)

### If the participant answers correctly, we shorten the intervals to increase difficulty.

<img width="1212" height="82" alt="Screenshot 2026-05-19 at 3 08 48 pm" src="https://github.com/user-attachments/assets/58a004f2-65d0-4bc0-881f-4af24c21d906" />

### Shorten the first stimulus interval to 1.5 seconds in real-time (Lists are mutable)

<img width="1210" height="112" alt="Screenshot 2026-05-19 at 3 09 23 pm" src="https://github.com/user-attachments/assets/c13dccb7-398f-4cb4-9e4c-d85bf01fec57" />


## Strings: concatenating

* concatenating or combining strings: we use the addition symbols. The result is a new string that is a combination of both.

<img width="1134" height="544" alt="Screenshot 2026-05-19 at 2 48 51 pm" src="https://github.com/user-attachments/assets/c63bcf6d-acfd-43b4-8d59-b16610f86b6d" />

* We can multiply the strings by the number of times we would like to replicate them.

<img width="1472" height="494" alt="Screenshot 2026-05-19 at 2 49 55 pm" src="https://github.com/user-attachments/assets/790777bf-cde1-4906-95c6-dc162a74557d" />


## Strings: Immutable

<img width="1614" height="586" alt="Screenshot 2026-05-19 at 2 50 41 pm" src="https://github.com/user-attachments/assets/df845fdf-ee11-42f7-8a6c-4d80f2d7f578" />

