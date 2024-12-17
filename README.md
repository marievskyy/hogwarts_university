# hogwarts_university
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Хогвартс: Учёба для Слизерина</title>
    <style>
        body {
            font-family: 'Georgia', serif;
            background-color: #1a1a1a;
            color: #d3d3d3;
            margin: 0;
            padding: 20px;
        }
        h1, h2 { text-align: center; color: #5a8f7b; }
        .section { margin: 20px auto; max-width: 600px; }
        button {
            background-color: #5a8f7b; color: white;
            border: none; padding: 10px; margin: 5px;
            cursor: pointer; border-radius: 5px;
        }
        .score { font-size: 1.2em; font-weight: bold; color: #94c47d; }
        .completed { text-decoration: line-through; color: gray; }
    </style>
</head>
<body>
    <h1>Хогвартс: Учёба для Слизерина</h1>
    <h2>3-й семестр</h2>

    <div class="section">
        <p>Очки для факультета Слизерин: <span id="points" class="score">0</span></p>
        <h3>Задания по предметам</h3>
        <ul id="tasks">
            <li>
                <span>Зельеварение: Изучить ферментативные реакции</span>
                <button onclick="completeTask(this, 10)">Завершить (+10 очков)</button>
            </li>
            <li>
                <span>Трансфигурация: Решить задачи по физической химии</span>
                <button onclick="completeTask(this, 15)">Завершить (+15 очков)</button>
            </li>
        </ul>

        <h3>Сайд-квесты</h3>
        <ul id="sideQuests">
            <li>
                <span>Плавание 2 раза в неделю</span>
                <button onclick="completeTask(this, 5)">Завершить (+5 очков)</button>
            </li>
            <li>
                <span>Урок по японскому</span>
                <button onclick="completeTask(this, 5)">Завершить (+5 очков)</button>
            </li>
        </ul>
    </div>

    <script>
        let totalPoints = 0;

        function completeTask(button, points) {
            totalPoints += points;
            document.getElementById('points').textContent = totalPoints;

            // Помечаем задачу как завершенную
            const taskItem = button.parentElement;
            taskItem.querySelector('span').classList.add('completed');
            button.remove(); // Удаляем кнопку
        }
    </script>
</body>
</html>
