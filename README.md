<!DOCTYPE html>
<html>
<head>
  <base target="_top">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    body {
      font-family: 'Arial', 'Helvetica', sans-serif;
      background: #000000; /* PRETO */
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 10px;
      position: relative;
    }
    
    .quiz-container {
      width: 100%;
      max-width: 400px;
      background: #f0f0f0; /* CINZA CLARO BEM CLARO */
      border-radius: 25px;
      padding: 20px;
      box-shadow: 0 10px 25px rgba(255,255,255,0.1);
      border: 2px solid #ffffff;
      position: relative;
      z-index: 1;
    }
    
    /* Header com "Quiz" centralizado */
    .quiz-header {
      margin-bottom: 25px;
      text-align: center;
      position: relative;
    }
    
    .quiz-title {
      color: #000000; /* PRETO */
      font-size: 48px;
      font-weight: bold;
      letter-spacing: 2px;
      text-shadow: 2px 2px 0 #cccccc;
      line-height: 1;
      text-align: center;
    }
    
    /* Área da pergunta */
    .question-area {
      background: #ffffff; /* BRANCO */
      border-radius: 15px;
      padding: 25px 15px;
      margin-bottom: 25px;
      border: 2px solid #000000;
      box-shadow: inset 0 0 10px rgba(0,0,0,0.1);
    }
    
    .question-text {
      color: #000000; /* PRETO */
      font-size: 24px;
      font-weight: 600;
      text-align: center;
      line-height: 1.3;
      word-break: break-word;
    }
    
    /* Opções de resposta */
    .options-container {
      display: flex;
      flex-direction: column;
      gap: 12px;
      margin-bottom: 25px;
    }
    
    .option-btn {
      background: #ffffff; /* BRANCO */
      border: 2px solid #000000; /* PRETO */
      border-radius: 15px;
      padding: 18px 15px;
      color: #000000; /* PRETO */
      font-size: 20px;
      font-weight: 500;
      text-align: left;
      cursor: pointer;
      transition: all 0.2s ease;
      width: 100%;
      display: block;
      box-shadow: 0 4px 0 #cccccc; /* CINZA CLARO */
    }
    
    .option-btn:active {
      transform: translateY(2px);
      box-shadow: 0 2px 0 #cccccc;
    }
    
    /* Estilo quando selecionada */
    .option-btn.selected {
      background: #e0e0e0; /* CINZA MÉDIO */
      border-color: #000000;
      color: #000000;
      box-shadow: 0 4px 0 #aaaaaa;
    }
    
    .option-btn.selected .option-prefix {
      background: #f0f0f0;
      color: #000000;
    }
    
    .option-btn.correct {
      background: #4CAF50; /* VERDE */
      border-color: #2e7d32;
      color: #ffffff;
      box-shadow: 0 4px 0 #1b5e20;
    }
    
    .option-btn.incorrect {
      background: #f44336; /* VERMELHO */
      border-color: #c62828;
      color: #ffffff;
      box-shadow: 0 4px 0 #8b0000;
    }
    
    .option-btn:disabled {
      opacity: 0.9;
      cursor: default;
      transform: none;
    }
    
    /* Letras das opções (A, B, C) */
    .option-prefix {
      display: inline-block;
      width: 40px;
      height: 40px;
      background: #f0f0f0; /* CINZA CLARO */
      color: #000000; /* PRETO */
      border-radius: 10px;
      text-align: center;
      line-height: 40px;
      font-size: 24px;
      font-weight: bold;
      margin-right: 15px;
      box-shadow: inset 0 -2px 0 #cccccc;
      border: 1px solid #000000;
    }
    
    /* Timer */
    .timer-container {
      text-align: center;
      margin-bottom: 15px;
    }
    
    .timer {
      display: inline-block;
      background: #ffffff; /* BRANCO */
      color: #000000; /* PRETO */
      font-size: 32px;
      font-weight: bold;
      padding: 10px 25px;
      border-radius: 50px;
      border: 2px solid #000000;
      box-shadow: 0 4px 0 #cccccc;
    }
    
    /* Loading overlay */
    .loading-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.9); /* PRETO */
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 1000;
      display: none;
    }
    
    .loading-content {
      background: #f0f0f0; /* CINZA CLARO */
      padding: 30px;
      border-radius: 20px;
      text-align: center;
      color: #000000; /* PRETO */
      border: 2px solid #ffffff;
    }
    
    .loading-spinner {
      width: 50px;
      height: 50px;
      border: 5px solid #cccccc;
      border-top-color: #000000;
      border-radius: 50%;
      animation: spin 1s linear infinite;
      margin: 20px auto;
    }
    
    @keyframes spin {
      to { transform: rotate(360deg); }
    }
    
    /* Tela de resultados */
    .result-screen {
      text-align: center;
    }
    
    .final-score {
      background: #ffffff; /* BRANCO */
      border-radius: 20px;
      padding: 30px;
      margin: 20px 0;
      border: 2px solid #000000;
    }
    
    .score-number {
      font-size: 80px;
      font-weight: bold;
      color: #000000; /* PRETO */
      line-height: 1;
      margin: 10px 0;
    }
    
    .score-label {
      color: #000000; /* PRETO */
      font-size: 24px;
    }
    
    .action-btn {
      background: #ffffff; /* BRANCO */
      border: none;
      border-radius: 15px;
      padding: 18px;
      color: #000000; /* PRETO */
      font-size: 24px;
      font-weight: bold;
      cursor: pointer;
      width: 100%;
      margin: 10px 0;
      box-shadow: 0 4px 0 #cccccc;
      transition: all 0.1s ease;
      border: 2px solid #000000;
    }
    
    .action-btn:active {
      transform: translateY(2px);
      box-shadow: 0 2px 0 #cccccc;
    }
    
    .action-btn.secondary {
      background: #e0e0e0; /* CINZA MÉDIO */
      color: #000000; /* PRETO */
      border: 2px solid #000000;
      box-shadow: 0 4px 0 #aaaaaa;
    }
    
    .name-input {
      width: 100%;
      padding: 15px;
      font-size: 18px;
      border-radius: 15px;
      border: 2px solid #000000;
      background: #ffffff;
      color: #000000;
      margin: 10px 0;
    }
    
    .name-input::placeholder {
      color: #666666;
    }
    
    /* Ajustes para mobile */
    @media (max-width: 400px) {
      .quiz-title {
        font-size: 42px;
      }
      
      .question-text {
        font-size: 22px;
      }
      
      .option-btn {
        font-size: 18px;
        padding: 15px;
      }
      
      .option-prefix {
        width: 35px;
        height: 35px;
        font-size: 20px;
        line-height: 35px;
        margin-right: 10px;
      }
    }
  </style>
  
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
</head>
<body>
  <div class="quiz-container">
    <div id="quizContent"></div>
  </div>
  
  <div id="loading" class="loading-overlay">
    <div class="loading-content">
      <div class="loading-spinner"></div>
      <div style="font-size: 18px;">Carregando...</div>
    </div>
  </div>

  <script>
    // Links (você pode alterar conforme necessário)
    const shopeeLink = "https://s.shopee.com.br/70DpcjasH2";
    const resultadosLink = "https://s.shopee.com.br/70DpcjasH2";

    // ===== 10 PERGUNTAS SOBRE ESPANHOL PARA BRASILEIROS =====
    const questions = [
      {
        question: "🇪🇸 Em espanhol, 'embarazada' significa:",
        options: ["Com vergonha", "Grávida", "Atrapalhada", "Embaraçada"],
        answer: 2
      },
      {
        question: "🇪🇸 Qual o significado de 'coger' na maioria dos países hispânicos?",
        options: ["Pegar", "Coçar", "Sentido vulgar", "Cozinhar"],
        answer: 3
      },
      {
        question: "🇪🇸 'Éxito' em espanhol quer dizer:",
        options: ["Saída", "Sucesso", "Exit", "Exercício"],
        answer: 2
      },
      {
        question: "🇪🇸 Como se diz 'escritório' em espanhol?",
        options: ["Escritorio", "Oficina", "Despacho", "Negocio"],
        answer: 2
      },
      {
        question: "🇪🇸 'Constipado' em espanhol significa:",
        options: ["Intestino preso", "Resfriado", "Prisão de ventre", "Constipação"],
        answer: 2
      },
      {
        question: "🇪🇸 Qual a tradução de 'borracha' para o espanhol?",
        options: ["Boracha", "Goma", "Caucho", "Borracha"],
        answer: 2
      },
      {
        question: "🇪🇸 'Pelado' em espanhol pode significar:",
        options: ["Sem roupa", "Careca", "Descascado", "Sem dinheiro"],
        answer: 4
      },
      {
        question: "🇪🇸 Como se fala 'brincadeira' em espanhol?",
        options: ["Brincadeira", "Broma", "Juego", "Diversión"],
        answer: 2
      },
      {
        question: "🇪🇸 'Rato' em espanhol significa:",
        options: ["Rato animal", "Momento", "Mouse", "Ratazana"],
        answer: 2
      },
      {
        question: "🇪🇸 Qual frase está gramaticalmente correta?",
        options: ["Me llamo es Juan", "Yo llamo Juan", "Me llamo Juan", "Mi llamo Juan"],
        answer: 3
      }
    ];

    let current = 0;
    let score = 0;
    let answered = false;
    let userAnswers = [];
    let timer;
    let timeLeft = 30;

    function startTimer() {
      clearInterval(timer);
      timeLeft = 30;
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
      if (timerEl) {
        timerEl.textContent = `⏳ ${timeLeft}s`;
      }
    }

    function showQuestion() {
      answered = false;
      const q = questions[current];
      
      let html = `
        <div class="quiz-header">
          <div class="quiz-title">QUIZ</div>
        </div>
        
        <div class="timer-container">
          <div class="timer" id="timer">⏳ 30s</div>
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
          confetti({
            particleCount: 50,
            spread: 60,
            colors: ['#000000', '#f0f0f0']
          });
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
      if (score >= 5) {
        confetti({
          particleCount: 100,
          spread: 100,
          colors: ['#000000', '#f0f0f0']
        });
      }
      
      let html = `
        <div class="quiz-header">
          <div class="quiz-title">QUIZ</div>
        </div>
        
        <div class="result-screen">
          <div class="final-score">
            <div class="score-label">Sua pontuação</div>
            <div class="score-number">${score}/${questions.length}</div>
          </div>
          
          <button class="action-btn" onclick="redirectToResultados()">
            🔗 VER RESULTADOS
          </button>
          
          <button class="action-btn secondary" onclick="redirectToShopee()">
            🚀 FAZER OUTRA ETAPA
          </button>
          
          <input type="text" class="name-input" id="participantName" 
                 placeholder="Digite seu nome">
          <button class="action-btn secondary" onclick="sendResults()">
            💾 SALVAR RESULTADO
          </button>
        </div>
      `;
      
      document.getElementById('quizContent').innerHTML = html;
    }

    function redirectToResultados() {
      window.open(resultadosLink, '_blank');
    }

    function redirectToShopee() {
      window.open(shopeeLink, '_blank');
    }

    function sendResults() {
      const name = document.getElementById('participantName').value.trim();
      if (!name) {
        alert('Por favor, digite seu nome');
        return;
      }
      
      document.getElementById('loading').style.display = 'flex';
      
      setTimeout(() => {
        document.getElementById('loading').style.display = 'none';
        alert(`¡Gracias ${name}! Pontuação: ${score}/${questions.length} 🇪🇸`);
      }, 1000);
    }

    // Inicia o quiz
    showQuestion();
  </script>
</body>
</html>
