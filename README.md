# SCT_SC_1
def shift_text(message, key, mode="encrypt"):
    result_text = ""

    # Determine shift direction
    shift_factor = key if mode == "encrypt" else (-1 * key)

    for letter in message:
        if letter.isalpha():  # Process only letters
            ascii_base = ord('A') if letter.isupper() else ord('a')
            new_letter = chr((ord(letter) - ascii_base + shift_factor) % 26 + ascii_base)
            result_text += new_letter
        else:
            result_text += letter  # Keep non-letters unchanged

    return result_text


# Handling User Input
try:
    user_message = input("Enter message: ")
    shift_key = int(input("Enter shift amount (1-25): "))

    # Validate shift key
    if not (1 <= shift_key <= 25):
        raise ValueError("Shift key must be between 1 and 25.")

    mode_choice = input("Type 'encrypt' or 'decrypt': ").strip().lower()

    if mode_choice in ["encrypt", "decrypt"]:
        final_output = shift_text(user_message, shift_key, mode_choice)
        print(f"Final Output: {final_output}")
    else:
        print("Invalid option! Choose either 'encrypt' or 'decrypt'.")

except ValueError as e:
    print(f"Error: {e}")
