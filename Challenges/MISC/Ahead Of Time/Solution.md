# Solution to Ahead Of Time - CTF Challenge

## Problem Overview
The challenge required solving 100 math questions in 1 second each. Each question involved a basic math operation, and we had to extract the numbers, solve the operation, and send the answer back to the server.

## Tools Used:
- **Python**: Used to automate solving the math questions.
- **Regex**: To extract numbers and operators from the questions.

## Steps:

1. **Connect to the Server:**
   Use Python's `socket` module to connect to the server `34.169.13.49 7001`.
 
2. **Extract Math Operations:**
   Use regex to get the numbers and operators from each question.

3. **Solve the Math Question:**
   Perform the math operation (`+`, `-`, `*`, `/`) based on the extracted data.

4. **Send the Answer Back:**
   Send the computed answer back to the server.

5. **Code:**
   ```python
   import socket
   import time
   import re

   # 1. Connect to the Server
   # Establishing connection to the server using socket
   host = '34.169.13.49'
   port = 7001
   conn = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
   conn.connect((host, port))

   # 2. Function to Extract and Solve Math Questions
   # Use regex to extract numbers and operator from the incoming question
   def solve_math_question(question):
       # Extract numbers and operator using regex
       match = re.search(r'(-?\d+)\s*([\+\-\/\*])\s(-?\d+)', question)
       if match:
           num1 = int(match.group(1))
           operator = match.group(2)
           num2 = int(match.group(3))

           # Perform the math operation based on the operator
           if operator == '+':
               return num1 + num2
           elif operator == '-':
               return num1 - num2
           elif operator == '*':
               return num1 * num2
           elif operator == '/':
               return num1 / num2
       return None

   # 3. Read and Respond to the Server
   # Loop to continuously receive data from the server, solve the questions, and send answers
   while True:
       data = conn.recv(1024).decode('utf-8')  # Receive data from server
       if not data:
           break  # Exit loop if no data is received
       if "?" in data:
           answer = solve_math_question(data)  # Solve the math question
           if answer is not None:
               conn.sendall(f"{answer}\n".encode('utf-8'))  # Send the answer back to the server
       time.sleep(0.5)  # Sleep for a short time to simulate a quick response (within 1 second)

   conn.close()  # Close the connection to the server
   
## Key Points:

- **Regex**: Extracts the numbers and operators from the server's questions.
- **Socket**: Handles communication with the server.
- **Python**: Automates the process of solving and sending answers.
