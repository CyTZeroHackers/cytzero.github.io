<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>503 Bad Gateway - Server Error</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: linear-gradient(135deg, #2a2c36, #1c1f26);
            font-family: 'Poppins', sans-serif;
            color: #ffffff;
            overflow: hidden;
        }

        /* Animated Background */
        body:before {
            content: '';
            position: absolute;
            top: -50px;
            left: -50px;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(0,0,0,0.5), rgba(0,0,0,0.7));
            background-size: 200% 200%;
            animation: backgroundAnimation 20s ease infinite;
            z-index: -1;
        }

        @keyframes backgroundAnimation {
            0% { background-position: 0% 0%; }
            50% { background-position: 100% 100%; }
            100% { background-position: 0% 0%; }
        }

        /* Error Container */
        .error-container {
            background: rgba(30, 30, 30, 0.9);
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0px 5px 30px rgba(0, 0, 0, 0.7);
            text-align: center;
            width: 400px;
            animation: fadeIn 1s forwards;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Error Code Style */
        .error-code {
            font-size: 120px; /* Larger size */
            font-weight: 700;
            color: #ff5757;
            margin: 0;
            animation: glitch 1.5s infinite;
        }

        @keyframes glitch {
            0% { transform: translate(0); }
            20% { transform: translate(-2px, -2px); }
            40% { transform: translate(2px, 2px); }
            60% { transform: translate(-1px, 1px); }
            80% { transform: translate(1px, -1px); }
            100% { transform: translate(0); }
        }

        .error-title {
            font-size: 26px; /* Larger title */
            margin: 10px 0;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
            animation: textFlicker 3s infinite;
        }

        @keyframes textFlicker {
            0%, 19%, 21%, 23%, 25%, 54%, 56%, 100% { opacity: 1; }
            20%, 24%, 55% { opacity: 0; }
        }

        .error-message {
            font-size: 14px; /* Slightly larger */
            color: #d3d3d3;
            margin-top: 10px;
            animation: slideIn 1s forwards;
        }

        @keyframes slideIn {
            from { transform: translateY(20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        /* Gear Animation */
        .gear-container {
            margin-top: 30px;
            position: relative;
            width: 100px; /* Larger gear */
            height: 100px;
            margin-left: auto;
            margin-right: auto;
            animation: spin 4s infinite linear;
        }

        @keyframes spin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .gear {
            stroke: #ff5757;
            stroke-width: 3;
            fill: none;
            animation: pulse 1.5s infinite alternate;
        }

        @keyframes pulse {
            0% { stroke-width: 3; }
            100% { stroke-width: 5; }
        }

        /* Retry Button */
        .retry-button {
            display: inline-block;
            margin-top: 30px;
            padding: 12px 25px; /* Larger button */
            background: #ff5757;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            font-size: 16px; /* Larger font */
            cursor: pointer;
            box-shadow: 0 0 20px rgba(255, 87, 87, 0.6);
            transition: background-color 0.3s, box-shadow 0.3s;
            animation: glowRetry 2s infinite alternate;
        }

        @keyframes glowRetry {
            0% { box-shadow: 0 0 10px rgba(255, 87, 87, 0.8); }
            100% { box-shadow: 0 0 20px rgba(255, 87, 87, 1); }
        }

        .retry-button:hover {
            background: #ff2e2e;
            box-shadow: 0 0 30px rgba(255, 87, 87, 1);
        }

        /* Console Log */
        .console-log {
            margin-top: 20px;
            background: #1c1f26;
            padding: 10px;
            height: 120px; /* Increased height */
            overflow-y: auto;
            color: #fff;
            font-size: 12px; /* Larger font */
            border-radius: 5px;
            box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.5);
            text-align: left;
        }

        .console-log p {
            margin: 5px 0;
            line-height: 1.4;
        }

        .footer {
            margin-top: 10px;
            font-size: 12px; /* Slightly larger footer */
            color: #999;
        }
    </style>
</head>
<body>
    <div class="error-container">
        <div class="error-code">503</div>
        <div class="error-title">Bad Gateway</div>
        <div class="error-message">The server is currently unavailable. We're working on it!</div>

        <!-- Gear Animation -->
        <div class="gear-container">
            <svg class="gear" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" width="100" height="100">
                <path d="M50,10 L60,20 L75,25 L80,40 L75,55 L60,60 L50,70 L40,60 L25,55 L20,40 L25,25 L40,20 Z"></path>
            </svg>
        </div>

        <!-- Console Log -->
        <div class="console-log" id="console-log">
            <p>Attempting to reconnect... <span class="log-time">[00:00]</span></p>
        </div>

        <div class="retry-button" onclick="retryPage()">Retry</div>

        <div class="footer">&copy; 2024 CyTZero</div>
    </div>

    <script>
        // Log simulation with timestamps
        const logs = [
            'Attempting to reconnect...',
            'Failed to reach the server. Retrying...',
            'Server overload. Attempting to route traffic...',
            'Reconnecting to backup server...',
            'Error: Server unresponsive.',
            'Retrying in 5 seconds...'
        ];

        let logIndex = 0;

        function updateLogs() {
            const logArea = document.getElementById('console-log');
            const newLog = document.createElement('p');
            newLog.textContent = logs[logIndex] + ' [' + new Date().toLocaleTimeString() + ']';
            logArea.appendChild(newLog);
            logArea.scrollTop = logArea.scrollHeight;
            logIndex = (logIndex + 1) % logs.length;
        }

        setInterval(updateLogs, 3000);  // Updates log every 3 seconds

        // Retry function reloads the page
        function retryPage() {
            document.querySelector('.retry-button').textContent = 'Retrying...';
            setTimeout(() => location.reload(), 2000);
        }
    </script>
</body>
</html>
