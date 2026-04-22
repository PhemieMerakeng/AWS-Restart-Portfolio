## Caesar Cipher Encryption & Decryption Program

### Project Overview
In this project, I built a functional Caesar cipher program in Python from scratch. I started by creating small, reusable user-defined functions, each handling a specific task like doubling the alphabet, getting user input for a message or cipher key, encrypting text, and decrypting text. I then combined these functions into a main program that takes a message and a shift key (1–25), encrypts the message by shifting each letter forward in the alphabet, and then decrypts it by shifting backward. This project gave me hands-on experience with string manipulation, loops, function design, and basic cryptography logic.

---

### Skills Covered
- Defining and using user-defined functions in Python
- String concatenation and slicing
- Using the input() function to collect user data
- Looping through strings with for loops
- Finding character positions with .find()
- Conditional logic (if/else) to handle non-alphabetic characters
- Reusing functions to avoid redundant code (e.g., using encryptMessage for decryption with a negative key)
- Debugging with print() statements
- Running a complete script from a main function

---

#### Creating a user-defined Double Alphabet Function
I started by defining a function called getDoubleAlphabet that takes a string and returns it concatenated with itself. This doubled alphabet would later allow me to shift letters without worrying about going past the end of the string.

<img width="895" height="66" alt="Screenshot (394)" src="https://github.com/user-attachments/assets/9a8d9d97-d9fd-4790-9ebc-197ab8461000" />

---

#### Get User Message
Next, I created a function to get the message the user wants to encrypt. I used Python’s built-in input() function to capture the message and return it as a string.

<img width="551" height="57" alt="Screenshot (395)" src="https://github.com/user-attachments/assets/4f2efd05-bf04-4a1b-9f80-9c31bcc939a0" />

---

#### Get Cipher Key
I then wrote a function to ask the user for a shift amount (cipher key) between 1 and 25. This key determines how many positions each letter will shift.

<img width="557" height="69" alt="Screenshot (396)" src="https://github.com/user-attachments/assets/e641c55a-346d-4943-94fb-a7557fc09474" />

---

####  Encrypt Message
This was the core encryption logic. I wrote a function that takes the message, cipher key, and doubled alphabet. It converts the message to uppercase, loops through each character, finds its position in the alphabet, adds the cipher key to get a new position, and builds the encrypted string. If a character isn’t a letter, it stays unchanged.

<img width="558" height="201" alt="Screenshot (397)" src="https://github.com/user-attachments/assets/c86e40f7-504d-431f-9e99-6c75dfed8516" />

---

#### Decrypting the message
def decryptMessage(message, cipherKey, alphabet):
    decryptKey = -1 * int(cipherKey)
    return encryptMessage(message, decryptKey, alphabet)

<img width="551" height="68" alt="Screenshot (398)" src="https://github.com/user-attachments/assets/b694923d-111f-4cb3-bc84-c5c5f4653dab" />

---

####  Creating a main function
Finally, I brought everything together in a runCaesarCipherProgram function. I defined the standard alphabet, doubled it, got the user’s message and cipher key, encrypted the message, decrypted it, and printed all the results.

<img width="750" height="229" alt="Screenshot (399)" src="https://github.com/user-attachments/assets/7d4241d2-5253-4431-98ce-06a3b402b22d" />

---

#### Result of the code
 After the program ran here is the output

 <img width="914" height="210" alt="Screenshot (401)" src="https://github.com/user-attachments/assets/590586b3-97ef-4f87-931b-4fd1d2cbf387" />

 ---

### Conclusion
Completing this project showed me how breaking down a problem into small, single-purpose functions makes complex logic manageable. I learned how to handle user input, manipulate strings, loop through characters, and even implement a basic encryption algorithm. Reusing the encryption function for decryption was a great lesson in writing DRY (Don’t Repeat Yourself) code. This Caesar cipher program is now a solid foundation I can build on for more advanced cryptography projects


