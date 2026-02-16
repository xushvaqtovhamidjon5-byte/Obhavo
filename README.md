    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Weather App - O'zbekiston viloyatlari</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
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
            overflow-x: hidden;
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
            max-width: 100%;
            margin: 0 auto;
            padding: clamp(8px, 3vw, 16px);
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
            margin-bottom: clamp(12px, 3vh, 20px);
            padding: 4px 0;
            flex-shrink: 0;
        }

        .header-title {
            font-size: clamp(18px, 5vw, 22px);
            font-weight: 700;
            color: white;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
            letter-spacing: 0.3px;
            text-align: center;
        }

        /* Icon Buttons */
        .icon-btn {
            width: clamp(36px, 10vw, 44px);
            height: clamp(36px, 10vw, 44px);
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.15);
            border: 1px solid var(--border-light);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: clamp(18px, 5vw, 22px);
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
            border-radius: clamp(20px, 5vw, 28px);
            padding: clamp(10px, 2.5vw, 14px) clamp(12px, 3vw, 18px);
            margin-bottom: clamp(12px, 3vh, 20px);
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow);
            flex-shrink: 0;
            width: 100%;
        }

        .location-info {
            display: flex;
            align-items: center;
            gap: clamp(8px, 2vw, 12px);
            flex: 1;
            min-width: 0;
        }

        .location-badge {
            width: clamp(32px, 8vw, 40px);
            height: clamp(32px, 8vw, 40px);
            border-radius: clamp(16px, 4vw, 24px);
            background: linear-gradient(145deg, var(--accent), var(--accent-dark));
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: clamp(16px, 4vw, 20px);
            flex-shrink: 0;
        }

        .location-details {
            display: flex;
            flex-direction: column;
            min-width: 0;
            flex: 1;
        }

        .location-label {
            font-size: clamp(9px, 2.5vw, 11px);
            color: var(--text-secondary);
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.3px;
        }

        .location-value {
            font-size: clamp(13px, 3.5vw, 15px);
            font-weight: 700;
            color: var(--text-primary);
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }

        .refresh-btn {
            background: rgba(255, 255, 255, 0.2);
            border: 1px solid var(--border-light);
            padding: clamp(6px, 1.5vw, 8px) clamp(10px, 2.5vw, 14px);
            border-radius: 24px;
            color: white;
            font-weight: 600;
            font-size: clamp(11px, 3vw, 13px);
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
            gap: clamp(6px, 2vw, 10px);
            margin-bottom: clamp(12px, 3vh, 20px);
            flex-shrink: 0;
            width: 100%;
        }

        .select-wrapper {
            flex: 1;
            position: relative;
            min-width: 0;
        }

        .select-wrapper select {
            width: 100%;
            padding: clamp(10px, 3vw, 14px) clamp(12px, 3vw, 18px);
            border-radius: 30px;
            border: none;
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            color: var(--text-primary);
            font-size: clamp(12px, 3.5vw, 14px);
            font-weight: 500;
            appearance: none;
            cursor: pointer;
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow);
            transition: all 0.2s;
        }

        .select-wrapper::after {
            content: '▼';
            font-size: clamp(9px, 2.5vw, 11px);
            color: var(--accent);
            position: absolute;
            right: clamp(12px, 3vw, 16px);
            top: 50%;
            transform: translateY(-50%);
            pointer-events: none;
        }

        .search-btn {
            padding: 0 clamp(12px, 4vw, 20px);
            background: linear-gradient(145deg, var(--accent), var(--accent-dark));
            border: none;
            border-radius: 30px;
            color: white;
            font-weight: 700;
            font-size: clamp(12px, 3.5vw, 14px);
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
            border-radius: clamp(20px, 5vw, 28px);
            padding: clamp(16px, 4vw, 20px) clamp(12px, 3vw, 16px);
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow);
            margin-bottom: clamp(12px, 3vh, 20px);
            flex-shrink: 0;
            width: 100%;
        }

        .city-header {
            text-align: center;
            margin-bottom: clamp(12px, 3vh, 16px);
        }

        .city-name {
            font-size: clamp(20px, 6vw, 26px);
            font-weight: 800;
            color: var(--text-primary);
            margin-bottom: 2px;
            line-height: 1.2;
            word-break: break-word;
        }

        .current-date {
            font-size: clamp(11px, 3vw, 13px);
            color: var(--text-secondary);
            font-weight: 500;
        }

        /* Weather Visual */
        .weather-visual {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: clamp(12px, 3vh, 16px);
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50px;
            padding: clamp(8px, 2vw, 12px) clamp(12px, 3vw, 20px);
            border: 1px solid var(--border-light);
            flex-wrap: wrap;
            gap: 8px;
        }

        .weather-icon-large {
            width: clamp(50px, 15vw, 70px);
            height: clamp(50px, 15vw, 70px);
            filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.2));
        }

        .temp-large {
            font-size: clamp(36px, 10vw, 52px);
            font-weight: 800;
            color: var(--text-primary);
            line-height: 1;
        }

        .temp-large small {
            font-size: clamp(18px, 5vw, 26px);
            font-weight: 500;
            color: var(--text-secondary);
        }

        .weather-desc {
            text-align: center;
            font-size: clamp(16px, 4.5vw, 20px);
            font-weight: 600;
            color: var(--text-primary);
            text-transform: capitalize;
            margin-bottom: clamp(12px, 3vh, 16px);
            padding: clamp(4px, 1vh, 6px) 0;
            border-bottom: 1px solid var(--border-light);
        }

        /* Sun Grid */
        .sun-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: clamp(4px, 2vw, 8px);
            background: rgba(255, 255, 255, 0.1);
            border-radius: clamp(16px, 4vw, 20px);
            padding: clamp(8px, 2vw, 12px);
            margin-bottom: clamp(12px, 3vh, 16px);
            border: 1px solid var(--border-light);
        }

        .sun-item {
            text-align: center;
            display: flex;
            flex-direction: column;
            gap: 2px;
        }

        .sun-emoji {
            font-size: clamp(18px, 5vw, 24px);
        }

        .sun-label {
            font-size: clamp(8px, 2.5vw, 10px);
            color: var(--text-secondary);
            font-weight: 600;
            text-transform: uppercase;
        }

        .sun-value {
            font-size: clamp(12px, 3.5vw, 14px);
            font-weight: 700;
            color: var(--text-primary);
        }

        /* Stats Grid */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: clamp(4px, 2vw, 8px);
            margin-bottom: clamp(12px, 3vh, 16px);
        }

        .stat-item {
            background: rgba(255, 255, 255, 0.1);
            border-radius: clamp(14px, 4vw, 18px);
            padding: clamp(8px, 2vw, 12px) clamp(3px, 1vw, 6px);
            text-align: center;
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid var(--border-light);
        }

        .stat-emoji {
            font-size: clamp(18px, 5vw, 24px);
            margin-bottom: 2px;
            display: block;
        }

        .stat-label {
            font-size: clamp(8px, 2.2vw, 10px);
            color: var(--text-secondary);
            font-weight: 600;
            margin-bottom: 2px;
            text-transform: uppercase;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .stat-value {
            font-size: clamp(14px, 4vw, 16px);
            font-weight: 800;
            color: var(--text-primary);
            line-height: 1.2;
        }

        .stat-unit {
            font-size: clamp(8px, 2.2vw, 10px);
            color: var(--text-secondary);
            font-weight: 500;
        }

        /* Rain Card */
        .rain-card {
            background: linear-gradient(145deg, var(--accent), var(--accent-dark));
            border-radius: clamp(16px, 4vw, 20px);
            padding: clamp(10px, 2.5vw, 14px) clamp(12px, 3vw, 18px);
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid rgba(255, 255, 255, 0.3);
            box-shadow: 0 4px 15px rgba(37, 99, 235, 0.3);
            flex-wrap: wrap;
            gap: 8px;
        }

        .rain-left {
            display: flex;
            align-items: center;
            gap: clamp(8px, 2vw, 12px);
            min-width: 0;
            flex: 1;
        }

        .rain-emoji {
            font-size: clamp(22px, 6vw, 30px);
            flex-shrink: 0;
        }

        .rain-text {
            font-weight: 700;
            color: white;
            font-size: clamp(13px, 3.5vw, 15px);
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .rain-percent {
            font-size: clamp(18px, 5vw, 26px);
            font-weight: 800;
            color: white;
            background: rgba(255, 255, 255, 0.2);
            padding: clamp(2px, 1vw, 4px) clamp(8px, 3vw, 14px);
            border-radius: 30px;
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            white-space: nowrap;
            flex-shrink: 0;
        }

        /* Section Titles */
        .section-title {
            display: flex;
            align-items: center;
            gap: 6px;
            color: white;
            font-size: clamp(16px, 4.5vw, 20px);
            font-weight: 700;
            margin-bottom: clamp(8px, 2vh, 12px);
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
            flex-shrink: 0;
        }

        .section-title span:first-child {
            font-size: clamp(18px, 5vw, 24px);
        }

        /* Hourly Scroll */
        .hourly-scroll {
            display: flex;
            gap: clamp(6px, 2vw, 10px);
            overflow-x: auto;
            padding: 4px 0 clamp(12px, 3vh, 16px);
            scrollbar-width: thin;
            -webkit-overflow-scrolling: touch;
            scroll-snap-type: x mandatory;
            margin-bottom: clamp(12px, 3vh, 16px);
            flex-shrink: 0;
            width: 100%;
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
            min-width: clamp(60px, 20vw, 70px);
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border-radius: clamp(14px, 4vw, 18px);
            padding: clamp(8px, 2vw, 12px) clamp(3px, 1vw, 6px);
            text-align: center;
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow);
            scroll-snap-align: start;
        }

        .hourly-time {
            font-weight: 700;
            color: var(--text-primary);
            font-size: clamp(11px, 3vw, 13px);
            margin-bottom: 2px;
        }

        .hourly-icon {
            width: clamp(28px, 8vw, 36px);
            height: clamp(28px, 8vw, 36px);
            margin: 0 auto 2px;
        }

        .hourly-icon img {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        .hourly-temp {
            font-weight: 800;
            color: var(--accent);
            font-size: clamp(13px, 3.5vw, 15px);
            margin-bottom: 2px;
        }

        .hourly-rain {
            font-size: clamp(9px, 2.5vw, 11px);
            color: var(--text-secondary);
            font-weight: 600;
        }

        /* Weekly List */
        .weekly-list {
            display: flex;
            flex-direction: column;
            gap: clamp(6px, 1.5vh, 8px);
            padding-bottom: clamp(16px, 4vh, 24px);
            flex-shrink: 0;
            width: 100%;
        }

        .weekly-item {
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border-radius: clamp(16px, 4vw, 20px);
            padding: clamp(10px, 2.5vw, 14px) clamp(12px, 3vw, 16px);
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow);
            width: 100%;
        }

        .weekly-item:active {
            transform: scale(0.99);
            background: rgba(255, 255, 255, 0.2);
        }

        .weekly-left {
            display: flex;
            align-items: center;
            gap: clamp(8px, 2vw, 12px);
            flex: 1;
            min-width: 0;
        }

        .weekly-day {
            font-weight: 700;
            color: var(--text-primary);
            min-width: clamp(50px, 15vw, 65px);
            font-size: clamp(12px, 3.2vw, 14px);
        }

        .weekly-icon {
            width: clamp(24px, 7vw, 30px);
            height: clamp(24px, 7vw, 30px);
            flex-shrink: 0;
        }

        .weekly-icon img {
            width: 100%;
            height: 100%;
        }

        .weekly-temp {
            font-weight: 800;
            color: var(--accent);
            font-size: clamp(13px, 3.5vw, 15px);
            min-width: clamp(35px, 10vw, 45px);
        }

        .weekly-rain {
            display: flex;
            align-items: center;
            gap: 3px;
            color: var(--text-secondary);
            font-weight: 600;
            font-size: clamp(10px, 2.8vw, 12px);
            white-space: nowrap;
        }

        /* Loading */
        .loading-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: clamp(30px, 10vh, 50px) clamp(15px, 5vw, 20px);
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border-radius: 28px;
            border: 1px solid var(--border-light);
            flex: 1;
            min-height: 200px;
            width: 100%;
        }

        .spinner {
            width: clamp(40px, 12vw, 50px);
            height: clamp(40px, 12vw, 50px);
            border-radius: 50%;
            border: 3px solid rgba(255, 255, 255, 0.1);
            border-top-color: var(--accent);
            animation: spin 0.8s linear infinite;
            margin-bottom: 16px;
        }

        .loading-text {
            color: white;
            font-size: clamp(13px, 3.5vw, 15px);
            font-weight: 500;
        }

        /* Error */
        .error-message {
            background: rgba(239, 68, 68, 0.2);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(239, 68, 68, 0.3);
            color: white;
            padding: clamp(8px,2vw, 12px) clamp(6px, 3vw, 11px);
            border-radius: 20px;
            text-align: center;
            font-weight: 600;
            font-size: clamp(12px, 3.5vw, 14px);
            margin-bottom: 16px;
            flex-shrink: 0;
            width: 100%;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .hidden {
            display: none !important;
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
    <div class="app-container">
        <!-- Header -->
        <div class="app-header">
            <button class="icon-btn" id="menuBtn">☰</button>
            <h1 class="header-title">Ob-havo</h1>
            <button class="icon-btn" id="themeToggle">🌙</button>
        </div>

        <!-- Location Card -->
        <div class="location-card">
            <div class="location-info">
                <div class="location-badge">📍</div>
                <div class="location-details">
                    <span class="location-label">JOYLASHUV</span>
                    <span class="location-value" id="locationDisplay">Toshkent, O'zbekiston</span>
                </div>
            </div>
            <button class="refresh-btn" id="refreshBtn">
                <span>🔄</span> Yangilash
            </button>
        </div>

        <!-- Search Section - 12 ta viloyat -->
        <div class="search-section">
            <div class="select-wrapper">
                <select id="citySelect">
                    <option value="tashkent">Toshkent</option>
                    <option value="samarkand">Samarqand</option>
                    <option value="bukhara">Buxoro</option>
                    <option value="khiva">Xiva</option>
                    <option value="namangan">Namangan</option>
                    <option value="andijan">Andijon</option>
                    <option value="fergana">Farg'ona</option>
                    <option value="qashqadaryo">Qashqadaryo (Qarshi)</option>
                    <option value="surxondaryo">Surxondaryo (Termiz)</option>
                    <option value="jizzax">Jizzax</option>
                    <option value="sirdaryo">Sirdaryo (Guliston)</option>
                    <option value="xorazm">Xorazm (Urganch)</option>
                    <option value="navoiy">Navoiy</option>
                </select>
            </div>
            <button class="search-btn" id="searchBtn">Qidirish</button>
        </div>

        <!-- Loading State -->
        <div class="loading-container" id="loadingIndicator">
            <div class="spinner"></div>
            <div class="loading-text">Ob-havo ma'lumotlari yuklanmoqda...</div>
        </div>

        <!-- Error Message -->
        <div class="error-message hidden" id="errorMessage">Xatolik yuz berdi</div>

        <!-- Weather Content -->
        <div id="weatherContent" class="hidden">
            <!-- Weather Card -->
            <div class="weather-card">
                <div class="city-header">
                    <h2 class="city-name" id="cityName">Toshkent</h2>
                    <div class="current-date" id="currentDate">21 Fevral, 2025</div>
                </div>

                <div class="weather-visual">
                    <img src="https://openweathermap.org/img/wn/04d@2x.png" alt="weather" class="weather-icon-large" id="weatherIcon">
                    <div class="temp-large" id="currentTemp">18°<small>C</small></div>
                </div>

                <div class="weather-desc" id="weatherDesc">Bulutli</div>

                <!-- Sun Grid -->
                <div class="sun-grid">
                    <div class="sun-item">
                        <span class="sun-emoji">🌅</span>
                        <span class="sun-label">Quyosh chiqishi</span>
                        <span class="sun-value" id="sunrise">06:43</span>
                    </div>
                    <div class="sun-item">
                        <span class="sun-emoji">☀️</span>
                        <span class="sun-label">Kun davomiyligi</span>
                        <span class="sun-value" id="dayLength">12s 24d</span>
                    </div>
                    <div class="sun-item">
                        <span class="sun-emoji">🌇</span>
                        <span class="sun-label">Quyosh botishi</span>
                        <span class="sun-value" id="sunset">18:15</span>
                    </div>
                </div>

                <!-- Stats Grid -->
                <div class="stats-grid">
                    <div class="stat-item">
                        <span class="stat-emoji">💧</span>
                        <span class="stat-label">Namlik</span>
                        <span class="stat-value" id="humidity">65<span class="stat-unit">%</span></span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-emoji">💨</span>
                        <span class="stat-label">Shamol</span>
                        <span class="stat-value" id="windSpeed">12<span class="stat-unit">km/s</span></span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-emoji">😷</span>
                        <span class="stat-label">Bosim</span>
                        <span class="stat-value" id="pressure">1012<span class="stat-unit">mb</span></span>
                    </div>
                </div>

                <!-- Rain Card -->
                <div class="rain-card">
                    <div class="rain-left">
                        <span class="rain-emoji">☔</span>
                        <span class="rain-text">Yomg'ir ehtimoli</span>
                    </div>
                    <span class="rain-percent" id="rainChance">30%</span>
                </div>
            </div>

            <!-- Hourly Forecast -->
            <div class="section-title">
                <span>⏰</span> Soatlik ob-havo
            </div>
            <div class="hourly-scroll" id="hourlyForecast"></div>

            <!-- Weekly Forecast -->
            <div class="section-title">
                <span>📅</span> 7 kunlik prognoz
            </div>
            <div class="weekly-list" id="weeklyForecast"></div>
        </div>
    </div>

    <script>
        // Telegram Web App integration
        let tg = null;
        try {
            tg = window.Telegram?.WebApp;
            if (tg) {
                tg.expand();
                tg.enableClosingConfirmation();
            }
        } catch (e) {
            console.log('Telegram Web App not available');
        }

        // Dark mode toggle
        const themeToggle = document.getElementById('themeToggle');
        themeToggle.addEventListener('click', () => {
            document.body.classList.toggle('dark-mode');
            themeToggle.textContent = document.body.classList.contains('dark-mode') ? '☀️' : '🌙';
        });

        // Viloyatlar uchun ob-havo ma'lumotlari (mock)
        const cityWeatherData = {
            'tashkent': { temp: 18, desc: 'Bulutli', humidity: 65, wind: 12, pressure: 1012, rain: 30 },
            'samarkand': { temp: 16, desc: 'Ochiq', humidity: 55, wind: 8, pressure: 1015, rain: 10 },
            'bukhara': { temp: 22, desc: 'Ochiq', humidity: 40, wind: 10, pressure: 1010, rain: 5 },
            'khiva': { temp: 20, desc: 'Ochiq', humidity: 45, wind: 15, pressure: 1008, rain: 0 },
            'namangan': { temp: 17, desc: 'Yomg\'ir', humidity: 75, wind: 7, pressure: 1013, rain: 60 },
            'andijan': { temp: 17, desc: 'Yomg\'ir', humidity: 78, wind: 6, pressure: 1013, rain: 65 },
            'fergana': { temp: 19, desc: 'Bulutli', humidity: 70, wind: 8, pressure: 1014, rain: 40 },
            'qashqadaryo': { temp: 21, desc: 'Ochiq', humidity: 35, wind: 12, pressure: 1011, rain: 0 },
            'surxondaryo': { temp: 23, desc: 'Ochiq', humidity: 30, wind: 9, pressure: 1009, rain: 0 },
            'jizzax': { temp: 18, desc: 'Bulutli', humidity: 50, wind: 11, pressure: 1012, rain: 20 },
            'sirdaryo': { temp: 18, desc: 'Bulutli', humidity: 55, wind: 10, pressure: 1012, rain: 25 },
            'xorazm': { temp: 21, desc: 'Ochiq', humidity: 42, wind: 14, pressure: 1010, rain: 0 },
            'navoiy': { temp: 20, desc: 'Ochiq', humidity: 38, wind: 13, pressure: 1011, rain: 0 }
        };

        // Mock data for demonstration
        function loadWeatherData() {
            const selectedCity = document.getElementById('citySelect').value;
            const cityName = document.getElementById('citySelect').options[document.getElementById('citySelect').selectedIndex].text;
            const weather = cityWeatherData[selectedCity] || cityWeatherData['tashkent'];
            
            document.getElementById('loadingIndicator').classList.remove('hidden');
            document.getElementById('weatherContent').classList.add('hidden');
            document.getElementById('errorMessage').classList.add('hidden');

            // Simulate API call
            setTimeout(() => {
                document.getElementById('loadingIndicator').classList.add('hidden');
                document.getElementById('weatherContent').classList.remove('hidden');
                
                // Update location display
                document.getElementById('locationDisplay').textContent = cityName + ', O\'zbekiston';
                document.getElementById('cityName').textContent = cityName;
                
                // Update weather data
                document.getElementById('currentTemp').innerHTML = weather.temp + '°<small>C</small>';
                document.getElementById('weatherDesc').textContent = weather.desc;
                document.getElementById('humidity').innerHTML = weather.humidity + '<span class="stat-unit">%</span>';
                document.getElementById('windSpeed').innerHTML = weather.wind + '<span class="stat-unit">km/s</span>';
                document.getElementById('pressure').innerHTML = weather.pressure + '<span class="stat-unit">mb</span>';
                document.getElementById('rainChance').textContent = weather.rain + '%';
                
                // Update date
                document.getElementById('currentDate').textContent = new Date().toLocaleDateString('uz-UZ', { 
                    day: 'numeric', 
                    month: 'long', 
                    year: 'numeric' 
                });
                
                // Populate hourly forecast
                const hourlyHtml = [];
                for (let i = 0; i < 8; i++) {
                    const time = new Date();
                    time.setHours(time.getHours() + i);
                    const hourTemp = weather.temp - 2 + Math.floor(Math.random() * 5);
                    const hourRain = Math.max(0, weather.rain - 10 + Math.floor(Math.random() * 20));
                    hourlyHtml.push(`
                        <div class="hourly-item">
                            <div class="hourly-time">${time.getHours()}:00</div>
                            <div class="hourly-icon"><img src="https://openweathermap.org/img/wn/04d.png" alt=""></div>
                            <div class="hourly-temp">${hourTemp}°</div>
                            <div class="hourly-rain">${hourRain}%</div>
                        </div>
                    `);
                }
                document.getElementById('hourlyForecast').innerHTML = hourlyHtml.join('');

                // Populate weekly forecast
                const days = ['Yak', 'Dush', 'Sesh', 'Chor', 'Pay', 'Jum', 'Shan'];
                const weeklyHtml = [];
                for (let i = 0; i < 7; i++) {
                    const dayIndex = (new Date().getDay() + i) % 7;
                    const dayTemp = weather.temp - 3 + Math.floor(Math.random() * 8);
                    const dayRain = Math.max(0, weather.rain - 15 + Math.floor(Math.random() * 30));
                    weeklyHtml.push(`
                        <div class="weekly-item">
                            <div class="weekly-left">
                                <span class="weekly-day">${days[dayIndex]}</span>
                                <div class="weekly-icon"><img src="https://openweathermap.org/img/wn/04d.png" alt=""></div>
                                <span class="weekly-temp">${dayTemp}°</span>
                            </div>
                            <div class="weekly-rain">
                                <span>🌧️</span> ${dayRain}%
                            </div>
                        </div>
                    `);
                }
                document.getElementById('weeklyForecast').innerHTML = weeklyHtml.join('');
            }, 800);
        }

        // Event listeners
        document.getElementById('searchBtn').addEventListener('click', loadWeatherData);
        document.getElementById('refreshBtn').addEventListener('click', loadWeatherData);
        document.getElementById('menuBtn').addEventListener('click', () => {
            alert('Menu');
        });

        // Initial load
        loadWeatherData();

        // Handle city selection
        document.getElementById('citySelect').addEventListener('change', (e) => {
            // loadWeatherData() is called by search button
            // Just update display when search is clicked
        });
    </script>
</body>
</html>
