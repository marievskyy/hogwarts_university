# hogwarts_university
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Хогвартс: Учёба для Слизерина</title>
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
            color: #a3c98f; /* Светло-зелёный цвет */
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
            font-size: 2.5em;
        }

        h2 {
            font-size: 1.8em;
            margin-bottom: 10px;
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

        .section h3 {
            color: #8ac79a;
            border-bottom: 1px solid #3b4f37;
            padding-bottom: 5px;
        }

        button {
            background-color: #4a6a5d;
            color: #e5e5e5;
            border: none;
            padding: 8px 12px;
            margin: 5px;
            cursor: pointer;
            border-radius: 5px;
            font-size: 1em;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #6b8e6b;
        }

        input {
            background-color: #222e24;
            color: #d4d4d4;
            border: 1px solid #3b4f37;
            padding: 5px;
            margin: 5px;
            border-radius: 5px;
            width: calc(100% - 12px);
            font-size: 1em;
        }

        .score {
            font-size: 1.2em;
            font-weight: bold;
            color: #a3c98f;
            text-align: center;
        }

        ul {
            list-style: none;
            padding: 0;
        }

        li {
            margin: 10px 0;
            font-size: 1.1em;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .completed {
            text-decoration: line-through;
            color: #707070;
        }
    </style>
</head>
<body>
    <h1>Хогвартс: Учёба для Слизерина</h1>
    <h2>3-й семестр</h2>

    <div class="section">
        <p class="score">Очки для факультета Слизерин: <span id="points">0</span></p>

        <!-- Задания по предметам -->
        <h3>Задания по предметам</h3>
        <ul id="tasks">
            <li>
                <span>Зельеварение: Изучить ферментативные реакции</span>
                <button onclick="completeTask(this, 10)">Завершить (+10 очков)</button>
            </li>
        </ul>
        <!-- Добавить задание -->
        <input type="text" id="taskInput" placeholder="Название нового задания">
        <input type="number" id="taskPoints" placeholder="Очки">
        <button onclick="addTask()">Добавить задание</button>

        <!-- Сайд-квесты -->
        <h3>Сайд-квесты</h3>
        <ul id="sideQuests">
            <li>
                <span>Плавание 2 раза в неделю</span>
                <button onclick="completeTask(this, 5)">Завершить (+5 очков)</button>
            </li>
        </ul>
        <!-- Добавить сайд-квест -->
        <input type="text" id="sideInput" placeholder="Название нового сайд-квеста">
        <input type="number" id="sidePoints" placeholder="Очки">
        <button onclick="addSideQuest()">Добавить сайд-квест</button>
    </div>

    <script>
        let totalPoints = 0;

        // Завершить задание
        function completeTask(button, points) {
            totalPoints += points;
            document.getElementById('points').textContent = totalPoints;

            const taskItem = button.parentElement;
            taskItem.querySelector('span').classList.add('completed');
            button.remove();
        }

        // Добавить новое задание по предметам
        function addTask() {
            const taskText = document.getElementById('taskInput').value;
            const taskPoints = parseInt(document.getElementById('taskPoints').value);

            if (taskText && taskPoints) {
                const tasksList = document.getElementById('tasks');
                const newTask = document.createElement('li');
                newTask.innerHTML = `
                    <span>${taskText}</span>
                    <button onclick="completeTask(this, ${taskPoints})">Завершить (+${taskPoints} очков)</button>
                `;
                tasksList.appendChild(newTask);
                document.getElementById('taskInput').value = '';
                document.getElementById('taskPoints').value = '';
            }
        }

        // Добавить новый сайд-квест
        function addSideQuest() {
            const sideText = document.getElementById('sideInput').value;
            const sidePoints = parseInt(document.getElementById('sidePoints').value);

            if (sideText && sidePoints) {
                const sideList = document.getElementById('sideQuests');
                const newQuest = document.createElement('li');
                newQuest.innerHTML = `
                    <span>${sideText}</span>
                    <button onclick="completeTask(this, ${sidePoints})">Завершить (+${sidePoints} очков)</button>
                `;
                sideList.appendChild(newQuest);
                document.getElementById('sideInput').value = '';
                document.getElementById('sidePoints').value = '';
            }
        }
    </script>
</body>
</html>
