# passwordgenerator
import random
import string

def generate_password(length=12, use_uppercase=True, use_lowercase=True, use_numbers=True, use_special=True):
    if length < 4:
        print("Password length should be at least 4 for better security.")
        return None

    # Define character pools
    uppercase_letters = string.ascii_uppercase if use_uppercase else ""
    lowercase_letters = string.ascii_lowercase if use_lowercase else ""
    digits = string.digits if use_numbers else ""
    special_chars = string.punctuation if use_special else ""

    # Combine all pools
    all_characters = uppercase_letters + lowercase_letters + digits + special_chars
    if not all_characters:
        print("No character set selected. Please enable at least one type of character.")
        return None

    # Ensure password includes at least one of each selected type
    password = []
    if use_uppercase:
        password.append(random.choice(uppercase_letters))
    if use_lowercase:
        password.append(random.choice(lowercase_letters))
    if use_numbers:
        password.append(random.choice(digits))
    if use_special:
        password.append(random.choice(special_chars))

    # Fill the rest of the password length with random choices
    remaining_length = length - len(password)
    if remaining_length > 0:
        password.extend(random.choices(all_characters, k=remaining_length))

    # Shuffle the result to avoid predictable patterns
    random.shuffle(password)
    return ''.join(password)

# User input for customization
length = int(input("Enter the desired password length: "))
use_uppercase = input("Include uppercase letters? (y/n): ").strip().lower() == 'y'
use_lowercase = input("Include lowercase letters? (y/n): ").strip().lower() == 'y'
use_numbers = input("Include numbers? (y/n): ").strip().lower() == 'y'
use_special = input("Include special characters? (y/n): ").strip().lower() == 'y'

# Generate and display the password
password = generate_password(length, use_uppercase, use_lowercase, use_numbers, use_special)
if password:
    print(f"Generated password: {password}")
