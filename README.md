<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <!-- To'liq moslashuvchanlik uchun meta teglar -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover, shrink-to-fit=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" content="#0B3B5C">
    <title>O'zbekiston Ob-havo | Barcha qurilmalar uchun</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        /* CSS Variables - oson moslashuv uchun */
        :root {
            --primary-dark: #0B3B5C;
            --primary: #1B5A7A;
            --primary-light: #2C7A9C;
            --bg-gradient: linear-gradient(145deg, #0B3B5C 0%, #1B5A7A 100%);
            --text-light: #ffffff;
            --text-dark: #0B3B5C;
            --card-bg: rgba(255, 255, 255, 0.98);
            --border-radius-sm: 20px;
            --border-radius-md: 25px;
            --border-radius-lg: 30px;
            --spacing-xs: 4px;
            --spacing-sm: 8px;
            --spacing-md: 12px;
            --spacing-lg: 16px;
            --spacing-xl: 20px;
        }

        /* Tungi rejim variables */
        body.dark-mode {
            --primary-dark: #0a0f1c;
            --primary: #1a1f2e;
            --primary-light: #2a2f3f;
            --bg-gradient: linear-gradient(145deg, #0a0f1c 0%, #1a1f2e 100%);
            --text-light: #ffffff;
            --text-dark: #ffffff;
            --card-bg: rgba(20, 25, 35, 0.98);
        }

        html, body {
            width: 100%;
            min-height: 100vh;
            min-height: -webkit-fill-available;
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background: var(--bg-gradient);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            padding: 0;
            margin: 0;
            position: relative;
        }

        /* Universal container - barcha ekranlar uchun */
        .container {
            width: 100%;
            max-width: 1200px; /* Katta ekranlar uchun */
            margin: 0 auto;
            padding: var(--spacing-lg);
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        /* Asosiy karta */
        .weather-card {
            width: 100%;
            max-width: 500px; /* Telefonlar uchun optimal */
            background: var(--card-bg);
            border-radius: var(--border-radius-lg);
            padding: clamp(16px, 4vw, 24px); /* Responsive padding */
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: all 0.3s ease;
        }

        /* Katta ekranlar uchun */
        @media (min-width: 768px) {
            .weather-card {
                max-width: 600px;
                padding: 28px;
                margin: 20px auto;
            }
        }

        /* Juda katta ekranlar */
        @media (min-width: 1024px) {
            .weather-card {
                max-width: 650px;
                padding: 32px;
            }
        }

        /* Telegram Header */
        .telegram-header {
            width: 100%;
            max-width: 500px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 12px 0;
            margin-bottom: 8px;
        }

        @media (min-width: 768px) {
            .telegram-header {
                max-width: 600px;
            }
        }

        .header-btn {
            background: rgba(255, 255, 255, 0.15);
            border: none;
            width: clamp(36px, 8vw, 44px);
            height: clamp(36px, 8vw, 44px);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: clamp(18px, 4vw, 22px);
            color: white;
            cursor: pointer;
            backdrop-filter: blur(5px);
            transition: all 0.2s;
            -webkit-tap-highlight-color: transparent;
        }

        .header-btn:active {
            transform: scale(0.92);
            background: rgba(255, 255, 255, 0.25);
        }

        .telegram-title {
            color: white;
            font-size: clamp(16px, 4vw, 20px);
            font-weight: 600;
        }

        .theme-toggle {
            background: rgba(255, 255, 255, 0.15);
            border: none;
            width: clamp(36px, 8vw, 44px);
            height: clamp(36px, 8vw, 44px);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: clamp(18px, 4vw, 22px);
            color: white;
            cursor: pointer;
        }

        /* Header */
        .header {
            text-align: center;
            margin-bottom: clamp(12px, 3vw, 20px);
        }

        .header h1 {
            font-size: clamp(20px, 5vw, 28px);
            background: linear-gradient(135deg, #fff, #e0e0e0);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: clamp(4px, 1vw, 8px);
            font-weight: 700;
            letter-spacing: -0.5px;
        }

        .date {
            background: rgba(255, 255, 255, 0.2);
            color: white;
            padding: clamp(6px, 1.5vw, 10px) clamp(12px, 3vw, 20px);
            border-radius: 40px;
            font-size: clamp(12px, 3vw, 15px);
            font-weight: 600;
            display: inline-block;
            backdrop-filter: blur(5px);
        }

        /* Location bar - flex-wrap bilan moslashuvchi */
        .location-bar {
            display: flex;
            align-items: center;
            flex-wrap: wrap;
            gap: clamp(6px, 2vw, 10px);
            background: rgba(255, 255, 255, 0.1);
            padding: clamp(8px, 2vw, 12px);
            border-radius: 50px;
            margin-bottom: clamp(12px, 3vw, 18px);
            backdrop-filter: blur(5px);
        }

        .current-location {
            flex: 1 1 auto;
            display: flex;
            align-items: center;
            gap: 6px;
            color: white;
            font-weight: 600;
            font-size: clamp(13px, 3vw, 15px);
            overflow: hidden;
            min-width: 140px;
        }

        .location-icon {
            font-size: clamp(16px, 4vw, 20px);
            flex-shrink: 0;
        }

        .location-name {
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }

        .location-btn {
            background: rgba(255, 255, 255, 0.25);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: white;
            padding: clamp(8px, 2vw, 12px) clamp(12px, 3vw, 18px);
            border-radius: 40px;
            font-size: clamp(12px, 2.5vw, 14px);
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            transition: all 0.2s;
            white-space: nowrap;
            flex-shrink: 0;
        }

        /* Search section - mobil uchun ustun */
        .search-section {
            display: flex;
            gap: clamp(6px, 2vw, 10px);
            margin-bottom: clamp(16px, 4vw, 22px);
            flex-wrap: wrap;
        }

        @media (max-width: 480px) {
            .search-section {
                flex-direction: column;
            }
        }

        .region-select {
            flex: 1 1 200px;
            padding: clamp(12px, 3vw, 16px);
            border: none;
            border-radius: 40px;
            font-size: clamp(14px, 3vw, 16px);
            font-weight: 500;
            outline: none;
            background: white;
            color: var(--text-dark);
            cursor: pointer;
            min-width: 0; /* Flex overflow uchun */
        }

        body.dark-mode .region-select {
            background: #2a2f3f;
            color: white;
        }

        .search-btn {
            padding: clamp(12px, 3vw, 16px) clamp(20px, 4vw, 28px);
            background: rgba(255, 255, 255, 0.25);
            color: white;
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 40px;
            font-size: clamp(14px, 3vw, 16px);
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s;
            white-space: nowrap;
            flex: 0 1 auto;
        }

        @media (max-width: 480px) {
            .search-btn {
                width: 100%;
            }
        }

        /* Loading spinner */
        .loading {
            text-align: center;
            padding: clamp(30px, 8vw, 50px) clamp(10px, 3vw, 20px);
            width: 100%;
        }

        .spinner {
            width: clamp(40px, 10vw, 60px);
            height: clamp(40px, 10vw, 60px);
            border: 4px solid rgba(255, 255, 255, 0.2);
            border-top: 4px solid white;
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
            margin: 0 auto clamp(10px, 2vw, 15px);
        }

        /* Error message */
        .error-message {
            background: rgba(255, 235, 235, 0.95);
            color: #c62828;
            padding: clamp(12px, 3vw, 16px);
            border-radius: var(--border-radius-md);
            text-align: center;
            font-weight: 600;
            font-size: clamp(13px, 3vw, 15px);
            margin-bottom: clamp(12px, 3vw, 16px);
            width: 100%;
        }

        /* Current weather */
        .current-weather {
            background: rgba(255, 255, 255, 0.95);
            padding: clamp(16px, 4vw, 24px);
            border-radius: var(--border-radius-lg);
            margin-bottom: clamp(16px, 4vw, 22px);
        }

        body.dark-mode .current-weather {
            background: #252b38;
        }

        .city-name {
            font-size: clamp(24px, 6vw, 32px);
            color: var(--text-dark);
            text-align: center;
            margin-bottom: clamp(10px, 2.5vw, 15px);
            font-weight: 800;
            word-break: break-word;
        }

        .weather-main {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: clamp(12px, 3vw, 20px);
            margin-bottom: clamp(12px, 3vw, 18px);
            flex-wrap: wrap;
        }

        .weather-icon {
            background: white;
            border-radius: 50%;
            padding: clamp(8px, 2vw, 12px);
            width: clamp(70px, 18vw, 90px);
            height: clamp(70px, 18vw, 90px);
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .weather-icon img {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        .temperature {
            font-size: clamp(42px, 10vw, 58px);
            font-weight: 800;
            color: var(--text-dark);
            line-height: 1;
        }

        .temperature small {
            font-size: clamp(20px, 5vw, 28px);
            font-weight: 500;
            color: var(--primary-light);
        }

        .feels-like {
            font-size: clamp(13px, 3vw, 15px);
            color: var(--primary);
            margin-top: 4px;
            font-weight: 600;
            text-align: center;
        }

        .weather-desc {
            text-align: center;
            font-size: clamp(16px, 4vw, 20px);
            color: var(--text-dark);
            margin: clamp(12px, 3vw, 18px) 0;
            font-weight: 700;
            text-transform: capitalize;
            background: rgba(255, 255, 255, 0.7);
            padding: clamp(8px, 2vw, 12px);
            border-radius: 40px;
            word-break: break-word;
        }

        body.dark-mode .weather-desc {
            background: #2a2f3f;
            color: white;
        }

        /* Sun info - grid bilan moslashuvchi */
        .sun-info {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: clamp(8px, 2vw, 12px);
            background: rgba(255, 255, 255, 0.7);
            padding: clamp(12px, 3vw, 16px);
            border-radius: 50px;
            margin-bottom: clamp(16px, 4vw, 20px);
        }

        body.dark-mode .sun-info {
            background: #2a2f3f;
        }

        .sun-item {
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
        }

        .sun-icon {
            font-size: clamp(20px, 5vw, 26px);
        }

        .sun-label {
            font-size: clamp(11px, 2.5vw, 13px);
            color: var(--primary);
            font-weight: 600;
        }

        body.dark-mode .sun-label {
            color: #b0c4de;
        }

        .sun-time {
            font-size: clamp(13px, 3vw, 16px);
            font-weight: 800;
            color: var(--text-dark);
        }

        body.dark-mode .sun-time {
            color: white;
        }

        /* Weather grid - avtomatik moslashuv */
        .weather-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
            gap: clamp(8px, 2vw, 12px);
            margin-bottom: clamp(16px, 4vw, 20px);
        }

        .grid-item {
            background: white;
            padding: clamp(10px, 2.5vw, 14px);
            border-radius: 20px;
            text-align: center;
        }

        body.dark-mode .grid-item {
            background: #2a2f3f;
        }

        .grid-icon {
            font-size: clamp(20px, 5vw, 26px);
            margin-bottom: 4px;
            display: block;
        }

        .grid-label {
            font-size: clamp(10px, 2.2vw, 12px);
            color: var(--primary);
            font-weight: 600;
            margin-bottom: 4px;
        }

        .grid-value {
            font-size: clamp(16px, 4vw, 20px);
            font-weight: 800;
            color: var(--text-dark);
        }

        body.dark-mode .grid-value {
            color: white;
        }

        .grid-unit {
            font-size: clamp(9px, 2vw, 11px);
            color: var(--primary-light);
            font-weight: 500;
        }

        /* Rain probability */
        .rain-probability {
            background: linear-gradient(145deg, rgba(227, 242, 253, 0.9), rgba(187, 222, 251, 0.9));
            padding: clamp(12px, 3vw, 16px);
            border-radius: 25px;
            margin-bottom: clamp(18px, 4vw, 22px);
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 10px;
        }

        body.dark-mode .rain-probability {
            background: linear-gradient(145deg, #252b38, #1e2330);
        }

        .rain-left {
            display: flex;
            align-items: center;
            gap: clamp(8px, 2vw, 12px);
            flex-wrap: wrap;
        }

        .rain-icon {
            font-size: clamp(24px, 6vw, 32px);
        }

        .rain-text {
            font-weight: 700;
            color: var(--text-dark);
            font-size: clamp(14px, 3.5vw, 18px);
        }

        body.dark-mode .rain-text {
            color: white;
        }

        .rain-percentage {
            font-size: clamp(22px, 5.5vw, 28px);
            font-weight: 800;
            color: var(--primary);
            background: white;
            padding: clamp(6px, 1.5vw, 8px) clamp(12px, 3vw, 18px);
            border-radius: 40px;
            white-space: nowrap;
        }

        body.dark-mode .rain-percentage {
            background: #2a2f3f;
            color: #8ab3ff;
        }

        /* Hourly forecast - horizontal scroll */
        .hourly-title {
            display: flex;
            align-items: center;
            gap: 8px;
            color: white;
            font-size: clamp(16px, 4vw, 20px);
            font-weight: 700;
            margin-bottom: 12px;
        }

        .hourly-scroll {
            display: grid;
            grid-auto-flow: column;
            grid-auto-columns: minmax(75px, 90px);
            gap: 10px;
            overflow-x: auto;
            overflow-y: hidden;
            padding: 5px 0 15px;
            scrollbar-width: thin;
            -webkit-overflow-scrolling: touch;
            scroll-snap-type: x mandatory;
            width: 100%;
        }

        @media (min-width: 768px) {
            .hourly-scroll {
                grid-auto-columns: minmax(90px, 100px);
            }
        }

        .hourly-item {
            background: rgba(255, 255, 255, 0.95);
            padding: 12px 6px;
            border-radius: 22px;
            text-align: center;
            scroll-snap-align: start;
            width: 100%;
        }

        body.dark-mode .hourly-item {
            background: #252b38;
        }

        /* Weekly forecast */
        .weekly-forecast {
            margin-top: 18px;
            width: 100%;
        }

        .weekly-title {
            color: white;
            font-size: clamp(16px, 4vw, 20px);
            font-weight: 700;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .forecast-item {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: clamp(10px, 2.5vw, 14px);
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 8px;
        }

        body.dark-mode .forecast-item {
            background: #252b38;
        }

        .forecast-left {
            display: flex;
            align-items: center;
            gap: clamp(8px, 2vw, 12px);
            flex: 1 1 auto;
            min-width: 180px;
        }

        .forecast-day {
            font-weight: 700;
            color: var(--text-dark);
            min-width: 70px;
            font-size: clamp(13px, 3vw, 15px);
        }

        body.dark-mode .forecast-day {
            color: white;
        }

        .forecast-icon {
            width: clamp(30px, 7vw, 35px);
            height: clamp(30px, 7vw, 35px);
            flex-shrink: 0;
        }

        .forecast-icon img {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        .forecast-temp {
            font-weight: 800;
            color: var(--primary);
            font-size: clamp(16px, 4vw, 19px);
            min-width: 50px;
        }

        body.dark-mode .forecast-temp {
            color: #8ab3ff;
        }

        .forecast-rain {
            display: flex;
            align-items: center;
            gap: 4px;
            color: var(--primary-light);
            font-weight: 600;
            font-size: clamp(12px, 3vw, 14px);
            min-width: 45px;
            white-space: nowrap;
        }

        body.dark-mode .forecast-rain {
            color: #b0c4de;
        }

        @media (max-width: 380px) {
            .forecast-left {
                flex-wrap: wrap;
                gap: 6px;
            }
            
            .forecast-day {
                min-width: 100%;
            }
        }

        .hidden {
            display: none !important;
        }

        /* Touch optimization */
        button, select {
            touch-action: manipulation;
        }

        /* Landscape orientation */
        @media (orientation: landscape) and (max-height: 500px) {
            .container {
                padding: 8px;
            }
            
            .weather-card {
                max-width: 100%;
            }
            
            .weather-main {
                flex-direction: row;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Telegram Header -->
        <div class="telegram-header">
            <button class="header-btn" onclick="window.Telegram?.WebApp?.close()" style="visibility: hidden;">←</button>
            <span class="telegram-title">🌤 Ob-havo</span>
            <div style="display: flex; gap: 8px;">
                <button class="theme-toggle" id="themeToggle">
                    <span class="sun-icon">☀️</span>
                    <span class="moon-icon" style="display: none;">🌙</span>
                </button>
                <button class="header-btn" onclick="window.Telegram?.WebApp?.close()">✕</button>
            </div>
        </div>

        <!-- Asosiy karta -->
        <div class="weather-card">
            <header class="header">
                <h1>O'ZBEKISTON OB-HAVO</h1>
                <p class="date" id="currentDate"></p>
            </header>

            <!-- Location bar -->
            <div class="location-bar">
                <div class="current-location">
                    <span class="location-icon">📍</span>
                    <span class="location-name" id="locationName">Joylashuv aniqlanmoqda...</span>
                </div>
                <button id="getLocationBtn" class="location-btn">
                    <span>📍</span> Joylashuv
                </button>
            </div>

            <!-- Search section -->
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

            <!-- Loading -->
            <div id="loading" class="loading hidden">
                <div class="spinner"></div>
                <p style="color: white;">Ma'lumotlar yuklanmoqda...</p>
            </div>

            <!-- Error message -->
            <div id="errorMessage" class="error-message hidden"></div>

            <!-- Weather data -->
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

                    <!-- Sun info -->
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

                    <!-- Weather grid -->
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

                    <!-- Rain probability -->
                    <div class="rain-probability">
                        <div class="rain-left">
                            <span class="rain-icon">☔️</span>
                            <span class="rain-text">Yomg'ir ehtimoli</span>
                        </div>
                        <span class="rain-percentage" id="rainProbability">0%</span>
                    </div>
                </div>

                <!-- Hourly forecast -->
                <div class="hourly-title">
                    <span>⏰</span>
                    <span>Soatlik ob-havo</span>
                </div>
                <div class="hourly-scroll" id="hourlyForecast"></div>

                <!-- Weekly forecast -->
                <div class="weekly-forecast">
                    <div class="weekly-title">
                        <span>📅</span>
                        <span>7 kunlik prognoz</span>
                    </div>
                    <div id="weeklyForecast"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Telegram Web App initialization
        const tg = window.Telegram?.WebApp;
        if (tg) {
            tg.expand();
            tg.ready();
            tg.setHeaderColor('#0B3B5C');
            tg.setBackgroundColor('#0B3B5C');
            tg.disableVerticalSwipes?.();
        }

        // DOM elements
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

        // API key
        const API_KEY = 'bd5e378503939ddaee76f12ad7a97608';

        // Week days
        const weekDays = ['Yakshanba', 'Dushanba', 'Seshanba', 'Chorshanba', 'Payshanba', 'Juma', 'Shanba'];

        // Region coordinates
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

        // Theme toggle
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

        // Update date
        function updateDate() {
            const now = new Date();
            elements.currentDate.textContent = now.toLocaleDateString('uz-UZ', { 
                year: 'numeric', month: 'long', day: 'numeric' 
            });
        }
        updateDate();

        // Format time
        function formatTime(timestamp) {
            const date = new Date(timestamp * 1000);
            return date.toLocaleTimeString('uz-UZ', { hour: '2-digit', minute: '2-digit' });
        }

        // Calculate day length
        function calculateDayLength(sunrise, sunset) {
            const diff = sunset - sunrise;
            const hours = Math.floor(diff / 3600);
            const minutes = Math.floor((diff % 3600) / 60);
            return `${hours}:${minutes.toString().padStart(2, '0')}`;
        }

        // Get weather data
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
                showError('Ma\'lumotlarni yuklashda xatolik');
            } finally {
                setLoading(false);
            }
        }

        // Display weather data
        function displayWeatherData(current, forecast, location) {
            elements.cityName.textContent = location;
            elements.weatherIcon.src = `https://openweathermap.org/img/wn/${current.weather[0].icon}@2x.png`;
            elements.currentTemp.textContent = Math.round(current.main.temp);
            elements.feelsLike.textContent = `His qilinadi: ${Math.round(current.main.feels_like)}°C`;
            elements.weatherDescription.textContent = current.weather[0].description;
            
            elements.sunrise.textContent = formatTime(current.sys.sunrise);
            elements.sunset.textContent = formatTime(current.sys.sunset);
            elements.dayLength.textContent = calculateDayLength(current.sys.sunrise, current.sys.sunset);
            
            elements.humidity.textContent = current.main.humidity;
            elements.windSpeed.textContent = current.wind.speed.toFixed(1);
            elements.pressure.textContent = current.main.pressure;

            const rain = current.rain ? current.rain['1h'] || current.rain['3h'] || 0 : 0;
            elements.rainProbability.textContent = `${rain > 0 ? Math.min(Math.round(rain * 20), 100) : 0}%`;

            // Hourly forecast
            elements.hourlyForecast.innerHTML = '';
            forecast.list.slice(0, 8).forEach(item => {
                const hour = new Date(item.dt * 1000).getHours().toString().padStart(2, '0') + ':00';
                const item_rain = item.pop ? Math.round(item.pop * 100) : 0;
                
                elements.hourlyForecast.innerHTML += `
                    <div class="hourly-item">
                        <div class="hourly-time">${hour}</div>
                        <div class="hourly-icon">
                            <img src="https://openweathermap.org/img/wn/${item.weather[0].icon}.png">
                        </div>
                        <div class="hourly-temp">${Math.round(item.main.temp)}°C</div>
                        <div class="hourly-rain">☔️ ${item_rain}%</div>
                    </div>
                `;
            });

            // Weekly forecast
            elements.weeklyForecast.innerHTML = '';
            const daily = {};
            forecast.list.forEach(item => {
                const date = new Date(item.dt * 1000).toDateString();
                if (!daily[date]) daily[date] = item;
            });

            Object.values(daily).slice(0, 7).forEach((day, index) => {
                const date = new Date(day.dt * 1000);
                const dayName = index === 0 ? 'Bugun' : index === 1 ? 'Ertaga' : weekDays[date.getDay()];
                const rainChance = day.pop ? Math.round(day.pop * 100) : 0;
                
                elements.weeklyForecast.innerHTML += `
                    <div class="forecast-item">
                        <div class="forecast-left">
                            <span class="forecast-day">${dayName}</span>
                            <div class="forecast-icon">
                                <img src="https://openweathermap.org/img/wn/${day.weather[0].icon}.png">
                            </div>
                            <span class="forecast-temp">${Math.round(day.main.temp)}°C</span>
                        </div>
                        <div class="forecast-rain">
                            <span>☔️</span>
                            <span>${rainChance}%</span>
                        </div>
                    </div>
                `;
            });

            elements.weatherContainer.classList.remove('hidden');
        }

        // Get current location
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
                        const city = data[0]?.name || 'Sizning joylashuvingiz';
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

        // Search weather by region
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

        // Loading state
        function setLoading(isLoading) {
            if (isLoading) {
                elements.loading.classList.remove('hidden');
                elements.weatherContainer.classList.add('hidden');
                elements.errorMessage.classList.add('hidden');
            } else {
                elements.loading.classList.add('hidden');
            }
        }

        // Show error
        function showError(message) {
            elements.errorMessage.textContent = message;
            elements.errorMessage.classList.remove('hidden');
            setTimeout(() => elements.errorMessage.classList.add('hidden'), 5000);
        }

        // Event listeners
        elements.searchBtn.addEventListener('click', searchWeather);
        elements.getLocationBtn.addEventListener('click', getCurrentLocation);
        elements.regionSelect.addEventListener('change', searchWeather);

        // Initialize theme
        initTheme();

        // Load current location on start
        window.addEventListener('load', () => {
            setTimeout(getCurrentLocation, 500);
            
            // Fallback
            setTimeout(() => {
                if (elements.weatherContainer.classList.contains('hidden') && 
                    !elements.loading.classList.contains('hidden')) {
                    elements.regionSelect.value = 'Toshkent';
                    searchWeather();
                }
            }, 8000);
        });
    </script>
</body>
</html>
