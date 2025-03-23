# Quizgame

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Quiz App</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            text-align: center; 
        }
        .quiz-container { 
            width: 50%; margin: auto; 
            padding: 20px; border: 1px solid #ccc; 
            border-radius: 10px; 
        }
        .question { 
            font-size: 1.2em; 
        }
        .options button { 
            display: block; margin: 10px auto; 
            padding: 10px; width: 80%; 
            cursor: pointer;
         }
        .correct { 
            background-color: lightgreen; 
        }
        .wrong { 
            background-color: lightcoral;
         }
    </style>
</head>
<body>
    <div class="quiz-container">
        <h1>Quiz App</h1>
        <p class="question"></p>
        <div class="options"></div>
        <p>Score: <span id="score">0</span></p>
        <button onclick="resetQuiz()">Reset</button>
    </div>

    <script>
        const questions = [
            { question: "What is the capital of France?", options: ["Paris", "London", "Berlin", "Madrid"], answer: 0 },
            { question: "What is 2 + 2?", options: ["3", "4", "5", "6"], answer: 1 },
            { question: "Which planet is known as the Red Planet?", options: ["Earth", "Mars", "Jupiter", "Venus"], answer: 1 }
        ];

        let currentQuestion = 0;
        let score = 0;

        function loadQuestion() {
            const quiz = document.querySelector(".quiz-container");
            const questionElement = document.querySelector(".question");
            const optionsElement = document.querySelector(".options");
            
            questionElement.textContent = questions[currentQuestion].question;
            optionsElement.innerHTML = "";

            questions[currentQuestion].options.forEach((option, index) => {
                let button = document.createElement("button");
                button.textContent = option;
                button.onclick = () => checkAnswer(index, button);
                optionsElement.appendChild(button);
            });
        }

        function checkAnswer(index, button) {
            if (index === questions[currentQuestion].answer) {
                button.classList.add("correct");
                score++;
                document.getElementById("score").textContent = score;
            } else {
                button.classList.add("wrong");
            }
            setTimeout(() => {
                currentQuestion++;
                if (currentQuestion < questions.length) {
                    loadQuestion();
                } else {
                    alert("Quiz Over! Your final score: " + score);
                }
            }, 1000);
        }

        function resetQuiz() {
            currentQuestion = 0;
            score = 0;
            document.getElementById("score").textContent = score;
            loadQuestion();
        }

        loadQuestion();
    </script>
</body>
</html>
