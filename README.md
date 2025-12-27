<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minimalist Focus Widget</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;500;600&family=Playfair+Display:italic,wght@600&display=swap" rel="stylesheet">
    
    <style>
        :root {
            /* Default Aesthetic: "Warm Sand" */
            --bg-color: #fdfaf7;
            --accent-color: #c2a38a;
            --text-main: #3d3d3d;
            --text-muted: #a3a3a3;
            --bar-bg: #ece5df;
        }

        body {
            background-color: transparent;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            font-family: 'Inter', sans-serif;
            overflow: hidden;
        }

        .widget-card {
            background-color: var(--bg-color);
            padding: 35px 30px;
            border-radius: 30px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.04);
            width: 280px;
            text-align: center;
            border: 1px solid rgba(0,0,0,0.03);
            transition: all 0.4s ease;
        }

        #clock {
            font-size: 3.2rem;
            font-weight: 600;
            color: var(--text-main);
            letter-spacing: -2px;
            margin-bottom: 2px;
        }

        #date {
            font-size: 0.75rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 1.5px;
            margin-bottom: 30px;
            font-weight: 500;
        }

        .progress-container {
            margin-bottom: 30px;
        }

        .label-row {
            display: flex;
            justify-content: space-between;
            font-size: 0.7rem;
            color: var(--text-main);
            margin-bottom: 10px;
            font-weight: 600;
            letter-spacing: 0.5px;
        }

        .progress-track {
            background-color: var(--bar-bg);
            height: 5px;
            border-radius: 10px;
            overflow: hidden;
        }

        #progress-fill {
            background-color: var(--accent-color);
            height: 100%;
            width: 0%;
            transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .quote-section {
            padding-top: 20px;
            border-top: 1px solid rgba(0,0,0,0.06);
        }

        #quote {
            font-family: 'Playfair Display', serif;
            font-size: 1.05rem;
            color: var(--text-main);
            line-height: 1.4;
            margin: 0;
            font-style: italic;
        }
    </style>
</head>
<body>

    <div class="widget-card">
        <div id="clock">00:00</div>
        <div id="date">Loading...</div>

        <div class="progress-container">
            <div class="label-row">
                <span>DAY PROGRESS</span>
                <span id="percent">0%</span>
            </div>
            <div class="progress-track">
                <div id="progress-fill"></div>
            </div>
        </div>

        <div class="quote-section">
            <p id="quote">"Create the life you want."</p>
        </div>
    </div>

    <script>
        function applyStyles() {
            const params = new URLSearchParams(window.location.search);
            if (params.has('bg')) document.documentElement.style.setProperty('--bg-color', '#' + params.get('bg'));
            if (params.has('accent')) document.documentElement.style.setProperty('--accent-color', '#' + params.get('accent'));
            if (params.has('text')) document.documentElement.style.setProperty('--text-main', '#' + params.get('text'));
            if (params.has('bar')) document.documentElement.style.setProperty('--bar-bg', '#' + params.get('bar'));
        }

        function refresh() {
            const now = new Date();
            
            // Clock & Date
            const timeStr = now.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit', hour12: false });
            const dateStr = now.toLocaleDateString('en-US', { weekday: 'long', month: 'short', day: 'numeric' });
            
            document.getElementById('clock').textContent = timeStr;
            document.getElementById('date').textContent = dateStr;

            // Day Progress
            const start = new Date(now.getFullYear(), now.getMonth(), now.getDate());
            const progress = Math.floor(((now - start) / 86400000) * 100);
            
            document.getElementById('progress-fill').style.width = progress + '%';
            document.getElementById('percent').textContent = progress + '%';
        }

        const quotes = [
            "Energy flows where intention goes.",
            "Focus on the step, not the mountain.",
            "Small progress is still progress.",
            "Simplicity is the ultimate sophistication.",
            "Your workspace, your sanctuary.",
            "Make today worth remembering."
        ];

        document.getElementById('quote').textContent = `"${quotes[Math.floor(Math.random() * quotes.length)]}"`;

        applyStyles();
        setInterval(refresh, 1000);
        refresh();
    </script>
</body>
</html>
