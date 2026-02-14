<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>O'zbekiston Ob-havo</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        html, body {
            width: 100%;
            height: 100%;
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background: linear-gradient(145deg, #0B3B5C 0%, #1B5A7A 100%);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            padding: 0;
            margin: 0;
            min-height: 100vh;
            min-height: -webkit-fill-available;
        }

        /* TUNGI REJIM */
        body.dark-mode {
            background: linear-gradient(145deg, #0a0f1c 0%, #1a1f2e 100%);
        }

        .container {
            width: 100%;
            max-width: 480px;
            background: rgba(255, 255, 255, 0.98);
            border-radius: 28px 28px 0 0;
            padding: 18px 16px 20px;
            margin: 10px auto 0;
            box-shadow: 0 -10px 30px rgba(0, 0, 0, 0.15);
            flex: 1;
            min-height: calc(100vh - 20px);
        }

        body.dark-mode .container {
            background: rgba(20, 25, 35, 0.98);
            box-shadow: 0 -10px 30px rgba(0, 0, 0, 0.5);
        }

        /* Telegram Web App Header */
        .telegram-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 8px 0 12px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
            margin-bottom: 12px;
        }

        .telegram-back-btn {
            background: rgba(255, 255, 255, 0.2);
            border: none;
            width: 36px;
            height: 36px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            color: white;
            cursor: pointer;
            backdrop-filter: blur(5px);
        }

        .telegram-title {
            color: white;
            font-size: 18px;
            font-weight: 600;
        }

        .telegram-close-btn {
            background: rgba(255, 255, 255, 0.2);
            border: none;
            width: 36px;
            height: 36px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            color: white;
            cursor: pointer;
        }

        .theme-toggle {
            background: rgba(255, 255, 255, 0.2);
            border: none;
            width: 36px;
            height: 36px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            color: white;
            cursor: pointer;
            backdrop-filter: blur(5px);
        }

        .header {
            text-align: center;
            margin-bottom: 16px;
        }

        .header h1 {
            font-size: 22px;
            background: linear-gradient(135deg, #0B3B5C, #1B5A7A);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 4px;
            font-weight: 700;
        }

        body.dark-mode .header h1 {
            background: linear-gradient(135deg, #8ab3ff, #5d8ad9);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .date {
            background: #E3F2FD;
            color: #0B3B5C;
            padding: 6px 16px;
            border-radius: 30px;
            font-size: 14px;
            font-weight: 600;
            display: inline-block;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        }

        body.dark-mode .date {
            background: #2a2f3f;
            color: #b0c4de;
        }

        .location-bar {
            display: flex;
            align-items: center;
            gap: 8px;
            background: #F0F8FF;
            padding: 8px 12px;
            border-radius: 30px;
            margin-bottom: 16px;
            border: 1px solid rgba(27, 90, 122, 0.2);
        }

        body.dark-mode .location-bar {
            background: #252b38;
            border: 1px solid #3a4050;
        }

        .current-location {
            flex: 1;
            display: flex;
            align-items: center;
            gap: 6px;
            color: #0B3B5C;
            font-weight: 600;
            font-size: 14px;
            overflow: hidden;
            white-space: nowrap;
            text-overflow: ellipsis;
        }

        body.dark-mode .current-location {
            color: #e0e0e0;
        }

        .location-icon {
            font-size: 18px;
            flex-shrink: 0;
        }

        .location-name {
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }

        .location-btn {
            background: linear-gradient(145deg, #1B5A7A, #0B3B5C);
            border: none;
            color: white;
            padding: 8px 14px;
            border-radius: 30px;
            font-size: 13px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            transition: all 0.2s;
            border: 1px solid rgba(255,255,255,0.2);
            flex-shrink: 0;
        }

        body.dark-mode .location-btn {
            background: linear-gradient(145deg, #3a4050, #2a2f3f);
        }

        .location-btn:active {
            transform: scale(0.96);
        }

        .search-section {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
        }

        .region-select {
            flex: 1;
            padding: 12px 14px;
            border: none;
            border-radius: 30px;
            font-size: 14px;
            font-weight: 500;
            outline: none;
            background: white;
            color: #0B3B5C;
            cursor: pointer;
            border: 1px solid #D1E0EB;
        }

        body.dark-mode .region-select {
            background: #2a2f3f;
            color: #e0e0e0;
            border: 1px solid #3a4050;
        }

        .search-btn {
            padding: 12px 20px;
            background: linear-gradient(145deg, #1B5A7A, #0B3B5C);
            color: white;
            border: none;
            border-radius: 30px;
            font-size: 14px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s;
            white-space: nowrap;
            border: 1px solid rgba(255,255,255,0.2);
        }

        body.dark-mode .search-btn {
            background: linear-gradient(145deg, #3a4050, #2a2f3f);
        }

        .search-btn:active {
            transform: scale(0.96);
        }

        .loading {
            text-align: center;
            padding: 30px 20px;
        }

        .spinner {
            width: 45px;
            height: 45px;
            border: 4px solid #E3F2FD;
            border-top: 4px solid #1B5A7A;
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
            margin: 0 auto 15px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        body.dark-mode .spinner {
            border: 4px solid #2a2f3f;
            border-top: 4px solid #5d8ad9;
        }

        .loading p {
            color: #0B3B5C;
            font-size: 15px;
        }

        body.dark-mode .loading p {
            color: #e0e0e0;
        }

        .error-message {
            background: #FFEBEE;
            color: #C62828;
            padding: 14px;
            border-radius: 20px;
            text-align: center;
            font-weight: 600;
            font-size: 14px;
            border: 1px solid #EF9A9A;
            margin-bottom: 16px;
        }

        .current-weather {
            background: linear-gradient(145deg, #F0F9FF, #E1F0FA);
            padding: 18px 16px;
            border-radius: 24px;
            margin-bottom: 18px;
            border: 1px solid rgba(255,255,255,0.7);
        }

        body.dark-mode .current-weather {
            background: linear-gradient(145deg, #252b38, #1e2330);
            border: 1px solid #3a4050;
        }

        .city-name {
            font-size: 26px;
            color: #0B3B5C;
            text-align: center;
            margin-bottom: 12px;
            font-weight: 800;
        }

        body.dark-mode .city-name {
            color: #fff;
        }

        .weather-main {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            margin-bottom: 15px;
        }

        .weather-icon {
            background: white;
            border-radius: 50%;
            padding: 8px;
            width: 80px;
            height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        body.dark-mode .weather-icon {
            background: #2a2f3f;
        }

        .weather-icon img {
            width: 70px;
            height: 70px;
        }

        .temperature {
            font-size: 48px;
            font-weight: 800;
            color: #0B3B5C;
            line-height: 1;
        }

        body.dark-mode .temperature {
            color: #fff;
        }

        .temperature small {
            font-size: 24px;
            font-weight: 500;
            color: #2C7A9C;
        }

        body.dark-mode .temperature small {
            color: #b0c4de;
        }

        .feels-like {
            font-size: 14px;
            color: #1B5A7A;
            margin-top: 4px;
            font-weight: 600;
            text-align: center;
        }

        body.dark-mode .feels-like {
            color: #b0c4de;
        }

        .weather-desc {
            text-align: center;
            font-size: 18px;
            color: #0B3B5C;
            margin: 15px 0 18px;
            font-weight: 700;
            text-transform: capitalize;
            background: rgba(255,255,255,0.7);
            padding: 10px;
            border-radius: 30px;
        }

        body.dark-mode .weather-desc {
            background: #2a2f3f;
            color: #fff;
        }

        .sun-info {
            display: flex;
            justify-content: space-around;
            background: rgba(255,255,255,0.7);
            padding: 14px 10px;
            border-radius: 40px;
            margin-bottom: 18px;
            border: 1px solid white;
        }

        body.dark-mode .sun-info {
            background: #2a2f3f;
            border: 1px solid #3a4050;
        }

        .sun-item {
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
        }

        .sun-icon {
            font-size: 22px;
        }

        .sun-label {
            font-size: 12px;
            color: #1B5A7A;
            font-weight: 600;
        }

        body.dark-mode .sun-label {
            color: #b0c4de;
        }

        .sun-time {
            font-size: 15px;
            font-weight: 800;
            color: #0B3B5C;
        }

        body.dark-mode .sun-time {
            color: #fff;
        }

        .weather-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-bottom: 18px;
        }

        .grid-item {
            background: white;
            padding: 12px 5px;
            border-radius: 20px;
            text-align: center;
            border: 1px solid rgba(27, 90, 122, 0.1);
        }

        body.dark-mode .grid-item {
            background: #252b38;
            border: 1px solid #3a4050;
        }

        .grid-icon {
            font-size: 22px;
            margin-bottom: 4px;
            display: block;
        }

        .grid-label {
            font-size: 11px;
            color: #2C7A9C;
            font-weight: 600;
            margin-bottom: 4px;
        }

        body.dark-mode .grid-label {
            color: #b0c4de;
        }

        .grid-value {
            font-size: 18px;
            font-weight: 800;
            color: #0B3B5C;
        }

        body.dark-mode .grid-value {
            color: #fff;
        }

        .grid-unit {
            font-size: 11px;
            color: #1B5A7A;
            font-weight: 500;
        }

        body.dark-mode .grid-unit {
            color: #b0c4de;
        }

        .rain-probability {
            background: linear-gradient(145deg, #E3F2FD, #BBDEFB);
            padding: 14px;
            border-radius: 22px;
            margin-bottom: 22px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid rgba(255,255,255,0.8);
        }

        body.dark-mode .rain-probability {
            background: linear-gradient(145deg, #252b38, #1e2330);
            border: 1px solid #3a4050;
        }

        .rain-left {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .rain-icon {
            font-size: 28px;
        }

        .rain-text {
            font-weight: 700;
            color: #0B3B5C;
            font-size: 16px;
        }

        body.dark-mode .rain-text {
            color: #fff;
        }

        .rain-percentage {
            font-size: 26px;
            font-weight: 800;
            color: #1B5A7A;
            background: white;
            padding: 6px 16px;
            border-radius: 30px;
        }

        body.dark-mode .rain-percentage {
            background: #2a2f3f;
            color: #8ab3ff;
        }

        .hourly-title {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 12px;
            color: white;
            font-size: 18px;
            font-weight: 700;
        }

        .hourly-scroll {
            display: flex;
            overflow-x: auto;
            gap: 10px;
            padding: 5px 0 15px;
            scrollbar-width: thin;
            -webkit-overflow-scrolling: touch;
            scroll-snap-type: x mandatory;
        }

        .hourly-scroll::-webkit-scrollbar {
            height: 3px;
        }

        .hourly-scroll::-webkit-scrollbar-track {
            background: rgba(255,255,255,0.2);
            border-radius: 10px;
        }

        .hourly-scroll::-webkit-scrollbar-thumb {
            background: #1B5A7A;
            border-radius: 10px;
        }

        body.dark-mode .hourly-scroll::-webkit-scrollbar-thumb {
            background: #5d8ad9;
        }

        .hourly-item {
            background: rgba(255,255,255,0.95);
            min-width: 80px;
            padding: 12px 6px;
            border-radius: 22px;
            text-align: center;
            border: 1px solid white;
            scroll-snap-align: start;
        }

        body.dark-mode .hourly-item {
            background: #252b38;
            border: 1px solid #3a4050;
        }

        .hourly-time {
            font-weight: 700;
            color: #0B3B5C;
            font-size: 14px;
            margin-bottom: 6px;
        }

        body.dark-mode .hourly-time {
            color: #fff;
        }

        .hourly-icon {
            width: 35px;
            height: 35px;
            margin: 0 auto 6px;
        }

        .hourly-icon img {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        .hourly-temp {
            font-weight: 800;
            color: #1B5A7A;
            font-size: 16px;
            margin-bottom: 4px;
        }

        body.dark-mode .hourly-temp {
            color: #8ab3ff;
        }

        .hourly-rain {
            font-size: 12px;
            color: #2C7A9C;
            font-weight: 600;
        }

        body.dark-mode .hourly-rain {
            color: #b0c4de;
        }

        .weekly-forecast {
            margin-top: 18px;
        }

        .weekly-title {
            color: white;
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .forecast-item {
            background: rgba(255,255,255,0.95);
            border-radius: 20px;
            padding: 12px 14px;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid white;
        }

        body.dark-mode .forecast-item {
            background: #252b38;
            border: 1px solid #3a4050;
        }

        .forecast-left {
            display: flex;
            align-items: center;
            gap: 12px;
            flex: 1;
        }

        .forecast-day {
            font-weight: 700;
            color: #0B3B5C;
            min-width: 80px;
            font-size: 14px;
        }

        body.dark-mode .forecast-day {
            color: #fff;
        }

        .forecast-icon {
            width: 35px;
            height: 35px;
        }

        .forecast-icon img {
            width: 100%;
            height: 100%;
        }

        .forecast-temp {
            font-weight: 800;
            color: #1B5A7A;
            font-size: 18px;
            min-width: 55px;
        }

        body.dark-mode .forecast-temp {
            color: #8ab3ff;
        }

        .forecast-rain {
            display: flex;
            align-items: center;
            gap: 4px;
            color: #2C7A9C;
            font-weight: 600;
            font-size: 13px;
            min-width: 50px;
        }

        body.dark-mode .forecast-rain {
            color: #b0c4de;
        }

        .hidden {
            display: none !important;
        }
    </style>
</head>
<body>
    <!-- Telegram Web App Header -->
    <div class="telegram-header">
        <button class="telegram-back-btn" onclick="window.Telegram?.WebApp?.BackButton?.show()" style="visibility: hidden;">←</button>
        <span class="telegram-title">🌤 Ob-havo</span>
        <div style="display: flex; gap: 8px;">
            <button class="theme-toggle" id="themeToggle">
                <span class="sun-icon">☀️</span>
                <span class="moon-icon" style="display: none;">🌙</span>
            </button>
            <button class="telegram-close-btn" onclick="window.Telegram?.WebApp?.close()">✕</button>
        </div>
    </div>

    <div class="container">
        <header class="header">
            <h1>O'ZBEKISTON OB-HAVO</h1>
            <p class="date" id="currentDate"></p>
        </header>

        <div class="location-bar">
            <div class="current-location">
                <span class="location-icon">📍</span>
                <span class="location-name" id="locationName">Joylashuv aniqlanmoqda...</span>
            </div>
            <button id="getLocationBtn" class="location-btn">
                <span>📍</span> Joylashuv
            </button>
        </div>

        <div class="search-section">
            <select id="regionSelect" class="region-select">
                <option value="">Viloyatni tanlang</option>
                <option value="Toshkent">Toshkent</option>
                <option value="Samarqand">Samarqand</option>
                <option value="Buxoro">Buxoro</option>
                <option value="Farg'ona">Farg'ona</option>
                <option value="Andijon">Andijon</option>
                <option value="Namangan">Namangan</option>
                <option value="Qarshi">Qarshi</option>
                <option value="Termiz">Termiz</option>
                <option value="Guliston">Guliston</option>
                <option value="Jizzax">Jizzax</option>
                <option value="Navoiy">Navoiy</option>
                <option value="Urganch">Urganch</option>
                <option value="Nukus">Nukus</option>
            </select>
            <button id="searchBtn" class="search-btn">Qidirish</button>
        </div>

        <div id="loading" class="loading hidden">
            <div class="spinner"></div>
            <p>Ma'lumotlar yuklanmoqda...</p>
        </div>

        <div id="errorMessage" class="error-message hidden"></div>

        <div id="weatherContainer" class="weather-container hidden">
            <div class="current-weather">
                <h2 class="city-name" id="cityName"></h2>
                
                <div class="weather-main">
                    <div class="weather-icon">
                        <img id="weatherIcon" src="" alt="weather">
                    </div>
                    <div>
                        <div class="temperature">
                            <span id="currentTemp"></span><small>°C</small>
                        </div>
                        <div class="feels-like" id="feelsLike"></div>
                    </div>
                </div>

                <div class="weather-desc" id="weatherDescription"></div>

                <div class="sun-info">
                    <div class="sun-item">
                        <span class="sun-icon">🌅</span>
                        <span class="sun-label">Quyosh chiqishi</span>
                        <span class="sun-time" id="sunrise"></span>
                    </div>
                    <div class="sun-item">
                        <span class="sun-icon">🌇</span>
                        <span class="sun-label">Quyosh botishi</span>
                        <span class="sun-time" id="sunset"></span>
                    </div>
                    <div class="sun-item">
                        <span class="sun-icon">⏳</span>
                        <span class="sun-label">Kun uzunligi</span>
                        <span class="sun-time" id="dayLength"></span>
                    </div>
                </div>

                <div class="weather-grid">
                    <div class="grid-item">
                        <span class="grid-icon">💧</span>
                        <span class="grid-label">Namlik</span>
                        <span class="grid-value" id="humidity"></span>
                        <span class="grid-unit">%</span>
                    </div>
                    <div class="grid-item">
                        <span class="grid-icon">💨</span>
                        <span class="grid-label">Shamol</span>
                        <span class="grid-value" id="windSpeed"></span>
                        <span class="grid-unit">m/s</span>
                    </div>
                    <div class="grid-item">
                        <span class="grid-icon">📊</span>
                        <span class="grid-label">Bosim</span>
                        <span class="grid-value" id="pressure"></span>
                        <span class="grid-unit">hPa</span>
                    </div>
                </div>

                <div class="rain-probability">
                    <div class="rain-left">
                        <span class="rain-icon">☔️</span>
                        <span class="rain-text">Yomg'ir ehtimoli</span>
                    </div>
                    <span class="rain-percentage" id="rainProbability">0%</span>
                </div>
            </div>

            <div class="hourly-title">
                <span>⏰</span>
                <span>Soatlik ob-havo</span>
            </div>
            <div class="hourly-scroll" id="hourlyForecast"></div>

            <div class="weekly-forecast">
                <div class="weekly-title">
                    <span>📅</span>
                    <span>7 kunlik prognoz</span>
                </div>
                <div id="weeklyForecast"></div>
            </div>
        </div>
    </div>

    <script>
        // Telegram Web App initialization
        const tg = window.Telegram?.WebApp;
        if (tg) {
            tg.expand(); // Expand to full screen
            tg.ready(); // Notify Telegram that app is ready
            tg.setHeaderColor('#0B3B5C'); // Set header color
            tg.setBackgroundColor('#0B3B5C'); // Set background color
            
            // Disable vertical swipes
            tg.disableVerticalSwipes?.();
        }

        // Tungi rejim funksiyasi
        const themeToggle = document.getElementById('themeToggle');
        const body = document.body;
        const sunIcon = document.querySelector('.sun-icon');
        const moonIcon = document.querySelector('.moon-icon');

        function initTheme() {
            const savedTheme = localStorage.getItem('theme');
            const hour = new Date().getHours();
            
            if (savedTheme === 'dark' || (savedTheme === null && (hour >= 19 || hour < 6))) {
                body.classList.add('dark-mode');
                sunIcon.style.display = 'none';
                moonIcon.style.display = 'inline';
                if (tg) tg.setHeaderColor('#1a1f2e');
            } else {
                body.classList.remove('dark-mode');
                sunIcon.style.display = 'inline';
                moonIcon.style.display = 'none';
                if (tg) tg.setHeaderColor('#0B3B5C');
            }
        }

        function toggleTheme() {
            if (body.classList.contains('dark-mode')) {
                body.classList.remove('dark-mode');
                localStorage.setItem('theme', 'light');
                sunIcon.style.display = 'inline';
                moonIcon.style.display = 'none';
                if (tg) tg.setHeaderColor('#0B3B5C');
            } else {
                body.classList.add('dark-mode');
                localStorage.setItem('theme', 'dark');
                sunIcon.style.display = 'none';
                moonIcon.style.display = 'inline';
                if (tg) tg.setHeaderColor('#1a1f2e');
            }
        }

        themeToggle.addEventListener('click', toggleTheme);

        // DOM elementlar
        const elements = {
            regionSelect: document.getElementById('regionSelect'),
            searchBtn: document.getElementById('searchBtn'),
            getLocationBtn: document.getElementById('getLocationBtn'),
            locationName: document.getElementById('locationName'),
            loading: document.getElementById('loading'),
            errorMessage: document.getElementById('errorMessage'),
            weatherContainer: document.getElementById('weatherContainer'),
            currentDate: document.getElementById('currentDate'),
            cityName: document.getElementById('cityName'),
            weatherIcon: document.getElementById('weatherIcon'),
            currentTemp: document.getElementById('currentTemp'),
            feelsLike: document.getElementById('feelsLike'),
            weatherDescription: document.getElementById('weatherDescription'),
            sunrise: document.getElementById('sunrise'),
            sunset: document.getElementById('sunset'),
            dayLength: document.getElementById('dayLength'),
            humidity: document.getElementById('humidity'),
            windSpeed: document.getElementById('windSpeed'),
            pressure: document.getElementById('pressure'),
            rainProbability: document.getElementById('rainProbability'),
            hourlyForecast: document.getElementById('hourlyForecast'),
            weeklyForecast: document.getElementById('weeklyForecast')
        };

        // API kalit
        const API_KEY = 'bd5e378503939ddaee76f12ad7a97608';

        // Hafta kunlari
        const weekDays = ['Yakshanba', 'Dushanba', 'Seshanba', 'Chorshanba', 'Payshanba', 'Juma', 'Shanba'];

        // Viloyatlar koordinatalari
        const regionCoordinates = {
            'Toshkent': { lat: 41.2995, lon: 69.2401 },
            'Samarqand': { lat: 39.6270, lon: 66.9750 },
            'Buxoro': { lat: 39.7747, lon: 64.4286 },
            "Farg'ona": { lat: 40.3864, lon: 71.7864 },
            'Andijon': { lat: 40.7821, lon: 72.3442 },
            'Namangan': { lat: 40.9983, lon: 71.6726 },
            'Qarshi': { lat: 38.8603, lon: 65.7895 },
            'Termiz': { lat: 37.2242, lon: 67.2783 },
            'Guliston': { lat: 40.4847, lon: 68.7833 },
            'Jizzax': { lat: 40.1158, lon: 67.8422 },
            'Navoiy': { lat: 40.1044, lon: 65.3792 },
            'Urganch': { lat: 41.5500, lon: 60.6333 },
            'Nukus': { lat: 42.4667, lon: 59.6000 }
        };

        // Sanani yangilash
        function updateDate() {
            const now = new Date();
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            elements.currentDate.textContent = now.toLocaleDateString('uz-UZ', options);
        }
        updateDate();

        // Vaqtni formatlash
        function formatTime(timestamp) {
            const date = new Date(timestamp * 1000);
            return date.toLocaleTimeString('uz-UZ', { hour: '2-digit', minute: '2-digit' });
        }

        // Kun uzunligini hisoblash
        function calculateDayLength(sunrise, sunset) {
            const diff = sunset - sunrise;
            const hours = Math.floor(diff / 3600);
            const minutes = Math.floor((diff % 3600) / 60);
            return `${hours}:${minutes.toString().padStart(2, '0')}`;
        }

        // Ob-havo ma'lumotlarini olish
        async function getWeatherData(lat, lon, location) {
            try {
                setLoading(true);
                
                const [currentRes, forecastRes] = await Promise.all([
                    fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric&lang=uz`),
                    fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric&lang=uz`)
                ]);

                if (!currentRes.ok || !forecastRes.ok) throw new Error('API xatolik');

                const current = await currentRes.json();
                const forecast = await forecastRes.json();

                displayWeatherData(current, forecast, location);
            } catch (error) {
                showError('Ma\'lumotlarni yuklashda xatolik');
                console.error(error);
            } finally {
                setLoading(false);
            }
        }

        // Ma'lumotlarni ko'rsatish
        function displayWeatherData(current, forecast, location) {
            elements.cityName.textContent = location;
            elements.weatherIcon.src = `https://openweathermap.org/img/wn/${current.weather[0].icon}@2x.png`;
            elements.currentTemp.textContent = Math.round(current.main.temp);
            elements.feelsLike.textContent = `His qilinadi: ${Math.round(current.main.feels_like)}°C`;
            elements.weatherDescription.textContent = current.weather[0].description;
            
            const sunrise = current.sys.sunrise;
            const sunset = current.sys.sunset;
            elements.sunrise.textContent = formatTime(sunrise);
            elements.sunset.textContent = formatTime(sunset);
            elements.dayLength.textContent = calculateDayLength(sunrise, sunset);
            
            elements.humidity.textContent = current.main.humidity;
            elements.windSpeed.textContent = current.wind.speed.toFixed(1);
            elements.pressure.textContent = current.main.pressure;

            const rain = current.rain ? current.rain['1h'] || current.rain['3h'] || 0 : 0;
            const rainProb = rain > 0 ? Math.min(Math.round(rain * 20), 100) : 0;
            elements.rainProbability.textContent = `${rainProb}%`;

            // Soatlik prognoz
            elements.hourlyForecast.innerHTML = '';
            forecast.list.slice(0, 8).forEach(item => {
                const time = new Date(item.dt * 1000);
                const hour = time.getHours().toString().padStart(2, '0') + ':00';
                const temp = Math.round(item.main.temp);
                const icon = item.weather[0].icon;
                const rainChance = item.pop ? Math.round(item.pop * 100) : 0;

                const hourlyItem = document.createElement('div');
                hourlyItem.className = 'hourly-item';
                hourlyItem.innerHTML = `
                    <div class="hourly-time">${hour}</div>
                    <div class="hourly-icon">
                        <img src="https://openweathermap.org/img/wn/${icon}.png" alt="icon">
                    </div>
                    <div class="hourly-temp">${temp}°C</div>
                    <div class="hourly-rain">☔️ ${rainChance}%</div>
                `;
                elements.hourlyForecast.appendChild(hourlyItem);
            });

            // Haftalik prognoz
            elements.weeklyForecast.innerHTML = '';
            const daily = {};
            forecast.list.forEach(item => {
                const date = new Date(item.dt * 1000).toDateString();
                if (!daily[date] || new Date(item.dt * 1000).getHours() === 12) {
                    daily[date] = item;
                }
            });

            Object.values(daily).slice(0, 7).forEach((day, index) => {
                const date = new Date(day.dt * 1000);
                const dayName = index === 0 ? 'Bugun' : index === 1 ? 'Ertaga' : weekDays[date.getDay()];
                const temp = Math.round(day.main.temp);
                const icon = day.weather[0].icon;
                const rainChance = day.pop ? Math.round(day.pop * 100) : 0;

                const forecastItem = document.createElement('div');
                forecastItem.className = 'forecast-item';
                forecastItem.innerHTML = `
                    <div class="forecast-left">
                        <span class="forecast-day">${dayName}</span>
                        <div class="forecast-icon">
                            <img src="https://openweathermap.org/img/wn/${icon}.png" alt="icon">
                        </div>
                        <span class="forecast-temp">${temp}°C</span>
                    </div>
                    <div class="forecast-rain">
                        <span>☔️</span>
                        <span>${rainChance}%</span>
                    </div>
                `;
                elements.weeklyForecast.appendChild(forecastItem);
            });

            elements.weatherContainer.classList.remove('hidden');
        }

        // Joylashuvni olish
        function getCurrentLocation() {
            if (!navigator.geolocation) {
                showError('Brauzer joylashuvni qo\'llab-quvvatlamaydi');
                return;
            }

            setLoading(true);
            elements.locationName.textContent = 'Joylashuv aniqlanmoqda...';

            navigator.geolocation.getCurrentPosition(
                async (position) => {
                    const { latitude, longitude } = position.coords;
                    
                    try {
                        const res = await fetch(
                            `https://api.openweathermap.org/geo/1.0/reverse?lat=${latitude}&lon=${longitude}&limit=1&appid=${API_KEY}`
                        );
                        const data = await res.json();
                        
                        let city = data[0]?.name || 'Sizning joylashuvingiz';
                        elements.locationName.textContent = city;
                        await getWeatherData(latitude, longitude, city);
                    } catch {
                        elements.locationName.textContent = 'Joylashuv topildi';
                        await getWeatherData(latitude, longitude, 'Sizning joylashuvingiz');
                    }
                },
                (error) => {
                    setLoading(false);
                    let msg = 'Joylashuv aniqlanmadi';
                    if (error.code === 1) msg = 'Iltimos, joylashuvga ruxsat bering';
                    showError(msg);
                    elements.locationName.textContent = 'Ruxsat berilmagan';
                },
                { enableHighAccuracy: true, timeout: 10000 }
            );
        }

        // Viloyat bo'yicha qidirish
        async function searchWeather() {
            const region = elements.regionSelect.value;
            if (!region) {
                showError('Viloyatni tanlang');
                return;
            }
            
            const coords = regionCoordinates[region];
            if (coords) {
                elements.locationName.textContent = region;
                await getWeatherData(coords.lat, coords.lon, region);
            }
        }

        function setLoading(isLoading) {
            if (isLoading) {
                elements.loading.classList.remove('hidden');
                elements.weatherContainer.classList.add('hidden');
                elements.errorMessage.classList.add('hidden');
            } else {
                elements.loading.classList.add('hidden');
            }
        }

        function showError(message) {
            elements.errorMessage.textContent = message;
            elements.errorMessage.classList.remove('hidden');
            setTimeout(() => elements.errorMessage.classList.add('hidden'), 5000);
        }

        // Event listeners
        elements.searchBtn.addEventListener('click', searchWeather);
        elements.getLocationBtn.addEventListener('click', getCurrentLocation);
        elements.regionSelect.addEventListener('change', searchWeather);

        // Enter tugmasi
        elements.regionSelect.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') searchWeather();
        });

        // Tungi rejimni ishga tushirish
        initTheme();

        // Sahifa yuklanganda
        window.addEventListener('load', () => {
            setTimeout(getCurrentLocation, 500);
            
            // Fallback
            setTimeout(() => {
                if (elements.weatherContainer.classList.contains('hidden') && 
                    !elements.loading.classList.contains('hidden') === false) {
                    elements.regionSelect.value = 'Toshkent';
                    searchWeather();
                }
            }, 8000);
        });

        // Telegram back button handling
        if (tg && tg.BackButton) {
            tg.BackButton.onClick(() => {
                tg.close();
            });
        }
    </script>
</body>
</html>
