### **File Name:** `python_quiz_app_fixed.py`

```python
import tkinter as tk
from tkinter import ttk, messagebox
from datetime import datetime
import os

# =======================
# QUIZ QUESTIONS
# =======================
questions = [
    # Section A: Basics of Python
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

    # Section B: Data Types & Operators
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

    # Section C: Control Flow
    {
        "question": "Which of the following is a correct syntax for an if statement?",
        "options": ["A) if x > 5:", "B) if (x > 5)", "C) if x > 5 then:", "D) if x > 5 ->"],
        "answer": "A"
    },
    {
        "question": "What will be the output of:\n\nfor i in range(3):\n    print(i)",
        "options": ["A) 0 1 2", "B) 1 2 3", "C) 0 1 2 3", "D) Error"],
        "answer": "A"
    },

    # Section D: Functions & Modules
    {
        "question": "Which statement is used to import a module in Python?",
        "options": ["A) get", "B) include", "C) import", "D) load"],
        "answer": "C"
    },
    {
        "question": "What is the output of:\n\ndef add(a, b=2):\n    return a + b\nprint(add(3))",
        "options": ["A) 3", "B) 5", "C) 2", "D) Error"],
        "answer": "B"
    },

    # Section E: Lists, Tuples, and Dictionaries
    {
        "question": "Which of the following is immutable?",
        "options": ["A) list", "B) set", "C) tuple", "D) dict"],
        "answer": "C"
    },
    {
        "question": "What will be the output?\n\nmy_list = [1, 2, 3]\nprint(my_list[1])",
        "options": ["A) 1", "B) 2", "C) 3", "D) Error"],
        "answer": "B"
    },
    {
        "question": "How do you access the value of key 'name' in a dictionary student = {'name': 'Alex', 'age': 20}?",
        "options": ["A) student.name", "B) student['name']", "C) student[name]", "D) student.get[name]"],
        "answer": "B"
    }
]


# =======================
# QUIZ APPLICATION CLASS
# =======================
class QuizApp:
    def __init__(self, root):
        self.root = root
        self.root.title("🐍 Python Quiz App")
        self.root.geometry("680x500")
        self.root.config(bg="#f5f6fa")

        self.q_no = 0
        self.score = 0
        self.selected_option = tk.StringVar()
        self.username = ""

        self.show_welcome_screen()

    # -------------------------------
    # WELCOME SCREEN
    # -------------------------------
    def show_welcome_screen(self):
        self.clear_window()

        tk.Label(
            self.root, text="🧠 Welcome to the Python Quiz Challenge",
            font=("Helvetica", 18, "bold"), bg="#f5f6fa", fg="#273c75", wraplength=550
        ).pack(pady=40)

        tk.Label(
            self.root, text="Please enter your name to begin:",
            font=("Arial", 12), bg="#f5f6fa", fg="#353b48"
        ).pack(pady=10)

        self.name_entry = tk.Entry(self.root, font=("Arial", 14), width=25, justify="center")
        self.name_entry.pack(pady=10)
        self.name_entry.focus()

        tk.Button(
            self.root, text="Start Quiz ➡️", command=self.start_quiz,
            font=("Arial", 12, "bold"), bg="#44bd32", fg="white", relief="flat", width=15
        ).pack(pady=20)

    def start_quiz(self):
        name = self.name_entry.get().strip()
        if not name:
            messagebox.showwarning("⚠️ Warning", "Please enter your name before starting.")
            return
        self.username = name
        self.create_quiz_ui()
        self.load_question()

    # -------------------------------
    # QUIZ UI
    # -------------------------------
    def create_quiz_ui(self):
        self.clear_window()

        tk.Label(
            self.root, text="🧠 Python Quiz Challenge",
            font=("Helvetica", 20, "bold"), bg="#f5f6fa", fg="#273c75"
        ).pack(pady=10)

        tk.Label(
            self.root, text=f"👤 Player: {self.username}",
            font=("Arial", 12, "italic"), bg="#f5f6fa", fg="#353b48"
        ).pack(pady=5)

        self.progress = ttk.Progressbar(self.root, length=400, mode="determinate")
        self.progress.pack(pady=10)

        self.question_label = tk.Label(
            self.root, text="", wraplength=600, justify="left",
            font=("Helvetica", 14), bg="#f5f6fa"
        )
        self.question_label.pack(pady=15)

        self.radio_buttons = []
        for i in range(4):
            btn = tk.Radiobutton(
                self.root, text="", variable=self.selected_option,
                value="", font=("Arial", 12), bg="#f5f6fa",
                anchor="w", padx=20
            )
            btn.pack(fill="x", padx=100, pady=5)
            self.radio_buttons.append(btn)

        # Buttons
        frame = tk.Frame(self.root, bg="#f5f6fa")
        frame.pack(pady=20)

        tk.Button(
            frame, text="Next ➡️", command=self.next_question,
            font=("Arial", 12, "bold"), bg="#44bd32", fg="white", relief="flat", width=12
        ).grid(row=0, column=0, padx=10)

        tk.Button(
            frame, text="🔁 Restart", command=self.restart_quiz,
            font=("Arial", 12, "bold"), bg="#273c75", fg="white", relief="flat", width=12
        ).grid(row=0, column=1, padx=10)

        tk.Button(
            frame, text="📄 View Results", command=self.view_results,
            font=("Arial", 12, "bold"), bg="#718093", fg="white", relief="flat", width=14
        ).grid(row=0, column=2, padx=10)

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
            msg += "🏆 Perfect! You’re a Python Pro!"
        elif percentage >= 70:
            msg += "💪 Great job! You know Python well."
        elif percentage >= 40:
            msg += "🙂 Not bad, keep practicing."
        else:
            msg += "📘 You need more practice."

        self.save_score(self.username, self.score, percentage)
        messagebox.showinfo("🎯 Quiz Result", msg)
        self.show_welcome_screen()

    def save_score(self, username, score, percentage):
        with open("results.txt", "a") as f:
            timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
            f.write(f"{timestamp} | {username} | Score: {score}/{len(questions)} ({percentage}%)\n")

    def view_results(self):
        if not os.path.exists("results.txt"):
            messagebox.showinfo("📄 No Results", "No results found yet.")
            return

        with open("results.txt", "r") as f:
            data = f.read().strip()

        if not data:
            messagebox.showinfo("📄 No Results", "No results found yet.")
        else:
            top = tk.Toplevel(self.root)
            top.title("📜 Past Quiz Results")
            top.geometry("550x350")
            top.config(bg="#f5f6fa")

            tk.Label(top, text="📄 Past Quiz Results", font=("Helvetica", 16, "bold"), bg="#f5f6fa", fg="#273c75").pack(pady=10)
            box = tk.Text(top, wrap="word", font=("Consolas", 11), bg="#ffffff", fg="#2f3640")
            box.pack(expand=True, fill="both", padx=15, pady=10)
            box.insert("1.0", data)
            box.config(state="disabled")

    def restart_quiz(self):
        self.q_no = 0
        self.score = 0
        self.load_question()
        self.progress["value"] = 0

    def clear_window(self):
        for widget in self.root.winfo_children():
            widget.destroy()


# =======================
# RUN APP
# =======================
if __name__ == "__main__":
    root = tk.Tk()
    app = QuizApp(root)
    root.mainloop()
```

---

### **Features**

✅ Runs in **one single window** (no popups for quiz start).
✅ Clean UI with **welcome screen**, **progress bar**, and **results storage**.
✅ **Auto-saves scores** with name and timestamp in `results.txt`.
✅ **Restart** or **view past results** anytime.

