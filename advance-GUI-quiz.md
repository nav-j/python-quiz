 **upgraded GUI Python Quiz App** with:

✅ A **progress bar**
✅ A **“Restart Quiz”** button
✅ A polished modern design

---

## **Python Quiz App (Tkinter GUI – Advanced Version)**

Copy-paste this code into a file named **`python_quiz_gui_advanced.py`** and run it:

```python
import tkinter as tk
from tkinter import ttk, messagebox

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


# Quiz App Class
class QuizApp:
    def __init__(self, root):
        self.root = root
        self.root.title("🐍 Python Quiz App")
        self.root.geometry("650x450")
        self.root.config(bg="#f5f6fa")

        self.q_no = 0
        self.score = 0
        self.selected_option = tk.StringVar()

        self.create_widgets()
        self.load_question()

    def create_widgets(self):
        # Title
        self.title_label = tk.Label(
            self.root, text="🧠 Python Quiz Challenge",
            font=("Helvetica", 20, "bold"), bg="#f5f6fa", fg="#273c75"
        )
        self.title_label.pack(pady=10)

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
        msg = f"Your Score: {self.score}/{len(questions)} ({percentage}%)\n\n"

        if percentage == 100:
            msg += " Perfect! You’re a Python Pro!"
        elif percentage >= 70:
            msg += " Great job! You know Python well."
        elif percentage >= 40:
            msg += " Not bad, keep practicing."
        else:
            msg += " You need more practice. Keep learning!"

        messagebox.showinfo(" Quiz Result", msg)
        self.restart_quiz()

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

### **Features Added**

✅ Clean modern GUI
✅ Progress bar (shows quiz progress)
✅ Restart quiz anytime
✅ Motivational feedback messages
✅ Auto-restart after results

---
