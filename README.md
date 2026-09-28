Test A (The Lazy Prompt):
"Explain bubble sort to me."
Look at the result: Notice how it gives you a long, generic textbook answer that might be wordy or hard to parse quickly.    
        ANSWER
Bubble sort is a simple, comparison-based sorting algorithm. It works by repeatedly stepping through a list, comparing adjacent items, and swapping them if they are in the wrong order.
This process repeats until the entire list is sorted. It is called "bubble sort" because smaller or larger elements gradually "bubble" to their correct positions at the top or bottom of the list with each pass.
How It Works
Start at the beginning of the list.
Compare the first two adjacent elements.
If the first element is larger than the second, swap them.
Move to the next pair of elements and repeat the comparison and swap.
Continue until you reach the end of the list. This completes one pass.
Repeat the entire process for the remaining unsorted elements until a full pass occurs with zero swaps.
Step-by-Step Example
Consider sorting the list [5, 1, 4, 2] in ascending order:
Pass 1:
Compare 5 and 1: $5 > 1$, so swap $\rightarrow$ [1, 5, 4, 2]
Compare 5 and 4: $5 > 4$, so swap $\rightarrow$ [1, 4, 5, 2]
Compare 5 and 2: $5 > 2$, so swap $\rightarrow$ [1, 4, 2, 5]
(The largest element, 5, has "bubbled" to its correct position at the end.)
Pass 2:
Compare 1 and 4: $1 < 4$, no swap $\rightarrow$ [1, 4, 2, 5]
Compare 4 and 2: $4 > 2$, so swap $\rightarrow$ [1, 2, 4, 5]
Compare 4 and 5: Already sorted.
Pass 3:
Compare 1 and 2: $1 < 2$, no swap $\rightarrow$ [1, 2, 4, 5]
Compare 2 and 4: $2 < 4$, no swap.
(No swaps performed during this pass, meaning the list is fully sorted.)
Key Properties
Time Complexity:
Worst & Average Case: $\mathcal{O}(n^2)$ — requires nested loops to iterate through elements.
Best Case (Optimized): $\mathcal{O}(n)$ — occurs when the list is already sorted, needing only one pass.
Space Complexity: $\mathcal{O}(1)$ — sorts in-place without requiring extra memory allocation.
Stability: Stable — preserves the relative order of duplicate elements.
Because of its $\mathcal{O}(n^2)$ time efficiency, bubble sort is rarely used in production software and is primarily taught as an introductory concept in computer science.
Test B (The Structured Prompt):
Role: Act as a Senior Software Engineer and Computer Science Professor.Context: I am a first-semester CS student trying to master fundamental sorting algorithms.Task: Explain how the Bubble Sort algorithm works and provide a clean Python implementation.Constraints:
Keep the explanation under 150 words.
Show a step-by-step dry run of the array [5, 1, 4, 2] using a markdown table.
Do not include any introductory or concluding pleasantries—start directly with the content.  
Bubble sort works by repeatedly stepping through an array, comparing adjacent elements, and swapping them if they are out of order. With each pass, the largest unsorted element "bubbles up" to its correct position at the end of the array. This process repeats until a complete pass occurs with zero swaps, indicating the array is sorted.
Python

def bubble_sort(arr):    n = len(arr)    for i in range(n):        swapped = False        for j in range(0, n - i - 1):            if arr[j] > arr[j + 1]:                arr[j], arr[j + 1] = arr[j + 1], arr[j]                swapped = True        if not swapped:            break    return arr
Step-by-Step Dry Run ([5, 2, 8, 1])
Pass
Pair Compared
Comparison
Action
Array State
Pass 1
(5, 2)
5 > 2
Swap
[2, 5, 8, 1]

(5, 8)
5 < 8
No Swap
[2, 5, 8, 1]

(8, 1)
8 > 1
Swap
[2, 5, 1, 8]
Pass 2
(2, 5)
2 < 5
No Swap
[2, 5, 1, 8]

(5, 1)
5 > 1
Swap
[2, 1, 5, 8]
Pass 3
(2, 1)
2 > 1
Swap
[1, 2, 5, 8]
Pass 4
(1, 2)
1 < 2
No Swap (Flag false)
[1, 2, 5, 8]

