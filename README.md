<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" content="#1a4d8c">
    <title>Ob-havo | O'zbekiston</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        :root {
            --bg-primary: #1a4d8c;
            --bg-gradient: linear-gradient(145deg, #1a4d8c 0%, #0f2f5c 100%);
            --text-primary: #1e293b;
            --text-secondary: #475569;
            --accent: #3b82f6;
            --accent-dark: #2563eb;
            --card-bg: rgba(255, 255, 255, 0.95);
            --border-light: rgba(255, 255, 255, 0.2);
            --shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
        }

        body.dark-mode {
            --bg-gradient: linear-gradient(145deg, #0f1a2b 0%, #050a12 100%);
            --text-primary: #f1f5f9;
            --text-secondary: #94a3b8;
            --card-bg: rgba(30, 38, 50, 0.98);
            --border-light: rgba(255, 255, 255, 0.1);
        }

        html, body {
            width: 100%;
            min-height: 100vh;
            background: var(--bg-gradient);
            display: flex;
            justify-content: center;
            align-items: flex-start;
            transition: background 0.3s ease;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        /* Telegram Web App height fix */
        body {
            height: 100vh;
            height: -webkit-fill-available;
            overflow-y: auto;
            overflow-x: hidden;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
        }

        .app-container {
            width: 100%;
            max-width: 480px;
            margin: 0 auto;
            padding: 12px 16px;
            height: 100%;
            overflow-y: auto;
            overflow-x: hidden;
            display: flex;
            flex-direction: column;
            -webkit-overflow-scrolling: touch;
            scroll-behavior: smooth;
        }

        /* Header */
        .app-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 16px;
            padding: 4px 0;
            flex-shrink: 0;
        }

        .header-title {
            font-size: 20px;
            font-weight: 700;
            color: white;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
            letter-spacing: 0.3px;
            text-align: center;
        }

        /* Icon Buttons */
        .icon-btn {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.15);
            border: 1px solid var(--border-light);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            color: white;
            cursor: pointer;
            transition: all 0.2s ease;
            flex-shrink: 0;
            padding: 0;
            -webkit-touch-callout: none;
        }

        .icon-btn:active {
            transform: scale(0.92);
            background: rgba(255, 255, 255, 0.25);
        }

        /* Location Card */
        .location-card {
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border-radius: 28px;
            padding: 12px 18px;
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow);
            flex-shrink: 0;
        }

        .location-info {
            display: flex;
            align-items: center;
            gap: 12px;
            flex: 1;
            min-width: 0;
        }

        .location-badge {
            width: 40px;
            height: 40px;
            border-radius: 24px;
            background: linear-gradient(145deg, var(--accent), var(--accent-dark));
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 20px;
            flex-shrink: 0;
        }

        .location-details {
            display: flex;
            flex-direction: column;
            min-width: 0;
            flex: 1;
        }

        .location-label {
            font-size: 11px;
            color: var(--text-secondary);
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.3px;
        }

        .location-value {
            font-size: 15px;
            font-weight: 700;
            color: var(--text-primary);
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }

        .refresh-btn {
            background: rgba(255, 255, 255, 0.2);
            border: 1px solid var(--border-light);
            padding: 8px 14px;
            border-radius: 24px;
            color: white;
            font-weight: 600;
            font-size: 13px;
            display: flex;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            transition: all 0.2s;
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            flex-shrink: 0;
            white-space: nowrap;
        }

        .refresh-btn:active {
            transform: translateY(1px);
            background: rgba(255, 255, 255, 0.3);
        }

        /* Search Section */
        .search-section {
            display: flex;
            gap: 10px;
            margin-bottom: 16px;
            flex-shrink: 0;
        }

        .select-wrapper {
            flex: 1;
            position: relative;
            min-width: 0;
        }

        .select-wrapper select {
            width: 100%;
            padding: 14px 18px;
            border-radius: 30px;
            border: none;
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            color: var(--text-primary);
            font-size: 14px;
            font-weight: 500;
            appearance: none;
            cursor: pointer;
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow);
            transition: all 0.2s;
        }

        .select-wrapper::after {
            content: '▼';
            font-size: 11px;
            color: var(--accent);
            position: absolute;
            right: 16px;
            top: 50%;
            transform: translateY(-50%);
            pointer-events: none;
        }

        .search-btn {
            padding: 0 20px;
            background: linear-gradient(145deg, var(--accent), var(--accent-dark));
            border: none;
            border-radius: 30px;
            color: white;
            font-weight: 700;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.2s;
            box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.3);
            white-space: nowrap;
            flex-shrink: 0;
        }

        .search-btn:active {
            transform: translateY(1px);
            box-shadow: 0 2px 8px rgba(37, 99, 235, 0.4);
        }

        /* Weather Card */
        .weather-card {
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border-radius: 28px;
            padding: 20px 16px;
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow);
            margin-bottom: 16px;
            flex-shrink: 0;
        }

        .city-header {
            text-align: center;
            margin-bottom: 16px;
        }

        .city-name {
            font-size: 24px;
            font-weight: 800;
            color: var(--text-primary);
            margin-bottom: 2px;
            line-height: 1.2;
        }

        .current-date {
            font-size: 13px;
            color: var(--text-secondary);
            font-weight: 500;
        }

        /* Weather Visual */
        .weather-visual {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 16px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50px;
            padding: 12px 20px;
            border: 1px solid var(--border-light);
        }

        .weather-icon-large {
            width: 70px;
            height: 70px;
            filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.2));
        }

        .temp-large {
            font-size: 48px;
            font-weight: 800;
            color: var(--text-primary);
            line-height: 1;
        }

        .temp-large small {
            font-size: 24px;
            font-weight: 500;
            color: var(--text-secondary);
        }

        .weather-desc {
            text-align: center;
            font-size: 18px;
            font-weight: 600;
            color: var(--text-primary);
            text-transform: capitalize;
            margin-bottom: 16px;
            padding: 6px 0;
            border-bottom: 1px solid var(--border-light);
        }

        /* Sun Grid */
        .sun-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            padding: 12px;
            margin-bottom: 16px;
            border: 1px solid var(--border-light);
        }

        .sun-item {
            text-align: center;
            display: flex;
            flex-direction: column;
            gap: 2px;
        }

        .sun-emoji {
            font-size: 22px;
        }

        .sun-label {
            font-size: 10px;
            color: var(--text-secondary);
            font-weight: 600;
            text-transform: uppercase;
        }

        .sun-value {
            font-size: 14px;
            font-weight: 700;
            color: var(--text-primary);
        }

        /* Stats Grid */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin-bottom: 16px;
        }

        .stat-item {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 18px;
            padding: 12px 6px;
            text-align: center;
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid var(--border-light);
        }

        .stat-emoji {
            font-size: 22px;
            margin-bottom: 4px;
            display: block;
        }

        .stat-label {
            font-size: 10px;
            color: var(--text-secondary);
            font-weight: 600;
            margin-bottom: 2px;
            text-transform: uppercase;
        }

        .stat-value {
            font-size: 16px;
            font-weight: 800;
            color: var(--text-primary);
        }

        .stat-unit {
            font-size: 10px;
            color: var(--text-secondary);
            font-weight: 500;
        }

        /* Rain Card */
        .rain-card {
            background: linear-gradient(145deg, var(--accent), var(--accent-dark));
            border-radius: 20px;
            padding: 14px 18px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid rgba(255, 255, 255, 0.3);
            box-shadow: 0 4px 15px rgba(37, 99, 235, 0.3);
        }

        .rain-left {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .rain-emoji {
            font-size: 28px;
        }

        .rain-text {
            font-weight: 700;
            color: white;
            font-size: 15px;
        }

        .rain-percent {
            font-size: 24px;
            font-weight: 800;
            color: white;
            background: rgba(255, 255, 255, 0.2);
            padding: 4px 14px;
            border-radius: 30px;
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }

        /* Section Titles */
        .section-title {
            display: flex;
            align-items: center;
            gap: 8px;
            color: white;
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 12px;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
            flex-shrink: 0;
        }

        .section-title span:first-child {
            font-size: 22px;
        }

        /* Hourly Scroll */
        .hourly-scroll {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding: 4px 0 16px;
            scrollbar-width: thin;
            -webkit-overflow-scrolling: touch;
            scroll-snap-type: x mandatory;
            margin-bottom: 16px;
            flex-shrink: 0;
        }

        .hourly-scroll::-webkit-scrollbar {
            height: 3px;
        }

        .hourly-scroll::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
        }

        .hourly-scroll::-webkit-scrollbar-thumb {
            background: var(--accent);
            border-radius: 10px;
        }

        .hourly-item {
            min-width: 70px;
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border-radius: 18px;
            padding: 12px 6px;
            text-align: center;
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow);
            scroll-snap-align: start;
        }

        .hourly-time {
            font-weight: 700;
            color: var(--text-primary);
            font-size: 13px;
            margin-bottom: 4px;
        }

        .hourly-icon {
            width: 36px;
            height: 36px;
            margin: 0 auto 4px;
        }

        .hourly-icon img {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        .hourly-temp {
            font-weight: 800;
            color: var(--accent);
            font-size: 15px;
            margin-bottom: 2px;
        }

        .hourly-rain {
            font-size: 10px;
            color: var(--text-secondary);
            font-weight: 600;
        }

        /* Weekly List */
        .weekly-list {
            display: flex;
            flex-direction: column;
            gap: 8px;
            padding-bottom: 20px;
            flex-shrink: 0;
        }

        .weekly-item {
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 12px 16px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow);
        }

        .weekly-item:active {
            transform: scale(0.99);
            background: rgba(255, 255, 255, 0.2);
        }

        .weekly-left {
            display: flex;
            align-items: center;
            gap: 12px;
            flex: 1;
            min-width: 0;
        }

        .weekly-day {
            font-weight: 700;
            color: var(--text-primary);
            min-width: 65px;
            font-size: 14px;
        }

        .weekly-icon {
            width: 30px;
            height: 30px;
            flex-shrink: 0;
        }

        .weekly-icon img {
            width: 100%;
            height: 100%;
        }

        .weekly-temp {
            font-weight: 800;
            color: var(--accent);
            font-size: 15px;
            min-width: 45px;
        }

        .weekly-rain {
            display: flex;
            align-items: center;
            gap: 3px;
            color: var(--text-secondary);
            font-weight: 600;
            font-size: 12px;
            white-space: nowrap;
        }

        /* Loading */
        .loading-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 40px 20px;
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border-radius: 28px;
            border: 1px solid var(--border-light);
            flex: 1;
            min-height: 200px;
        }

        .spinner {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border: 3px solid rgba(255, 255, 255, 0.1);
            border-top-color: var(--accent);
            animation: spin 0.8s linear infinite;
            margin-bottom: 16px;
        }

        .loading-text {
            color: white;
            font-size: 15px;
            font-weight: 500;
        }

        /* Error */
        .error-message {
            background: rgba(239, 68, 68, 0.2);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(239, 68, 68, 0.3);
            color: white;
            padding: 14px 18px;
            border-radius: 20px;
            text-align: center;
            font-weight: 600;
            font-size: 14px;
            margin-bottom: 16px;
            flex-shrink: 0;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .hidden {
            display: none !important;
        }

        /* Mobile optimizations */
        @media (max-width: 360px) {
            .app-container {
                padding: 8px 12px;
            }
            
            .city-name {
                font-size: 22px;
            }
            
            .temp-large {
                font-size: 42px;
            }
            
            .weekly-day {
                min-width: 60px;
                font-size: 13px;
            }
        }

        /* iPhone safe area */
        @supports (padding: max(0px)) {
            .app-container {
                padding-left: max(16px, env(safe-area-inset-left));
                padding-right: max(16px, env(safe-area-inset-right));
                padding-top: max(12px, env(safe-area-inset-top));
                padding-bottom: max(12px, env(safe-area-inset-bottom));
            }
        }
    </style>
</head>
<body>
    <div class="app-container" id="appContainer">
        <!-- Header -->
        <div class="app-header">
            <div class="header-left">
                <button class="icon-btn" style="visibility: hidden;">☰</button>
            </div>
            <span class="header-title">O'zbekiston Ob-havo</span>
            <div class="header-right">
                <button class="icon-btn" id="themeToggle">
                    <span class="sun-icon">☀️</span>
                    <span class="moon-icon" style="display: none;">🌙</span>
                </button>
                <button class="icon-btn" id="closeBtn">✕</button>
            </div>
        </div>

        <!-- Location Card -->
        <div class="location-card">
            <div class="location-info">
                <div class="location-badge">📍</div>
                <div class="location-details">
                    <span class="location-label">JOYLASHUV</span>
                    <span class="location-value" id="locationName">Aniqlanmoqda...</span>
                </div>
            </div>
            <button class="refresh-btn" id="getLocationBtn">
                <span>🔄</span> Yangilash
            </button>
        </div>

        <!-- Search Section -->
        <div class="search-section">
            <div class="select-wrapper">
                <select id="regionSelect">
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
            </div>
            <button class="search-btn" id="searchBtn">Qidirish</button>
        </div>

        <!-- Loading -->
        <div id="loading" class="loading-container hidden">
            <div class="spinner"></div>
            <div class="loading-text">Ma'lumotlar yuklanmoqda...</div>
        </div>

        <!-- Error -->
        <div id="errorMessage" class="error-message hidden"></div>

        <!-- Weather Data -->
        <div id="weatherContainer" class="hidden">
            <!-- Main Weather Card -->
            <div class="weather-card">
                <div class="city-header">
                    <h2 class="city-name" id="cityName">Toshkent</h2>
                    <div class="current-date" id="currentDate"></div>
                </div>

                <div class="weather-visual">
                    <img class="weather-icon-large" id="weatherIcon" src="" alt="weather">
                    <div class="temp-large">
                        <span id="currentTemp">--</span><small>°C</small>
                    </div>
                </div>

                <div class="weather-desc" id="weatherDescription">--</div>

                <!-- Sun Info -->
                <div class="sun-grid">
                    <div class="sun-item">
                        <span class="sun-emoji">🌅</span>
                        <span class="sun-label">Quyosh chiqishi</span>
                        <span class="sun-value" id="sunrise">--:--</span>
                    </div>
                    <div class="sun-item">
                        <span class="sun-emoji">🌇</span>
                        <span class="sun-label">Quyosh botishi</span>
                        <span class="sun-value" id="sunset">--:--</span>
                    </div>
                    <div class="sun-item">
                        <span class="sun-emoji">⏳</span>
                        <span class="sun-label">Kun uzunligi</span>
                        <span class="sun-value" id="dayLength">--:--</span>
                    </div>
                </div>

                <!-- Stats Grid -->
                <div class="stats-grid">
                    <div class="stat-item">
                        <span class="stat-emoji">💧</span>
                        <span class="stat-label">Namlik</span>
                        <span class="stat-value" id="humidity">--</span>
                        <span class="stat-unit">%</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-emoji">💨</span>
                        <span class="stat-label">Shamol</span>
                        <span class="stat-value" id="windSpeed">--</span>
                        <span class="stat-unit">m/s</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-emoji">📊</span>
                        <span class="stat-label">Bosim</span>
                        <span class="stat-value" id="pressure">--</span>
                        <span class="stat-unit">hPa</span>
                    </div>
                </div>

                <!-- Rain Card -->
                <div class="rain-card">
                    <div class="rain-left">
                        <span class="rain-emoji">☔️</span>
                        <span class="rain-text">Yomg'ir ehtimoli</span>
                    </div>
                    <span class="rain-percent" id="rainProbability">0%</span>
                </div>
            </div>

            <!-- Hourly Forecast -->
            <div class="section-title">
                <span>⏰</span>
                <span>Soatlik prognoz</span>
            </div>
            <div class="hourly-scroll" id="hourlyForecast"></div>

            <!-- Weekly Forecast -->
            <div class="section-title">
                <span>📅</span>
                <span>7 kunlik prognoz</span>
            </div>
            <div class="weekly-list" id="weeklyForecast"></div>
        </div>
    </div>

    <script>
        // Telegram Web App
        const tg = window.Telegram?.WebApp;
        if (tg) {
            tg.expand(); // Expand to full height
            tg.ready();
            tg.setHeaderColor('#1a4d8c');
            tg.setBackgroundColor('#1a4d8c');
            tg.disableVerticalSwipes?.();
            
            // Set viewport height
            const setViewportHeight = () => {
                const vh = window.innerHeight * 0.01;
                document.documentElement.style.setProperty('--vh', `${vh}px`);
            };
            
            window.addEventListener('resize', setViewportHeight);
            setViewportHeight();
        }

        // DOM Elements
        const elements = {
            regionSelect: document.getElementById('regionSelect'),
            searchBtn: document.getElementById('searchBtn'),
            getLocationBtn: document.getElementById('getLocationBtn'),
            closeBtn: document.getElementById('closeBtn'),
            locationName: document.getElementById('locationName'),
            loading: document.getElementById('loading'),
            errorMessage: document.getElementById('errorMessage'),
            weatherContainer: document.getElementById('weatherContainer'),
            currentDate: document.getElementById('currentDate'),
            cityName: document.getElementById('cityName'),
            weatherIcon: document.getElementById('weatherIcon'),
            currentTemp: document.getElementById('currentTemp'),
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

        // API Key
        const API_KEY = 'bd5e378503939ddaee76f12ad7a97608';

        // Week Days
        const weekDays = ['Yakshanba', 'Dushanba', 'Seshanba', 'Chorshanba', 'Payshanba', 'Juma', 'Shanba'];

        // Region Coordinates
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

        // Theme Toggle
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
                if (tg) tg.setHeaderColor('#0f1a2b');
            }
        }

        function toggleTheme() {
            if (body.classList.contains('dark-mode')) {
                body.classList.remove('dark-mode');
                localStorage.setItem('theme', 'light');
                sunIcon.style.display = 'inline';
                moonIcon.style.display = 'none';
                if (tg) tg.setHeaderColor('#1a4d8c');
            } else {
                body.classList.add('dark-mode');
                localStorage.setItem('theme', 'dark');
                sunIcon.style.display = 'none';
                moonIcon.style.display = 'inline';
                if (tg) tg.setHeaderColor('#0f1a2b');
            }
        }

        themeToggle.addEventListener('click', toggleTheme);

        // Close button
        if (elements.closeBtn) {
            elements.closeBtn.addEventListener('click', () => {
                if (tg) {
                    tg.close();
                }
            });
        }

        // Update Date
        function updateDate() {
            const now = new Date();
            elements.currentDate.textContent = now.toLocaleDateString('uz-UZ', { 
                year: 'numeric', month: 'long', day: 'numeric' 
            });
        }
        updateDate();

        // Format Time
        function formatTime(timestamp) {
            const date = new Date(timestamp * 1000);
            return date.toLocaleTimeString('uz-UZ', { hour: '2-digit', minute: '2-digit' });
        }

        // Calculate Day Length
        function calculateDayLength(sunrise, sunset) {
            const diff = sunset - sunrise;
            const hours = Math.floor(diff / 3600);
            const minutes = Math.floor((diff % 3600) / 60);
            return `${hours}:${minutes.toString().padStart(2, '0')}`;
        }

        // Get Weather Data
        async function getWeatherData(lat, lon, location) {
            try {
                setLoading(true);
                
                const [currentRes, forecastRes] = await Promise.all([
                    fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric&lang=uz`),
                    fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric&lang=uz`)
                ]);

                if (!currentRes.ok || !forecastRes.ok) throw new Error();

                const current = await currentRes.json();
                const forecast = await forecastRes.json();

                displayWeatherData(current, forecast, location);
            } catch (error) {
                showError('Ma\'lumotlarni yuklashda xatolik yuz berdi');
                console.error(error);
            } finally {
                setLoading(false);
            }
        }

        // Display Weather Data
        function displayWeatherData(current, forecast, location) {
            // Current Weather
            elements.cityName.textContent = location;
            elements.weatherIcon.src = `https://openweathermap.org/img/wn/${current.weather[0].icon}@4x.png`;
            elements.currentTemp.textContent = Math.round(current.main.temp);
            elements.weatherDescription.textContent = current.weather[0].description;
            
            // Sun Times
            elements.sunrise.textContent = formatTime(current.sys.sunrise);
            elements.sunset.textContent = formatTime(current.sys.sunset);
            elements.dayLength.textContent = calculateDayLength(current.sys.sunrise, current.sys.sunset);
            
            // Stats
            elements.humidity.textContent = current.main.humidity;
            elements.windSpeed.textContent = current.wind.speed.toFixed(1);
            elements.pressure.textContent = current.main.pressure;

            // Rain Probability
            const rain = current.rain ? current.rain['1h'] || current.rain['3h'] || 0 : 0;
            const rainProb = rain > 0 ? Math.min(Math.round(rain * 20), 100) : Math.round((current.clouds?.all || 0) * 0.3);
            elements.rainProbability.textContent = `${rainProb}%`;

            // Hourly Forecast
            elements.hourlyForecast.innerHTML = '';
            forecast.list.slice(0, 8).forEach(item => {
                const hour = new Date(item.dt * 1000).getHours().toString().padStart(2, '0') + ':00';
                const rainChance = item.pop ? Math.round(item.pop * 100) : 0;
                
                const hourlyItem = document.createElement('div');
                hourlyItem.className = 'hourly-item';
                hourlyItem.innerHTML = `
                    <div class="hourly-time">${hour}</div>
                    <div class="hourly-icon">
                        <img src="https://openweathermap.org/img/wn/${item.weather[0].icon}.png" alt="icon" loading="lazy">
                    </div>
                    <div class="hourly-temp">${Math.round(item.main.temp)}°C</div>
                    <div class="hourly-rain">☔️ ${rainChance}%</div>
                `;
                elements.hourlyForecast.appendChild(hourlyItem);
            });

            // Weekly Forecast
            elements.weeklyForecast.innerHTML = '';
            const daily = {};
            forecast.list.forEach(item => {
                const date = new Date(item.dt * 1000).toDateString();
                if (!daily[date]) {
                    daily[date] = item;
                }
            });

            Object.values(daily).slice(0, 7).forEach((day, index) => {
                const date = new Date(day.dt * 1000);
                const dayName = index === 0 ? 'Bugun' : index === 1 ? 'Ertaga' : weekDays[date.getDay()];
                const rainChance = day.pop ? Math.round(day.pop * 100) : 0;
                
                const weeklyItem = document.createElement('div');
                weeklyItem.className = 'weekly-item';
                weeklyItem.innerHTML = `
                    <div class="weekly-left">
                        <span class="weekly-day">${dayName}</span>
                        <div class="weekly-icon">
                            <img src="https://openweathermap.org/img/wn/${day.weather[0].icon}.png" alt="icon" loading="lazy">
                        </div>
                        <span class="weekly-temp">${Math.round(day.main.temp)}°C</span>
                    </div>
                    <div class="weekly-rain">
                        <span>☔️</span>
                        <span>${rainChance}%</span>
                    </div>
                `;
                elements.weeklyForecast.appendChild(weeklyItem);
            });

            elements.weatherContainer.classList.remove('hidden');
        }

        // Get Current Location
        function getCurrentLocation() {
            if (!navigator.geolocation) {
                showError('Brauzeringiz joylashuvni qo\'llab-quvvatlamaydi');
                return;
            }

            setLoading(true);
            elements.locationName.textContent = 'Aniqlanmoqda...';

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
                    let message = 'Joylashuv aniqlanmadi';
                    if (error.code === 1) message = 'Iltimos, joylashuvga ruxsat bering';
                    else if (error.code === 2) message = 'Joylashuv mavjud emas';
                    else if (error.code === 3) message = 'So\'rov vaqti tugadi';
                    
                    showError(message);
                    elements.locationName.textContent = 'Ruxsat berilmagan';
                    
                    // Fallback to Tashkent
                    setTimeout(() => {
                        elements.regionSelect.value = 'Toshkent';
                        searchWeather();
                    }, 1000);
                },
                {
                    enableHighAccuracy: true,
                    timeout: 10000,
                    maximumAge: 0
                }
            );
        }

        // Search by Region
        async function searchWeather() {
            const region = elements.regionSelect.value;
            if (!region) {
                showError('Iltimos, viloyatni tanlang');
                return;
            }
            
            const coords = regionCoordinates[region];
            if (coords) {
                elements.locationName.textContent = region;
                await getWeatherData(coords.lat, coords.lon, region);
            }
        }

        // Loading State
        function setLoading(isLoading) {
            if (isLoading) {
                elements.loading.classList.remove('hidden');
                elements.weatherContainer.classList.add('hidden');
                elements.errorMessage.classList.add('hidden');
            } else {
                elements.loading.classList.add('hidden');
            }
        }

        // Show Error
        function showError(message) {
            elements.errorMessage.textContent = message;
            elements.errorMessage.classList.remove('hidden');
            setTimeout(() => {
                elements.errorMessage.classList.add('hidden');
            }, 4000);
        }

        // Event Listeners
        elements.searchBtn.addEventListener('click', searchWeather);
        elements.getLocationBtn.addEventListener('click', getCurrentLocation);
        
        // Enter key on select
        elements.regionSelect.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') searchWeather();
        });

        // Touch optimization
        document.addEventListener('touchstart', () => {}, { passive: true });

        // Initialize
        initTheme();
        updateDate();

        // Auto-load on start
        window.addEventListener('load', () => {
            setTimeout(getCurrentLocation, 500);
        });

        // Handle orientation change
        window.addEventListener('orientationchange', () => {
            setTimeout(() => {
                if (tg) tg.expand();
            }, 100);
        });
    </script>
</body>
</html>
