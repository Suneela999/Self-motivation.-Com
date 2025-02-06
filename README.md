<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Self Management System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }
        body {
            background-color: #f4f4f4;
            color: #333;
            text-align: center;
            padding: 20px;
        }
        h1 {
            margin-bottom: 20px;
        }
        .container {
            max-width: 900px;
            margin: auto;
            padding: 20px;
            background: white;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .section {
            margin: 20px 0;
            padding: 15px;
            border: 1px solid #ddd;
            background: #fff;
        }
        .btn {
            padding: 10px 15px;
            margin-top: 10px;
            cursor: pointer;
            border: none;
            background: #007BFF;
            color: white;
        }
        input, textarea {
            width: 90%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
        }
        ul {
            list-style: none;
        }
        ul li {
            padding: 10px;
            background: #eee;
            margin: 5px 0;
            display: flex;
            justify-content: space-between;
        }
        .completed {
            text-decoration: line-through;
            color: green;
        }
    </style>
</head>
<body>

    <h1>Self-Management Dashboard</h1>
    <div class="container">

        <!-- Goal Setting Section -->
        <div class="section">
            <h2>Goal Setting</h2>
            <input type="text" id="goalInput" placeholder="Enter your goal">
            <button class="btn" onclick="addGoal()">Add Goal</button>
            <ul id="goalList"></ul>
        </div>

        <!-- To-Do List Section -->
        <div class="section">
            <h2>To-Do List</h2>
            <input type="text" id="todoInput" placeholder="Enter task">
            <button class="btn" onclick="addTask()">Add Task</button>
            <ul id="todoList"></ul>
        </div>

        <!-- Pomodoro Timer Section -->
        <div class="section">
            <h2>Pomodoro Timer</h2>
            <p id="timer">25:00</p>
            <button class="btn" onclick="startTimer()">Start</button>
            <button class="btn" onclick="resetTimer()">Reset</button>
        </div>

        <!-- Notes Section -->
        <div class="section">
            <h2>Notes</h2>
            <textarea id="notes" rows="5" placeholder="Write your notes here..."></textarea>
            <button class="btn" onclick="saveNotes()">Save Notes</button>
        </div>

    </div>

    <script>
        // Goal Setting
        function addGoal() {
            let goalInput = document.getElementById("goalInput").value;
            if (goalInput === "") return;
            let goalList = document.getElementById("goalList");
            let li = document.createElement("li");
            li.innerHTML = goalInput + ' <button onclick="this.parentElement.remove()">❌</button>';
            goalList.appendChild(li);
            document.getElementById("goalInput").value = "";
        }

        // To-Do List
        function addTask() {
            let taskInput = document.getElementById("todoInput").value;
            if (taskInput === "") return;
            let todoList = document.getElementById("todoList");
            let li = document.createElement("li");
            li.innerHTML = taskInput + ' <button onclick="this.parentElement.classList.toggle(\'completed\')">✔️</button> <button onclick="this.parentElement.remove()">❌</button>';
            todoList.appendChild(li);
            document.getElementById("todoInput").value = "";
        }

        // Pomodoro Timer
        let time = 1500, timerRunning = false, timerInterval;
        function startTimer() {
            if (timerRunning) return;
            timerRunning = true;
            timerInterval = setInterval(() => {
                if (time <= 0) {
                    clearInterval(timerInterval);
                    timerRunning = false;
                    alert("Time's up!");
                    return;
                }
                time--;
                let minutes = Math.floor(time / 60);
                let seconds = time % 60;
                document.getElementById("timer").innerText = `${minutes}:${seconds < 10 ? "0" + seconds : seconds}`;
            }, 1000);
        }
        function resetTimer() {
            clearInterval(timerInterval);
            timerRunning = false;
            time = 1500;
            document.getElementById("timer").innerText = "25:00";
        }

        // Notes Section
        function saveNotes() {
            let notes = document.getElementById("notes").value;
            localStorage.setItem("userNotes", notes);
            alert("Notes saved!");
        }
        document.getElementById("notes").value = localStorage.getItem("userNotes") || "";
    </script>

</body>
</html># Self-motivation.-Com