AI as a Code Reviewer & Bug Hunter
The Concept: Instead of just asking an AI to write code for you, you are going to use a structured prompt to turn it into a strict, eagle-eyed code reviewer. In software engineering, code reviews catch bugs, security flaws, and performance issues before they hit production.
The Business/Developer Value: Being able to quickly audit code using AI makes you significantly faster and catches silly mistakes early.
Action Plan
            Python code snippet below, and then use the Structured Code Review Prompt to see how the AI handles it.
CODE :
   def calculate_average(numbers):
    total = 0
    for num in numbers:
        total = total + num
    # Bug or edge case hiding here!
    avg = total / len(numbers)
    return avg

print(calculate_average([]))
The Structured Prompt to Run Right Now
Role: Act as a Principal Security and Reliability Software Engineer.Context: I am reviewing a junior developer's Python code snippet before it gets merged into our main branch.Task: Review the provided Python function for bugs, edge cases, and best practice violations.Constraints:
Identify why the code will crash on specific inputs.
Output your findings strictly in a markdown table with columns: Issue Type, Severity (High/Med/Low), and Detailed Explanation & Fix.
Provide the refactored, production-ready version of the code underneath the table.
Keep explanations concise and technical. Do not add conversational intro text.
Next Step
Run that prompt right now, look at how it spots the division-by-zero error on an empty list, and notice how clean the markdown table format is.
ANSWER
Issue Type
Severity
Detailed Explanation & Fix
ZeroDivisionError
High
Passing an empty list ([]) causes len(numbers) to evaluate to 0, resulting in a runtime ZeroDivisionError: division by zero. Fix: Add a check for an empty sequence and return 0.0, None, or raise a explicit ValueError depending on domain requirements.
Type Safety / Non-Iterable Input
Med
If numbers is passed as None or a non-iterable type (e.g., an int), the for loop or len() call will raise a TypeError. Fix: Implement Type Hinting (Sequence[Union[int, float]]) to enable static analysis via mypy.
Pythonic Syntax
Low
Manually iterating with a for loop to compute a sum is inefficient and non-idiomatic CPython. Fix: Use the built-in sum() function, which is implemented in C and significantly faster.
CODE  
   from typing import Sequence, Union

def calculate_average(numbers: Sequence[Union[int, float]]) -> float:
    """Calculates the arithmetic mean of a sequence of numbers.
   
    Args:
        numbers: A sequence (list, tuple, etc.) of integers or floats.
       
    Returns:
        The average as a float, or 0.0 if the sequence is empty.
    """
    if not numbers:
        return 0.0
   
    return sum(numbers) / len(numbers)
Turning Messy Logs or Raw Text into Clean JSON Data
The Concept: As a computer science student, you will frequently deal with unstructured data (like messy server logs, raw text files, or messy API responses) that you need to parse into structured formats like JSON so your code can actually read it.
The Developer Value: Instead of writing complex Regular Expressions (Regex) or parsing loops from scratch, you can use structured prompts to have the AI clean and structure raw data for you instantly.
CODE
[ERROR] 2026-09-16 10:12:05 - Connection timeout on database port 5432 from user_id: 4021.
[WARNING] 2026-09-16 10:14:22 - High memory usage detected: 89% utilized on worker-node-03.
[ERROR] 2026-09-16 10:20:11 - Invalid API key provided by client_ip: 192.168.1.55 for endpoint /api/v1/login.
The Structured Prompt
Role: Act as a Backend Data Engineer and Parsing Specialist.Context: I have raw, unstructured server log text that I need to parse into a clean programmatic format for a monitoring dashboard.Task: Extract the key details from each log entry and format them into a valid, parseable JSON array.Constraints:
Each JSON object in the array must contain these exact keys: timestamp, log_level, component_or_target, and message.
Output only the raw JSON block inside a markdown code block.
Do not include any explanations, introductory remarks, or conversational text outside of the code block.
 ANSWER
      [
  {
    "timestamp": "2026-09-16 10:12:05",
    "log_level": "ERROR",
    "component_or_target": "database port 5432",
    "message": "Connection timeout on database port 5432 from user_id: 4021."
  },
  {
    "timestamp": "2026-09-16 10:14:22",
    "log_level": "WARNING",
    "component_or_target": "worker-node-03",
    "message": "High memory usage detected: 89% utilized on worker-node-03."
  },
  {
    "timestamp": "2026-09-16 10:20:11",
    "log_level": "ERROR",
    "component_or_target": "/api/v1/login",
    "message": "Invalid API key provided by client_ip: 192.168.1.55 for endpoint /api/v1/login."
  }
]
Automated Unit Test Generation
The Concept: Writing unit tests is one of the most important (and sometimes tedious) parts of software development. Today, you are going to use a structured prompt to act as a Quality Assurance (QA) engineer that writes your unit test boilerplate for you.
The Developer Value: Instead of spending 20 minutes writing test cases from scratch, you can use structured prompts to generate edge-case tests instantly using frameworks like Python's unittest or pytest.
Action Plan
def validate_password(password):
    if not password or len(password) < 8:
        return False
    has_digit = any(char.isdigit() for char in password)
    has_upper = any(char.isupper() for char in password)
    return has_digit and has_upper

