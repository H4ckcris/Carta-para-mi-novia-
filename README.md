# Carta-para-mi-novia-
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Para Sandra, con Amor ❤️</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');

    body {
      font-family: 'Pacifico', cursive;
      background: linear-gradient(135deg, #ffe6f0, #ffe0ec);
      text-align: center;
      padding: 40px;
      overflow-x: hidden;
    }

    h1 {
      color: #d63384;
      font-size: 2.5em;
    }

    .heart {
      font-size: 60px;
      cursor: pointer;
      transition: transform 0.3s ease;
      user-select: none;
      color: #ff4d6d;
      margin: 20px auto;
      display: inline-block;
    }

    .heart:hover {
      transform: scale(1.2);
    }

    .heart.latido {
      animation: latido 0.6s ease;
      color: #ff1a75;
    }

    @keyframes latido {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.5); }
    }

    .message, .final {
      margin: 30px auto;
      font-size: 22px;
      color: #4a4a4a;
      background: #fff;
      padding: 20px;
      border-radius: 15px;
      width: 90%;
      max-width: 500px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      min-height: 90px;
      display: flex;
      align-items: center;
      justify-content: center;
      opacity: 1;
      transition: opacity 0.5s ease;
    }

    .message.oculto, .final.oculto {
      opacity: 0;
    }

    .btn-reset, .btn-final {
      margin-top: 20px;
      background: #ff4d6d;
      border: none;
      color: white;
      padding: 12px 25px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 16px;
      transition: background-color 0.3s ease;
      user-select: none;
    }

    .btn-reset:hover, .btn-final:hover {
      background: #c9184a;
    }

    .floating-hearts {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      overflow: hidden;
      z-index: 0;
    }

    .floating-hearts span {
      position: absolute;
      width: 30px;
      height: 30px;
      background: url('https://cdn-icons-png.flaticon.com/512/833/833472.png') no-repeat center;
      background-size: contain;
      animation: float 10s linear infinite;
      opacity: 0.6;
      will-change: transform;
    }

    @keyframes float {
      0% { transform: translateY(100vh) scale(0.5); }
      100% { transform: translateY(-10vh) scale(1.2); }
    }

    .final {
      display: none;
      flex-direction: column;
    }

    .final h2 {
      margin-bottom: 15px;
      font-size: 1.8em;
      color: #c2185b;
    }

    .corazon-final {
      font-size: 80px;
      animation: pulse 1s infinite alternate;
      color: #ff1a75;
      margin-top: 20px;
    }

    @keyframes pulse {
      from { transform: scale(1); }
      to { transform: scale(1.3); }
    }

    audio {
      display: none;
    }
  </style>
</head>
<body>
  <h1>Para Sandra Olivet Diego Flores 💖</h1>

  <div class="heart" id="heart" onclick="mostrarMensaje()">❤️</div>

  <div class="message" id="mensaje">Haz clic en el corazón para empezar ✨</div>

  <button class="btn-reset" onclick="reiniciarJuego()">Reiniciar</button>

  <div class="final" id="final">
    <h2>Gracias por leer todo esto, mi amor ❤️</h2>
    <p>
      Quería que sintieras todo lo que haces en mí.<br>
      Tu amor es mi motor, mi paz y mi razón de sonreír todos los días.<br>
      Siempre te elegiré, Sandra. Hoy, mañana y toda la vida. 💍
    </p>

    <img src="https://i.ibb.co/ksQfxCzC/IMG-0257.jpg" alt="Nosotros" style="max-width: 90%; border-radius: 15px; margin-top: 25px; box-shadow: 0 4px 15px rgba(0,0,0,0.2);" />

    <h3 style="margin-top: 20px; color: #c2185b;">Las amo, mi pequeña familia ❤️</h3>

    <div class="corazon-final">💖</div>

    <button class="btn-final" onclick="reiniciarJuego()">Volver a empezar 🔄</button>
  </div>

  <div class="floating-hearts" id="corazones"></div>

  <audio id="musica" autoplay loop>
    <source src="https://www.bensound.com/bensound-music/bensound-romantic.mp3" type="audio/mpeg">
    Tu navegador no soporta música de fondo.
  </audio>

  <script>
    const mensajes = [
      "Eres mi persona favorita en el mundo 🌎",
      "Contigo todo es mejor 🧑‍🧑‍🧒",
      "Gracias por existir, hermosa mujer 💫",
      "Tu sonrisa es mi lugar feliz 😊",
      "Te amo más que a los postres 🍰",
      "Eres mi razón de sonreír cada día 😘",
      "Si pudiera darte una estrella por cada vez que pienso en ti, el cielo estaría vacío ✨",
      "Eres lo mejor que me ha pasado. Junto con mi hija, son lo más bello de este mundo 🥺❤️",
      "Te amo infinitamente ♾️",
      "Lo mejor del mundo eres tú y nuestra criatura 🐥❤️",
      "Amo tus ojos 👀❤️",
      "Amo tu carita hermosa 🥰",
      "Amo tu sonrisa más bella 😍",
      "Amo tu cuerpo 😋",
      "Amo todo de ti 😮‍💨❤️",
      "Gracias por ser parte de mi vida 💖"
    ];

    let usado = [];
    const heart = document.getElementById("heart");
    const mensajeDiv = document.getElementById("mensaje");
    const finalDiv = document.getElementById("final");
    const musica = document.getElementById("musica");

    function mostrarMensaje() {
      if (usado.length === mensajes.length) {
        heart.classList.add("latido");
        setTimeout(() => heart.classList.remove("latido"), 600);

        mensajeDiv.classList.add("oculto");
        setTimeout(() => {
          mensajeDiv.style.display = "none";
          finalDiv.style.display = "flex";
        }, 600);
        return;
      }

      heart.classList.add("latido");
      setTimeout(() => heart.classList.remove("latido"), 600);

      let index;
      do {
        index = Math.floor(Math.random() * mensajes.length);
      } while (usado.includes(index));

      usado.push(index);
      mensajeDiv.classList.add("oculto");
      setTimeout(() => {
        mensajeDiv.textContent = mensajes[index];
        mensajeDiv.classList.remove("oculto");
      }, 500);
    }

    function reiniciarJuego() {
      usado = [];
      mensajeDiv.textContent = "Haz clic en el corazón para empezar ✨";
      mensajeDiv.style.display = "flex";
      finalDiv.style.display = "none";
      // Reiniciar música si quieres (opcional)
      musica.currentTime = 0;
      musica.play();
    }

    // Corazones flotantes
    const container = document.getElementById('corazones');
    for (let i = 0; i < 20; i++) {
      const heartSpan = document.createElement('span');
      heartSpan.style.left = Math.random() * 100 + 'vw';
      heartSpan.style.animationDuration = (5 + Math.random() * 5) + 's';
      heartSpan.style.animationDelay = (Math.random() * 10) + 's';
      container.appendChild(heartSpan);
    }
  </script>
</body>
</html>
