<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bible Study Pomodoro</title>
    <link href="https://fonts.googleapis.com/css2?family=Lobster&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Lobster', cursive;
            text-align: center;
            padding: 50px;
            background-image: url('https://www.kmeel.com/wp-content/uploads/2023/06/230615-Como-52F-22-scaled.jpg');
            background-size: cover;
            background-position: center;
            color: white;
        }

        h1 {
            font-family: 'Lobster', cursive;
            font-size: 4em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.5);
        }

        .pomodoro-description {
            font-size: 1.2em;
            color: #f8f8f8;
            margin-bottom: 20px;
            text-shadow: 1px 1px 4px rgba(0, 0, 0, 0.4);
        }

        .pomodoro-description a {
            color: #ff3385;
            text-decoration: none;
            font-weight: bold;
            margin-left: 10px;
        }

        .pomodoro-description a:hover {
            color: #f1b6c6;
        }

        .timer {
            font-size: 6em;
            margin-bottom: 20px;
        }

        .timer-buttons {
            margin-bottom: 30px;
        }

        .timer-button {
            font-size: 1.2em;
            padding: 15px 30px;
            cursor: pointer;
            background-color: transparent;
            color: white;
            border: 2px solid white;
            border-radius: 12px;
            margin: 0 10px;
            transition: all 0.3s ease;
        }

        .timer-button:hover {
            background-color: rgba(255, 255, 255, 0.3);
            transform: scale(1.05);
        }

        button {
            padding: 15px 30px;
            font-size: 1.2em;
            margin: 0 10px;
            cursor: pointer;
            font-family: 'Lobster', cursive;
            border-radius: 12px;
            border: none;
            background-color: transparent;
            color: white;
            transition: all 0.3s ease;
        }

        button:hover {
            transform: scale(1.05);
            box-shadow: 0px 6px 10px rgba(0, 0, 0, 0.2);
        }

        button:active {
            transform: scale(1);
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 10px;
            padding: 20px;
            width: 300px;
            text-align: center;
            box-shadow: 0px 6px 10px rgba(0, 0, 0, 0.2);
        }

        .modal button {
            margin-top: 20px;
        }

        .exit-modal {
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: rgba(244, 67, 54, 0.7);
            color: white;
            font-size: 1em;
            padding: 5px 10px;
            cursor: pointer;
            border-radius: 8px;
            border: none;
        }

        .exit-modal:hover {
            background-color: rgba(244, 67, 54, 0.9);
            transform: scale(1.05);
        }

        .bible-mascot {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 60px;
            height: auto;
        }

        .footer {
            margin-top: 50px;
            font-size: 1em;
            color: black;
            font-style: italic;
        }

        .task-list-button {
            font-size: 2em;
            color: #ff3385;
            cursor: pointer;
            margin-bottom: 30px;
        }

        .task-list {
            position: fixed;
            left: 50%;
            bottom: -400px;
            transform: translateX(-50%);
            width: 400px;
            height: 300px;
            background-color: #f4f4f4;
            border-radius: 10px;
            box-shadow: 0px 6px 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            text-align: left;
            transition: bottom 0.5s ease;
        }

        .task-list textarea {
            width: 100%;
            height: 70%;
            font-size: 1.2em;
            padding: 15px;
            margin-bottom: 10px;
            resize: none;
            border-radius: 8px;
        }

        .exit-button {
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: transparent;
            color: #ff3385;
            font-size: 2em;
            border: none;
            cursor: pointer;
        }

        .exit-button:hover {
            color: #f1b6c6;
            transform: scale(1.2);
        }

        .bible-verse {
            font-size: 3em;
            color: #f8f8f8;
            text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.5);
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <img src="https://cdn-icons-png.freepik.com/512/6373/6373634.png" class="bible-mascot">

    <h1>Bible Study Pomodoro</h1>

    <div class="pomodoro-description">
        Use the Pomodoro technique to read the word of God. May our Lord Jesus Christ be with you. Amen! ♡
        <div class="pomodoro-description">
            <a href="https://en.wikipedia.org/wiki/Pomodoro_Technique" target="_blank">What is the Pomodoro technique?</a>
        </div>
    </div>

    <div class="timer-buttons">
        <button class="timer-button" onclick="setTime(25)">25 Minute Focus</button>
        <button class="timer-button" onclick="setTime(5)">5 Minute Break</button>
        <button class="timer-button" onclick="setTime(30)">30 Minute Break</button>
    </div>

    <div class="timer" id="timerDisplay">00:00</div>

    <div class="buttons">
        <button id="startButton" onclick="startTimer()">Start</button>
        <button id="stopButton" onclick="stopTimer()">Stop</button>
        <button id="restartButton" onclick="restartTimer()">Restart</button>
    </div>

    <div class="bible-verse" id="bibleVerse">"For I know the plans I have for you, declares the Lord." - Jeremiah 29:11</div>

    <button class="task-list-button" onclick="toggleTaskList()">Task List</button>

    <div class="task-list">
        <textarea id="taskInput" placeholder="Write your tasks here..." onkeydown="if(event.key === 'Enter') addTask()"></textarea>
        <ul id="taskList"></ul>
        <button class="exit-button" onclick="toggleTaskList()">×</button>
    </div>

    <div class="modal" id="sessionEndModal">
        <button onclick="startNextSession(5)">Take a 5 Minute Break</button>
        <button onclick="startNextSession(25)">Study Another 25 Minutes</button>
        <button class="exit-modal" onclick="closeModal()">Exit</button>
    </div>

    <div class="footer">Made by Kourtney Smith</div>

    <script>
        let timeInSeconds = 0;
        let initialTimeInSeconds = 0;
        let timerInterval;
        let pomodoroCount = 0;
        const bibleVerses = [
            '"For I know the plans I have for you, declares the Lord." - Jeremiah 29:11',
            '"The Lord is my shepherd; I shall not want." - Psalm 23:1',
            '"I can do all things through Christ who strengthens me." - Philippians 4:13',
            '"But the fruit of the Spirit is love, joy, peace, forbearance, kindness, goodness, faithfulness." - Galatians 5:22',
            '"The Lord will fight for you; you need only to be still." - Exodus 14:14',
            '"I have fought the good fight, I have finished the race, I have kept the faith." - 2 Timothy 4:7',
            '"Be strong and courageous. Do not be afraid; do not be discouraged, for the Lord your God will be with you wherever you go." - Joshua 1:9',
            '"The peace of God, which transcends all understanding, will guard your hearts and your minds in Christ Jesus." - Philippians 4:7',
            '"You are the light of the world. A town built on a hill cannot be hidden." - Matthew 5:14',
            '"And we know that in all things God works for the good of those who love him, who have been called according to his purpose." - Romans 8:28',
            '"The Lord is close to the brokenhearted and saves those who are crushed in spirit." - Psalm 34:18',
            '"Do not be afraid or discouraged, for the Lord will personally go ahead of you. He will be with you; he will neither fail you nor abandon you." - Deuteronomy 31:8',
            '"Let all that you do be done with love." - 1 Corinthians 16:14',
            '"The Lord is my light and my salvation— whom shall I fear? The Lord is the stronghold of my life— of whom shall I be afraid?" - Psalm 27:1',
            '"No weapon formed against you shall prosper, and every tongue which rises against you in judgment you shall condemn." - Isaiah 54:17',
            '"For nothing will be impossible with God." - Luke 1:37',
            '"The name of the Lord is a fortified tower; the righteous run to it and are safe." - Proverbs 18:10',
            '"And God is able to bless you abundantly, so that in all things at all times, having all that you need, you will abound in every good work." - 2 Corinthians 9:8',
            '"I am the way, the truth, and the life. No one comes to the Father except through me." - John 14:6',
            '"If you confess with your mouth, “Jesus is Lord,” and believe in your heart that God raised him from the dead, you will be saved." - Romans 10:9',
            '"Be anxious for nothing, but in everything by prayer and supplication, with thanksgiving, let your requests be made known to God." - Philippians 4:6',
            '"Jesus Christ is the same yesterday, today, and forever." - Hebrews 13:8',
            '"Cast your burden on the Lord, and He shall sustain you; He shall never permit the righteous to be moved." - Psalm 55:22',
            '"The joy of the Lord is your strength." - Nehemiah 8:10',
            '"And my God will meet all your needs according to the riches of his glory in Christ Jesus." - Philippians 4:19',
            '"If God is for us, who can be against us?" - Romans 8:31',
            '"So do not fear, for I am with you; do not be dismayed, for I am your God. I will strengthen you and help you; I will uphold you with my righteous right hand." - Isaiah 41:10',
            '"The Lord bless you and keep you; the Lord make his face shine on you and be gracious to you." - Numbers 6:24-25'
        ];
        let verseIndex = Math.floor(Math.random() * bibleVerses.length); 

        document.getElementById('bibleVerse').textContent = bibleVerses[verseIndex];

        function setTime(minutes) {
            timeInSeconds = minutes * 60;
            initialTimeInSeconds = timeInSeconds;
            updateTimerDisplay();
        }

        function updateTimerDisplay() {
            const minutes = Math.floor(timeInSeconds / 60);
            const seconds = timeInSeconds % 60;
            document.getElementById('timerDisplay').textContent = `${minutes < 10 ? '0' : ''}${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;

            // Update browser tab title with the remaining time
            document.title = `${minutes}:${seconds < 10 ? '0' : ''}${seconds} - Bible Study Pomodoro`;
        }

        function startTimer() {
            if (!timerInterval) {
                timerInterval = setInterval(function () {
                    if (timeInSeconds <= 0) {
                        clearInterval(timerInterval);
                        timerInterval = null;
                        updateTimerDisplay();
                        playSound();
                        showSessionEndModal();
                    } else {
                        timeInSeconds--;
                        updateTimerDisplay();
                    }
                }, 1000);
            }
        }

        function stopTimer() {
            clearInterval(timerInterval);
            timerInterval = null;
            updateTimerDisplay();
        }

        function restartTimer() {
            stopTimer();
            setTime(25);
            startTimer();
        }

        function showSessionEndModal() {
            document.getElementById("sessionEndModal").style.display = "block";
        }

        function closeModal() {
            document.getElementById("sessionEndModal").style.display = "none";
        }

        function startNextSession(minutes) {
            setTime(minutes);
            startTimer();
            closeModal();
        }

        function toggleTaskList() {
            const taskList = document.querySelector('.task-list');
            taskList.style.bottom = (taskList.style.bottom === '0px') ? '-400px' : '0px';
        }

        function addTask() {
            const taskInput = document.getElementById('taskInput');
            const taskList = document.getElementById('taskList');
            const newTask = document.createElement('li');
            newTask.textContent = taskInput.value;
            taskList.appendChild(newTask);
            taskInput.value = '';
        }
    </script>

</body>
</html>