Role: Act as a Senior QA Automation Engineer and Python Testing Expert.Context: I have written a basic password validation function and need comprehensive unit tests to ensure it handles normal inputs and edge cases correctly.Task: Generate a complete set of unit tests using Python's built-in unittest framework for this function.Constraints:
Include test cases for: a valid password, a password that is too short, a password missing a number, a password missing an uppercase letter, and a None/empty input.
Output only the Python test code inside a markdown code block.
Do not include conversational filler, greetings, or explanations outside the code block.
: Algorithm Breakdown & Logic Tracing
The Concept: As a CS student, you are going to run into dense, complicated algorithms or data structures that look like a foreign language at first glance. Today, you are going to use a structured prompt to turn the AI into a patient tutor that breaks down complex logic step-by-step.
The Developer Value: Instead of getting stuck staring at a loop or recursive function for hours, you can use structured prompts to generate clear execution traces and plain-English explanations instantly.
Action Plan
def recursive_factorial(n):
    if n <= 1:
        return 1
    return n * recursive_factorial(n - 1)

Role: Act as an Expert Computer Science Professor and Algorithm Tutor.Context: I am a first-semester computer science student trying to understand how recursion works under the hood.Task: Explain the execution flow of the provided recursive function when called with n = 4.Constraints:
Provide a step-by-step trace showing how the function calls stack up and then unwind.
Format the step-by-step trace using a clean markdown table with columns: Call Stack Level, Function Input (n), Operation / Action, and Return Value.
Keep the explanation brief, clear, and beginner-friendly. Avoid overly dense academic jargon.
ANSWER

hen a function calls itself recursively, Python uses an internal memory structure called the Call Stack to keep track of where each function call is and what work remains to be done.
Think of the Call Stack like a stack of plates:
Every time a new function call happens, a frame is pushed onto the top of the stack.
Python pauses the previous call until the new one finishes.
Once a call reaches a base case, it calculates its answer and pops off the stack, returning its value back down the line to complete the pending calculations.
Step-by-Step Execution Trace for recursive_factorial(4)
Call Stack Level
Function Input (n)
Operation / Action
Return Value
Level 1 (Pushed)
n = 4
Pauses at 4 * recursive_factorial(3)
Pending...
Level 2 (Pushed)
n = 3
Pauses at 3 * recursive_factorial(2)
Pending...
Level 3 (Pushed)
n = 2
Pauses at 2 * recursive_factorial(1)
Pending...
Level 4 (Pushed)
n = 1
Base Case Hit! (n <= 1)
1
Level 3 (Unwinding)
n = 2
Resumes: 2 * 1
2
Level 2 (Unwinding)
n = 3
Resumes: 3 * 2
6
Level 1 (Unwinding)
n = 4
Resumes: 4 * 6
24
Key Takeaway
Stack Phase: The function keeps calling itself, diving deeper into stack levels ($n = 4 \rightarrow 3 \rightarrow 2 \rightarrow 1$). No actual multiplication happens yet because each step is waiting on the result of the next call.
Base Case: Reaching n = 1 stops further recursive calls and provides the first concrete answer (1).
Unwind Phase: The stack shrinks back down as each paused call receives its missing piece, computes its multiplication, and passes the result up to the parent caller until the final result (24) is produced.

Auto-Generating Professional README & Documentation
The Concept: Writing clean documentation, comments, and README files is crucial for any coding project, but it's often neglected by developers. Today, you are going to use a structured prompt to turn the AI into a technical writer that documents your code instantly.
The Developer Value: When you build a project for class or an open-source repo, a great README makes it look professional and easy to understand. You can have the AI analyze your raw script and build the documentation for you.
Action Plan

