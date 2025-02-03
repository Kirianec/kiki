<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¿Quieres ser mi San Valentín?</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #ffe6e6;
            text-align: center;
            padding: 50px;
            color: #ff0066;
            position: relative;
            overflow: hidden;
        }
        
        /* New heart background animation */
        .heart-background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }

        .heart {
            position: absolute;
            width: 20px;
            height: 20px;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%23ff0066" fill-opacity="0.3"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>') no-repeat center center;
            background-size: contain;
            opacity: 0.6;
            animation: fall linear infinite;
        }

        @keyframes fall {
            0% {
                transform: translateY(-100%) rotate(0deg);
                opacity: 0.6;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        h1 {
            font-size: 3em;
            margin-bottom: 20px;
            text-shadow: 2px 2px 5px rgba(255, 0, 102, 0.5);
            font-weight: 600;
            position: relative;
            z-index: 10;
        }
        p {
            font-size: 1.5em;
            margin-bottom: 30px;
            font-weight: 300;
            position: relative;
            z-index: 10;
        }
        .button {
            background-color: #ff0066;
            color: white;
            padding: 15px 30px;
            font-size: 1.2em;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
            text-decoration: none;
            box-shadow: 2px 2px 10px rgba(255, 0, 102, 0.5);
            font-weight: 400;
            animation: glow 2s infinite alternate;
            position: relative;
            z-index: 10;
        }
        .button:hover {
            background-color: #ff3399;
            transform: scale(1.05);
        }

        @keyframes glow {
            0% { box-shadow: 0 0 10px rgba(255, 0, 102, 0.5); }
            50% { box-shadow: 0 0 20px rgba(255, 0, 102, 0.8); }
            100% { box-shadow: 0 0 10px rgba(255, 0, 102, 0.5); }
        }

        .floating {
            position: absolute;
            font-size: 24px;
            animation: float 5s linear infinite;
            opacity: 0.7;
        }
        @keyframes float {
            0% { transform: translateY(100vh) scale(1); opacity: 0; }
            50% { opacity: 1; }
            100% { transform: translateY(-10vh) scale(1.5); opacity: 0; }
        }

        .photo {
            position: absolute;
            width: 120px;
            height: 120px;
            border-radius: 10px;
            opacity: 0.8;
            box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.3);
            object-fit: cover;
            z-index: 10;
        }

        /* Notitas flotantes */
        .note {
            position: absolute;
            background-color: #fff7f7;
            color: #ff0066;
            font-size: 1.2em;
            padding: 10px 20px;
            border-radius: 8px;
            border: 1px solid #ff0066;
            box-shadow: 2px 2px 5px rgba(255, 0, 102, 0.5);
            opacity: 0;
            animation: floatNote 8s linear forwards;
            z-index: 10;
        }

        @keyframes floatNote {
            0% { transform: translateY(100vh) scale(0.8); opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
            100% { transform: translateY(-10vh) scale(1.2); opacity: 0; }
        }

    </style>
</head>
<body>

    <div class="heart-background" id="heart-background"></div>

    <audio autoplay loop>
        <source src="https://www.bensound.com/bensound-music/bensound-love.mp3" type="audio/mpeg">
    </audio>

    <h1>¡Hola, mi princesa! 💖</h1>
    <p>Quiero preguntarte algo especial...</p>
    <p>¿Quieres ser mi San Valentín este 14 de febrero y por todos los que sigan durante muchos años? 💕</p>
    <a href="carta.html" class="button">¡Sí, claro! 💘</a>


    <img src="https://i.imgur.com/yhUnAwr.jpg" class="photo" style="top: 5%; left: 5%;"> 
    <img src="https://i.imgur.com/g3ATYh3.jpg" class="photo" style="top: 25%; right: 15%;">
    <img src="https://i.imgur.com/2FRejXM.jpg" class="photo" style="bottom:-25%; left: 46%;">

    <script>
        function createFloatingElement(symbol) {
            const element = document.createElement("div");
            element.innerHTML = symbol;
            element.classList.add("floating");
            document.body.appendChild(element);

            const size = Math.random() * 20 + 20 + "px"; 
            element.style.fontSize = size;
            element.style.left = Math.random() * 100 + "vw";
            element.style.animationDuration = Math.random() * 3 + 3 + "s";

            setTimeout(() => { element.remove(); }, 5000);
        }

        function createFloatingNote(text, position) {
            const note = document.createElement("div");
            note.classList.add("note");
            note.innerHTML = text;
            document.body.appendChild(note);

            // Separar las notas en mitades de pantalla
            if (position === "left") {
                note.style.left = Math.random() * 40 + 5 + "vw"; 
            } else {
                note.style.left = Math.random() * 40 + 50 + "vw"; 
            }
            
            note.style.top = Math.random() * 50 + 20 + "vh";
            note.style.animationDuration = Math.random() * 5 + 5 + "s";

            setTimeout(() => { note.remove(); }, 8000);
        }

        // Function to create falling hearts background
        function createHeartBackground() {
            const background = document.getElementById('heart-background');
            const heartCount = 50; // Number of hearts

            for (let i = 0; i < heartCount; i++) {
                const heart = document.createElement('div');
                heart.classList.add('heart');
                
                // Randomize position, size, and fall duration
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.width = (Math.random() * 30 + 10) + 'px';
                heart.style.height = heart.style.width;
                heart.style.animationDuration = (Math.random() * 10 + 5) + 's';
                heart.style.animationDelay = Math.random() * -10 + 's';

                background.appendChild(heart);
            }
        }

        // Generate falling hearts on page load
        createHeartBackground();

        // Generar corazones y flores flotantes de forma continua
        const symbols = ["💖", "💘", "💝", "🌸", "💕"];
        setInterval(() => {
            const randomSymbol = symbols[Math.floor(Math.random() * symbols.length)];
            createFloatingElement(randomSymbol);
        }, 1200);

        // Notas de amor que aparecerán aleatoriamente
        const notes = [
            "Te amo más de lo que mis palabras pueden expresar. 💗",
            "Cada momento contigo es un regalo. 🎁",
            "Mi corazón es tuyo, siempre. 💘",
            "Eres el amor de mi vida. 💕",
            "Nuestro amor es eterno. ✨",
            "No hay día que no piense en ti. 💞",
            "Gracias por hacer mi vida más hermosa. 🌹",
            "Juntos, para siempre. 💑"
        ];

        let noteIndex = 0;
        setInterval(() => {
            if (noteIndex < notes.length) {
                createFloatingNote(notes[noteIndex], "left");
                createFloatingNote(notes[(noteIndex + 1) % notes.length], "right");
                noteIndex = (noteIndex + 2) % notes.length;
            }
        }, 3000); // Aparecen dos nuevas notas cada 3 segundos en zonas separadas

    </script>

</body>
</html> 
