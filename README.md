<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Esercizio di Vocabolario Italiano</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a89cc 0%, #4a69bd 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .container {
            max-width: 900px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
            margin-bottom: 30px;
        }

        .header {
            background: linear-gradient(135deg, #6a89cc, #4a69bd);
            color: white;
            padding: 25px;
            text-align: center;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="2" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="30" r="1.5" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="70" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="90" cy="80" r="2.5" fill="rgba(255,255,255,0.1)"/></svg>');
        }

        .header h1 {
            font-size: 2.2em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.1em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .instructions {
            background: #f8f9fa;
            padding: 20px;
            border-bottom: 1px solid #e9ecef;
        }

        .instructions p {
            margin-bottom: 10px;
            line-height: 1.5;
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 20px;
            border-radius: 15px;
            margin: 20px;
            border: 2px solid #6a89cc;
            box-shadow: 0 4px 15px rgba(106,137,204,0.2);
        }

        .word-bank h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.3em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #6a89cc, #4a69bd);
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 15px;
            box-shadow: 0 3px 10px rgba(106,137,204,0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(106,137,204,0.4);
        }

        .story-container {
            padding: 25px;
        }

        .story-text {
            font-size: 18px;
            line-height: 1.8;
            margin-bottom: 25px;
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
            text-align: center;
        }

        .fill-blank:focus {
            outline: none;
            border-color: #6a89cc;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 20px;
            flex-wrap: wrap;
        }

        .check-btn {
            background: linear-gradient(135deg, #6a89cc, #4a69bd);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(106,137,204,0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(106,137,204,0.4);
        }

        .hint-btn {
            background: #ffc107;
            color: #333;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255,193,7,0.3);
        }

        .hint-btn:hover {
            background: #e0a800;
            transform: translateY(-2px);
        }

        .reset-btn {
            background: #6c757d;
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(108,117,125,0.3);
        }

        .reset-btn:hover {
            background: #5a6268;
            transform: translateY(-2px);
        }

        .feedback {
            margin-top: 20px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
            display: none;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            background: linear-gradient(135deg, #6a89cc, #4a69bd);
            color: white;
            padding: 12px 18px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(106,137,204,0.3);
            margin-bottom: 20px;
            text-align: center;
        }

        .hint-text {
            background: #fff3cd;
            color: #856404;
            padding: 15px;
            border-radius: 10px;
            margin-top: 20px;
            border-left: 4px solid #ffc107;
            display: none;
        }

        @media (max-width: 768px) {
            .fill-blank {
                min-width: 100px;
                margin: 5px 2px;
            }
            
            .story-text {
                font-size: 16px;
                padding: 15px;
            }
            
            .controls {
                flex-direction: column;
                align-items: center;
            }
            
            .check-btn, .hint-btn, .reset-btn {
                width: 200px;
            }
        }
    </style>
</head>
<body>
    <div class="score">Punteggio: <span id="score">0</span>/10</div>
    
    <div class="container">
        <div class="header">
            <h1>📚 Vocabolario Italiano - Completa la Storia</h1>
            <p>Inserisci le parole corrette per completare la storia</p>
        </div>

        <div class="instructions">
            <p><strong>Istruzioni:</strong> Completa la storia utilizzando le parole dalla lista qui sotto. Clicca su "Controlla le Risposte" per verificare le tue scelte.</p>
        </div>

        <div class="word-bank">
            <h3>📝 Banca Parole - Scegli tra queste parole:</h3>
            <div class="word-options">
                <span class="word-option">volte</span>
                <span class="word-option">cappello</span>
                <span class="word-option">correre</span>
                <span class="word-option">dappertutto</span>
                <span class="word-option">potessi</span>
                <span class="word-option">anche</span>
                <span class="word-option">aereo</span>
                <span class="word-option">pensavo</span>
                <span class="word-option">pericoloso</span>
                <span class="word-option">alcuni</span>
            </div>
        </div>

        <div class="story-container">
            <div class="story-text">
                <p>Ci sono state molte <input type="text" class="fill-blank" data-answer="volte" placeholder="risposta"> in cui ho viaggiato in <input type="text" class="fill-blank" data-answer="aereo" placeholder="risposta">, ma questa volta era diverso.</p>
                
                <p><input type="text" class="fill-blank" data-answer="pensavo" placeholder="risposta"> che sarebbe stato noioso, ma invece è stata un'avventura! Mentre cercavo il mio <input type="text" class="fill-blank" data-answer="cappello" placeholder="risposta"> che era volato via, ho dovuto <input type="text" class="fill-blank" data-answer="correre" placeholder="risposta"> <input type="text" class="fill-blank" data-answer="dappertutto" placeholder="risposta">.</p>
                
                <p>La situazione stava diventando <input type="text" class="fill-blank" data-answer="pericoloso" placeholder="risposta">, e ho wishato che <input type="text" class="fill-blank" data-answer="potessi" placeholder="risposta"> trovarlo prima del decollo. Fortunatamente, <input type="text" class="fill-blank" data-answer="alcuni" placeholder="risposta"> passeggeri mi hanno aiutato, e <input type="text" class="fill-blank" data-answer="anche" placeholder="risposta"> l'assistente di volo!</p>
                
                <p>Alla fine ho trovato il cappello proprio prima di salire sull'aereo. Che giornata emozionante!</p>
            </div>

            <div class="hint-text" id="hint-text">
                <strong>Suggerimenti:</strong>
                <ul>
                    <li><strong>volte</strong>: significa "times" in inglese</li>
                    <li><strong>aereo</strong>: mezzo di trasporto che vola</li>
                    <li><strong>pensavo</strong>: forma passata di "pensare" (to think)</li>
                    <li><strong>cappello</strong>: accessorio che si indossa sulla testa</li>
                    <li><strong>correre</strong>: verbo che significa "to run"</li>
                    <li><strong>dappertutto</strong>: avverbio che significa "everywhere"</li>
                    <li><strong>pericoloso</strong>: aggettivo che significa "dangerous"</li>
                    <li><strong>potessi</strong>: forma congiuntiva di "potere" (to be able to)</li>
                    <li><strong>alcuni</strong>: significa "some" in inglese</li>
                    <li><strong>anche</strong>: significa "also" o "too" in inglese</li>
                </ul>
            </div>

            <div class="feedback" id="feedback"></div>

            <div class="controls">
                <button class="check-btn" onclick="checkAnswers()">Controlla le Risposte</button>
                <button class="hint-btn" onclick="toggleHints()">Mostra/Nascondi Suggerimenti</button>
                <button class="reset-btn" onclick="resetExercise()">Azzera Esercizio</button>
            </div>
        </div>
    </div>

    <script>
        let score = 0;
        
        function checkAnswers() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            let allFilled = true;
            
            blanks.forEach(blank => {
                if (blank.value.trim() === '') {
                    allFilled = false;
                }
            });
            
            if (!allFilled) {
                document.getElementById('feedback').textContent = 'Per favore, riempi tutti gli spazi vuoti prima di controllare!';
                document.getElementById('feedback').className = 'feedback incorrect';
                document.getElementById('feedback').style.display = 'block';
                return;
            }
            
            blanks.forEach(blank => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
            });
            
            score = correctCount;
            document.getElementById('score').textContent = score;
            
            const feedback = document.getElementById('feedback');
            if (score === 10) {
                feedback.textContent = '🎉 Complimenti! Hai completato perfettamente la storia!';
                feedback.className = 'feedback correct';
            } else {
                feedback.textContent = `Hai ${score} su 10 risposte corrette. Continua a provare!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }
        
        function toggleHints() {
            const hintText = document.getElementById('hint-text');
            hintText.style.display = hintText.style.display === 'block' ? 'none' : 'block';
        }
        
        function resetExercise() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct');
                blank.classList.remove('incorrect');
            });
            
            document.getElementById('feedback').style.display = 'none';
            document.getElementById('hint-text').style.display = 'none';
            
            score = 0;
            document.getElementById('score').textContent = score;
        }
        
        // Allow pressing Enter to check answers
        document.addEventListener('keydown', function(event) {
            if (event.key === 'Enter') {
                checkAnswers();
            }
        });
    </script>
</body>
</html>
