<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Used To vs Would Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            background-color: #f4f4f4;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        #quiz-container {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .question {
            margin-bottom: 20px;
        }
        .options label {
            display: block;
            margin: 10px 0;
            cursor: pointer;
        }
        input[type="radio"], input[type="text"] {
            margin-right: 10px;
        }
        button {
            background-color: #28a745;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            display: block;
            margin: 20px auto;
        }
        button:hover {
            background-color: #218838;
        }
        #result {
            margin-top: 20px;
            font-weight: bold;
            text-align: center;
        }
        #explanation {
            margin-top: 10px;
            color: #555;
        }
        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <h1>Used To vs Would Quiz</h1>
    <div id="quiz-container">
        <div id="question"></div>
        <div id="options" class="options"></div>
        <div id="explanation" class="hidden"></div>
        <button id="submit-btn">Submit Answer</button>
        <button id="next-btn" class="hidden">Next Question</button>
        <div id="result" class="hidden"></div>
    </div>

    <script>
        const quizData = [
            {
                question: "When I was a child, I ______ play soccer every weekend.",
                type: "multiple",
                options: ["used to", "would", "Both are correct"],
                correct: "Both are correct",
                explanation: "'Used to' and 'would' both work for repeated actions in the past. 'Used to' emphasizes the habit, while 'would' sounds more like storytelling."
            },
            {
                question: "She ______ be very shy, but now she’s confident.",
                type: "multiple",
                options: ["used to", "would", "Both are correct"],
                correct: "used to",
                explanation: "'Used to' is correct for past states (like 'be shy'). 'Would' is only for repeated actions, so it doesn’t fit here."
            },
            {
                question: "Every summer, we ______ visit our cousins in the countryside.",
                type: "multiple",
                options: ["used to", "would", "Both are correct"],
                correct: "Both are correct",
                explanation: "Both 'used to' and 'would' can describe repeated actions in the past. 'Would' is especially good for nostalgic or storytelling contexts like this."
            },
            {
                question: "I ______ like spicy food, but now I love it. (Use negative form)",
                type: "fill",
                correct: "didn’t use to",
                explanation: "For negative past states or habits, use 'didn’t use to.' 'Would' doesn’t work for states or negatives in this context."
            },
            {
                question: "In the 1990s, people ______ write letters instead of emails.",
                type: "multiple",
                options: ["used to", "would", "Both are correct"],
                correct: "Both are correct",
                explanation: "Both 'used to' and 'would' work for repeated actions. 'Used to' highlights the change (emails now), while 'would' describes the past habit."
            },
            {
                question: "He ______ have long hair when he was younger.",
                type: "multiple",
                options: ["used to", "would", "Both are correct"],
                correct: "used to",
                explanation: "'Used to' is correct for past states (like 'have long hair'). 'Would' is only for actions, not states."
            },
            {
                question: "Every evening, my dad ______ read us a bedtime story.",
                type: "multiple",
                options: ["used to", "would", "Both are correct"],
                correct: "Both are correct",
                explanation: "Both 'used to' and 'would' can describe this repeated action. 'Would' feels more vivid and storytelling-like."
            },
            {
                question: "They ______ live in a big city, but now they prefer the countryside.",
                type: "fill",
                correct: "used to",
                explanation: "'Used to' is correct for past states (like 'live in a big city') and emphasizes the contrast with now. 'Would' doesn’t work for states."
            }
        ];

        let currentQuestion = 0;
        let score = 0;

        const questionEl = document.getElementById("question");
        const optionsEl = document.getElementById("options");
        const submitBtn = document.getElementById("submit-btn");
        const nextBtn = document.getElementById("next-btn");
        const explanationEl = document.getElementById("explanation");
        const resultEl = document.getElementById("result");

        function loadQuestion() {
            const q = quizData[currentQuestion];
            questionEl.textContent = `Question ${currentQuestion + 1}: ${q.question}`;
            optionsEl.innerHTML = "";
            explanationEl.classList.add("hidden");
            submitBtn.classList.remove("hidden");
            nextBtn.classList.add("hidden");

            if (q.type === "multiple") {
                q.options.forEach((option, index) => {
                    const label = document.createElement("label");
                    label.innerHTML = `<input type="radio" name="answer" value="${option}"> ${option}`;
                    optionsEl.appendChild(label);
                });
            } else {
                const input = document.createElement("input");
                input.type = "text";
                input.id = "fill-answer";
                input.placeholder = "Type your answer here";
                optionsEl.appendChild(input);
            }
        }

        function checkAnswer() {
            const q = quizData[currentQuestion];
            let userAnswer;

            if (q.type === "multiple") {
                const selected = document.querySelector('input[name="answer"]:checked');
                if (!selected) {
                    alert("Please select an answer!");
                    return;
                }
                userAnswer = selected.value;
            } else {
                userAnswer = document.getElementById("fill-answer").value.trim();
            }

            if (userAnswer.toLowerCase() === q.correct.toLowerCase()) {
                score++;
                explanationEl.innerHTML = `<strong>Correct!</strong> ${q.explanation}`;
                explanationEl.style.color = "#28a745";
            } else {
                explanationEl.innerHTML = `<strong>Incorrect.</strong> The correct answer is "${q.correct}". ${q.explanation}`;
                explanationEl.style.color = "#dc3545";
            }

            explanationEl.classList.remove("hidden");
            submitBtn.classList.add("hidden");
            nextBtn.classList.remove("hidden");
        }

        function nextQuestion() {
            currentQuestion++;
            if (currentQuestion < quizData.length) {
                loadQuestion();
            } else {
                questionEl.textContent = "Quiz Completed!";
                optionsEl.innerHTML = "";
                explanationEl.classList.add("hidden");
                submitBtn.classList.add("hidden");
                nextBtn.classList.add("hidden");
                resultEl.textContent = `Your score: ${score} out of ${quizData.length}`;
                resultEl.classList.remove("hidden");
            }
        }

        submitBtn.addEventListener("click", checkAnswer);
        nextBtn.addEventListener("click", nextQuestion);

        loadQuestion();
    </script>
</body>
</html>