Imagine you have a small utility script that handles basic file processing:
Python

import os 

def clean_text_file(filepath):
    if not os.path.exists(filepath):
        return "File not found."
    with open(filepath, 'r') as f:
        lines = f.readlines()
    cleaned = [line.strip() for line in lines if line.strip()]
    new_path = filepath.replace(".txt", "_cleaned.txt")
    with open(new_path, 'w') as f:
        f.writelines('\n'.join(cleaned))
    return f"Successfully cleaned and saved to {new_path}"

Role: Act as a Senior Technical Writer and Open-Source Project Maintainer.Context: I have written a simple Python text-cleaning utility script and need a professional README section for it.Task: Generate a markdown documentation snippet for this script.Constraints:
Include sections for: Overview, How It Works, Function Parameters, and a quick Usage Example.
Keep the formatting clean, professional, and ready to paste directly into a GitHub repository.
Do not include conversational filler or greetings. Start straight with the markdown headers.
RESULT:
Overview
The Text Cleaner Utility is a lightweight Python script designed to process and sanitize plain text files. It automatically strips extraneous whitespace from individual lines and removes empty lines, outputting a fresh, clean version of the document while preserving the original file.
How It Works
Existence Check: The utility first verifies whether the target file exists at the specified path. If the file cannot be found, it gracefully exits and returns an error message.
File Reading: It reads the contents of the file line by line.
Sanitization: Using a list comprehension, it iterates through every line, applying .strip() to remove leading and trailing whitespace, and filters out any resulting empty lines.
File Generation: It constructs a new destination filename by appending _cleaned to the original base name and writes the sanitized lines back to disk, separated by standard newline characters.
Function Parameters
Parameter
Type
Description
filepath
str
The relative or absolute path to the target .txt file that requires cleaning.
Usage Example
import osdef clean_text_file(filepath):    if not os.path.exists(filepath):        return "File not found."    with open(filepath, 'r') as f:        lines = f.readlines()    cleaned = [line.strip() for line in lines if line.strip()]    new_path = filepath.replace(".txt", "_cleaned.txt")    with open(new_path, 'w') as f:        f.writelines('\n'.join(cleaned))    return f"Successfully cleaned and saved to {new_path}"# Example executionresult = clean_text_file("sample.txt")print(result)
Converting SQL Queries from Plain English
The Concept: As a computer science student, you will take database courses where you have to write complex SQL queries. Today, you are going to use a structured prompt to turn the AI into a database administrator that translates natural language business requirements into precise, optimized SQL queries.
The Developer Value: When working with databases, writing joins, aggregations, and filters can get tricky. Knowing how to prompt an AI to write and explain SQL keeps your backend logic accurate.
Action Plan
1. The Scenario
Imagine you have a database with a table named students (columns: id, name, major, gpa) and you need to write a query to find all Computer Science students with a GPA above 3.5, sorted from highest GPA to lowest.
2. The Structured Prompt to Run Right
Role: Act as a Senior Database Administrator and SQL Expert.Context: I am writing a backend database script and need to query a table named students with columns id, name, major, and gpa.Task: Write a SQL query that selects all students whose major is 'Computer Science' and whose GPA is greater than 3.5, ordered by GPA in descending order.Constraints:
Output the SQL query inside a clean markdown code block.
Below the code block, provide a brief 2-sentence explanation of what each clause (SELECT, WHERE, ORDER BY) is doing.
Keep the response concise and technical with no conversational fluff.
SELECT id, name, major, gpa
FROM students
WHERE major = 'Computer Science' AND gpa > 3.5
ORDER BY gpa DESC;
The SELECT clause specifies which columns to retrieve from the students table, while the WHERE clause filters the rows to include only records matching both conditions: a 'Computer Science' major and a GPA strictly greater than 3.5. The ORDER BY clause sorts the resulting dataset by the gpa column in descending order (DESC), ensuring the highest GPAs appear first.
Debugging Confusing Error Logs
The Concept: When code throws a cryptic runtime error or a massive stack trace, it can take hours to figure out where the bug actually lives. Today, you are going to use a structured prompt to turn the AI into a senior debugger that diagnoses errors instantly.
The Developer Value: Instead of getting overwhelmed by a long red wall of error text in your terminal, you can feed it to your structured AI prompt to isolate the exact line causing the issue and get a precise fix.

