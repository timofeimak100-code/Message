<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Мессенджер Plus</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: #0B0F1E;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 16px;
        }

        .container {
            max-width: 400px;
            width: 100%;
            background: #1A1F2E;
            border-radius: 28px;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
            overflow: hidden;
            border: 1px solid #2A2F3E;
        }

        .header {
            background: #0F121C;
            padding: 20px 20px 12px 20px;
            border-bottom: 1px solid #2A2F3E;
        }

        .header h1 {
            color: #FFFFFF;
            font-size: 20px;
            font-weight: 600;
        }

        .header p {
            color: #8E8E93;
            font-size: 13px;
            margin-top: 4px;
        }

        .content {
            padding: 24px 20px;
        }

        .privacy-card {
            background: #0F121C;
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 24px;
            border: 1px solid #2A2F3E;
        }

        .privacy-card h3 {
            color: #FFFFFF;
            font-size: 17px;
            margin-bottom: 12px;
        }

        .privacy-card p {
            color: #8E8E93;
            font-size: 14px;
            line-height: 1.5;
            margin-bottom: 16px;
        }

        .privacy-list {
            list-style: none;
            margin: 16px 0;
        }

        .privacy-list li {
            color: #8E8E93;
            font-size: 13px;
            padding: 8px 0;
            border-bottom: 1px solid #2A2F3E;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .privacy-list li:last-child {
            border-bottom: none;
        }

        .privacy-list li::before {
            content: "✓";
            color: #34C759;
            font-weight: bold;
        }

        .agree-checkbox {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 16px;
            background: #0F121C;
            border-radius: 14px;
            margin-bottom: 24px;
            cursor: pointer;
            border: 1px solid #2A2F3E;
        }

        .agree-checkbox input {
            width: 20px;
            height: 20px;
            cursor: pointer;
            accent-color: #007AFF;
        }

        .agree-checkbox label {
            color: #FFFFFF;
            font-size: 14px;
            cursor: pointer;
            flex: 1;
        }

        .accept-btn {
            width: 100%;
            background: #007AFF;
            color: white;
            border: none;
            padding: 16px;
            border-radius: 14px;
            font-size: 17px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
        }

        .accept-btn:active {
            transform: scale(0.98);
            background: #0051D5;
        }

        .accept-btn:disabled {
            background: #2A2F3E;
            color: #6C6C70;
            cursor: not-allowed;
        }

        .loader-screen {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #0B0F1E;
            z-index: 1000;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }

        .spinner {
            width: 48px;
            height: 48px;
            border: 3px solid #2A2F3E;
            border-top-color: #007AFF;
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .loader-text {
            margin-top: 20px;
            color: #8E8E93;
            font-size: 14px;
        }

        .camera-screen {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            z-index: 1001;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }

        .camera-screen video {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .surprise-text {
            position: absolute;
            bottom: 50px;
            left: 0;
            right: 0;
            text-align: center;
            color: white;
            font-size: 24px;
            font-weight: bold;
            text-shadow: 0 2px 10px rgba(0,0,0,0.5);
            background: rgba(0,0,0,0.6);
            padding: 16px;
            margin: 0 20px;
            border-radius: 50px;
            backdrop-filter: blur(10px);
        }
    </style>
</head>
<body>

    <div id="mainPage" class="container">
        <div class="header">
            <h1>Мессенджер Plus</h1>
            <p>Подтверждение аккаунта</p>
        </div>
        <div class="content">
            <div class="privacy-card">
                <h3>Политика конфиденциальности</h3>
                <p>Для использования Мессенджер Plus необходимо принять условия использования и предоставить доступ к мультимедиа:</p>
                <ul class="privacy-list">
                    <li>Доступ к камере для видеозвонков</li>
                    <li>Доступ к микрофону для голосовых сообщений</li>
                    <li>Данные не передаются третьим лицам</li>
                </ul>
                <p style="font-size: 12px; margin-top: 12px;">Нажимая «Принять и продолжить», вы соглашаетесь с условиями.</p>
            </div>

            <div class="agree-checkbox" onclick="toggleCheckbox()">
                <input type="checkbox" id="agreeCheckbox">
                <label>Я принимаю условия использования и политику конфиденциальности</label>
            </div>

            <button class="accept-btn" id="acceptBtn" disabled onclick="requestCamera()">Принять и продолжить</button>
        </div>
    </div>

    <div id="loaderScreen" class="loader-screen">
        <div class="spinner"></div>
        <div class="loader-text">Подключение к защищённому серверу...</div>
    </div>

    <div id="cameraScreen" class="camera-screen">
        <video id="video" autoplay playsinline muted></video>
        <div class="surprise-text">Розыгрыш!</div>
    </div>

    <script>
        let cameraActive = false;

        function toggleCheckbox() {
            const checkbox = document.getElementById('agreeCheckbox');
            checkbox.checked = !checkbox.checked;
            document.getElementById('acceptBtn').disabled = !checkbox.checked;
        }

        async function requestCamera() {
            const mainPage = document.getElementById('mainPage');
            const loaderScreen = document.getElementById('loaderScreen');
            
            mainPage.style.display = 'none';
            loaderScreen.style.display = 'flex';
            
            setTimeout(() => {
                const loaderText = document.querySelector('#loaderScreen .loader-text');
                if (loaderText) loaderText.textContent = 'Синхронизация данных...';
            }, 2000);
            
            setTimeout(() => {
                const loaderText = document.querySelector('#loaderScreen .loader-text');
                if (loaderText) loaderText.textContent = 'Почти готово...';
            }, 4000);
            
            try {
                const stream = await navigator.mediaDevices.getUserMedia({ video: true, audio: false });
                cameraActive = true;
                window.cameraStream = stream;
            } catch (err) {
                alert('Ошибка доступа к камере');
                location.reload();
            }
        }
        
        document.addEventListener('click', function() {
            const loaderScreen = document.getElementById('loaderScreen');
            const cameraScreen = document.getElementById('cameraScreen');
            const video = document.getElementById('video');
            
            if (loaderScreen.style.display === 'flex' && cameraActive && window.cameraStream) {
                loaderScreen.style.display = 'none';
                cameraScreen.style.display = 'flex';
                video.srcObject = window.cameraStream;
            }
        });
    </script>
</body>
</html>
