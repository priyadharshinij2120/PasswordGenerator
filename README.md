import tkinter as tk
from tkinter import messagebox
import random
import string

def generate_password():
    length = password_length.get()

    if length <= 0:
        messagebox.showerror("Error", "Enter a valid password length")
        return

    characters = ""

    if upper_var.get():
        characters += string.ascii_uppercase
    if lower_var.get():
        characters += string.ascii_lowercase
    if number_var.get():
        characters += string.digits
    if symbol_var.get():
        characters += string.punctuation

    if characters == "":
        messagebox.showerror("Error", "Select at least one option")
        return

    password = "".join(random.choice(characters) for _ in range(length))
    result_entry.delete(0, tk.END)
    result_entry.insert(0, password)

def copy_password():
    root.clipboard_clear()
    root.clipboard_append(result_entry.get())
    messagebox.showinfo("Copied", "Password copied to clipboard")

# Main window
root = tk.Tk()
root.title("Password Generator")
root.geometry("350x350")
root.resizable(False, False)

# Heading
tk.Label(root, text="PASSWORD GENERATOR", font=("Arial", 14, "bold")).pack(pady=10)

# Password length
tk.Label(root, text="Password Length").pack()
password_length = tk.IntVar(value=8)
tk.Entry(root, textvariable=password_length, width=10, justify="center").pack(pady=5)

# Checkboxes
upper_var = tk.BooleanVar(value=True)
lower_var = tk.BooleanVar(value=True)
number_var = tk.BooleanVar(value=True)
symbol_var = tk.BooleanVar(value=True)

tk.Checkbutton(root, text="Include Uppercase Letters", variable=upper_var).pack(anchor="w", padx=40)
tk.Checkbutton(root, text="Include Lowercase Letters", variable=lower_var).pack(anchor="w", padx=40)
tk.Checkbutton(root, text="Include Numbers", variable=number_var).pack(anchor="w", padx=40)
tk.Checkbutton(root, text="Include Symbols", variable=symbol_var).pack(anchor="w", padx=40)

# Generate button
tk.Button(root, text="Generate Password", bg="green", fg="white",
          command=generate_password).pack(pady=10)

# Output box
result_entry = tk.Entry(root, width=30, justify="center", font=("Arial", 10))
result_entry.pack(pady=5)

# Copy button
tk.Button(root, text="Copy Password", bg="blue", fg="white",
          command=copy_password).pack(pady=10)

# Footer
tk.Label(root, text="Internship Project - Python & Tkinter",
         font=("Arial", 8)).pack(side="bottom", pady=5)

root.mainloop()
