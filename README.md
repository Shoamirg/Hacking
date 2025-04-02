# Hacking
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <title>Hacking</title>
    
    <style>
    
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            background: black;
            overflow: hidden;
            font-family: 'Courier New', monospace;
            color: #00FF00;
        }
        
        canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            background: black;
        }
    
        #terminal {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            padding: 20px;
            z-index: 2;
            white-space: pre-wrap;
            pointer-events: none;
        }
        
        .blink {
            animation: blink 1s infinite;
        }
        
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }
    </style>
</head>
<body>

<canvas id="matrixCanvas"></canvas>
<div id="terminal"></div>

<script>
    const canvas = document.getElementById('matrixCanvas');
    const ctx = canvas.getContext('2d');

    function resizeCanvas() {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();  

    const katakana = 'アァカサタナハマヤャラワガザダバパイィキシチニヒミリヰギジヂビピウゥクスツヌフムユュルグズブヅプエェケセテネヘメレヱゲゼデベペオォコソトノホモヨョロヲゴゾドボポヴッン';
    const latin = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
    const nums = '0123456789';
    const alphabet = katakana + latin + nums;

    const fontSize = 16;
    const columns = Math.floor(canvas.width / fontSize);
    const rainDrops = Array(columns).fill(1);

    function drawMatrix() {
        ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        ctx.fillStyle = '#0F0';
        ctx.font = `${fontSize}px monospace`;

        rainDrops.forEach((y, index) => {
            const text = alphabet.charAt(Math.floor(Math.random() * alphabet.length));
            const x = index * fontSize;
            ctx.fillText(text, x, y * fontSize);

            if (y * fontSize > canvas.height && Math.random() > 0.975) {
                rainDrops[index] = 0;
            } else {
                rainDrops[index]++;
            }
        });
    }
    setInterval(drawMatrix, 50);

    const terminal = document.getElementById('terminal');
    const commands = [
        '[SYSTEM] Initializing hack.exe...',
        '[FIREWALL] Bypassing encryption...',
        '[ACCESS] Connecting to secure server...',
        '[ACCESS] Root privileges acquired!',
        '[WARNING] Unauthorized access detected!',
        '[DATA] Extracting sensitive files...',
        '[UPLOAD] Injecting malware...',
        '[CRITICAL] SYSTEM FAILURE IMMINENT!',
        '[ERROR] Blue Screen Detected!',
        '[JOKE] Haha! Just kidding :)'
    ];

    let commandIndex = 0;
    let charIndex = 0;

    function typeCommand() {
        if (commandIndex < commands.length) {
            const currentCommand = commands[commandIndex];
            if (charIndex < currentCommand.length) {
                terminal.innerHTML += currentCommand.charAt(charIndex);
                charIndex++;
                setTimeout(typeCommand, 50);
            } else {
                terminal.innerHTML += '\n';
                charIndex = 0;
                commandIndex++;
                setTimeout(typeCommand, 500);
            }
        } else {
            terminal.innerHTML += '\n> ';
            setInterval(() => {
                terminal.innerHTML = terminal.innerHTML.slice(0, -1) + (terminal.innerHTML.endsWith(' ') ? '█' : ' ');
            }, 500);
        }
    }

    setTimeout(typeCommand, 1000);
</script>

</body>
</html>
