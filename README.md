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

<img width="1668" height="2154" alt="Python Basic-6" src="https://github.com/user-attachments/assets/3d45f274-217f-4d0a-a71e-2bf0355d05f4" />

<img width="1668" height="2154" alt="Python Basic-7" src="https://github.com/user-attachments/assets/7e2c6149-a352-42ae-8b85-298c5ead968b" />


<img width="1668" height="2154" alt="Python Basic-8" src="https://github.com/user-attachments/assets/4bbc370a-a84e-48fb-ac56-f795313e0539" />


<img width="1668" height="2154" alt="Python Basic-9" src="https://github.com/user-attachments/assets/abd1cf52-b0f8-47ce-a252-808bf76c411f" />


<img width="1668" height="2154" alt="Python Basic-10" src="https://github.com/user-attachments/assets/fcdc899a-7b49-45f5-a76b-3ae484ad5c18" />


<img width="1668" height="2154" alt="Python Basic-11" src="https://github.com/user-attachments/assets/2da08886-3e8d-44aa-9969-f5be48e8bb3c" />


<img width="1668" height="2154" alt="Python Basic-16" src="https://github.com/user-attachments/assets/792518c3-7031-4b7a-b2a8-66aa616f43ab" />

<img width="1668" height="2154" alt="Python Basic-15" src="https://github.com/user-attachments/assets/60bcf4d0-6b66-46a1-b2db-4c79196c17b0" />

<img width="1668" height="2154" alt="Python Basic-14" src="https://github.com/user-attachments/assets/1ebee93f-8751-4d3f-9a17-51e6dda203ac" />

<img width="1668" height="2154" alt="Python Basic-13" src="https://github.com/user-attachments/assets/50aadc33-e1e2-4a0a-ae84-8699267ba45a" />

<img width="1668" height="2154" alt="Python Basic-12" src="https://github.com/user-attachments/assets/73548598-3310-4ea6-8a47-9ce19c64f9ee" />

<img width="1668" height="2154" alt="Python Basic-19" src="https://github.com/user-attachments/assets/0c69655d-1b62-482a-9d78-dbbd8aa7dcd9" />
<img width="1668" height="2154" alt="Python Basic-18" src="https://github.com/user-attachments/assets/cef5d4f2-8614-4051-859e-1fa30f164628" />

<img width="1668" height="2154" alt="Python Basic-17" src="https://github.com/user-attachments/assets/ce78a4af-e182-4b3d-b5ea-f49b95508e8f" />

<img width="1668" height="2154" alt="Python Basic-20" src="https://github.com/user-attachments/assets/7db7aa74-a856-4b84-a03c-0fbfa4dd1ce8" />


