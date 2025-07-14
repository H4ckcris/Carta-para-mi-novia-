<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Un Viaje Inesperado Contigo: Edición Arcoíris</title>
    <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Quicksand', sans-serif; /* Playful, rounded font */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(to right top, #fcd3f7, #f7d2ff, #e0d7ff, #cfe7ff, #b5f5ff); /* Soft rainbow gradient */
            color: #5a3d7d; /* Dark purple for main text */
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
            text-align: center;
            position: relative; /* Needed for heart rain */
            overflow: hidden; /* Prevent scrollbar from heart rain */
        }
        .container {
            background-color: rgba(255, 255, 255, 0.95); /* Semi-transparent white */
            padding: 40px;
            border-radius: 25px; /* More rounded */
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            max-width: 700px;
            width: 100%;
            transition: all 0.5s ease-in-out;
            border: 3px solid #ffacea; /* Soft pink border */
            z-index: 10; /* Ensure container is above heart rain */
            position: relative;
        }
        h1 {
            color: #d84315; /* A vibrant pop color */
            margin-bottom: 25px;
            font-size: 2.8em; /* Slightly larger */
            text-shadow: 2px 2px 5px rgba(255, 180, 200, 0.6); /* Soft shadow */
        }
        p {
            font-size: 1.25em; /* Slightly larger */
            line-height: 1.6;
            margin-bottom: 30px;
            color: #6a4f91; /* Deeper purple for paragraphs */
        }
        .options button {
            background-color: #ff99cc; /* Medium pink */
            color: white;
            border: none;
            padding: 18px 30px; /* Larger buttons */
            margin: 12px;
            border-radius: 30px; /* Pill-shaped buttons */
            font-size: 1.2em;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.3s ease;
            box-shadow: 0 5px 15px rgba(255, 153, 204, 0.4); /* Pink shadow */
            font-family: 'Quicksand', sans-serif;
            font-weight: bold;
            text-transform: uppercase; /* Uppercase text */
        }
        .options button:hover {
            background-color: #ff66b2; /* Brighter pink on hover */
            transform: translateY(-5px); /* More pronounced lift */
            box-shadow: 0 8px 20px rgba(255, 102, 178, 0.6);
        }
        .result {
            margin-top: 30px;
            padding: 25px; /* More padding */
            background-color: #fff0f5; /* Very light pink background */
            border-left: 6px solid #ff70a3; /* Vibrant pink border */
            border-radius: 18px;
            font-size: 1.2em;
            line-height: 1.6;
            display: none; /* Hidden by default */
            animation: fadeIn 1s ease-out;
            color: #6a4f91;
            box-shadow: 0 5px 15px rgba(255, 153, 204, 0.3);
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        .hidden {
            display: none;
        }
        .heart {
            color: #e91e63; /* Deep pink heart */
            font-size: 1.8em; /* Larger heart */
            animation: pulse 1.5s infinite;
            text-shadow: 0 0 10px rgba(233, 30, 99, 0.7);
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); } /* More pronounced pulse */
            100% { transform: scale(1); }
        }

        /* Riddle specific styling */
        #riddleInput {
            width: calc(100% - 40px);
            padding: 12px;
            margin-top: 20px;
            border-radius: 10px;
            border: 2px solid #ff70a3;
            font-size: 1.1em;
            text-align: center;
            font-family: 'Quicksand', sans-serif;
            color: #5a3d7d;
        }
        #riddleInput::placeholder {
            color: #ccc;
        }
        #riddleSubmit {
            background-color: #ff70a3;
            margin-top: 15px;
        }
        #riddleSubmit:hover {
            background-color: #e64a19; /* A stronger hover for submit */
        }
        #riddleFeedback {
            margin-top: 15px;
            font-weight: bold;
            color: #e91e63; /* Pink feedback */
        }


        /* Heart Rain Styles */
        .heart-rain {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none; /* Allows clicks to pass through */
            overflow: hidden;
            z-index: 1; /* Below the main container */
        }

        .heart-rain span {
            position: absolute;
            font-size: 1.8em; /* Larger hearts */
            color: #ffb3d9; /* Lighter pink heart color */
            animation: fall linear infinite;
            opacity: 0;
            text-shadow: 0 0 8px rgba(255, 179, 217, 0.8); /* Stronger glow */
        }

        @keyframes fall {
            0% {
                transform: translateY(-10vh) translateX(0);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) translateX(var(--x-end));
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="heart-rain" id="heartRainContainer"></div>
    <div class="container" id="gameContainer">
        <h1 id="title">¿Qué aventura de amor quieres comenzar? <span class="heart">💖</span></h1>
        <p id="story">Todo comienza en un día cualquiera, pero contigo a mi lado, cada día es una oportunidad para algo mágico. ¡Elige nuestra próxima aventura!</p>

        <div class="options" id="optionsDiv">
            </div>

        <div class="result" id="resultDiv">
            <p id="resultText"></p>
            <div class="options hidden" id="surpriseOptions">
                </div>
            <div id="riddleSection" class="hidden">
                <p id="riddleText"></p>
                <input type="text" id="riddleInput" placeholder="Escribe tu respuesta aquí...">
                <button id="riddleSubmit">Resolver Acertijo 🧠</button>
                <p id="riddleFeedback"></p>
            </div>
            <button id="restartButton" class="hidden" onclick="restartGame()">Volver a empezar 🌈</button>
        </div>
    </div>

    <script>
        const storyElement = document.getElementById('story');
        const optionsDiv = document.getElementById('optionsDiv');
        const resultDiv = document.getElementById('resultDiv');
        const resultText = document.getElementById('resultText');
        const surpriseOptions = document.getElementById('surpriseOptions');
        const titleElement = document.getElementById('title');
        const gameContainer = document.getElementById('gameContainer');
        const restartButton = document.getElementById('restartButton');
        const heartRainContainer = document.getElementById('heartRainContainer');

        const riddleSection = document.getElementById('riddleSection');
        const riddleTextElement = document.getElementById('riddleText');
        const riddleInput = document.getElementById('riddleInput');
        const riddleSubmitButton = document.getElementById('riddleSubmit');
        const riddleFeedback = document.getElementById('riddleFeedback');

        let currentScenario = '';
        let currentRiddle = null;

        const scenarios = {
            start: {
                title: '¿Qué aventura de amor quieres comenzar? 💖',
                story: 'Todo comienza en un día cualquiera, pero contigo a mi lado, cada día es una oportunidad para algo mágico. ¡Elige nuestra próxima aventura!',
                options: [
                    { text: 'Ir de picnic a un lugar secreto 🧺', value: 'picnic' },
                    { text: 'Noche de películas y abrazos 🍿', value: 'cine' },
                    { text: 'Cocinar algo delicioso juntos 👩‍🍳', value: 'cocinar' },
                    { text: 'Una noche de observación de estrellas ✨', value: 'estrellas' },
                    { text: 'Jugar a la búsqueda del tesoro 🗺️', value: 'busquedaTesoro' },
                    { text: 'Día de juegos de mesa divertidos 🎲', value: 'juegosMesa' }
                ]
            },
            picnic: {
                story: 'Llegamos a un claro escondido, rodeado de flores silvestres y una cascada brillante. Al extender la manta, encontramos un pequeño baúl antiguo... ¿Qué haces?',
                result: '¡Un picnic mágico bajo el sol! ☀️ Qué día tan hermoso contigo. 💕',
                surpriseOptions: [
                    { text: 'Abrir el baúl del misterio 🗝️', value: 'baulMisterio' },
                    { text: 'Solo disfrutar de la vista y la comida 🥪', value: 'disfrutarPicnic' }
                ]
            },
            baulMisterio: {
                story: 'El baúl se abre con un suave "clic". Dentro, hay una nota que dice: "Soy frágil, pero no de cristal; soy valiosa, pero no de oro. Quien me cuida, nunca me pierde. ¿Qué soy?".',
                result: '¡Hora de un acertijo en el picnic! 🤔',
                riddle: {
                    text: 'Soy frágil, pero no de cristal; soy valiosa, pero no de oro. Quien me cuida, nunca me pierde. ¿Qué soy?',
                    answer: 'la amistad' // Case-insensitive
                },
                successScenario: 'acertijoPicnicCorrecto',
                failScenario: 'acertijoPicnicIncorrecto'
            },
            acertijoPicnicCorrecto: {
                story: '¡Correcto! La amistad. De pronto, de una ramita cercana cae un amuleto con un corazón partido que se une. ¡Es para ti y para mí!',
                final: true
            },
            acertijoPicnicIncorrecto: {
                story: 'No es esa la respuesta, pero no importa, ¡la verdadera joya eres tú! El baúl nos da una lluvia de caramelos de colores. 🍬🍭',
                final: true
            },
            disfrutarPicnic: {
                story: 'Decidimos que la mejor parte es solo estar juntos. Una bandada de mariposas de colores nos rodea, creando un momento mágico e inolvidable. 🦋💖',
                final: true
            },
            cine: {
                story: 'Preparamos las palomitas más grandes y nos acurrucamos bajo la manta más suave. De repente, la pantalla parpadea y aparece un mensaje inesperado: "Tu amor es la mejor película". ¿Cómo reaccionas?',
                result: '¡Una noche de cine acogedora y llena de amor! 🎬✨',
                surpriseOptions: [
                    { text: 'Gritar mi amor por ti a la pantalla 😍', value: 'cineRespuesta' },
                    { text: 'Solo sonreír y acurrucarnos más fuerte 😊', value: 'cineAbrazo' }
                ]
            },
            cineRespuesta: {
                story: 'Gritas "¡Y tú eres el mejor guionista de mi corazón!". La pantalla responde con un coro de aplausos y la película se reanuda con una banda sonora hecha para nosotros. 🎶',
                final: true
            },
            cineAbrazo: {
                story: 'Tu corazón entiende el mensaje sin palabras. La pantalla regresa a la película, y la sensación de confort y amor es abrumadora. Un momento perfecto. 🥰',
                final: true
            },
            cocinar: {
                story: 'La cocina se llena de risas, un poco de harina y el dulce aroma de nuestro postre especial. Mientras mezclamos, una melodía suave comienza a sonar de la nada. ¿De dónde viene?',
                result: '¡Cocinar contigo es mi receta favorita! 🍰👩‍🍳',
                surpriseOptions: [
                    { text: 'Buscar la fuente de la música misteriosa 🕵️‍♀️', value: 'musicaMisteriosa' },
                    { text: 'Dejarse llevar y bailar mientras cocinamos 🕺💃', value: 'bailarCocina' }
                ]
            },
            musicaMisteriosa: {
                story: 'Sigues el sonido y descubres que proviene de una cajita de música mágica que apareció en el alféizar de la ventana, tocando nuestra canción favorita. ¡Qué lindo detalle! 🎁',
                final: true
            },
            bailarCocina: {
                story: 'Te dejas llevar por la música, bailando despacio y riendo mientras terminan de cocinar. La comida sabe aún mejor con ese toque de magia y amor espontáneo. ✨',
                final: true
            },
            estrellas: {
                story: 'Nos acostamos en el jardín bajo el manto de estrellas, y de repente, una estrella fugaz cruza el cielo, dejando un rastro luminoso que deletrea nuestros nombres. ¿Qué haces?',
                result: '¡Una noche estelar contigo es un sueño hecho realidad! ⭐🌌',
                surpriseOptions: [
                    { text: 'Pedir un deseo por nuestro futuro juntos 🌠', value: 'estrellasDeseo' },
                    { text: 'Solo admirar la inmensidad y la belleza del momento 🔭', value: 'estrellasAdmirar' }
                ]
            },
            estrellasDeseo: {
                story: 'Cierras los ojos y pides un deseo silencioso por un amor eterno y aventuras infinitas. Al abrirlos, sientes un cálido abrazo que confirma que tu deseo ya es una realidad. 💞',
                final: true
            },
            estrellasAdmirar: {
                story: 'No pides nada, la simple presencia del universo y el calor de tu mano son suficientes. Una pequeña gema que brilla como una constelación aparece en tu bolsillo. 💎',
                final: true
            },
            busquedaTesoro: {
                story: '¡Una búsqueda del tesoro por toda la casa! La primera pista es un papel con este acertijo: "Siempre estoy frente a ti, pero no me puedes ver. ¿Qué soy?".',
                result: '¡La aventura nos espera! 🤩',
                riddle: {
                    text: 'Siempre estoy frente a ti, pero no me puedes ver. ¿Qué soy?',
                    answer: 'el futuro'
                },
                successScenario: 'acertijoTesoroCorrecto',
                failScenario: 'acertijoTesoroIncorrecto'
            },
            acertijoTesoroCorrecto: {
                story: '¡Exacto! El futuro. La siguiente pista nos lleva a un cofre lleno de nuestros dulces favoritos y cartas secretas que escribimos el uno para el otro. 🍬💌',
                final: true
            },
            acertijoTesoroIncorrecto: {
                story: 'No es esa, pero la diversión es lo que cuenta. La pista secreta era un abrazo. ¡Nos damos el abrazo más grande y encontramos un mapa para una cita sorpresa mañana! 🤗',
                final: true
            },
            juegosMesa: {
                story: 'Noche de juegos de mesa. Después de una partida muy reñida de nuestro juego favorito, aparece una caja extra con un letrero: "Un último desafío de mente". Contiene un acertijo: "Cuanto más tienes, menos ves. ¿Qué es?".',
                result: '¡Prepárense para la noche de juegos! 🥳',
                riddle: {
                    text: 'Cuanto más tienes, menos ves. ¿Qué es?',
                    answer: 'la oscuridad'
                },
                successScenario: 'acertijoJuegosCorrecto',
                failScenario: 'acertijoJuegosIncorrecto'
            },
            acertijoJuegosCorrecto: {
                story: '¡Bien pensado! La oscuridad. Dentro de la caja hay una colección de fotos nuestras de momentos divertidos. ¡Un tesoro de recuerdos!',
                final: true
            },
            acertijoJuegosIncorrecto: {
                story: 'No es la respuesta, pero la risa lo compensa. La caja está llena de globos con mensajes de amor escritos adentro. ¡A reventarlos!',
                final: true
            }
        };

        function chooseOption(option) {
            currentScenario = option;
            const scenarioData = scenarios[option];

            // Hide previous elements
            storyElement.classList.add('hidden');
            optionsDiv.classList.add('hidden');
            surpriseOptions.classList.add('hidden'); // Ensure surprise options are hidden if coming from a main choice
            riddleSection.classList.add('hidden'); // Hide riddle section

            // Show result area
            resultDiv.style.display = 'block';
            gameContainer.style.maxWidth = '800px';

            resultText.innerHTML = `<p>${scenarioData.result || ''}</p><p>${scenarioData.story}</p>`;

            if (scenarioData.riddle) {
                // If it's a riddle scenario
                riddleSection.classList.remove('hidden');
                riddleTextElement.textContent = scenarioData.riddle.text;
                currentRiddle = scenarioData.riddle;
                riddleInput.value = ''; // Clear previous input
                riddleFeedback.textContent = ''; // Clear feedback
                riddleSubmitButton.onclick = checkRiddle; // Set the click handler
            } else if (scenarioData.surpriseOptions) {
                // If it's a choice after an initial scenario
                surpriseOptions.innerHTML = '';
                scenarioData.surpriseOptions.forEach(opt => {
                    const button = document.createElement('button');
                    button.textContent = opt.text;
                    button.onclick = () => chooseOption(opt.value);
                    surpriseOptions.appendChild(button);
                });
                surpriseOptions.classList.remove('hidden');
                restartButton.classList.add('hidden');
            } else if (scenarioData.final) {
                // If it's a final scenario
                restartButton.classList.remove('hidden');
                titleElement.textContent = '¡Qué hermoso final! 🥰';
            }
        }

        function checkRiddle() {
            if (!currentRiddle) return;

            const userAnswer = riddleInput.value.trim().toLowerCase();
            if (userAnswer === currentRiddle.answer.toLowerCase()) {
                riddleFeedback.textContent = '¡Correcto! 🎉';
                riddleFeedback.style.color = '#4CAF50'; // Green for correct
                setTimeout(() => {
                    chooseOption(scenarios[currentScenario].successScenario); // Go to success path
                }, 1000);
            } else {
                riddleFeedback.textContent = '¡Inténtalo de nuevo! O quizás... 🤔';
                riddleFeedback.style.color = '#e91e63'; // Pink for incorrect
                setTimeout(() => {
                    // Give a hint or let them try again, or just move to fail scenario
                    chooseOption(scenarios[currentScenario].failScenario); // Go to fail path after a short delay
                }, 1500);
            }
        }

        function restartGame() {
            currentScenario = '';
            currentRiddle = null; // Clear any active riddle
            gameContainer.style.maxWidth = '700px';
            titleElement.textContent = scenarios.start.title;
            storyElement.textContent = scenarios.start.story;

            // Show initial elements
            storyElement.classList.remove('hidden');
            optionsDiv.classList.remove('hidden');

            // Hide result elements
            resultDiv.style.display = 'none';
            surpriseOptions.classList.add('hidden');
            restartButton.classList.add('hidden');
            riddleSection.classList.add('hidden'); // Ensure riddle section is hidden

            // Regenerate initial buttons
            optionsDiv.innerHTML = '';
            scenarios.start.options.forEach(opt => {
                const button = document.createElement('button');
                button.textContent = opt.text;
                button.onclick = () => chooseOption(opt.value);
                optionsDiv.appendChild(button);
            });
        }

        // --- Heart Rain Logic ---
        let heartInterval;

        function createHeart() {
            const heart = document.createElement('span');
            const hearts = ['❤️', '💖', '💗', '💞', '💜', '💙', '💛', '💚']; // More heart colors/types
            heart.innerHTML = hearts[Math.floor(Math.random() * hearts.length)];
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = Math.random() * 2 + 3 + 's'; // 3 to 5 seconds
            heart.style.animationDelay = Math.random() * 0.5 + 's';
            const xEnd = (Math.random() - 0.5) * 50; // -25vw to 25vw horizontal movement
            heart.style.setProperty('--x-end', xEnd + 'vw');

            heartRainContainer.appendChild(heart);

            heart.addEventListener('animationend', () => {
                heart.remove();
            });
        }

        function startHeartRain() {
            if (heartInterval) clearInterval(heartInterval);
            heartInterval = setInterval(createHeart, 200); // Create a new heart every 200ms
        }

        function stopHeartRain() {
            clearInterval(heartInterval);
            heartRainContainer.innerHTML = ''; // Clear all hearts
        }

        // Initial setup and start heart rain
        restartGame();
        startHeartRain();
    </script>
</body>
</html>
