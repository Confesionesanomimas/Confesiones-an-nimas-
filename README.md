# Confesiones-an-nimas-
Manden mensajes anónimos 
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Envíame un mensaje</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin-top: 50px; }
        form { max-width: 500px; margin: 0 auto; padding: 1em; border: 1px solid #ccc; border-radius: 1em; }
        textarea { width: 100%; height: 100px; margin-bottom: 1em; }
        button { padding: 10px 20px; background-color: #4CAF50; color: white; border: none; cursor: pointer; }
        button:hover { background-color: #45a049; }
    </style>
</head>
<body>
    <h1>Envíame un mensaje</h1>
    <form id="contactForm">
        <label for="message">Tu mensaje:</label><br>
        <textarea id="message" name="message" required></textarea><br>
        <button type="button" onclick="sendMessage()">Enviar</button>
    </form>
    <p id="responseMessage"></p>

    <script>
        async function sendMessage() {
            const message = document.getElementById('message').value;
            const responseMessage = document.getElementById('responseMessage');

            if (message.trim() === "") {
                responseMessage.textContent = "Por favor, escribe un mensaje.";
                return;
            }

            try {
                const response = await fetch('https://formspree.io/f/xjkvygwb‘,{  
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ message })
                });
                if (response.ok) {
                    responseMessage.textContent = "Mensaje enviado. ¡Gracias!";
                } else {
                    responseMessage.textContent = "Hubo un problema al enviar tu mensaje.";
                }
            } catch (error) {
                responseMessage.textContent = "Error de conexión.";
            }
        }
    </script>
</body>
</html>