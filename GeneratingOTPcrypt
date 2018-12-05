Generating a one-time pad
Open a new Python file in your preferred editor.

The first thing you need is some random numbers, 
so import the randint method from the random module:

from random import randint
It is worth noting, that if we were real secret agents, 
then using random might be a little insecure. os.urandom 
is a much more secure way of generating random numbers.

Later on you’re going to need the alphabet as well, 
so it’s best to declare this constant now:

ALPHABET = 'abcdefghijklmnopqrstuvwxyz'
Next, you can create a function to generate an OTP. 
It will need to have parameters for the number of sheets in 
the pad and the number of characters that each sheet can encrypt:

def generate_otp(sheets, length):
Now a new file needs to be created for every sheet. 
Each file will be saved as .txt with the following naming convention: 
otp0.txt, otp1.txt, otp2.txt. You can use a for loop for this:

def generate_otp(sheets, length):
    for sheet in range(sheets):
        with open("otp" + str(sheet) + ".txt","w") as f:
Finally for this function, you can add in two lines of code t
hat will write out the random numbers to the file. Here, you’re adding a 
\n character to the end of each number, so it’s written to a new line.

def generate_otp(sheets, length):
    for sheet in range(sheets):
        with open("otp" + str(sheet) + ".txt","w") as f:
            for i in range(length):
                f.write(str(randint(0,26))+"\n")
Test your code by saving (ctrl+s) and running (F5). 
Then type generate_otp(5, 100) into the shell

Loading a sheet from the OTP
Now that the OTP has been generated, you need a way to load a sheet 
and store all its numbers in a list.

First, you can create a function to open a file:

def load_sheet(filename):
    with open(filename, "r") as f:

Then you can load the contents of the file into a list. The splitlines() part breaks each line up into a single item in the list and also removes the \n character (newline):

def load_sheet(filename):
    with open(filename, "r") as f:
        contents = f.read().splitlines()
    return contents
Test this function by saving and running your code again. Now in the shell you can type the following:

sheet = load_sheet('otp0.txt')
print(sheet)

def get_plain_text():
    plain_text = input('Please type your message ')
    return plain_text.lower()

Loading and saving the messages
Next, you’re going to need a method of opening messages written to you, and saving the messages that have been encrypted. Again, you’re going to need a couple of fairly basic functions - one to open and read a file, the other to open and write a file:

def load_file(filename):
    with open(filename, "r") as f:
        contents = f.read()
    return contents

def save_file(filename, data):
    with open(filename, 'w') as f:
        f.write(data)

Encrypting a message
Now comes the fun part: you’re going to encrypt a message using a sheet from the one-time pad. This function will have two parameters. The first will be for a string that contains the plaintext message; the second will be for the one-time pad sheet that will be used.

To start with, you can define the function:

def encrypt(plaintext, sheet):
Once you start encrypting the plaintext, you’ll need to store the ciphertext. You can use an empty string to do this:

def encrypt(plaintext, sheet):
    ciphertext = ''
Now comes the clever part. This function is going to act on every character in the plaintext, a process called ‘iteration’. While it’s doing this, it needs to keep track of which character it’s working on and what position that character has in the plaintext. To do this, you can use the built-in function enumerate():

def encrypt(plaintext, sheet):
    ciphertext = ''
    for position, character in enumerate(plaintext):
The next thing to do is check if the character from the plaintext is in the alphabet or not. In this program you’re not going to bother encrypting spaces or punctuation, so if the character is not a letter, it can just be added to the ciphertext string. This is where we use that ALPHABET constant you wrote earlier:

def encrypt(plaintext, sheet):
    ciphertext = ''
    for position, character in enumerate(plaintext):
        if character not in ALPHABET:
            ciphertext += character
The next part is quite tricky to understand.

Firstly, you need to find the position of the plaintext character in the alphabet - ALPHABET.index(character).
Then you need to add this number to the value from the equivalent position on the sheet from the OTP - int(sheet[position]).
This new number needs converted back into a letter. If the new number was 0 it would become a, if it was 5 it would become f and so on. What if the number is greater than 25, though? If the number is 26 it needs to be changed to 0, and if it’s 30 it should be changed to 4. To do this we can use the modulo operator (%), which finds the remainder after a division.
Lastly, the number is converted to a letter.
Putting that all together into your function, it would look like this:

def encrypt(plaintext, sheet):
    ciphertext = ''
    for position, character in enumerate(plaintext):
        if character not in ALPHABET:
            ciphertext += character
        else:
            encrypted = (ALPHABET.index(character) + int(sheet[position])) % 26
            ciphertext += ALPHABET[encrypted]
You can finish off by returning the ciphertext:

def encrypt(plaintext, sheet):
    ciphertext = ''
    for position, character in enumerate(plaintext):
        if character not in ALPHABET:
            ciphertext += character
        else:
            encrypted = (ALPHABET.index(character) + int(sheet[position])) % 26
            ciphertext += ALPHABET[encrypted]
    return ciphertext
To test your function you can save and run your code and then type the following into the shell.

sheet = load_sheet('otp0.txt')
encrypt('This is a secret message.', sheet)

Decrypting messages
When communicating with your friends, you’ll need a way to decrypt the message as well. 
The next function is very similar to the previous one, but instead of adding the value from 
the one-time pad’s sheet, you just need to subtract the value:

def decrypt(ciphertext, sheet):
    plaintext = ''
    for position, character in enumerate(ciphertext):
        if character not in ALPHABET:
            plaintext += character
        else:
            decrypted = (ALPHABET.index(character) - int(sheet[position])) % 26
            plaintext += ALPHABET[decrypted]
    return plaintext
Let’s test the decryption. Save and run your code, then type the following into the shell

sheet = load_sheet('otp0.txt')
ciphertext = encrypt('Nobody can read this - hehehe', sheet)
ciphertext
You should see the encrypted text. To decrypt, just type the following line:

decrypt(ciphertext, sheet)


Adding a menu
Although you now have working OTP generation, encryption and decryption, you should make 
the program a little easier for the user. This should include saving the encrypted text, 
so that it can be emailed to your friend.


