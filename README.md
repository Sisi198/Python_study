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



# Slicing 

* It is helpful to think of a string as a list or tuple: we can treat the string as a sequence and perform sequence operations. 