1. The Target Error Log
Imagine you ran a Python script and your terminal threw this classic KeyError:
Plaintext

Traceback (most recent call last):  File "app.py", line 14, in <module>    user_role = user_data["permissions"]["role"]KeyError: 'permissions'
2. The Structured Prompt to Run Right Now
Role: Act as a Principal Python Debugger and Systems Reliability Engineer.Context: I am running a backend script and encountered a runtime crash with a stack trace.Task: Diagnose the exact root cause of this error and provide a defensive code fix so it doesn't crash again.Constraints:
Identify which line and dictionary key caused the failure.
Output your answer using a markdown table with columns: Error Type, Root Cause, and Defensive Fix Solution.
Provide the corrected code snippet using safe dictionary access (like the .get() method) underneath the table.
Keep the response concise and technical with no conversational intro.
Error Type
Root Cause
Defensive Fix Solution
KeyError: 'permissions'
Line 14 attempts to access user_data["permissions"], but the "permissions" key does not exist at the top level of the user_data dictionary.
Use chain .get() calls or standard dictionary checks to safely handle missing keys and prevent a runtime crash.
Python

# Safe nested lookup using chaining .get()user_role = user_data.get("permissions", {}).get("role")# Optional: Provide a default value if 'role' might also be missing or Noneuser_role = user_data.get("permissions", {}).get("role", "default_role")
: Translating Plain English Logic into Production-Ready Code
The Concept: Often in computer science, you get a problem description or pseudocode in plain English, and your job is to turn it into precise code syntax. Today, you are going to use a structured prompt to turn the AI into a translator that converts business requirements or logic descriptions straight into clean, working code.
The Developer Value: When starting a new homework assignment or feature from a loose description, this workflow helps you spin up the baseline architecture instantly so you can focus on fine-tuning.
Action Plan
1. The Scenario
Imagine you have this plain-English requirement from an assignment:
"Write a Python function that takes a string, removes all spaces and punctuation, converts it to lowercase, and checks if it's a palindrome (reads the same forwards and backwards). It should return True or False."
2. The Structured Prompt to Run Right Now
Role: Act as a Senior Software Engineer and Algorithms Instructor.Context: I am working on a string-manipulation utility script for a university programming assignment.Task: Translate the provided plain-English requirement into a clean, optimized Python function.Constraints:
Use Python's built-in libraries (like string or built-in string methods) to handle punctuation cleaning efficiently.
Include clear docstrings and inline comments explaining how the logic works.
Provide one quick example of how to call the function at the bottom.
Output the solution inside a single markdown code block with no conversational intro text.
import string


def is_palindrome(text: str) -> bool:
    """Checks if a given string is a palindrome, ignoring spaces, punctuation, and case.

    Args:
        text (str): The input string to check.

    Returns:
        bool: True if the cleaned string is a palindrome, False otherwise.
    """
    # Create a translation table that maps all punctuation characters to None
    translator = str.maketrans("", "", string.punctuation)

    # Remove punctuation, strip spaces, and convert to lowercase
    cleaned_text = text.translate(translator).replace(" ", "").lower()

    # Compare the cleaned string to its reverse using slicing
    return cleaned_text == cleaned_text[::-1]


# Example usage:
if __name__ == "__main__":
    sample_text = "A man, a plan, a canal: Panama!"
    result = is_palindrome(sample_text)
    print(f"Is '{sample_text}' a palindrome? {result}")  # Output: True

Code Refactoring & Time Complexity Optimization
The Concept: Writing code that works is only half the battle; writing code that is fast, clean, and resource-efficient is what separates junior developers from senior engineers. Today, you are going to use a structured prompt to turn the AI into a performance optimization expert.
The Developer Value: When you write a naive solution that has poor performance (like a nested loop running in $O(n^2)$ time), a structured prompt can help you refactor it into an optimized, clean approach.
Action Plan
1. The Naive Code
Imagine you wrote a simple script to find if there are any duplicate numbers in a list using a slow, nested loop approach:
def has_duplicates(numbers):
    for i in range(len(numbers)):
        for j in range(i + 1, len(numbers)):
            if numbers[i] == numbers[j]:
                return True
    return False
