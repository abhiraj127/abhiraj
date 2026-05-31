# abhiraj
calculator
import tkinter as tk
import math

# Create window
root = tk.Tk()
root.title("Scientific Calculator")
root.geometry("450x600")
root.resizable(False, False)

# Display
display = tk.Entry(root, font=("Arial", 24), bd=10, relief=tk.RIDGE, justify="right")
display.grid(row=0, column=0, columnspan=5, padx=10, pady=10)

# Functions
def click(value):
    display.insert(tk.END, value)

def clear():
    display.delete(0, tk.END)

def calculate():
    try:
        expression = display.get()

        # Replace scientific functions
        expression = expression.replace("π", str(math.pi))
        expression = expression.replace("sin", "math.sin")
        expression = expression.replace("cos", "math.cos")
        expression = expression.replace("tan", "math.tan")
        expression = expression.replace("sqrt", "math.sqrt")
        expression = expression.replace("log", "math.log10")
        expression = expression.replace("ln", "math.log")

        result = eval(expression)
        display.delete(0, tk.END)
        display.insert(tk.END, result)

    except Exception:
        display.delete(0, tk.END)
        display.insert(tk.END, "Error")

# Buttons
buttons = [
    ('7',1,0), ('8',1,1), ('9',1,2), ('/',1,3), ('C',1,4),
    ('4',2,0), ('5',2,1), ('6',2,2), ('*',2,3), ('(',2,4),
    ('1',3,0), ('2',3,1), ('3',3,2), ('-',3,3), (')',3,4),
    ('0',4,0), ('.',4,1), ('+',4,2), ('=',4,3), ('π',4,4),

    ('sin(',5,0), ('cos(',5,1), ('tan(',5,2), ('sqrt(',5,3), ('x²',5,4),

    ('log(',6,0), ('ln(',6,1), ('**',6,2), ('%',6,3), ('⌫',6,4)
]

# Create buttons
for (text, row, col) in buttons:

    if text == '=':
        cmd = calculate
    elif text == 'C':
        cmd = clear
    elif text == '⌫':
        cmd = lambda: display.delete(len(display.get())-1, tk.END)
    elif text == 'x²':
        cmd = lambda: click("**2")
    else:
        cmd = lambda t=text: click(t)

    tk.Button(
        root,
        text=text,
        width=8,
        height=3,
        font=("Arial", 14),
        command=cmd
    ).grid(row=row, column=col, padx=5, pady=5)

root.mainloop()
