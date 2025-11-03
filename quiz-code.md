```python
# Python Quiz Game

def run_quiz():
    questions = [
        {
            "question": "1. Which of the following is the correct file extension for Python files?",
            "options": ["A) .pyt", "B) .pyth", "C) .pt", "D) .py"],
            "answer": "D"
        },
        {
            "question": "2. What is the output of print(2 ** 3)?",
            "options": ["A) 6", "B) 8", "C) 9", "D) 5"],
            "answer": "B"
        },
        {
            "question": "3. Which keyword is used to define a function in Python?",
            "options": ["A) func", "B) define", "C) def", "D) function"],
            "answer": "C"
        },
        {
            "question": "4. Which of the following is a valid variable name in Python?",
            "options": ["A) 2var", "B) my-var", "C) my_var", "D) my var"],
            "answer": "C"
        },
        {
            "question": "5. What is the output of print(type([]))?",
            "options": ["A) <class 'tuple'>", "B) <class 'dict'>", "C) <class 'list'>", "D) <class 'set'>"],
            "answer": "C"
        },
        {
            "question": "6. Which operator is used for floor division in Python?",
            "options": ["A) /", "B) //", "C) %", "D) **"],
            "answer": "B"
        },
        {
            "question": "7. What is the data type of True in Python?",
            "options": ["A) string", "B) int", "C) bool", "D) float"],
            "answer": "C"
        },
        {
            "question": "8. What is the result of 3 + 2 * 2?",
            "options": ["A) 10", "B) 7", "C) 8", "D) 9"],
            "answer": "B"
        },
        {
            "question": "9. Which of the following is a correct syntax for an if statement?",
            "options": ["A) if x > 5:", "B) if (x > 5)", "C) if x > 5 then:", "D) if x > 5 ->"],
            "answer": "A"
        },
        {
            "question": "10. What is the output of:\nfor i in range(3): print(i)",
            "options": ["A) 0 1 2", "B) 1 2 3", "C) 0 1 2 3", "D) Error"],
            "answer": "A"
        },
        {
            "question": "11. Which statement is used to import a module in Python?",
            "options": ["A) get", "B) include", "C) import", "D) load"],
            "answer": "C"
        },
        {
            "question": "12. What is the output of:\ndef add(a, b=2): return a + b\nprint(add(3))",
            "options": ["A) 3", "B) 5", "C) 2", "D) Error"],
            "answer": "B"
        },
        {
            "question": "13. Which of the following is immutable?",
            "options": ["A) list", "B) set", "C) tuple", "D) dict"],
            "answer": "C"
        },
        {
            "question": "14. What will be the output?\nmy_list = [1, 2, 3]\nprint(my_list[1])",
            "options": ["A) 1", "B) 2", "C) 3", "D) Error"],
            "answer": "B"
        },
        {
            "question": "15. How do you access the value of key 'name' in a dictionary student = {'name': 'Alex', 'age': 20}?",
            "options": ["A) student.name", "B) student['name']", "C) student[name]", "D) student.get[name]"],
            "answer": "B"
        }
    ]

    print("Welcome to the Python Quiz!")
    print("--------------------------------------------------")
    print("There are 15 questions. Type A, B, C, or D for each.\n")

    score = 0

    for q in questions:
        print(q["question"])
        for opt in q["options"]:
            print(opt)
        answer = input("Your answer: ").strip().upper()

        if answer == q["answer"]:
            print(" Correct!\n")
            score += 1
        else:
            print(f" Wrong! Correct answer: {q['answer']}\n")

    print("--------------------------------------------------")
    print(f"Your Final Score: {score} / {len(questions)}")

    if score == len(questions):
        print(" Excellent! Perfect score!")
    elif score >= 10:
        print(" Great job! You know Python well.")
    elif score >= 5:
        print(" Not bad, keep practicing.")
    else:
        print(" You need more practice. Keep learning!")

# Run the quiz
if __name__ == "__main__":
    run_quiz()
```

---

### Features:

✅ 15 MCQs
✅ Automatic score calculation
✅ Shows correct answers for mistakes
✅ Motivational feedback at the end

---
