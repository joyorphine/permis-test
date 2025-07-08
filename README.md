<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test Permis de Conduire</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        
        .container {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            text-align: center;
        }
        
        h1 {
            color: #333;
            margin-bottom: 30px;
        }
        
        .question {
            margin: 20px 0;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 8px;
            border-left: 4px solid #007bff;
        }
        
        .question h3 {
            color: #333;
            margin-bottom: 15px;
        }
        
        input[type="number"] {
            width: 200px;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            margin: 10px;
        }
        
        button {
            background: #007bff;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin: 10px;
        }
        
        button:hover {
            background: #0056b3;
        }
        
        .result {
            margin: 20px 0;
            padding: 20px;
            border-radius: 8px;
            font-size: 18px;
            font-weight: bold;
        }
        
        .success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        
        .warning {
            background: #fff3cd;
            color: #856404;
            border: 1px solid #ffeaa7;
        }
        
        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🚗 Test d'Éligibilité au Permis</h1>
        
        <!-- Étape 1: Âge -->
        <div class="question">
            <h3>📋 Quel est votre âge ?</h3>
            <input type="number" id="ageInput" placeholder="Entrez votre âge" min="0" max="100">
            <br>
            <button onclick="checkAge()">Vérifier</button>
        </div>
        
        <!-- Résultat âge -->
        <div id="ageResult" class="result hidden"></div>
        
        <!-- Étape 2: Test de conduite -->
        <div id="driverQuestion" class="question hidden">
            <h3>🚗 Avez-vous réussi le test de conduite ?</h3>
            <button onclick="checkDriverTest(true)">Oui</button>
            <button onclick="checkDriverTest(false)">Non</button>
        </div>
        
        <!-- Résultat final -->
        <div id="finalResult" class="result hidden"></div>
        
        <!-- Recommencer -->
        <button id="restartBtn" class="hidden" onclick="restart()">Recommencer</button>
    </div>

    <script>
        function checkAge() {
            // Récupérer l'âge
            const age = document.getElementById('ageInput').value;
            const ageResult = document.getElementById('ageResult');
            const driverQuestion = document.getElementById('driverQuestion');
            const finalResult = document.getElementById('finalResult');
            const restartBtn = document.getElementById('restartBtn');
            
            // Cacher les résultats précédents
            driverQuestion.classList.add('hidden');
            finalResult.classList.add('hidden');
            restartBtn.classList.add('hidden');
            
            // Vérifier si l'âge est valide
            if (age === '' || age < 0) {
                ageResult.innerHTML = '❌ Veuillez entrer un âge valide';
                ageResult.className = 'result error';
                ageResult.classList.remove('hidden');
                return;
            }
            
            // Vérifier l'éligibilité
            if (age >= 18) {
                ageResult.innerHTML = '✅ Vous êtes éligible pour passer le test !';
                ageResult.className = 'result success';
                driverQuestion.classList.remove('hidden');
            } else {
                ageResult.innerHTML = '❌ Vous devez avoir au moins 18 ans pour passer le permis';
                ageResult.className = 'result error';
                restartBtn.classList.remove('hidden');
            }
            
            ageResult.classList.remove('hidden');
        }
        
        function checkDriverTest(passed) {
            const finalResult = document.getElementById('finalResult');
            const restartBtn = document.getElementById('restartBtn');
            
            if (passed) {
                finalResult.innerHTML = '🎉 Félicitations ! Vous avez votre permis de conduire !';
                finalResult.className = 'result success';
            } else {
                finalResult.innerHTML = '😔 Vous devez repasser le test de conduite';
                finalResult.className = 'result warning';
            }
            
            finalResult.classList.remove('hidden');
            restartBtn.classList.remove('hidden');
        }
        
        function restart() {
            // Réinitialiser tout
            document.getElementById('ageInput').value = '';
            document.getElementById('ageResult').classList.add('hidden');
            document.getElementById('driverQuestion').classList.add('hidden');
            document.getElementById('finalResult').classList.add('hidden');
            document.getElementById('restartBtn').classList.add('hidden');
        }
        
        // Permettre de valider avec Enter
        document.getElementById('ageInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                checkAge();
            }
        });
    </script>
</body>
</html>