The Structured Prompt to Run Right Now
Role: Act as a Principal Software Engineer and Performance Optimization Specialist.
Context: I have written a naive Python function to check for duplicates, but its time complexity is too high ($O(n^2)$) for large datasets.
Task: Refactor and optimize this function to run with better time complexity (e.g., using a Set for $O(n)$ time).
Constraints:
Provide a markdown table comparing the Original Approach vs. the Optimized Approach with columns: Approach, Time Complexity, and Space Complexity.
Output the refactored, high-performance Python code inside a markdown code block.
Keep explanations brief and technical with no conversational fluff.
 Result
Approach
Time Complexity
Space Complexity
Original (Nested Loop)
$O(n^2)$
$O(1)$
Optimized (Hash Set)
$O(n)$
$O(n)$
Python

def has_duplicates(numbers: list) -> bool:    """Checks for duplicates in a list using a set for O(1) average lookups."""    seen = set()    for num in numbers:        if num in seen:            return True        seen.add(num)    return False# Alternative one-liner (identical space/time complexity bounds):# def has_duplicates(numbers: list) -> bool:#     return len(numbers) != len(set(numbers))
Technical Summary
Time Complexity ($O(n)$): A single traversal through the collection. Set lookups (in) and insertions (add) operate in $O(1)$ average time via hash tables.
Space Complexity ($O(n)$): At most $n$ unique elements stored in memory in the worst-case scenario where no duplicates exist.
Designing REST API Specifications & Mock Payloads
The Concept: In modern software development, applications talk to each other using APIs (Application Programming Interfaces). Today, you are going to use a structured prompt to turn the AI into a backend API architect that designs clean endpoint specifications and JSON request/response payloads.
The Developer Value: When building full-stack apps or backend services, mapping out what data goes in and what comes out prevents messy bugs before you even start writing the server code.
Action Plan
1. The Scenario
Imagine you are building a student portal backend and need to design a REST API endpoint where a frontend app can register a new user.
2. The Structured Prompt to Run Right Now
Role: Act as a Principal Backend API Architect and RESTful Services Expert.Context: I am building a backend service for a university portal and need to design a clean POST endpoint for registering a new student user.Task: Design the API specification for this registration endpoint.Constraints:
Include the Endpoint URL, HTTP Method (POST), and expected request headers.
Provide a markdown table of the Request Body Fields containing columns: Field Name, Data Type, Required (Yes/No), and Description.
Provide a successful JSON response example (201 Created) inside a markdown code block.
Keep the response concise, professional, and free of conversational filler.
API Specification: Student User Registration
Endpoint URL: /api/v1/students/register
HTTP Method: POST
Request Headers:
Content-Type: application/json
Accept: application/json
Request Body Fields
Field Name
Data Type
Required
Description
email
String
Yes
University-issued email address (must be unique).
password
String
Yes
User password meeting security criteria (min 8 characters).
firstName
String
Yes
Legal first name of the student.
lastName
String
Yes
Legal last name of the student.
studentId
String
Yes
Official university student identification number.
department
String
Yes
Department or major academic department code (e.g., CS, EE).
enrollmentYear
Integer
No
Year of entry into the institution (e.g., 2026).

Success Response (201 Created)
JSON

