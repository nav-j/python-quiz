## **Python Quiz App (Tkinter GUI Version)**

Copy-paste this code into a file named **`python_quiz_gui.py`** and run it.

```python
import tkinter as tk
from tkinter import messagebox

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

# Quiz logic
class QuizApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Python Quiz App")
        self.root.geometry("600x400")
        self.root.config(bg="#f5f6fa")

        self.q_no = 0
        self.score = 0
        self.selected_option = tk.StringVar()

        self.create_widgets()
        self.load_question()

    def create_widgets(self):
        self.title_label = tk.Label(
            self.root, text=" Python Quiz", font=("Arial", 20, "bold"), bg="#f5f6fa", fg="#273c75"
        )
        self.title_label.pack(pady=10)

        self.question_label = tk.Label(
            self.root, text="", wraplength=500, justify="left", font=("Arial", 14), bg="#f5f6fa"
        )
        self.question_label.pack(pady=20)

        self.radio_buttons = []
        for i in range(4):
            btn = tk.Radiobutton(
                self.root,
                text="",
                variable=self.selected_option,
                value="",
                font=("Arial", 12),
                bg="#f5f6fa",
                anchor="w",
                padx=20,
            )
            btn.pack(fill="x", padx=100, pady=5)
            self.radio_buttons.append(btn)

        self.next_button = tk.Button(
            self.root,
            text="Next ➡️",
            command=self.next_question,
            font=("Arial", 12, "bold"),
            bg="#44bd32",
            fg="white",
            relief="flat",
            width=12,
        )
        self.next_button.pack(pady=20)

    def load_question(self):
        q_data = questions[self.q_no]
        self.question_label.config(text=f"Q{self.q_no + 1}. {q_data['question']}")
        self.selected_option.set(None)
        for i, option in enumerate(q_data["options"]):
            self.radio_buttons[i].config(text=option, value=option[0])  # A, B, C, D

    def next_question(self):
        chosen = self.selected_option.get()
        if not chosen:
            messagebox.showwarning("Warning", "Please select an answer before continuing.")
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
        message = f"Your Score: {self.score}/{len(questions)} ({percentage}%)\n\n"
        if percentage == 100:
            message += " Perfect! You’re a Python Pro!"
        elif percentage >= 70:
            message += " Great job! You know Python well."
        elif percentage >= 40:
            message += " Not bad, keep practicing."
        else:
            message += " You need more practice. Keep learning!"

        messagebox.showinfo("Quiz Result", message)
        self.root.destroy()


# Run App
if __name__ == "__main__":
    root = tk.Tk()
    app = QuizApp(root)
    root.mainloop()
```

---

### Features:

✅ Beautiful Tkinter GUI
✅ 10 Python MCQs
✅ Next button navigation
✅ Score with percentage & motivational feedback
✅ Auto-closes after results

---
