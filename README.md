[U<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8" />
<title>100 razones por amarte 💖</title>
<style>
  body {
    background: #000;
    color: #f0c;
    font-family: 'Courier New', monospace;
    text-align: center;
    padding: 300px;
  }
  button {
    padding: 20px 30px;
    font-size: 28px;
    background: #f0c;
    border: none;
    border-radius: 500px;
    color: #000;
    cursor: pointer;
    margin-top: 100px;
  }
  #razon {
    font-size: 50px;
    margin-top: 100px;
  }
</style>
</head>
<body>
  <h1>100 razones por amarte</h1>
  <button onclick="mostrarRazon()">Dame una razón 💕</button>
  <div id="razon"></div>

  <script>
    const razones = [
      "Por tu sonrisa que ilumina mi día.",
      "Porque eres mi paz en medio del caos.",
      "Por cada abrazo que me das.",
      "Porque haces que mi corazón lata más rápido.",
      "Por tu ternura y tu risa contagiosa.",
      "Por apoyarme siempre.",
      "Porque haces que la vida sea mejor.",
      "Por tus ojos que brillan como estrellas.",
      "Porque contigo todo es posible.",
      "Por ser mi mejor amiga y amor."
    ];

    function mostrarRazon() {
      const idx = Math.floor(Math.random() * razones.length);
      document.getElementById("razon").textContent = razones[idx];
    }
  </script>
</body>
</html>ploading MUJer.html…]()
