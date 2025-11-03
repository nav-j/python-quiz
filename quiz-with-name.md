✅ Ask the **user’s name** before the quiz starts
✅ Show that name during the quiz
✅ Save the name, score, and timestamp to `results.txt`

---

## **Python Quiz App (Final Personalized Version)**

Save this as **`python_quiz_personalized.py`** and run it:

```python
import tkinter as tk
from tkinter import ttk, messagebox, simpledialog
from datetime import datetime

# Quiz Data
questions = [
    {
        "question": "Which of the following is the correct file extension for Python files?",
        "options": ["A) .pyt", "B) .pyth", "C) .pt", "D) .py"],
        "answer": "D"
    },
    {
        "question": "What is the output of print(2 ** 3)?",
        "options": ["A) 6", "B) 8", "C) 9", "D) 5"],
        "answer": "B"
    },
    {
        "question": "Which keyword is used to define a function in Python?",
        "options": ["A) func", "B) define", "C) def", "D) function"],
        "answer": "C"
    },
    {
        "question": "Which of the following is a valid variable name in Python?",
        "options": ["A) 2var", "B) my-var", "C) my_var", "D) my var"],
        "answer": "C"
    },
    {
        "question": "What is the output of print(type([]))?",
        "options": ["A) <class 'tuple'>", "B) <class 'dict'>", "C) <class 'list'>", "D) <class 'set'>"],
        "answer": "C"
    },
    {
        "question": "Which operator is used for floor division in Python?",
        "options": ["A) /", "B) //", "C) %", "D) **"],
        "answer": "B"
    },
    {
        "question": "What is the data type of True in Python?",
        "options": ["A) string", "B) int", "C) bool", "D) float"],
        "answer": "C"
    },
    {
        "question": "What is the result of 3 + 2 * 2?",
        "options": ["A) 10", "B) 7", "C) 8", "D) 9"],
        "answer": "B"
    },
    {
        "question": "Which of the following is a correct syntax for an if statement?",
        "options": ["A) if x > 5:", "B) if (x > 5)", "C) if x > 5 then:", "D) if x > 5 ->"],
        "answer": "A"
    },
    {
        "question": "Which of the following is immutable?",
        "options": ["A) list", "B) set", "C) tuple", "D) dict"],
        "answer": "C"
    }
]


class QuizApp:
    def __init__(self, root):
        self.root = root
        self.root.title("🐍 Python Quiz App")
        self.root.geometry("650x450")
        self.root.config(bg="#f5f6fa")

        self.q_no = 0
        self.score = 0
        self.selected_option = tk.StringVar()
        self.username = ""

        # Ask for name before starting
        self.ask_username()

        self.create_widgets()
        self.load_question()

    def ask_username(self):
        """Prompt the user to enter their name before starting."""
        self.username = simpledialog.askstring("Enter Your Name", "Please enter your name:")
        if not self.username:
            self.username = "Guest"

    def create_widgets(self):
        # Title
        self.title_label = tk.Label(
            self.root, text="🧠 Python Quiz Challenge",
            font=("Helvetica", 20, "bold"), bg="#f5f6fa", fg="#273c75"
        )
        self.title_label.pack(pady=10)

        # Show Username
        self.user_label = tk.Label(
            self.root, text=f"👤 Player: {self.username}",
            font=("Arial", 12, "italic"), bg="#f5f6fa", fg="#353b48"
        )
        self.user_label.pack(pady=5)

        # Progress Bar
        self.progress = ttk.Progressbar(self.root, length=400, mode="determinate")
        self.progress.pack(pady=10)

        # Question Label
        self.question_label = tk.Label(
            self.root, text="", wraplength=550, justify="left",
            font=("Helvetica", 14), bg="#f5f6fa"
        )
        self.question_label.pack(pady=15)

        # Radio Buttons
        self.radio_buttons = []
        for i in range(4):
            btn = tk.Radiobutton(
                self.root, text="", variable=self.selected_option,
                value="", font=("Arial", 12), bg="#f5f6fa",
                anchor="w", padx=20
            )
            btn.pack(fill="x", padx=100, pady=5)
            self.radio_buttons.append(btn)

        # Buttons Frame
        self.button_frame = tk.Frame(self.root, bg="#f5f6fa")
        self.button_frame.pack(pady=20)

        self.next_button = tk.Button(
            self.button_frame, text="Next ➡️",
            command=self.next_question,
            font=("Arial", 12, "bold"), bg="#44bd32",
            fg="white", relief="flat", width=12
        )
        self.next_button.grid(row=0, column=0, padx=10)

        self.restart_button = tk.Button(
            self.button_frame, text="🔁 Restart",
            command=self.restart_quiz,
            font=("Arial", 12, "bold"), bg="#273c75",
            fg="white", relief="flat", width=12
        )
        self.restart_button.grid(row=0, column=1, padx=10)

    def load_question(self):
        q_data = questions[self.q_no]
        self.question_label.config(text=f"Q{self.q_no + 1}. {q_data['question']}")
        self.selected_option.set(None)

        for i, option in enumerate(q_data["options"]):
            self.radio_buttons[i].config(text=option, value=option[0])

        self.progress["value"] = (self.q_no / len(questions)) * 100

    def next_question(self):
        chosen = self.selected_option.get()
        if not chosen:
            messagebox.showwarning("⚠️ Warning", "Please select an answer before continuing.")
            return

        correct = questions[self.q_no]["answer"]
        if chosen == correct:
            self.score += 1

        self.q_no += 1

        if self.q_no < len(questions):
            self.load_question()
        else:
            self.show_result()

    def show_result(self):
        percentage = int((self.score / len(questions)) * 100)
        msg = f"{self.username}, your Score: {self.score}/{len(questions)} ({percentage}%)\n\n"

        if percentage == 100:
            msg += " Perfect! You’re a Python Pro!"
        elif percentage >= 70:
            msg += " Great job! You know Python well."
        elif percentage >= 40:
            msg += " Not bad, keep practicing."
        else:
            msg += " You need more practice. Keep learning!"

        # Save results to file
        self.save_score(self.username, self.score, percentage)

        messagebox.showinfo("🎯 Quiz Result", msg)
        self.restart_quiz()

    def save_score(self, username, score, percentage):
        """Save quiz result with username and timestamp."""
        with open("results.txt", "a") as file:
            timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
            file.write(f"{timestamp} | {username} | Score: {score}/{len(questions)} ({percentage}%)\n")

    def restart_quiz(self):
        self.q_no = 0
        self.score = 0
        self.load_question()
        self.progress["value"] = 0


# Run App
if __name__ == "__main__":
    root = tk.Tk()
    app = QuizApp(root)
    root.mainloop()
```

---

###  **Results file now looks like this:**

```
2025-11-03 11:45:12 | Navjot | Score: 9/10 (90%)
2025-11-03 12:02:37 | Guest | Score: 7/10 (70%)
```

---

###  **New Features**

✅ Asks for user name
✅ Displays name during quiz
✅ Saves name + score + timestamp
✅ Progress bar & restart option
✅ Clean UI and motivational messages

---
