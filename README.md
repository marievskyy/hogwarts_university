# hogwarts_university
<!DOCTYPE html>
<html lang="ru">
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

        h1, h2 {
            text-align: center;
            color: #a3c98f;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
            font-size: 2.5em;
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

        h3 { color: #8ac79a; border-bottom: 1px solid #3b4f37; }

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

        .score { font-size: 1.2em; font-weight: bold; color: #a3c98f; text-align: center; }

        ul { list-style: none; padding: 0; }

        li { margin: 10px 0; display: flex; justify-content: space-between; }

        .completed { text-decoration: line-through; color: #707070; }

        .hourglass {
            text-align: center;
            margin-top: 20px;
        }

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

        .reward { margin-top: 10px; color: #d4d4d4; font-style: italic; text-align: center; }

        iframe {
            display: block;
            margin: 20px auto;
            border: 2px solid #4a6a5d;
            border-radius: 10px;
        }
    </style>
</head>
<body>
    <h1>Hogwarts | Slytherin Alumni | Maria Black</h1>

    <div class="section">
        <p class="score">Очки для факультета Слизерин: <span id="points">0</span></p>

        <!-- Задания по предметам -->
        <h3>Задания по предметам</h3>
        <ul id="tasks">
            <li>
                <span>Зельеварение: Изучить ферментативные реакции</span>
                <button onclick="completeTask(this, 10, 'study')">Завершить (+10 очков)</button>
            </li>
        </ul>
        <input type="text" id="taskInput" placeholder="Название нового задания">
        <input type="number" id="taskPoints" placeholder="Очки">
        <button onclick="addTask()">Добавить задание</button>

        <!-- Сайд-квесты -->
        <h3>Сайд-квесты</h3>
        <ul id="sideQuests">
            <li>
                <span>Плавание 2 раза в неделю</span>
                <button onclick="completeTask(this, 5, 'life')">Завершить (+5 очков)</button>
            </li>
        </ul>
        <input type="text" id="sideInput" placeholder="Название нового сайд-квеста">
        <input type="number" id="sidePoints" placeholder="Очки">
        <button onclick="addSideQuest()">Добавить сайд-квест</button>
    </div>

    <!-- Песочные часы -->
    <div class="hourglass">
        <h3>Учебные задания</h3>
        <div class="glass">
            <div class="fill" id="studyFill" style="height: 0;"></div>
        </div>
        <p class="reward">Награда: Придумай свою награду</p>

        <h3>Сайд-квесты</h3>
        <div class="glass">
            <div class="fill" id="lifeFill" style="height: 0;"></div>
        </div>
        <p class="reward">Награда: Придумай свою награду</p>
    </div>

    <!-- Встроенные видео -->
    <h3>Видео для вдохновения</h3>
    <iframe width="560" height="315" src="https://www.youtube.com/embed/BMlo8u56VOY?si=NkY2qVe7uWy5yAmk" allowfullscreen></iframe>
    <iframe width="560" height="315" src="https://www.youtube.com/embed/rJf72mokEng?si=K36FJnJqrZbWMM4H" allowfullscreen></iframe>

    <script>
        let totalPoints = 0;
        let studyPoints = 0;
        let lifePoints = 0;

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

            button.parentElement.remove();
        }

        function addTask() {
            const taskText = document.getElementById('taskInput').value;
            const taskPoints = parseInt(document.getElementById('taskPoints').value);

            if (taskText && taskPoints) {
                const tasksList = document.getElementById('tasks');
                const newTask = document.createElement('li');
                newTask.innerHTML = `
                    <span>${taskText}</span>
                    <button onclick="completeTask(this, ${taskPoints}, 'study')">Завершить (+${taskPoints} очков)</button>
                `;
                tasksList.appendChild(newTask);
            }
        }

        function addSideQuest() {
            const sideText = document.getElementById('sideInput').value;
            const sidePoints = parseInt(document.getElementById('sidePoints').value);

            if (sideText && sidePoints) {
                const sideList = document.getElementById('sideQuests');
                const newQuest = document.createElement('li');
                newQuest.innerHTML = `
                    <span>${sideText}</span>
                    <button onclick="completeTask(this, ${sidePoints}, 'life')">Завершить (+${sidePoints} очков)</button>
                `;
                sideList.appendChild(newQuest);
            }
        }
    </script>
</body>
</html>
