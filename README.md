# hogwarts_university
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hogwarts | Slytherin Alumni | Maria Black</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=EB+Garamond&display=swap');

        body {
            font-family: 'EB Garamond', serif;
            background-color: #0d1117;
            color: #d4d4d4;
            margin: 0;
            padding: 0;
            background-image: url('https://www.transparenttextures.com/patterns/black-paper.png');
        }

        h1, h2, h3 {
            text-align: center;
            color: #a3c98f;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
        }

        .quote {
            text-align: center;
            font-size: 1.4em;
            margin: 20px;
            color: #8ac79a;
            font-style: italic;
        }

        .section {
            margin: 30px auto;
            max-width: 700px;
            background-color: #0f1a12;
            border: 2px solid #3b4f37;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
        }

        button {
            background-color: #4a6a5d;
            color: #e5e5e5;
            border: none;
            padding: 8px 12px;
            margin: 5px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s ease;
        }

        button:hover { background-color: #6b8e6b; }

        input {
            background-color: #222e24;
            color: #d4d4d4;
            border: 1px solid #3b4f37;
            padding: 5px;
            margin: 5px;
            border-radius: 5px;
            width: calc(100% - 12px);
        }

        .score { text-align: center; font-size: 1.2em; color: #8ac79a; }

        .hourglass .glass {
            width: 80px;
            height: 150px;
            border: 2px solid #5a8f7b;
            border-radius: 10px;
            margin: 10px auto;
            background: linear-gradient(to top, #3b4f37 0%, transparent 50%, #3b4f37 100%);
            position: relative;
        }

        .hourglass .fill {
            position: absolute;
            bottom: 0;
            width: 100%;
            background-color: #8ac79a;
            transition: height 0.3s ease-in-out;
        }

        iframe {
            display: block;
            margin: 20px auto;
            border-radius: 10px;
        }
    </style>
</head>
<body>
    <!-- Мотивационная цитата -->
    <div class="quote">
        "Ambition and determination pave the way to greatness. Stay focused, Slytherin."
    </div>

    <h1>Hogwarts | Slytherin Alumni | Maria Black</h1>

    <div class="section">
        <p class="score">Slytherin Points: <span id="points">0</span></p>

        <!-- Tasks Section -->
        <h3>Academic Tasks</h3>
        <ul id="tasks"></ul>
        <input type="text" id="taskInput" placeholder="Task Title">
        <input type="number" id="taskPoints" placeholder="Points">
        <button onclick="addTask()">Add Task</button>

        <h3>Side Quests</h3>
        <ul id="sideQuests"></ul>
        <input type="text" id="sideInput" placeholder="Side Quest">
        <input type="number" id="sidePoints" placeholder="Points">
        <button onclick="addSideQuest()">Add Quest</button>

        <!-- Buttons for Reset -->
        <button onclick="resetAll()">Reset All Points & Hours</button>
    </div>

    <!-- Hourglasses -->
    <div class="hourglass">
        <h3>Academic Hourglass</h3>
        <div class="glass"><div class="fill" id="studyFill" style="height: 0;"></div></div>
        <h3>Side Quest Hourglass</h3>
        <div class="glass"><div class="fill" id="lifeFill" style="height: 0;"></div></div>
    </div>

    <!-- Videos -->
    <h3>Inspiration Videos</h3>
    <iframe width="560" height="315" src="https://www.youtube.com/embed/BMlo8u56VOY" allowfullscreen></iframe>
    <iframe width="560" height="315" src="https://www.youtube.com/embed/rJf72mokEng" allowfullscreen></iframe>

    <script>
        let totalPoints = 0, studyPoints = 0, lifePoints = 0;

        function addTask() {
            addNewTask("tasks", 'study');
        }

        function addSideQuest() {
            addNewTask("sideQuests", 'life');
        }

        function addNewTask(listId, category) {
            const inputText = document.getElementById(category === 'study' ? 'taskInput' : 'sideInput').value;
            const inputPoints = parseInt(document.getElementById(category === 'study' ? 'taskPoints' : 'sidePoints').value);

            if (inputText && inputPoints) {
                const list = document.getElementById(listId);
                const newTask = document.createElement('li');
                newTask.innerHTML = `
                    <span>${inputText}</span>
                    <button onclick="completeTask(this, ${inputPoints}, '${category}')">Complete (+${inputPoints})</button>
                    <button onclick="removeTask(this)">Remove</button>
                `;
                list.appendChild(newTask);
            }
        }

        function completeTask(button, points, category) {
            totalPoints += points;
            document.getElementById('points').textContent = totalPoints;

            if (category === 'study') {
                studyPoints += points;
                document.getElementById('studyFill').style.height = studyPoints + 'px';
            } else {
                lifePoints += points;
                document.getElementById('lifeFill').style.height = lifePoints + 'px';
            }
            button.parentElement.classList.add('completed');
        }

        function removeTask(button) {
            button.parentElement.remove();
        }

        function resetAll() {
            totalPoints = 0; studyPoints = 0; lifePoints = 0;
            document.getElementById('points').textContent = totalPoints;
            document.getElementById('studyFill').style.height = '0';
            document.getElementById('lifeFill').style.height = '0';
            document.getElementById('tasks').innerHTML = '';
            document.getElementById('sideQuests').innerHTML = '';
        }
    </script>
</body>
</html>
