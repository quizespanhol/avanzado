<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>Español Avanzado - Quiz para Brasileiros</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Arial', 'Helvetica', sans-serif;
            background: #8B0000; /* Vermelho escuro sólido */
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 15px;
        }
        
        .quiz-container {
            width: 100%;
            max-width: 550px;
            background: #FFFFFF; /* Branco sólido */
            border-radius: 30px;
            padding: 25px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
            border: 4px solid #FFD700; /* Amarelo ouro */
        }
        
        .quiz-header {
            text-align: center;
            margin-bottom: 25px;
        }
        
        .quiz-title {
            color: #FF0000; /* Vermelho vivo */
            font-size: 42px;
            font-weight: 800;
            letter-spacing: 1px;
            margin-bottom: 10px;
            text-transform: uppercase;
            text-shadow: 2px 2px 0 #FFD700;
        }
        
        .progress-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding: 10px 15px;
            background: #FFF0F0; /* Rosa muito claro */
            border-radius: 60px;
            border: 2px solid #FFD700;
        }
        
        .question-counter {
            background: #FF0000;
            color: white;
            font-size: 18px;
            font-weight: bold;
            padding: 8px 20px;
            border-radius: 40px;
            border: 2px solid #FFD700;
            min-width: 80px;
            text-align: center;
        }
        
        .progress-bar {
            flex: 1;
            height: 20px;
            background: #FFB6C1; /* Rosa claro */
            border-radius: 30px;
            margin: 0 15px;
            overflow: hidden;
            border: 1px solid #FFD700;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #FF0000, #FFD700);
            width: 0%;
            transition: width 0.3s ease;
            border-radius: 30px;
        }
        
        .category-badge {
            background: #8B0000;
            color: white;
            font-size: 14px;
            font-weight: bold;
            padding: 8px 15px;
            border-radius: 30px;
            border: 2px solid #FFD700;
            min-width: 120px;
            text-align: center;
        }
        
        .timer-container {
            text-align: center;
            margin: 15px 0;
        }
        
        .timer {
            display: inline-block;
            background: #8B0000;
            color: white;
            font-size: 36px;
            font-weight: bold;
            padding: 12px 30px;
            border-radius: 60px;
            border: 3px solid #FFD700;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
        }
        
        .question-area {
            background: #FFF5F5;
            border-radius: 20px;
            padding: 30px 20px;
            margin-bottom: 25px;
            border-left: 5px solid #FF0000;
            border-right: 5px solid #FFD700;
            box-shadow: 0 5px 15px rgba(255,0,0,0.2);
        }
        
        .question-text {
            color: #8B0000;
            font-size: 22px;
            font-weight: 600;
            text-align: center;
            line-height: 1.5;
        }
        
        .options-container {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 25px;
        }
        
        .option-btn {
            background: white;
            border: 2px solid #FFB6C1;
            border-radius: 15px;
            padding: 18px 20px;
            color: #8B0000;
            font-size: 18px;
            font-weight: 500;
            text-align: left;
            cursor: pointer;
            transition: all 0.2s ease;
            width: 100%;
            display: block;
            box-shadow: 0 4px 6px rgba(139,0,0,0.2);
        }
        
        .option-btn:hover:not(:disabled) {
            background: #FFE4E1;
            border-color: #FF0000;
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(255,0,0,0.3);
        }
        
        .option-btn.selected {
            background: #FFB6C1;
            border-color: #FF0000;
            box-shadow: 0 4px 0 #8B0000;
        }
        
        .option-btn.correct {
            background: #4CAF50;
            border-color: #FFD700;
            color: white;
            box-shadow: 0 4px 0 #2d6a2d;
        }
        
        .option-btn.incorrect {
            background: #f44336;
            border-color: #FFD700;
            color: white;
            box-shadow: 0 4px 0 #9a2828;
        }
        
        .option-btn:disabled {
            opacity: 0.9;
            cursor: default;
            transform: none;
        }
        
        .option-prefix {
            display: inline-block;
            width: 35px;
            height: 35px;
            background: #FF0000;
            color: white;
            border-radius: 10px;
            text-align: center;
            line-height: 35px;
            font-size: 20px;
            font-weight: bold;
            margin-right: 15px;
            border: 2px solid #FFD700;
        }
        
        .loading-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255,255,255,0.95);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            display: none;
        }
        
        .loading-content {
            background: white;
            padding: 40px;
            border-radius: 30px;
            text-align: center;
            border: 4px solid #FF0000;
        }
        
        .loading-spinner {
            width: 60px;
            height: 60px;
            border: 6px solid #FFB6C1;
            border-top-color: #FF0000;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        .result-screen {
            text-align: center;
        }
        
        .final-score {
            background: linear-gradient(135deg, #FF0000, #8B0000);
            border-radius: 25px;
            padding: 35px;
            margin: 20px 0;
            color: white;
            border: 4px solid #FFD700;
        }
        
        .score-number {
            font-size: 90px;
            font-weight: bold;
            line-height: 1;
            margin: 15px 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        
        .score-label {
            font-size: 28px;
            opacity: 0.9;
        }
        
        .level-result {
            font-size: 26px;
            margin: 20px 0;
            padding: 15px;
            background: rgba(255,215,0,0.3);
            border-radius: 60px;
            border: 2px solid #FFD700;
        }
        
        .action-btn {
            background: white;
            border: none;
            border-radius: 15px;
            padding: 18px;
            color: #8B0000;
            font-size: 22px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            margin: 12px 0;
            box-shadow: 0 4px 10px rgba(139,0,0,0.3);
            border: 3px solid #FFD700;
            transition: all 0.2s ease;
        }
        
        .action-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(255,215,0,0.5);
            background: #FFF0F0;
        }
        
        .action-btn.secondary {
            background: #FFF5F5;
        }
        
        .name-input {
            width: 100%;
            padding: 15px;
            font-size: 18px;
            border-radius: 15px;
            border: 3px solid #FFD700;
            margin: 10px 0;
            transition: all 0.2s ease;
            color: #8B0000;
            font-weight: bold;
        }
        
        .name-input:focus {
            outline: none;
            border-color: #FF0000;
            box-shadow: 0 0 0 3px rgba(255,215,0,0.3);
        }
        
        .name-input::placeholder {
            color: #FFB6C1;
            font-weight: normal;
        }
        
        @media (max-width: 480px) {
            .quiz-title { font-size: 36px; }
            .question-text { font-size: 20px; }
            .option-btn { font-size: 16px; padding: 15px; }
            .score-number { font-size: 70px; }
            .progress-container { 
                flex-direction: column; 
                gap: 10px; 
            }
            .progress-bar { 
                width: 100%; 
                margin: 10px 0; 
            }
            .category-badge { 
                min-width: 100%; 
            }
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <div id="quizContent"></div>
    </div>

    <div id="loading" class="loading-overlay">
        <div class="loading-content">
            <div class="loading-spinner"></div>
            <div style="font-size: 20px; color: #8B0000; font-weight: bold;">Cargando...</div>
        </div>
    </div>

    <script>
        // LINKS DE REDIRECIONAMENTO (ALTERE AQUI)
        const SHOPEE_LINK = "https://s.shopee.com.br/70DpcjasH2";
        const RESULTADOS_LINK = "https://s.shopee.com.br/70DpcjasH2";

        // ===== 20 PERGUNTAS AVANÇADAS DE ESPANHOL =====
        const questions = [
            // SUBJUNTIVO E TEMPOS VERBAIS (1-5)
            {
                question: "🇪🇸 Complete con el subjuntivo: 'Espero que ___ buen viaje.'",
                options: ["tengas", "tienes", "tener", "tenías"],
                answer: 1,
                category: "SUBJUNTIVO"
            },
            {
                question: "🇪🇸 ¿Cuál es la forma correcta? 'Si ___ dinero, viajaría por el mundo.'",
                options: ["tuviera", "tengo", "tendría", "tener"],
                answer: 1,
                category: "CONDICIONAL"
            },
            {
                question: "🇪🇸 Pretérito perfecto: 'Ya ___ (comer) cuando llegaste.'",
                options: ["he comido", "había comido", "comí", "comeré"],
                answer: 2,
                category: "PLUSCUAMPERFECTO"
            },
            {
                question: "🇪🇸 Subjuntivo imperfecto: 'Ojalá ___ (venir) más temprano.'",
                options: ["viniera", "venga", "vendría", "vino"],
                answer: 1,
                category: "SUBJUNTIVO"
            },
            {
                question: "🇪🇸 Futuro perfecto: 'Para el año que viene, ya ___ (terminar) la carrera.'",
                options: ["habré terminado", "terminaré", "he terminado", "terminaba"],
                answer: 1,
                category: "FUTURO PERFECTO"
            },
            
            // EXPRESSÕES IDIOMÁTICAS (6-10)
            {
                question: "🇪🇸 ¿Qué significa 'tomar el pelo'?",
                options: ["Cortar el cabello", "Bromear/Engañar", "Peinarse", "Tener vergüenza"],
                answer: 2,
                category: "EXPRESIONES"
            },
            {
                question: "🇪🇸 'Estar en las nubes' significa:",
                options: ["Estar distraído", "Viajar en avión", "Estar feliz", "Tener sueño"],
                answer: 1,
                category: "EXPRESIONES"
            },
            {
                question: "🇪🇸 ¿Qué es 'una ganga'?",
                options: ["Una pandilla", "Una oferta/Baratija", "Una fruta", "Un problema"],
                answer: 2,
                category: "EXPRESIONES"
            },
            {
                question: "🇪🇸 'Meter la pata' quiere decir:",
                options: ["Cometer un error", "Patear", "Entrar en un lugar", "Bailar"],
                answer: 1,
                category: "EXPRESIONES"
            },
            {
                question: "🇪🇸 'Ser un lince' significa:",
                options: ["Ser muy astuto", "Ser un animal", "Ser perezoso", "Ser rápido"],
                answer: 1,
                category: "EXPRESIONES"
            },
            
            // FALSOS COGNATOS AVANÇADOS (11-15)
            {
                question: "🇪🇸 'Constipado' en español significa:",
                options: ["Constipado (intestino)", "Resfriado", "Estreñido", "Congestionado"],
                answer: 2,
                category: "FALSOS COGNATOS"
            },
            {
                question: "🇪🇸 'Embargado' quiere decir:",
                options: ["Con vergüenza", "Bloqueado/Retenido", "Embarazado", "Abrazado"],
                answer: 2,
                category: "FALSOS COGNATOS"
            },
            {
                question: "🇪🇸 'Bizarro' en español significa:",
                options: ["Extraño/Raro", "Valiente", "Bizarro (estilo)", "Divertido"],
                answer: 2,
                category: "FALSOS COGNATOS"
            },
            {
                question: "🇪🇸 'Exitoso' quiere decir:",
                options: ["Saída", "Bem-sucedido", "Exercício", "Exit"],
                answer: 2,
                category: "FALSOS COGNATOS"
            },
            {
                question: "🇪🇸 'Sensato' significa:",
                options: ["Sensível", "Sensato/Juicioso", "Sensacional", "Sensível demais"],
                answer: 2,
                category: "FALSOS COGNATOS"
            },
            
            // GRAMÁTICA AVANÇADA (16-20)
            {
                question: "🇪🇸 'Le' en 'Le di el libro' es un:",
                options: ["Objeto directo", "Objeto indirecto", "Pronombre reflexivo", "Artículo"],
                answer: 2,
                category: "GRAMÁTICA"
            },
            {
                question: "🇪🇸 'Se lo dije' - ¿Qué función tiene 'se'?",
                options: ["Reflexivo", "Sustituto de 'le'", "Impersonal", "Pasivo"],
                answer: 2,
                category: "GRAMÁTICA"
            },
            {
                question: "🇪🇸 'Cuyo' en 'El hombre cuyo hijo llegó' se refiere a:",
                options: ["El hombre", "El hijo", "Llegó", "Hombre e hijo"],
                answer: 1,
                category: "GRAMÁTICA"
            },
            {
                question: "🇪🇸 'Quizás ___ a tiempo' (llegar) - forma correcta:",
                options: ["llegue", "llega", "llegará", "llegaba"],
                answer: 1,
                category: "GRAMÁTICA"
            },
            {
                question: "🇪🇸 'A pesar de ___ estudiado, no aprobó' - forma correcta:",
                options: ["haber", "había", "ha", "habrá"],
                answer: 1,
                category: "GRAMÁTICA"
            }
        ];

        const TOTAL_QUESTIONS = questions.length;
        let current = 0;
        let score = 0;
        let answered = false;
        let userAnswers = [];
        let timer;
        let timeLeft = 50;

        function startTimer() {
            clearInterval(timer);
            timeLeft = 50;
            updateTimerDisplay();
            
            timer = setInterval(() => {
                timeLeft--;
                updateTimerDisplay();
                
                if (timeLeft <= 0) {
                    clearInterval(timer);
                    if (!answered) {
                        userAnswers.push(0);
                        nextQuestion();
                    }
                }
            }, 1000);
        }

        function updateTimerDisplay() {
            const timerEl = document.getElementById('timer');
            if (timerEl) timerEl.textContent = `⏳ ${timeLeft}s`;
        }

        function showQuestion() {
            answered = false;
            const q = questions[current];
            
            let html = `
                <div class="quiz-header">
                    <div class="quiz-title">🇪🇸 ESPAÑOL AVANZADO</div>
                    
                    <div class="progress-container">
                        <div class="question-counter">${current + 1}/${TOTAL_QUESTIONS}</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: ${((current + 1) / TOTAL_QUESTIONS) * 100}%"></div>
                        </div>
                        <div class="category-badge">${q.category}</div>
                    </div>
                    
                    <div class="timer-container">
                        <div class="timer" id="timer">⏳ 50s</div>
                    </div>
                </div>
                
                <div class="question-area">
                    <div class="question-text">${q.question}</div>
                </div>
                
                <div class="options-container" id="optionsContainer">
            `;
            
            const letters = ['A', 'B', 'C', 'D'];
            q.options.forEach((opt, i) => {
                html += `
                    <button class="option-btn" onclick="selectOption(${i+1})">
                        <span class="option-prefix">${letters[i]}</span>
                        ${opt}
                    </button>
                `;
            });
            
            html += `</div>`;
            
            document.getElementById('quizContent').innerHTML = html;
            startTimer();
        }

        function selectOption(selected) {
            if (answered) return;
            answered = true;
            clearInterval(timer);
            
            const correct = questions[current].answer;
            const buttons = document.querySelectorAll('.option-btn');
            
            buttons.forEach(b => b.classList.remove('selected', 'correct', 'incorrect'));
            buttons[selected-1].classList.add('selected');
            
            setTimeout(() => {
                buttons.forEach((btn, i) => {
                    if (i+1 === correct) {
                        btn.classList.add('correct');
                    } else if (i+1 === selected && selected !== correct) {
                        btn.classList.add('incorrect');
                    }
                    btn.disabled = true;
                });
                
                userAnswers.push(selected);
                if (selected === correct) {
                    score++;
                    if (typeof confetti !== 'undefined') {
                        confetti({
                            particleCount: 30,
                            spread: 50,
                            colors: ['#FF0000', '#FFD700']
                        });
                    }
                }
                
                setTimeout(nextQuestion, 800);
            }, 300);
        }

        function nextQuestion() {
            current++;
            if (current < questions.length) {
                showQuestion();
            } else {
                showFinalScreen();
            }
        }

        function showFinalScreen() {
            let levelMessage = "";
            let levelEmoji = "";
            
            if (score >= 16) {
                levelMessage = "MAESTRO - ¡Excelente! 🌟";
                levelEmoji = "🏆";
                if (typeof confetti !== 'undefined') {
                    confetti({ particleCount: 200, spread: 120, colors: ['#FF0000', '#FFD700'] });
                }
            } else if (score >= 12) {
                levelMessage = "AVANZADO - ¡Muy bien! 👍";
                levelEmoji = "📚";
                if (typeof confetti !== 'undefined') {
                    confetti({ particleCount: 100, spread: 80, colors: ['#FFD700'] });
                }
            } else if (score >= 8) {
                levelMessage = "INTERMEDIO - ¡Bien! 💪";
                levelEmoji = "📝";
            } else {
                levelMessage = "BÁSICO - ¡Sigue estudiando! 📖";
                levelEmoji = "📖";
            }
            
            let html = `
                <div class="quiz-header">
                    <div class="quiz-title">🇪🇸 ESPAÑOL AVANZADO</div>
                </div>
                
                <div class="result-screen">
                    <div class="final-score">
                        <div class="score-label">Tu Puntuación</div>
                        <div class="score-number">${score}/${TOTAL_QUESTIONS}</div>
                        <div class="level-result">${levelEmoji} ${levelMessage}</div>
                    </div>
                    
                    <button class="action-btn" onclick="redirectToResultados()">
                        🔗 VER RESULTADOS
                    </button>
                    
                    <button class="action-btn secondary" onclick="redirectToShopee()">
                        🚀 SIGUIENTE NIVEL
                    </button>
                    
                    <input type="text" class="name-input" id="participantName" 
                           placeholder="Digite seu nome">
                    <button class="action-btn secondary" onclick="sendResults()">
                        💾 GUARDAR RESULTADO
                    </button>
                </div>
            `;
            
            document.getElementById('quizContent').innerHTML = html;
        }

        function redirectToResultados() {
            window.open(RESULTADOS_LINK, '_blank');
        }

        function redirectToShopee() {
            window.open(SHOPEE_LINK, '_blank');
        }

        function sendResults() {
            const name = document.getElementById('participantName').value.trim();
            if (!name) {
                alert('¡Por favor, digite su nombre!');
                return;
            }
            
            document.getElementById('loading').style.display = 'flex';
            
            setTimeout(() => {
                document.getElementById('loading').style.display = 'none';
                alert(`¡Gracias ${name}! Tu puntuación: ${score}/${TOTAL_QUESTIONS}`);
            }, 1000);
        }

        // Carrega a biblioteca de confete e inicia o quiz
        function loadConfettiAndStart() {
            if (typeof confetti === 'undefined') {
                const script = document.createElement('script');
                script.src = 'https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js';
                script.onload = function() {
                    showQuestion();
                };
                document.head.appendChild(script);
            } else {
                showQuestion();
            }
        }

        // Inicia o quiz
        loadConfettiAndStart();
    </script>
</body>
</html>
