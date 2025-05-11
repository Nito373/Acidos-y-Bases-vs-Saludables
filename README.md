<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ácidos y Bases vs Saludable</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f8ff;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            flex-direction: column;
        }

        h1 {
            color: #333;
        }

        .question-container {
            text-align: center;
        }

        .question {
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 20px;
        }

        .options {
            display: flex;
            justify-content: center;
            gap: 20px;
        }

        .option-button {
            padding: 10px 20px;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .option-button:hover {
            background-color: #0056b3;
        }

        .score {
            font-size: 20px;
            margin-top: 20px;
        }

        .message {
            font-size: 24px;
            font-weight: bold;
            margin-top: 30px;
        }

        .timer {
            font-size: 20px;
            color: red;
            margin-top: 10px;
        }

        .reset-button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 20px;
        }

        .reset-button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

    <h1>Ácidos y Bases vs Saludable</h1>
    <p>Responde correctamente las preguntas sobre alimentos.</p>

    <div class="question-container">
        <div class="question" id="question">Pregunta</div>

        <div class="options">
            <button class="option-button" onclick="checkAnswer('acid')">Ácido</button>
            <button class="option-button" onclick="checkAnswer('base')">Base</button>
            <button class="option-button" onclick="checkAnswer('healthy')">Saludable</button>
        </div>

        <div class="timer" id="timer">Tiempo: 10s</div>
    </div>

    <div class="score">Puntaje: <span id="score">0</span></div>

    <div class="message" id="message"></div>

    <button class="reset-button" onclick="resetGame()">Reiniciar Juego</button>

    <script>
        const questions = [
            // Preguntas Ácido
            {
                question: "¿El limón es ácido o saludable?",
                correctAnswer: "acid",
                difficulty: 1,
            },
            {
                question: "¿El vinagre es ácido o saludable?",
                correctAnswer: "acid",
                difficulty: 1,
            },
            {
                question: "¿El jugo de naranja es ácido o saludable?",
                correctAnswer: "acid",
                difficulty: 1,
            },
            {
                question: "¿El tomate es ácido o saludable?",
                correctAnswer: "acid",
                difficulty: 2,
            },
            {
                question: "¿El aguacate es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 2,
            },
            {
                question: "¿El jugo de manzana es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 3,
            },
            {
                question: "¿El café es ácido o saludable?",
                correctAnswer: "acid",
                difficulty: 3,
            },
            {
                question: "¿El agua con gas es ácido o básico?",
                correctAnswer: "acid",
                difficulty: 4,
            },
            {
                question: "¿La Coca Cola es ácida o saludable?",
                correctAnswer: "acid",
                difficulty: 5,
            },
            {
                question: "¿El limón tiene un pH bajo, por lo tanto, es ácido?",
                correctAnswer: "acid",
                difficulty: 5,
            },
            // Preguntas Base
            {
                question: "¿La leche es ácida o básica?",
                correctAnswer: "base",
                difficulty: 1,
            },
            {
                question: "¿El bicarbonato de sodio es ácido o básico?",
                correctAnswer: "base",
                difficulty: 1,
            },
            {
                question: "¿El jabón es ácido o básico?",
                correctAnswer: "base",
                difficulty: 2,
            },
            {
                question: "¿El agua con bicarbonato es ácido o básico?",
                correctAnswer: "base",
                difficulty: 3,
            },
            {
                question: "¿La amoniaco es ácido o básico?",
                correctAnswer: "base",
                difficulty: 3,
            },
            {
                question: "¿La sal de mesa es ácido o básico?",
                correctAnswer: "base",
                difficulty: 4,
            },
            {
                question: "¿El vinagre tiene pH bajo y es ácido?",
                correctAnswer: "acid",
                difficulty: 5,
            },
            {
                question: "¿El limpiador doméstico tiene un pH básico?",
                correctAnswer: "base",
                difficulty: 5,
            },
            // Preguntas Saludables
            {
                question: "¿El plátano es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 1,
            },
            {
                question: "¿La manzana es saludable o ácida?",
                correctAnswer: "healthy",
                difficulty: 1,
            },
            {
                question: "¿La zanahoria es saludable o ácida?",
                correctAnswer: "healthy",
                difficulty: 1,
            },
            {
                question: "¿La espinaca es saludable o ácida?",
                correctAnswer: "healthy",
                difficulty: 2,
            },
            {
                question: "¿El pepino es saludable o ácido?",
                correctAnswer: "healthy",
                difficulty: 2,
            },
            {
                question: "¿La lechuga es saludable o ácida?",
                correctAnswer: "healthy",
                difficulty: 2,
            },
            {
                question: "¿El pepino es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 3,
            },
            {
                question: "¿El aguacate es saludable o ácido?",
                correctAnswer: "healthy",
                difficulty: 3,
            },
            {
                question: "¿El tomate es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 3,
            },
            {
                question: "¿El aceite de oliva es saludable o ácido?",
                correctAnswer: "healthy",
                difficulty: 4,
            },
            {
                question: "¿Las fresas son saludables o ácidas?",
                correctAnswer: "healthy",
                difficulty: 4,
            },
            {
                question: "¿El brócoli es saludable o ácido?",
                correctAnswer: "healthy",
                difficulty: 4,
            },
            {
                question: "¿Las zanahorias son saludables o ácidas?",
                correctAnswer: "healthy",
                difficulty: 5,
            },
            {
                question: "¿El mango es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 5,
            },
            {
                question: "¿Las moras son saludables o ácidas?",
                correctAnswer: "healthy",
                difficulty: 5,
            },
            {
                question: "¿El pepino es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 5,
            },
            // Más Preguntas (más de 30 preguntas adicionales)
            {
                question: "¿El ajo es saludable o ácido?",
                correctAnswer: "healthy",
                difficulty: 3,
            },
            {
                question: "¿El jengibre es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 3,
            },
            {
                question: "¿El apio es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 3,
            },
            {
                question: "¿Las nueces son saludables o ácidas?",
                correctAnswer: "healthy",
                difficulty: 4,
            },
            {
                question: "¿El pepino tiene un pH bajo o saludable?",
                correctAnswer: "healthy",
                difficulty: 2,
            },
            {
                question: "¿El coliflor es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 3,
            },
            {
                question: "¿El tomate tiene un pH bajo, por lo que es ácido?",
                correctAnswer: "healthy",
                difficulty: 2,
            },
            {
                question: "¿La granada es saludable o ácida?",
                correctAnswer: "healthy",
                difficulty: 3,
            },
            {
                question: "¿Las uvas son saludables o ácidas?",
                correctAnswer: "healthy",
                difficulty: 4,
            },
            {
                question: "¿El pimiento rojo es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 2,
            },
            {
                question: "¿El aceite de coco es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 4,
            },
            {
                question: "¿La naranja es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 4,
            },
            {
                question: "¿La sandía es ácido o saludable?",
                correctAnswer: "healthy",
                difficulty: 4,
            },
            {
                question: "¿Las almendras son saludables o ácidas?",
                correctAnswer: "healthy",
                difficulty: 4,
            },
            {
                question: "¿El aguacate tiene un pH bajo o saludable?",
                correctAnswer: "healthy",
                difficulty: 4,
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;
        let timeLeft = 10; // Tiempo en segundos
        let timerInterval;
        let gameOver = false;

        function loadQuestion() {
            if (currentQuestionIndex < questions.length && !gameOver) {
                const questionData = questions[currentQuestionIndex];
                document.getElementById("question").innerText = questionData.question;
                timeLeft = 10; // Resetear el tiempo
                document.getElementById("timer").innerText = `Tiempo: ${timeLeft}s`;
                startTimer();

            } else {
                endGame();
            }
        }

        function checkAnswer(answer) {
            const correctAnswer = questions[currentQuestionIndex].correctAnswer;
            
            if (answer === correctAnswer) {
                score += questions[currentQuestionIndex].difficulty;
                document.getElementById("message").innerText = "¡Correcto!";
            } else {
                score -= questions[currentQuestionIndex].difficulty;
                document.getElementById("message").innerText = "¡Incorrecto!";
            }

            document.getElementById("score").innerText = score;
            currentQuestionIndex++;
            stopTimer();
            loadQuestion();
        }

        function startTimer() {
            timerInterval = setInterval(() => {
                timeLeft--;
                document.getElementById("timer").innerText = `Tiempo: ${timeLeft}s`;

                if (timeLeft <= 0) {
                    stopTimer();
                    score -= 2; // Penalización por tiempo agotado
                    document.getElementById("score").innerText = score;
                    document.getElementById("message").innerText = "¡Tiempo agotado!";
                    currentQuestionIndex++;
                    loadQuestion();
                }
            }, 1000);
        }

        function stopTimer() {
            clearInterval(timerInterval);
        }

        function endGame() {
            gameOver = true;
            document.getElementById("message").innerText = `¡Juego terminado! Tu puntaje final es: ${score}`;
            document.querySelector(".options").style.display = "none"; // Ocultar las opciones
        }

        function resetGame() {
            score = 0;
            currentQuestionIndex = 0;
            document.getElementById("score").innerText = score;
            document.getElementById("message").innerText = "";
            document.querySelector(".options").style.display = "flex";
            gameOver = false;
            loadQuestion();
        }

        // Iniciar el juego
        loadQuestion();
    </script>

</body>
</html>      