{  "status": "success",  "message": "Student account successfully created.",  "data": {    "id": "usr_9f8a2b3c-4d5e-6f7a-8b9c-0d1e2f3a4b5c",    "studentId": "STU-2026-8841",    "email": "j.doe@university.edu",    "firstName": "Jane",    "lastName": "Doe",    "department": "CS",    "enrollmentYear": 2026,    "createdAt": "2026-09-25T21:20:10Z"  }}
Creating Reusable Prompt Templates for Code Scaffolding
The Concept: Up until now, you've written individual prompts for specific tasks. Today, you are going to learn how to build a Meta-Prompt—a reusable prompt template that you can save and reuse every time you start a brand-new coding feature or project.
The Developer Value: Professional software engineers don't rewrite prompts from scratch every time; they build standardized workflows (templates) to spin up new scripts, modules, or features in seconds.
Action Plan
1. The Concept
Instead of asking an AI casually to "write a Python script for X," you are going to create a master template where you only have to swap out the [FEATURE_NAME] and [REQUIREMENTS] variables each time.
2. The Structured Prompt to Run Right Now
Paste this prompt into your chat window to build your first reusable code-scaffolding template:
Role: Act as a Principal Software Architect and Developer Productivity Expert.Context: I want to create a master prompt template that I can reuse every time I need to generate a new Python module or script for my university projects.Task: Design a reusable structured prompt template using clear placeholder variables (like [TASK_DESCRIPTION], [INPUT_DATA_FORMAT], and [OUTPUT_REQUIREMENTS]).Constraints:
Structure the template using clear Role, Context, Task, and Constraints sections so it acts as a fill-in-the-blank form.
Provide a brief example showing how a developer would fill it out for a real task (e.g., building a CSV parser).
Output the response in clean markdown format with no conversational fluff.
Generating Mock Test Data for Database & Algorithms
The Concept: When building apps, writing algorithms, or testing database queries, you constantly need realistic sample data (like lists of fake users, test scores, or log records) to see if your code actually works. Today, you are going to use a structured prompt to turn the AI into a mock data generator.
The Developer Value: Instead of manually typing out fake data to test your scripts, you can use structured prompts to generate clean JSON, CSV, or Python data structures instantly.
Action Plan
1. The Scenario
Imagine you are writing a Python script to analyze student grades and you need a mock dataset of 5 students with names, IDs, majors, and grades to test your code.
2. The Structured Prompt to Run Right Now
Role: Act as a Senior Database Administrator and Test Data Generator.Context: I am writing a Python script to process student grades and need realistic sample data to test my sorting and filtering functions.Task: Generate a mock dataset of 5 computer science and engineering students.Constraints:
Include fields for student_id, name, major, and gpa.
Output the data strictly as a valid Python list of dictionaries inside a markdown code block.
Do not include conversational intro text or explanations outside the code block.
[
    {
        "student_id": "CS1001",
        "name": "Alex Chen",
        "major": "Computer Science",
        "gpa": 3.85
    },
    {
        "student_id": "EN1002",
        "name": "Sarah Jenkins",
        "major": "Electrical Engineering",
        "gpa": 3.42
    },
    {
        "student_id": "CS1003",
        "name": "Marcus Vance",
        "major": "Computer Science",
        "gpa": 2.91
    },
    {
        "student_id": "EN1004",
        "name": "Priya Patel",
        "major": "Mechanical Engineering",
        "gpa": 3.98
    },
    {
        "student_id": "CS1005",
        "name": "Liam O'Connor",
        "major": "Software Engineering",
        "gpa": 3.15
    }
]
Assembling Your Developer Portfolio README
The Concept: You’ve spent the last two weeks building an incredible toolkit of structured prompts for coding, debugging, refactoring, and testing. Today, you are going to use a structured prompt to generate a professional GitHub Portfolio README that organizes all your work so recruiters or professors can see your skills instantly.
The Developer Value: Having a clean, professional portfolio repository on GitHub shows that you aren't just a coding student—you are a modern engineer who knows how to leverage AI workflows efficiently.
Action Plan
1. The Scenario
You want to create a clean, professional README.md file for your free GitHub repository named ai-prompt-engineering-playbook that summarizes what you learned and showcases your best prompt templates.
2. The Structured Prompt to Run Right Now
Role: Act as a Senior Technical Recruiter and Open-Source Project Maintainer.Context: I am a first-semester computer science student who has just completed a 15-day intensive challenge on Structured Prompt Engineering for Software Development.Task: Generate a professional GitHub README template that showcases this portfolio project.Constraints:
Include sections for: Project Overview, What I Learned (Code Review, Debugging, SQL, Architecture, Mock Data), and a Sample Prompt Playbook section.
Format the entire response using clean, professional markdown with badges or bullet points.
Keep the tone professional, ambitious, and ready to publish directly to GitHub.
Prompt Engineering Playbook
A structured collection of battle-tested prompt engineering patterns, strategies, and templates developed over a 15-day intensive engineering challenge. Designed to streamline common software development workflows including code review, debugging, architecture design, and database queries.
Project Overview
As LLMs become core to the modern software development stack, the ability to control model outputs deterministically is a critical skill. This repository documents a structured approach to Prompt Engineering for Software Engineers.
Rather than relying on conversational chat, this playbook uses system instructions, few-shot examples, chain-of-thought prompting, and strict output constraints to make AI models act as reliable code generators, reviewers, and architectural advisors.
What I Learned & Capabilities Developed
During this 15-day challenge, I systematically tested prompt templates across five core software development domains:
1. Code Review & Refactoring
System Persona: Senior Security & Quality Auditor.
Technique: Role-based prompting combined with constraint enforcement.
Key Outcome: Prompts that enforce specific coding standards (e.g., PEP 8, clean code principles), identify memory leaks, flag edge-case vulnerabilities, and propose optimized refactored solutions without altering business logic.
2. Systematic Debugging
System Persona: Staff Reliability Engineer.
Technique: Chain-of-Thought (CoT) prompting.
Key Outcome: Prompts that force the model to analyze stack traces step-by-step, hypothesize root causes before suggesting code fixes, and provide regression test cases to prevent recurrence.
3. SQL & Database Query Optimization
System Persona: Senior Database Administrator (DBA).
Technique: Schema-driven few-shot prompting.
Key Outcome: Generating safe, index-aware SQL queries (PostgreSQL/MySQL), converting complex natural language requirements into efficient JOINs, and identifying performance bottlenecks in existing queries.
4. Software Architecture & System Design
System Persona: Principal Solutions Architect.
Technique: Markdown-constrained structured output.
Key Outcome: Converting high-level application requirements into trade-off analyses (SQL vs. NoSQL, monolithic vs. microservices), component sequence descriptions, and API schemas (OpenAPI / JSON Schema).
5. Mock Data & Test Suite Generation
System Persona: QA Automation Specialist.
Technique: Schema enforcement & JSON-only output constraints.
Key Outcome: Generating edge-case-heavy test datasets (boundary values, nulls, special characters) and unit test scaffolding (PyTest, Jest) matching exact domain models.
Sample Prompt Playbook
Below are selected production-ready prompt templates from this repository.
Template 1: Production Code Reviewer
Markdown
**Role:** Act as a Senior Software Engineer specializing in Code Quality and Security.**Context:** I am submitting code for review prior to a production pull request.**Task:** Review the provided code snippet and return a structured critique.**Output Constraints:**1. **Security Vulnerabilities:** Flag any injection, auth, or memory risks.2. **Performance Bottlenecks:** Identify suboptimal time/space complexity ($O(n^2)$ loops, unnecessary DB queries).3. **Refactored Code:** Provide the improved version in a single code block with clear comments.**Code to Review:**```[INSERT LANGUAGE][INSERT CODE HERE]
---### Template 2: Root-Cause Debugger```markdown**Role:** Act as a Systems Debugging Expert.**Context:** My application encountered an unexpected runtime error.**Task:** Analyze the provided code snippet and stack trace using step-by-step reasoning.**Required Steps in Response:**1. **Step-by-Step Execution Trace:** Explain what the code was doing immediately before the error occurred.2. **Root Cause Analysis:** Identify the exact line and state condition causing the failure.3. **Fix & Prevention:** Provide the corrected code along with a unit test designed to catch this specific edge case.**Stack Trace:**[INSERT STACK TRACE HERE]**Relevant Code:**```[INSERT LANGUAGE][INSERT CODE HERE]
---### Template 3: SQL Query Generator & Optimizer```markdown**Role:** Act as a Senior Database Administrator.**Context:** I need an optimized SQL query for a relational database.**Database Engine:** [PostgreSQL / MySQL / SQLite]**Schema Information:**[INSERT TABLE SCHEMAS AND INDEXES HERE]**Request:** "[INSERT NATURAL LANGUAGE QUESTION OR TASK HERE]"**Output Constraints:**- Provide the exact SQL query inside a markdown code block.- Explain the execution plan, detailing how indexes are utilized.- Flag any potential full-table scans or performance hazards.
How to Use This Repository
Browse Templates: Check the /templates directory for specific use cases (debugging, architecture, testing).
Adapt Parameters: Replace placeholders like [INSERT CODE HERE] with your project details.
Integrate: Use these prompts in CLI tools, IDE extensions, or LLM chat interfaces for consistent code assistance.
Author
Computer Science Student – Initial work & prompt development
GitHub: @your-username
LinkedIn: Your Name
License
This project is licensed under the MIT License - see the LICENSE file for details.
# ai-prompt-engineering-playbook
A 15-day portfolio showcasing my journey mastering structured prompt engineering for computer science, software debugging, SQL generation, and AI-assisted developer workflows. Built with 100% free tools.
