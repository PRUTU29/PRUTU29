import tkinter as tk
from tkinter import simpledialog, messagebox

class BankManagementSystem:
    def __init__(self, master):
        self.master = master
        self.master.title("Bank Management System")
        self.master.geometry("600x400")

        # Variables
        self.account_balance = 0

        # Labels
        self.balance_label = tk.Label(self.master, text="Account Balance: $0")
        self.balance_label.pack(pady=10)

        # Buttons
        self.deposit_button = tk.Button(self.master, text="Deposit", command=self.deposit)
        self.deposit_button.pack(pady=10)

        self.withdraw_button = tk.Button(self.master, text="Withdraw", command=self.withdraw)
        self.withdraw_button.pack(pady=10)

        self.check_balance_button = tk.Button(self.master, text="Check Balance", command=self.check_balance)
        self.check_balance_button.pack(pady=10)

        # Module Buttons
        self.module_buttons = []
        module_names = ["loan", "Module 2", "Module 3", "Module 4", "Module 5", "Module 6", "Module 7", "Module 8", "Module 9", "Module 10"]

        for module_name in module_names:
            button = tk.Button(self.master, text=module_name, command=lambda name=module_name: self.module_placeholder(name))
            button.pack(pady=5)
            self.module_buttons.append(button)

    def deposit(self):
        amount = self.get_amount("Enter deposit amount:")
        if amount:
            self.account_balance += amount
            self.update_balance_label()

    def withdraw(self):
        amount = self.get_amount("Enter withdrawal amount:")
        if amount:
            if amount <= self.account_balance:
                self.account_balance -= amount
                self.update_balance_label()
            else:
                messagebox.showerror("Error", "Insufficient funds")

    def check_balance(self):
        messagebox.showinfo("Balance", f"Your account balance is: ${self.account_balance}")

    def module_placeholder(self, module_name):
        messagebox.showinfo("Module Placeholder", f"This is a placeholder for {module_name}")

    def get_amount(self, prompt):
        amount = simpledialog.askfloat("Input", prompt)
        if amount is not None:
            return amount
        return None

    def update_balance_label(self):
        self.balance_label.config(text=f"Account Balance: ${self.account_balance}")


if __name__ == "__main__":
    root = tk.Tk()
    app = BankManagementSystem(root)
    root.mainloop()
