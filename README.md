<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Message</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #ff7eb3, #ff758c, #42a5f5);
            font-family: 'Times New Roman', serif;
            overflow: hidden;
        }

        #content {
            text-align: center;
            color: white;
            font-size: 2em;
            display: none;
        }

        #question {
            display: none;
        }

        .button {
            margin: 10px;
            padding: 10px 20px;
            font-size: 1em;
            color: white;
            background: #4caf50;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        .button:hover {
            background: #388e3c;
        }

        .restart {
            background: #f44336;
        }

        .restart:hover {
            background: #d32f2f;
        }
    </style>
</head>
<body>
    <div id="content">Hello Anvita</div>
    <div id="question">
        <p id="message">Meko Porsche kab mil rahi hai (tere us jane ke bina)?</p>
        <button class="button" id="yesButton">Yes</button>
        <button class="button" id="noButton">No</button>
    </div>

    <script>
        const content = document.getElementById('content');
        const question = document.getElementById('question');
        const message = document.getElementById('message');
        const yesButton = document.getElementById('yesButton');
        const noButton = document.getElementById('noButton');

        function fadeIn(element, callback) {
            element.style.display = 'block';
            element.style.opacity = 0;

            let opacity = 0;
            const fade = setInterval(() => {
                opacity += 0.05;
                element.style.opacity = opacity;
                if (opacity >= 1) {
                    clearInterval(fade);
                    if (callback) callback();
                }
            }, 50);
        }

        function fadeOut(element, callback) {
            let opacity = 1;
            const fade = setInterval(() => {
                opacity -= 0.05;
                element.style.opacity = opacity;
                if (opacity <= 0) {
                    clearInterval(fade);
                    element.style.display = 'none';
                    if (callback) callback();
                }
            }, 50);
        }

        function startProgram() {
            fadeIn(content, () => {
                setTimeout(() => {
                    fadeOut(content, () => {
                        fadeIn(question);
                    });
                }, 2000);
            });
        }

        yesButton.addEventListener('click', () => {
            fadeOut(question, () => {
                message.textContent = "Meko tere pe bharosa hai tu vet banegi aur meko Porsche leke degi!";
                fadeIn(message);
            });
        });

        noButton.addEventListener('click', () => {
            fadeOut(question, () => {
                message.innerHTML = "Pls<br><button class='button restart'>Restart</button>";
                fadeIn(message);
                document.querySelector('.restart').addEventListener('click', () => {
                    fadeOut(message, startProgram);
                });
            });
        });

        startProgram();
    </script>
</body>
</html>
