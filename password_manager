from tkinter import *
from tkinter import messagebox
from random import choice, randint, shuffle
from pyperclip import copy
import json

FONT = ("Ariel", 10, "normal")


# ---------------------------- SEARCH FUNCTION ------------------------------- #
def search():
    website = web_input.get()
    try:
        with open("data.json", mode="r") as check:
            data = json.load(check)
    except FileNotFoundError:
        messagebox.showinfo(title="Error", message="No Data File Found.")
    else:
        if website in data:
            username = data[website]['email']
            password = data[website]['password']
            messagebox.showinfo(title=f"{website} Details", message=f"Username/Email: {username}\n"
                                                                    f"Password: {password}")
        else:
            messagebox.showinfo(title="Error", message="You dont have details for this website.")


# ---------------------------- PASSWORD GENERATOR ------------------------------- #
def generate_pw():
    letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u',
               'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P',
               'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
    numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
    symbols = ['!', '#', '$', '%', '&', '(', ')', '*', '+']

    password_list = []
    password_list += [choice(letters) for _ in range(randint(8, 10))]
    password_list += [choice(symbols) for _ in range(randint(2, 4))]
    password_list += [choice(numbers) for _ in range(randint(2, 4))]

    shuffle(password_list)

    password = "".join(password_list)
    pass_input.insert(0, password)
    copy(password)


# ---------------------------- SAVE PASSWORD ------------------------------- #
def save():
    website = web_input.get()
    email = user_input.get()
    password = pass_input.get()
    new_data = {
        website: {
            "email": email,
            "password": password,
        }
    }

    if len(website) == 0 or len(password) == 0:
        messagebox.showwarning(title="Unfilled Fields", message="Please fill out all the fields.")
    else:
        try:
            with open("data.json", mode="r") as saves:
                data = json.load(saves)
        except FileNotFoundError:
            with open("data.json", mode="w") as saves:
                json.dump(new_data, saves, indent=4)
        else:
            data.update(new_data)
            with open("data.json", mode="w") as saves:
                json.dump(data, saves, indent=4)
        finally:
            pass_input.delete(0, END)
            web_input.delete(0, END)


# ---------------------------- UI SETUP ------------------------------- #
window = Tk()
window.title("Password Manager")
window.config(padx=50, pady=50, bg="white")

canvas = Canvas(width=200, height=200, bg="white", highlightthickness=0)
lock_image = PhotoImage(file="logo.png")
canvas.create_image(100, 100, image=lock_image)
canvas.grid(column=1, row=0)

website_label = Label(text="Website:", font=FONT, bg="white")
website_label.grid(column=0, row=1)

email_label = Label(text="Email/Username:", font=FONT, bg="white")
email_label.grid(column=0, row=2)

password_label = Label(text="Password:", font=FONT, bg="white")
password_label.grid(column=0, row=3)

web_input = Entry(width=32)
web_input.config(highlightthickness=1)
web_input.grid(column=1, row=1)
web_input.focus()

user_input = Entry(width=51)
user_input.config(highlightthickness=1)
user_input.insert(0, "jay99@gmail.com")
user_input.grid(column=1, row=2, columnspan=2)

pass_input = Entry(width=32)
pass_input.config(highlightthickness=1)
pass_input.grid(column=1, row=3)

gen_but = Button(text="Generate Password", command=generate_pw)
gen_but.grid(column=2, row=3)

add_but = Button(text="Add", width=43, command=save)
add_but.grid(column=1, row=4, columnspan=2)

search_but = Button(text="Search", width=15, command=search)
search_but.grid(column=2, row=1)
window.mainloop()
