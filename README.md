<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2026 西班牙花漾深度遊 | 互動旅程指南</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Plotly.js -->
    <script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@400;700&family=Noto+Sans+TC:wght@300;400;500;700&display=swap" rel="stylesheet">

    <!-- Chosen Palette: "Andalusian Sunset" -->
    <!-- 
        Palette Name: "Andalusian Sunset"
        - Background: #FDFBF7 (Warm Cream) - Soft base for reading
        - Primary Text: #4A403A (Deep Coffee) - Elegant readability
        - Accent Rose: #D45D79 (Soft Red/Pink) - Highlighting emotions/flowers/Mother-Daughter theme
        - Accent Gold: #E0A458 (Muted Gold) - Highlighting luxury/history
        - Secondary Green: #87A878 (Sage) - Highlighting nature
        - UI Elements: White cards with soft shadows
    -->

    <style>
        :root {
            --color-bg: #FDFBF7;
            --color-text: #4A403A;
            --color-rose: #D45D79;
            --color-gold: #E0A458;
            --color-green: #87A878;
        }

        body {
            font-family: 'Noto Sans TC', sans-serif;
            background-color: var(--color-bg);
            color: var(--color-text);
            scroll-behavior: smooth;
        }

        h1, h2, h3, .serif {
            font-family: 'Noto Serif TC', serif;
        }

        /* Chart Container Styling - MANDATORY */
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 400px;
            overflow: hidden; 
        }

        @media (min-width: 768px) {
            .chart-container {
                height: 400px;
            }
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        ::-webkit-scrollbar-thumb {
            background: var(--color-rose);
            border-radius: 4px;
        }

        /* Timeline Line */
        .timeline-container::before {
            content: '';
            position: absolute;
            left: 20px;
            top: 0;
            bottom: 0;
            width: 2px;
            background: #E5E7EB;
            z-index: 0;
        }
        @media (min-width: 768px) {
            .timeline-container::before {
                left: 50%;
                transform: translateX(-1px);
            }
        }

        /* Interaction States */
        .day-card {
            transition: all 0.3s ease;
            cursor: pointer;
        }
        .day-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            border-left-color: var(--color-rose);
        }
        
        /* Flight Ticket Card Style */
        .flight-card {
            background: linear-gradient(135deg, #fff 0%, #f9f9f9 100%);
            border: 1px solid #e5e7eb;
            border-left: 4px solid #006b70; /* Cathay Teal-ish */
        }
    </style>

    <!-- Application Structure Plan:
         1. Hero Section: Emotional hook, highlighting the "Direct Flight" confirmation based on user upload.
         2. Flight Dashboard: Visualizing the specific flight times (CX321/CX372) and how they benefit the schedule.
         3. Comfort & Balance: Metrics reassuring the user about the pace (Walking intensity, Activity mix).
         4. Interactive Itinerary: A vertical timeline adjusted for the 08:30 arrival (Day 1) and 12:20 departure (Day 11).
         5. Logistics & Booking: "Critical Path" chart for tickets (Alhambra, etc.), marking Flights as DONE.
         6. Preparation Checklist: Interactive packing list tailored for Spain in Spring.
    -->

    <!-- Visualization & Content Choices:
         1. Flight Visualizer (HTML Grid): Inform -> Clear display of flight times/durations from source -> Shows convenience.
         2. Trip Balance (Chart.js Doughnut): Compare -> Activity mix -> Reassure balance.
         3. Walking Intensity (Plotly Bar): Inform -> Daily step estimate (Peaks on Day 2/5) -> Manage expectations.
         4. Booking Timeline (Chart.js Horizontal Bar): Organize -> Critical path -> Highlights 'Flights' as 'Booked'.
         5. Itinerary Flow (HTML/CSS): Organize -> Day-by-day card flow -> Narrative structure.
         NO SVG. NO Mermaid.
    -->

    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
</head>
<body class="antialiased">

    <!-- Navigation -->
    <nav class="sticky top-0 z-50 bg-white/90 backdrop-blur-sm shadow-sm border-b border-gray-100">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <span class="text-2xl font-bold text-[#D45D79] serif">🇪🇸 2026 花漾之旅</span>
                </div>
                <div class="hidden md:flex items-center space-x-8">
                    <a href="#flight-info" class="text-gray-600 hover:text-[#D45D79] transition">航班資訊</a>
                    <a href="#overview" class="text-gray-600 hover:text-[#D45D79] transition">旅程概覽</a>
                    <a href="#itinerary" class="text-gray-600 hover:text-[#D45D79] transition">每日行程</a>
                    <a href="#checklist" class="text-gray-600 hover:text-[#D45D79] transition">行前準備</a>
                </div>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <header class="relative bg-white overflow-hidden">
        <div class="max-w-6xl mx-auto">
            <div class="relative z-10 pb-8 bg-white sm:pb-16 md:pb-20 lg:max-w-2xl lg:w-full lg:pb-28 xl:pb-32 px-4 sm:px-6 lg:px-8 pt-20">
                <main class="mt-10 mx-auto max-w-7xl sm:mt-12 md:mt-16 lg:mt-20 xl:mt-28">
                    <div class="sm:text-center lg:text-left">
                        <span class="inline-block py-1 px-3 rounded-full bg-[#FFF0F3] text-[#D45D79] text-sm font-semibold mb-4 tracking-wide">
                            🌹 母女專屬 · 國泰直飛確認
                        </span>
                        <h1 class="text-4xl tracking-tight font-extrabold text-gray-900 sm:text-5xl md:text-6xl serif">
                            <span class="block xl:inline">2026 西班牙</span>
                            <span class="block text-[#D45D79] xl:inline">春日深度遊</span>
                        </h1>
                        <p class="mt-3 text-base text-gray-500 sm:mt-5 sm:text-lg sm:max-w-xl sm:mx-auto md:mt-5 md:text-xl lg:mx-0">
                            12天11夜 (4/23 - 5/4)。<br>
                            既然機票已定 (CX321/CX372)，我們將善用 08:30 早抵達的優勢，安排一場最舒適的時差調整與浪漫漫步。
                        </p>
                        <div class="mt-5 sm:mt-8 sm:flex sm:justify-center lg:justify-start gap-3">
                            <div class="flex items-center space-x-2 text-sm text-green-700 bg-green-50 px-4 py-2 rounded-lg border border-green-200">
                                <span>✅</span>
                                <span>機票已確認 HKD 8,522</span>
                            </div>
                        </div>
                    </div>
                </main>
            </div>
        </div>
        <div class="lg:absolute lg:inset-y-0 lg:right-0 lg:w-1/2 bg-[#FDFBF7]">
            <canvas id="heroCanvas" class="w-full h-full object-cover"></canvas>
        </div>
    </header>

    <!-- Section 1: Flight Dashboard (New based on Source) -->
    <section id="flight-info" class="py-12 bg-white border-b border-gray-100">
        <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
            <h2 class="text-2xl font-bold text-gray-900 serif mb-6">✈️ 您的航班安排</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Outbound -->
                <div class="flight-card p-6 rounded-xl shadow-sm relative overflow-hidden group">
                    <div class="absolute top-0 right-0 bg-[#006b70] text-white text-xs px-3 py-1 rounded-bl-lg">去程</div>
                    <div class="flex justify-between items-end mb-4">
                        <div>
                            <p class="text-3xl font-bold text-gray-800">HKG</p>
                            <p class="text-sm text-gray-500">00:25 (4/23)</p>
                        </div>
                        <div class="flex-1 px-4 text-center">
                            <p class="text-xs text-gray-400">14h 5m</p>
                            <div class="h-0.5 bg-gray-300 w-full relative">
                                <div class="absolute -top-1 right-0 w-2 h-2 bg-gray-300 rounded-full"></div>
                            </div>
                            <p class="text-xs text-[#006b70] font-bold mt-1">CX321</p>
                        </div>
                        <div class="text-right">
                            <p class="text-3xl font-bold text-gray-800">BCN</p>
                            <p class="text-sm text-gray-500">08:30 (4/23)</p>
                        </div>
                    </div>
                    <div class="bg-blue-50 p-3 rounded-lg text-sm text-blue-800">
                        <span class="font-bold">✨ 行程優勢：</span> 早上抵達，有一整天的時間適應時差。建議先去飯店寄放行李，享用早午餐後再 Check-in。
                    </div>
                </div>

                <!-- Inbound -->
                <div class="flight-card p-6 rounded-xl shadow-sm relative overflow-hidden group">
                    <div class="absolute top-0 right-0 bg-[#006b70] text-white text-xs px-3 py-1 rounded-bl-lg">回程</div>
                    <div class="flex justify-between items-end mb-4">
                        <div>
                            <p class="text-3xl font-bold text-gray-800">MAD</p>
                            <p class="text-sm text-gray-500">12:20 (5/3)</p>
                        </div>
                        <div class="flex-1 px-4 text-center">
                            <p class="text-xs text-gray-400">12h 35m</p>
                            <div class="h-0.5 bg-gray-300 w-full relative">
                                <div class="absolute -top-1 right-0 w-2 h-2 bg-gray-300 rounded-full"></div>
                            </div>
                            <p class="text-xs text-[#006b70] font-bold mt-1">CX372</p>
                        </div>
                        <div class="text-right">
                            <p class="text-3xl font-bold text-gray-800">HKG</p>
                            <p class="text-sm text-gray-500">06:55 (5/4)</p>
                        </div>
                    </div>
                    <div class="bg-yellow-50 p-3 rounded-lg text-sm text-yellow-800">
                        <span class="font-bold">⚠️ 注意事項：</span> 馬德里機場 T4S 很大，建議 09:00 就從市區出發。當天早上不安排景點，悠閒早餐後直奔機場。
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Section 2: Dashboard (Overview & Reassurance) -->
    <section id="overview" class="py-16 bg-[#FDFBF7]">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="mb-10 text-center md:text-left">
                <h2 class="text-3xl font-bold text-gray-900 serif">旅程舒適度分析</h2>
                <p class="mt-4 text-lg text-gray-500">
                    這不是一趟趕路的旅行。我們根據長輩體力，量化了行程的「舒適度」與「豐富度」。
                </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <!-- Activity Balance Chart -->
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
                    <h3 class="text-lg font-bold text-[#D45D79] mb-4">體驗黃金比例</h3>
                    <div class="chart-container">
                        <canvas id="balanceChart"></canvas>
                    </div>
                    <p class="text-sm text-gray-400 mt-4 text-center">
                        觀光與放鬆各半，購物與美食點綴，拒絕審美疲勞。
                    </p>
                </div>

                <!-- Walking Intensity Chart -->
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
                    <h3 class="text-lg font-bold text-[#E0A458] mb-4">體力消耗預報</h3>
                    <div class="chart-container">
                        <div id="intensityChart"></div>
                    </div>
                    <p class="text-sm text-gray-400 mt-4 text-center">
                        Day 2 & 5 稍需腳力，Day 5 晚上特別安排 SPA 修復。
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- Section 3: Interactive Itinerary -->
    <section id="itinerary" class="py-16 bg-white">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-3xl font-bold text-gray-900 serif">每日行程亮點</h2>
                <p class="mt-4 text-lg text-gray-500">點擊卡片查看詳細安排與貼心提醒</p>
            </div>

            <div class="relative timeline-container space-y-8" id="timelineContent">
                <!-- Javascript will populate this -->
            </div>
        </div>
    </section>

    <!-- Section 4: Logistics & Critical Booking -->
    <section id="logistics" class="py-16 bg-[#FFF9FA]">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-12">
                <div class="lg:col-span-1">
                    <h2 class="text-3xl font-bold text-gray-900 serif mb-6">預訂攻略</h2>
                    <p class="text-gray-500 mb-6">
                        機票已搞定！接下來的重點是搶這兩張世界級景點的門票。
                    </p>
                    
                    <div class="bg-white p-6 rounded-xl shadow-sm border-l-4 border-[#E0A458]">
                        <h4 class="font-bold text-gray-800 mb-2">🚕 市區交通策略</h4>
                        <p class="text-sm text-gray-600">
                            母女出遊原則：<br>
                            <span class="font-bold">「能搭車就不走路」</span>。<br>
                            善用 Uber 或 Cabify App，保留體力給美麗的景點。
                        </p>
                    </div>
                </div>

                <div class="lg:col-span-2">
                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
                        <h3 class="text-lg font-bold text-[#D45D79] mb-4">⏰ 搶票關鍵時間軸 (Critical Path)</h3>
                        <div class="chart-container">
                            <canvas id="bookingChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Section 5: Preparation Checklist -->
    <section id="checklist" class="py-16 bg-white">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <h2 class="text-3xl font-bold text-gray-900 serif text-center mb-10">行前準備清單</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Column 1 -->
                <div class="space-y-4">
                    <h3 class="font-bold text-[#87A878] border-b pb-2">📂 文件與票券</h3>
                    <label class="flex items-start space-x-3 p-3 hover:bg-gray-50 rounded-lg cursor-pointer">
                        <input type="checkbox" class="form-checkbox h-5 w-5 text-[#D45D79] rounded mt-1">
                        <span class="text-gray-700">護照 (檢查有效期 > 6個月)</span>
                    </label>
                    <label class="flex items-start space-x-3 p-3 hover:bg-gray-50 rounded-lg cursor-pointer">
                        <input type="checkbox" checked disabled class="form-checkbox h-5 w-5 text-green-500 rounded mt-1">
                        <span class="text-gray-500 line-through">列印電子機票 (CX321/CX372) - 已完成</span>
                    </label>
                    <label class="flex items-start space-x-3 p-3 hover:bg-gray-50 rounded-lg cursor-pointer">
                        <input type="checkbox" class="form-checkbox h-5 w-5 text-[#D45D79] rounded mt-1">
                        <span class="text-gray-700">下載阿爾罕布拉宮/聖家堂門票 PDF</span>
                    </label>
                    <label class="flex items-start space-x-3 p-3 hover:bg-gray-50 rounded-lg cursor-pointer">
                        <input type="checkbox" class="form-checkbox h-5 w-5 text-[#D45D79] rounded mt-1">
                        <span class="text-gray-700">火車票 Renfe (存入手機 Wallet)</span>
                    </label>
                </div>

                <!-- Column 2 -->
                <div class="space-y-4">
                    <h3 class="font-bold text-[#E0A458] border-b pb-2">🧳 貼心打包</h3>
                    <label class="flex items-start space-x-3 p-3 hover:bg-gray-50 rounded-lg cursor-pointer">
                        <input type="checkbox" class="form-checkbox h-5 w-5 text-[#D45D79] rounded mt-1">
                        <span class="text-gray-700">厚底球鞋 (石板路剋星)</span>
                    </label>
                    <label class="flex items-start space-x-3 p-3 hover:bg-gray-50 rounded-lg cursor-pointer">
                        <input type="checkbox" class="form-checkbox h-5 w-5 text-[#D45D79] rounded mt-1">
                        <span class="text-gray-700">歐洲網卡 (eSIM 或實體卡)</span>
                    </label>
                    <label class="flex items-start space-x-3 p-3 hover:bg-gray-50 rounded-lg cursor-pointer">
                        <input type="checkbox" class="form-checkbox h-5 w-5 text-[#D45D79] rounded mt-1">
                        <span class="text-gray-700">高保濕乳液 & 護唇膏 (氣候乾燥)</span>
                    </label>
                    <label class="flex items-start space-x-3 p-3 hover:bg-gray-50 rounded-lg cursor-pointer">
                        <input type="checkbox" class="form-checkbox h-5 w-5 text-[#D45D79] rounded mt-1">
                        <span class="text-gray-700">墨鏡 & 帽子 (南部陽光強烈)</span>
                    </label>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-[#4A403A] text-white py-10">
        <div class="max-w-6xl mx-auto px-4 text-center">
            <h2 class="text-2xl serif mb-4">祝您和媽媽有一趟美好的旅程 🌹</h2>
            <p class="text-gray-400 text-sm">2026 西班牙春日深度遊規劃</p>
        </div>
    </footer>

    <!-- JavaScript Implementation -->
    <script>
        // --- Data Source ---
        const itineraryData = [
            { day: 1, date: "4/23 (四)", city: "巴塞隆納", title: "晨光與玫瑰", icon: "🌹", highlight: "08:30 抵達 & 聖喬治節", intensity: "Medium", desc: "CX321 08:30 抵達。建議：機場接送 -> 飯店寄放行李 -> El Nacional 早午餐 -> 15:00 Check-in 補眠 -> 傍晚格拉西亞大道看花海。", stay: "Barcelona" },
            { day: 2, date: "4/24 (五)", city: "巴塞隆納", title: "上帝的建築", icon: "⛪", highlight: "聖家堂 & 奎爾公園", intensity: "High", desc: "上午參觀聖家堂光影森林，下午搭車去奎爾公園散步。今日步行量較大，晚上早點休息。", stay: "Barcelona" },
            { day: 3, date: "4/25 (六)", city: "巴塞隆納", title: "聖山大自然", icon: "⛰️", highlight: "蒙特塞拉特聖山", intensity: "Medium", desc: "參加 Local Tour 舒適上山。看鋸齒山峰，聽男童合唱團，呼吸芬多精。", stay: "Barcelona" },
            { day: 4, date: "4/26 (日)", city: "巴塞隆納 ✈️", title: "購物與南飛", icon: "🛍️", highlight: "Outlet & 移動", intensity: "Medium", desc: "週日商店休息，正好去 La Roca Village 購物。傍晚搭 Vueling 飛往格拉納達。", stay: "Granada" },
            { day: 5, date: "4/27 (一)", city: "格拉納達", title: "皇宮與SPA", icon: "🧖‍♀️", highlight: "阿爾罕布拉宮", intensity: "High", desc: "參觀世界遺產夏宮花園 (Generalife)。傍晚安排阿拉伯澡堂精油按摩，消除疲勞。", stay: "Granada" },
            { day: 6, date: "4/28 (二)", city: "哥多華", title: "前往花之城", icon: "🚅", highlight: "百花巷漫步", intensity: "Low", desc: "搭車前往哥多華。欣賞掛滿藍色花盆的白色巷弄，羅馬橋看夕陽。", stay: "Cordoba" },
            { day: 7, date: "4/29 (三)", city: "馬德里", title: "清真寺與高鐵", icon: "🕌", highlight: "清真寺主教堂", intensity: "Medium", desc: "上午參觀壯觀的紅白拱門清真寺。下午搭 AVE 高鐵前往馬德里。", stay: "Madrid" },
            { day: 8, date: "4/30 (四)", city: "馬德里", title: "水晶宮殿", icon: "✨", highlight: "雷提朗公園", intensity: "Low", desc: "在水晶宮殿拍美照，下午去 Salamanca 區優雅逛街 (Zara/Mango 旗艦店)。", stay: "Madrid" },
            { day: 9, date: "5/1 (五)", city: "馬德里", title: "古城漫遊", icon: "🏰", highlight: "托雷多半日遊", intensity: "Medium", desc: "勞動節市區休息，參加托雷多 Tour。搭乘觀光小火車輕鬆繞城看全景。", stay: "Madrid" },
            { day: 10, date: "5/2 (六)", city: "馬德里", title: "美食衝刺", icon: "🥘", highlight: "聖米格爾市場", intensity: "Medium", desc: "Tapas 早午餐，最後補貨時間 (英國宮百貨)。晚上打包行李。", stay: "Madrid" },
            { day: 11, date: "5/3 (日)", city: "返程", title: "告別西班牙", icon: "✈️", highlight: "前往機場", intensity: "Low", desc: "09:00 出發前往機場 T4S。搭乘 CX372 12:20 起飛返港。", stay: "Flight" },
            { day: 12, date: "5/4 (一)", city: "香港", title: "抵達溫暖家", icon: "🏠", highlight: "06:55 抵達", intensity: "Low", desc: "抵達香港，結束美好旅程。", stay: "Home" }
        ];

        // --- Render Itinerary ---
        const timelineContainer = document.getElementById('timelineContent');
        
        itineraryData.forEach((day, index) => {
            const isLeft = index % 2 === 0;
            const card = document.createElement('div');
            card.className = `relative flex items-center justify-between md:justify-normal md:odd:flex-row-reverse group day-card`;
            
            // Content HTML
            card.innerHTML = `
                <!-- Icon Marker -->
                <div class="flex items-center justify-center w-10 h-10 rounded-full border-4 border-white bg-[#D45D79] text-white shrink-0 md:order-1 md:group-odd:-translate-x-1/2 md:group-even:translate-x-1/2 shadow absolute left-0 md:left-1/2 transform -translate-x-1/2 md:translate-x-0 z-10 text-xl">
                    ${day.icon}
                </div>
                
                <!-- Spacer for Desktop Alignment -->
                <div class="hidden md:block w-1/2"></div>

                <!-- Card Content -->
                <div class="w-[calc(100%-3rem)] md:w-[calc(50%-2rem)] bg-white p-6 rounded-xl shadow-sm border-l-4 ${day.city.includes('巴塞隆納') ? 'border-[#D45D79]' : (day.city.includes('格拉納達') ? 'border-[#E0A458]' : (day.city.includes('馬德里') ? 'border-[#87A878]' : 'border-gray-300'))} ml-12 md:ml-0 md:mx-8">
                    <div class="flex justify-between items-start mb-2">
                        <div>
                            <span class="font-bold text-gray-400 text-xs tracking-wider uppercase">Day ${day.day} • ${day.date}</span>
                            <h3 class="font-bold text-lg text-gray-800 mt-1">${day.city} - ${day.title}</h3>
                        </div>
                        <span class="px-2 py-1 bg-gray-50 text-xs rounded text-gray-500 font-medium">${day.stay}</span>
                    </div>
                    <p class="text-gray-600 text-sm mb-3">${day.desc}</p>
                    <div class="flex items-center gap-2">
                        <span class="text-xs font-semibold px-2 py-1 rounded bg-[#FFF0F3] text-[#D45D79]">✨ ${day.highlight}</span>
                        ${day.intensity === 'High' ? '<span class="text-xs font-semibold px-2 py-1 rounded bg-red-50 text-red-500">🔥 體力挑戰</span>' : ''}
                    </div>
                </div>
            `;
            timelineContainer.appendChild(card);
        });

        // --- Chart 1: Trip Balance (Doughnut) ---
        // Label wrapping helper
        function wrapLabel(str, maxChars) {
            if (str.length <= maxChars) return str;
            const words = str.split(' ');
            const lines = [];
            let currentLine = words[0];
            for (let i = 1; i < words.length; i++) {
                if (currentLine.length + 1 + words[i].length <= maxChars) {
                    currentLine += ' ' + words[i];
                } else {
                    lines.push(currentLine);
                    currentLine = words[i];
                }
            }
            lines.push(currentLine);
            return lines;
        }

        const ctxBalance = document.getElementById('balanceChart').getContext('2d');
        const activityLabels = ['經典觀光 (Sightseeing)', '自然放鬆 (Nature & Relax)', '購物行程 (Shopping)', '美食體驗 (Food)'];
        
        new Chart(ctxBalance, {
            type: 'doughnut',
            data: {
                labels: activityLabels.map(l => wrapLabel(l, 16)),
                datasets: [{
                    data: [40, 30, 15, 15], 
                    backgroundColor: [
                        '#D45D79', // Rose
                        '#87A878', // Green
                        '#E0A458', // Gold
                        '#4A403A'  // Coffee
                    ],
                    borderWidth: 2,
                    borderColor: '#ffffff',
                    hoverOffset: 10
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { position: 'bottom', labels: { font: { family: "'Noto Sans TC', sans-serif" } } },
                    tooltip: {
                        callbacks: {
                            title: function(tooltipItems) {
                                const item = tooltipItems[0];
                                let label = item.chart.data.labels[item.dataIndex];
                                return Array.isArray(label) ? label.join(' ') : label;
                            }
                        }
                    }
                },
                cutout: '65%'
            }
        });

        // --- Chart 2: Walking Intensity (Plotly Bar) ---
        const intensityMap = { 'High': 8, 'Medium': 5, 'Low': 3 };
        const intensityValues = itineraryData.slice(0, 11).map(d => intensityMap[d.intensity]);
        const days = itineraryData.slice(0, 11).map(d => `D${d.day}`);
        
        const colors = intensityValues.map(v => {
            if (v >= 8) return '#D45D79'; // High - Rose
            if (v >= 5) return '#E0A458'; // Med - Gold
            return '#87A878';             // Low - Sage
        });

        const trace1 = {
            x: days,
            y: intensityValues,
            type: 'bar',
            marker: { color: colors },
            text: intensityValues.map(v => v >= 8 ? '🔥 High' : (v >= 5 ? '🚶 Med' : '😌 Low')),
            textposition: 'auto',
            hoverinfo: 'x+text'
        };

        const layout = {
            font: { family: 'Noto Sans TC' },
            xaxis: { title: '行程天數' },
            yaxis: { title: '強度指數 (1-10)', range: [0, 10], fixedrange: true },
            margin: { t: 20, b: 40, l: 40, r: 20 },
            paper_bgcolor: 'rgba(0,0,0,0)',
            plot_bgcolor: 'rgba(0,0,0,0)',
            showlegend: false
        };

        const config = { responsive: true, displayModeBar: false };
        Plotly.newPlot('intensityChart', [trace1], layout, config);

        // --- Chart 3: Booking Timeline (Horizontal Bar) ---
        const ctxBooking = document.getElementById('bookingChart').getContext('2d');
        const bookingLabels = ['阿爾罕布拉宮 (Alhambra)', '聖家堂 (Sagrada Familia)', '米拉之家 (Casa Mila)', '國泰機票 (Flights)', '高鐵車票 (Renfe)'];
        
        new Chart(ctxBooking, {
            type: 'bar',
            data: {
                labels: bookingLabels.map(l => wrapLabel(l, 16)),
                datasets: [{
                    label: '提前預訂天數 (Days in Advance)',
                    data: [90, 60, 30, 0, 60], // Flight is 0 (booked)
                    backgroundColor: [
                        '#E0A458', // Todo
                        '#E0A458', // Todo
                        '#E0A458', // Todo
                        '#87A878', // Done (Green)
                        '#E0A458'  // Todo
                    ],
                    borderRadius: 6
                }]
            },
            options: {
                indexAxis: 'y',
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    x: {
                        beginAtZero: true,
                        title: { display: true, text: '出發前幾天 (Days Before)' }
                    }
                },
                plugins: {
                    legend: { display: false },
                    tooltip: {
                        callbacks: {
                            title: function(tooltipItems) {
                                const item = tooltipItems[0];
                                let label = item.chart.data.labels[item.dataIndex];
                                if(label.includes('國泰機票')) return '已完成預訂';
                                return Array.isArray(label) ? label.join(' ') : label;
                            }
                        }
                    }
                }
            }
        });

        // --- Decorative Hero Canvas (Soft Particles) ---
        const canvas = document.getElementById('heroCanvas');
        const ctx = canvas.getContext('2d');
        
        // Resize canvas
        function resizeCanvas() {
            canvas.width = canvas.parentElement.offsetWidth;
            canvas.height = canvas.parentElement.offsetHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        // Particles
        const particles = [];
        for(let i=0; i<25; i++) {
            particles.push({
                x: Math.random() * canvas.width,
                y: Math.random() * canvas.height,
                r: Math.random() * 15 + 5,
                color: Math.random() > 0.5 ? '#FFF0F3' : '#FDFBF7', // Very subtle
                speedX: Math.random() * 0.5 - 0.25,
                speedY: Math.random() * 0.5 - 0.25
            });
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach(p => {
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
                ctx.fillStyle = p.color;
                ctx.fill();
                p.x += p.speedX;
                p.y += p.speedY;
                
                if(p.x < 0 || p.x > canvas.width) p.speedX *= -1;
                if(p.y < 0 || p.y > canvas.height) p.speedY *= -1;
            });
            requestAnimationFrame(animate);
        }
        animate();

    </script>
</body>
</html>
