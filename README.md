<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>จดหมายถึงสุดหล่อ</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FFF0F5; /* Light pink */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            overflow: hidden; /* Prevent scroll on mobile */
        }
        .envelope-container {
            position: relative;
            width: 90vw; /* Responsive width */
            max-width: 400px; /* Max width for desktop */
            height: 250px;
            perspective: 1000px;
            cursor: pointer;
            border-radius: 1rem; /* Rounded corners */
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); /* Soft shadow */
        }
        .envelope {
            position: relative;
            width: 100%;
            height: 100%;
            transition: transform 0.8s ease-in-out;
            transform-style: preserve-3d;
            border-radius: 1rem;
            background-color: #FFFAFA; /* Snow white */
        }
        .envelope.open {
            transform: rotateX(180deg);
        }
        .front, .back {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            border-radius: 1rem;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            gap: 0.5rem;
        }
        .front {
            background-color: #FFFAFA; /* Snow white */
            z-index: 2;
            transform: rotateX(0deg);
            padding: 1.5rem;
            box-sizing: border-box;
            border: 2px solid #FFC0CB; /* Pink border */
        }
        .back {
            background-color: #FFFAFA; /* Snow white */
            z-index: 1;
            transform: rotateX(180deg);
            padding: 1.5rem;
            box-sizing: border-box;
            border: 2px solid #FFC0CB; /* Pink border */
        }
        .message-box {
            background-color: #FFFAFA; /* Snow white */
            padding: 2rem;
            border-radius: 1.5rem;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15); /* Stronger shadow for message */
            text-align: center;
            font-size: 1.8rem;
            color: #FF69B4; /* Hot pink text */
            font-weight: bold;
            line-height: 1.4;
            max-width: 90vw;
            width: fit-content;
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.8s ease-in-out, transform 0.8s ease-in-out;
        }
        .message-box.visible {
            opacity: 1;
            transform: translateY(0);
        }
        .tap-instruction {
            font-size: 0.9rem;
            color: #C0C0C0; /* Silver for instruction */
            margin-top: 1rem;
        }
    </style>
</head>
<body>
    <div id="envelope-container" class="envelope-container">
        <div id="envelope" class="envelope">
            <!-- Front of the envelope -->
            <div class="front">
                <span class="text-6xl" role="img" aria-label="Heart Emoji">💖</span>
                <p class="text-xl font-semibold text-pink-500">แตะเพื่อเปิด</p>
                <p class="tap-instruction">💌</p>
            </div>
            <!-- Back of the envelope (hidden when closed, revealed when open) -->
            <div class="back">
                <p class="text-xl font-semibold text-pink-500">ความลับเล็กๆ น้อยๆ</p>
            </div>
        </div>
    </div>

    <div id="message-box" class="message-box fixed top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 z-30 hidden">
        พี่น่ารักที่สุดเลย อิอิ 
    </div>

    <script>
        // Get the envelope and message box elements
        const envelope = document.getElementById('envelope');
        const envelopeContainer = document.getElementById('envelope-container');
        const messageBox = document.getElementById('message-box');

        // Function to handle opening the envelope
        function openEnvelope() {
            // Add 'open' class to trigger the rotation animation
            envelope.classList.add('open');

            // Hide the envelope container after the animation completes
            // This timeout should match the CSS transition duration
            setTimeout(() => {
                envelopeContainer.classList.add('hidden');
                // Show and animate the message box
                messageBox.classList.remove('hidden');
                // Use a slight delay to ensure CSS transition applies correctly
                setTimeout(() => {
                    messageBox.classList.add('visible');
                }, 50); // Small delay
            }, 800); // Matches the 0.8s transition in CSS
        }

        // Add click event listener to the envelope container
        envelopeContainer.addEventListener('click', openEnvelope);

        // Optional: Make the message box disappear if clicked after opening
        messageBox.addEventListener('click', () => {
            messageBox.classList.remove('visible');
            setTimeout(() => {
                messageBox.classList.add('hidden');
                // You could reset the envelope here if you want it to be replayable
                // envelope.classList.remove('open');
                // envelopeContainer.classList.remove('hidden');
            }, 800);
        });
    </script>
</body>
</html>

