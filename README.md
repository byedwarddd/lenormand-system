<!DOCTYPE html>
<html lang="zh-TW" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Aethelgard - 雷諾曼占卜復盤與雲端心智殿堂</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        parchment: {
                            50: '#fffdfa',
                            100: '#fcf8f0',
                            200: '#f3e9db',
                            300: '#e5d3bc',
                            400: '#cdae91',
                        },
                        taupe: {
                            600: '#8c7a6b',
                            700: '#6b5c4d',
                            800: '#4a3f33',
                            900: '#2b241d'
                        },
                        antique: {
                            gold: '#c29b38',
                            light: '#a6822c',
                            dark: '#7d611b'
                        }
                    },
                    fontFamily: {
                        serif: ['"Cinzel"', '"Noto Serif TC"', 'serif'],
                        sans: ['"Inter"', '"Noto Sans TC"', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600;700&family=Inter:wght@300;400;500;600&family=Noto+Serif+TC:wght@300;400;600&display=swap" rel="stylesheet">
    <!-- FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        body {
            background-color: #fcf8f0;
            color: #2b241d;
            font-family: 'Inter', 'Noto Sans TC', sans-serif;
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
        }
        .font-occult {
            font-family: 'Cinzel', 'Noto Serif TC', serif;
        }
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f3e9db;
        }
        ::-webkit-scrollbar-thumb {
            background: #cdae91;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #c29b38;
        }
        .card-glow {
            box-shadow: 0 4px 20px -3px rgba(194, 155, 56, 0.25);
        }
        .card-glow-active {
            box-shadow: 0 0 20px 2px rgba(194, 155, 56, 0.45);
            border-color: #c29b38 !important;
        }
        @keyframes floatSlow {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-4px); }
        }
        .animate-float {
            animation: floatSlow 4s ease-in-out infinite;
        }
        .lenormand-card-svg {
            width: 100%;
            height: 100%;
            display: block;
        }
    </style>
</head>
<body class="min-h-screen bg-parchment-100 text-taupe-900 flex flex-col selection:bg-antique-gold selection:text-white">

    <header class="border-b border-parchment-300 bg-parchment-50/95 backdrop-blur-md sticky top-0 z-50 shadow-sm">
        <div class="max-w-7xl mx-auto px-3 sm:px-6 lg:px-8 h-18 sm:h-20 flex items-center justify-between">
            <div class="flex items-center space-x-2 sm:space-x-3 min-w-0">
                <div class="w-9 h-9 sm:w-10 sm:h-10 rounded-full border border-antique-gold flex items-center justify-center bg-parchment-200 text-antique-gold font-occult text-lg sm:text-xl shadow-inner flex-shrink-0">
                    <i class="fa-solid fa-cloud-sun"></i>
                </div>
                <div class="min-w-0">
                    <h1 class="font-occult text-base sm:text-2xl font-bold tracking-widest text-taupe-900 truncate">AETHELGARD</h1>
                    <p class="text-[10px] sm:text-xs text-taupe-600 tracking-wider truncate flex items-center">
                        <span>雲端雷諾曼心智殿堂</span>
                        <span id="cloud-sync-status" class="ml-2 inline-flex items-center text-emerald-700 bg-emerald-50 px-1.5 py-0.5 rounded text-[9px] border border-emerald-200 font-medium">
                            <i class="fa-solid fa-circle-check mr-1 text-[8px]"></i> 雲端同步中
                        </span>
                    </p>
                </div>
            </div>
            
            <div class="flex items-center space-x-1 sm:space-x-2.5 flex-shrink-0">
                <button onclick="openExportModal()" class="px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm rounded-xl border border-parchment-300 hover:border-antique-gold text-taupe-700 hover:text-antique-dark transition flex items-center space-x-1 bg-white shadow-sm font-medium">
                    <i class="fa-solid fa-vault text-antique-gold"></i>
                    <span class="hidden md:inline">資料保險箱</span>
                </button>
                <button onclick="switchTab('analytics')" id="nav-analytics-btn" class="px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm font-occult rounded-xl border border-parchment-300 text-taupe-700 hover:text-taupe-900 transition flex items-center space-x-1 bg-white shadow-sm font-medium">
                    <i class="fa-solid fa-chart-pie text-antique-gold"></i>
                    <span class="hidden sm:inline">統計分析</span>
                </button>
                <button onclick="switchTab('divination')" id="nav-divination-btn" class="px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm font-occult rounded-xl bg-antique-gold text-white font-bold transition shadow-md flex items-center space-x-1 hover:bg-antique-light">
                    <i class="fa-solid fa-wand-magic-sparkles"></i>
                    <span class="hidden sm:inline">新占卜祭壇</span>
                    <span class="sm:hidden">占卜</span>
                </button>
                <button onclick="switchTab('records')" id="nav-records-btn" class="px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm font-occult rounded-xl border border-parchment-300 text-taupe-700 hover:text-taupe-900 transition flex items-center space-x-1 bg-white shadow-sm font-medium">
                    <i class="fa-solid fa-book-journal-quill"></i>
                    <span class="hidden sm:inline">紀錄殿堂 <span id="record-count-badge" class="ml-1 px-1.5 py-0.2 text-[10px] bg-parchment-200 rounded-full text-taupe-900 font-bold">0</span></span>
                    <span class="sm:hidden">紀錄</span>
                </button>
            </div>
        </div>
    </header>

    <main class="flex-grow max-w-7xl w-full mx-auto px-3 sm:px-6 lg:px-8 py-4 sm:py-8">
        
        <div id="view-divination" class="space-y-6 sm:space-y-8">
            <div class="text-center max-w-2xl mx-auto space-y-2 py-2 sm:py-4">
                <div class="inline-block text-antique-gold text-xs sm:text-sm tracking-widest font-occult uppercase border-b border-antique-gold/40 pb-1">Morning Sanctuary</div>
                <h2 class="text-2xl sm:text-3xl font-occult font-bold text-taupe-900">探求命運之微光</h2>
                <p class="text-xs sm:text-sm text-taupe-700 font-light px-2">靜心凝神，設定您的提問。系統將為您完整封存當下直覺，並自動安全同步至雲端伺服器。</p>
            </div>

            <form id="divination-form" onsubmit="handleFormSubmit(event)" class="space-y-6 sm:space-y-8 bg-white border border-parchment-300 rounded-2xl p-4 sm:p-8 shadow-md">
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 sm:gap-6">
                    <div class="md:col-span-2 space-y-4">
                        <div class="space-y-2">
                            <label class="block text-xs font-occult uppercase tracking-wider text-taupe-800 font-semibold">
                                <i class="fa-solid fa-feather-pointed mr-1 text-antique-gold"></i> 占卜問題 (Question) <span class="text-antique-gold">*</span>
                            </label>
                            <textarea required id="input-question" rows="3" placeholder="例如：近期心靈成長與事業轉折的方向為何？"
                                class="w-full bg-parchment-50 border border-parchment-300 rounded-xl p-3 text-sm text-taupe-900 focus:outline-none focus:border-antique-gold transition resize-none shadow-sm"></textarea>
                            <p class="text-[11px] text-taupe-600">提示：送出建檔後問題將自動進入「唯讀鎖定」狀態，無法再行修改。</p>
                        </div>
                    </div>

                    <div class="space-y-4">
                        <div>
                            <label class="block text-xs font-occult uppercase tracking-wider text-taupe-800 font-semibold mb-1">
                                <i class="fa-solid fa-tag mr-1 text-antique-gold"></i> 主題標籤 (Tags)
                            </label>
                            <select id="input-tag" class="w-full bg-parchment-50 border border-parchment-300 rounded-xl p-2.5 text-sm text-taupe-900 focus:outline-none focus:border-antique-gold transition shadow-sm">
                                <option value="#愛情">#愛情</option>
                                <option value="#事業">#事業</option>
                                <option value="#財運">#財運</option>
                                <option value="#人際">#人際</option>
                                <option value="#股票占卜">#股票占卜</option>
                                <option value="#靈性成長" selected>#靈性成長</option>
                                <option value="#綜合指引">#綜合指引</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-occult uppercase tracking-wider text-taupe-800 font-semibold mb-1">
                                <i class="fa-solid fa-hourglass-half mr-1 text-antique-gold"></i> 預計驗證時效
                            </label>
                            <input type="date" id="input-deadline" class="w-full bg-parchment-50 border border-parchment-300 rounded-xl p-2.5 text-sm text-taupe-900 focus:outline-none focus:border-antique-gold transition shadow-sm">
                        </div>
                    </div>
                </div>

                <div class="space-y-3 pt-4 border-t border-parchment-200">
                    <label class="block text-xs font-occult uppercase tracking-wider text-taupe-800 font-semibold">
                        <i class="fa-solid fa-chess-board mr-1 text-antique-gold"></i> 選擇雷諾曼牌陣 (Spread)
                    </label>
                    <div class="grid grid-cols-2 sm:grid-cols-5 gap-2.5 sm:gap-3" id="spread-selector">
                        <button type="button" onclick="setSpread('3')" class="spread-btn p-3 rounded-xl border border-antique-gold bg-parchment-200 text-taupe-900 font-bold text-xs font-occult transition flex flex-col items-center space-y-1 shadow-sm" data-spread="3">
                            <i class="fa-solid fa-cards text-base sm:text-lg text-antique-gold"></i>
                            <span>三張牌陣 (3)</span>
                        </button>
                        <button type="button" onclick="setSpread('4')" class="spread-btn p-3 rounded-xl border border-parchment-300 bg-parchment-50 text-taupe-700 text-xs font-occult transition flex flex-col items-center space-y-1 hover:border-antique-gold shadow-sm" data-spread="4">
                            <i class="fa-solid fa-clone text-base sm:text-lg text-taupe-600"></i>
                            <span>四張線性 (4)</span>
                        </button>
                        <button type="button" onclick="setSpread('5')" class="spread-btn p-3 rounded-xl border border-parchment-300 bg-parchment-50 text-taupe-700 text-xs font-occult transition flex flex-col items-center space-y-1 hover:border-antique-gold shadow-sm" data-spread="5">
                            <i class="fa-solid fa-layer-group text-base sm:text-lg text-taupe-600"></i>
                            <span>五張牌陣 (5)</span>
                        </button>
                        <button type="button" onclick="setSpread('9')" class="spread-btn p-3 rounded-xl border border-parchment-300 bg-parchment-50 text-taupe-700 text-xs font-occult transition flex flex-col items-center space-y-1 hover:border-antique-gold shadow-sm" data-spread="9">
                            <i class="fa-solid fa-table-cells text-base sm:text-lg text-taupe-600"></i>
                            <span>九宮格 (3x3)</span>
                        </button>
                        <button type="button" onclick="setSpread('36')" class="spread-btn col-span-2 sm:col-span-1 p-3 rounded-xl border border-parchment-300 bg-parchment-50 text-taupe-700 text-xs font-occult transition flex flex-col items-center space-y-1 hover:border-antique-gold shadow-sm" data-spread="36">
                            <i class="fa-solid fa-border-all text-base sm:text-lg text-antique-gold"></i>
                            <span>大藍圖 (8×4+4)</span>
                        </button>
                    </div>
                </div>

                <div id="tableau-import-panel" class="hidden space-y-3 p-4 bg-parchment-100 border border-antique-gold/40 rounded-xl shadow-inner">
                    <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-1">
                        <span class="text-xs font-occult text-taupe-900 font-bold flex items-center">
                            <i class="fa-solid fa-wand-magic mr-2 text-antique-gold"></i> 大藍圖文字快速帶入與智慧容錯解析 (8×4+4)
                        </span>
                        <div class="flex items-center space-x-2">
                            <button type="button" onclick="randomFillTableau()" class="text-[11px] text-antique-dark underline font-medium hover:text-antique-gold">
                                <i class="fa-solid fa-shuffle mr-1"></i>隨機洗牌填滿
                            </button>
                            <span class="text-[11px] text-taupe-600">支援編號、牌名或分隔符號</span>
                        </div>
                    </div>
                    <div class="flex flex-col sm:flex-row gap-2">
                        <textarea id="tableau-paste-input" rows="2" placeholder="例如：1.騎士, 2.三葉草, 3.航船... 或直接貼上36行牌名清單"
                            class="flex-grow bg-white border border-parchment-300 rounded-xl p-2 text-xs text-taupe-900 focus:outline-none focus:border-antique-gold shadow-sm resize-none"></textarea>
                        <button type="button" onclick="parseTableauText()" class="px-4 py-2.5 sm:py-2 bg-antique-gold text-white rounded-xl font-bold text-xs hover:bg-antique-light transition flex items-center justify-center shadow-sm flex-shrink-0">
                            智慧解析
                        </button>
                    </div>
                    <div id="import-feedback" class="text-[11px] text-taupe-700 font-medium"></div>
                </div>

                <div class="space-y-4 pt-2">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 border-b border-parchment-200 pb-2">
                        <div>
                            <span class="text-xs font-occult uppercase tracking-wider text-taupe-800 font-semibold">牌陣配置區 (Card Placement)</span>
                            <p class="text-[11px] text-taupe-600">點選牌位後，可從下方「1-36雷諾曼卡牌選單」指派牌卡（右鍵或長按可標記核心代表牌）。</p>
                        </div>
                        <div class="flex items-center space-x-2 text-xs">
                            <span class="text-antique-dark font-medium"><i class="fa-solid fa-star text-antique-gold"></i> 核心代表牌 (Significator):</span>
                            <span id="active-significator-count" class="px-2 py-0.5 rounded bg-parchment-100 border border-parchment-300 text-taupe-900 font-bold">0 / 2</span>
                        </div>
                    </div>

                    <div id="card-slots-container" class="flex flex-wrap gap-2.5 sm:gap-4 justify-center py-4 bg-parchment-50 rounded-2xl border border-parchment-300/80 min-h-[220px] p-3 sm:p-4 shadow-inner overflow-x-auto">
                        <!-- 動態生成 -->
                    </div>
                </div>

                <div class="space-y-3 pt-2">
                    <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-1">
                        <span class="text-xs font-occult uppercase tracking-wider text-taupe-800 font-semibold flex items-center">
                            <i class="fa-solid fa-book-open mr-2 text-antique-gold"></i> 雷諾曼 1-36 號精緻卡牌選單 (點選指派至目前牌位)
                        </span>
                        <span class="text-[11px] text-taupe-700 font-medium">目前選中牌位: <strong id="current-selected-slot-label" class="text-antique-dark">尚未選取 (請先點上方牌位)</strong></span>
                    </div>
                    <div class="grid grid-cols-3 sm:grid-cols-6 md:grid-cols-12 gap-2 max-h-64 sm:max-h-72 overflow-y-auto p-2 bg-parchment-50 border border-parchment-300 rounded-xl shadow-sm" id="deck-quick-picker">
                        <!-- 動態生成 1-36 牌卡按鈕 -->
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 sm:gap-6 pt-4 border-t border-parchment-200">
                    <div class="space-y-2">
                        <label class="block text-xs font-occult uppercase tracking-wider text-taupe-800 font-semibold">
                            <i class="fa-solid fa-eye mr-1 text-antique-gold"></i> 當下直覺與初步預測 (Initial Prediction) <span class="text-antique-gold">*</span>
                        </label>
                        <textarea required id="input-prediction" rows="4" placeholder="記錄抽牌當下的直覺感應、核心解讀與初步結論..."
                            class="w-full bg-parchment-50 border border-parchment-300 rounded-xl p-3 text-sm text-taupe-900 focus:outline-none focus:border-antique-gold transition resize-none shadow-sm"></textarea>
                        <p class="text-[11px] text-taupe-600">提示：建檔後此欄位將永久鎖定，確保客觀復盤。</p>
                    </div>

                    <div class="space-y-2">
                        <label class="block text-xs font-occult uppercase tracking-wider text-taupe-800 font-semibold">
                            <i class="fa-solid fa-link mr-1 text-antique-gold"></i> 牌卡組合與連綴解讀筆記 (Pairing Notes)
                        </label>
                        <textarea id="input-pairing" rows="4" placeholder="例如：騎士(1) + 三葉草(2) = 迅速而短暫的喜訊..."
                            class="w-full bg-parchment-50 border border-parchment-300 rounded-xl p-3 text-sm text-taupe-900 focus:outline-none focus:border-antique-gold transition resize-none shadow-sm"></textarea>
                        <p class="text-[11px] text-taupe-600">提示：大藍圖或複雜牌陣允許在建檔後 24 小時內調整牌面配置。</p>
                    </div>
                </div>

                <div class="flex justify-end pt-4">
                    <button type="submit" class="w-full sm:w-auto px-8 py-3 bg-gradient-to-r from-antique-dark via-antique-gold to-antique-light text-white font-occult font-bold rounded-xl shadow-lg hover:opacity-95 transition flex items-center justify-center space-x-2 text-sm">
                        <i class="fa-solid fa-cloud-arrow-up"></i>
                        <span>封存占卜紀錄至雲端殿堂</span>
                    </button>
                </div>
            </form>
        </div>

        <div id="view-records" class="hidden space-y-4 sm:space-y-6">
            <div class="flex flex-col md:flex-row justify-between items-stretch md:items-center gap-3 bg-white p-4 rounded-2xl border border-parchment-300 shadow-sm">
                <div class="flex flex-col sm:flex-row flex-wrap items-stretch sm:items-center gap-2.5 sm:gap-3">
                    <div class="relative flex-grow sm:flex-grow-0">
                        <i class="fa-solid fa-magnifying-glass absolute left-3 top-3 text-taupe-600 text-xs"></i>
                        <input type="text" id="search-keyword" oninput="renderRecordsList()" placeholder="搜尋問題或筆記..."
                            class="w-full sm:w-64 bg-parchment-50 border border-parchment-300 rounded-xl pl-9 pr-3 py-2 text-xs text-taupe-900 focus:outline-none focus:border-antique-gold shadow-sm">
                    </div>
                    <div class="grid grid-cols-2 sm:flex gap-2">
                        <select id="filter-status" onchange="renderRecordsList()" class="bg-parchment-50 border border-parchment-300 rounded-xl px-3 py-2 text-xs text-taupe-900 focus:outline-none focus:border-antique-gold shadow-sm flex-grow">
                            <option value="ALL">全部狀態 (All)</option>
                            <option value="Active">追蹤中 (Active)</option>
                            <option value="Due">待驗證 (Due)</option>
                            <option value="Archived">長期封存 (Archived)</option>
                        </select>
                        <select id="filter-tag" onchange="renderRecordsList()" class="bg-parchment-50 border border-parchment-300 rounded-xl px-3 py-2 text-xs text-taupe-900 focus:outline-none focus:border-antique-gold shadow-sm flex-grow">
                            <option value="ALL">所有主題標籤</option>
                            <option value="#靈性成長">#靈性成長</option>
                            <option value="#愛情">#愛情</option>
                            <option value="#事業">#事業</option>
                            <option value="#財運">#財運</option>
                            <option value="#人際">#人際</option>
                            <option value="#股票占卜">#股票占卜</option>
                            <option value="#綜合指引">#綜合指引</option>
                        </select>
                    </div>
                </div>
                <div class="flex items-center justify-end text-xs text-taupe-700 font-medium">
                    <span>雲端共計紀錄: <strong id="stats-total" class="text-antique-dark font-bold">0</strong> 筆</span>
                </div>
            </div>

            <div id="records-grid" class="grid grid-cols-1 gap-4">
                <!-- 動態生成紀錄卡片 -->
            </div>
            
            <div id="empty-records-state" class="hidden text-center py-16 space-y-3 bg-white rounded-2xl border border-parchment-300 shadow-sm">
                <i class="fa-solid fa-book-skull text-3xl text-taupe-600/60"></i>
                <p class="text-sm font-occult text-taupe-700">雲端殿堂內尚無符合條件的占卜紀錄</p>
                <button onclick="switchTab('divination')" class="px-4 py-2 bg-parchment-50 text-antique-dark rounded-xl text-xs hover:border-antique-gold border border-parchment-300 shadow-sm font-bold">
                    開始第一次占卜
                </button>
            </div>
        </div>

        <div id="view-detail" class="hidden space-y-4 sm:space-y-6">
            <div class="flex items-center justify-between bg-white p-4 rounded-2xl border border-parchment-300 shadow-sm">
                <button onclick="switchTab('records')" class="px-3 sm:px-4 py-2 rounded-xl bg-parchment-50 border border-parchment-300 hover:border-antique-gold text-xs text-taupe-800 font-occult font-bold transition flex items-center space-x-2 shadow-sm">
                    <i class="fa-solid fa-arrow-left"></i>
                    <span>返回紀錄殿堂</span>
                </button>
                <div class="flex items-center space-x-2">
                    <button id="detail-archive-btn" onclick="toggleArchiveCurrentRecord()" class="px-2.5 sm:px-3 py-1.5 rounded-xl border border-parchment-300 text-xs text-taupe-700 hover:text-taupe-900 hover:border-antique-gold transition bg-white shadow-sm font-medium">
                        歸檔/解除
                    </button>
                    <button onclick="deleteCurrentRecord()" class="px-2.5 sm:px-3 py-1.5 rounded-xl bg-red-50 border border-red-200 text-xs text-red-700 hover:bg-red-100 transition shadow-sm font-medium">
                        刪除
                    </button>
                </div>
            </div>

            <div class="bg-white border border-antique-gold/40 rounded-2xl p-4 sm:p-8 space-y-6 shadow-md">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2 border-b border-parchment-200 pb-4">
                    <div>
                        <div class="flex flex-wrap items-center gap-1.5 sm:gap-2 mb-1">
                            <span id="detail-tag-badge" class="px-2 py-0.5 rounded text-[10px] bg-parchment-100 text-antique-dark font-occult border border-antique-gold/30 font-bold">#靈性成長</span>
                            <span id="detail-date-badge" class="text-xs text-taupe-600">2026-09-21 14:00</span>
                            <span id="detail-status-badge" class="px-2 py-0.5 rounded text-[10px] font-bold">追蹤中</span>
                        </div>
                        <h3 id="detail-question-title" class="text-base sm:text-xl font-occult font-bold text-taupe-900">問題載入中...</h3>
                    </div>
                </div>

                <div class="space-y-3">
                    <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-1">
                        <span class="text-xs font-occult uppercase tracking-wider text-taupe-800 font-bold">
                            <i class="fa-solid fa-cards mr-1 text-antique-gold"></i> 牌陣配置與核心代表牌 (Grand Tableau 8×4+4)
                        </span>
                        <span id="detail-edit-buffer-status" class="text-[11px] text-taupe-600 font-medium"></span>
                    </div>
                    <div id="detail-cards-display" class="flex flex-wrap gap-2.5 justify-center p-3 sm:p-4 bg-parchment-50 rounded-xl border border-parchment-300 shadow-inner overflow-x-auto">
                        <!-- 動態渲染卡片 -->
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="space-y-3 bg-parchment-50 p-4 rounded-xl border border-parchment-300 shadow-sm relative">
                        <div class="flex items-center justify-between">
                            <span class="text-xs font-occult uppercase tracking-wider text-taupe-800 font-bold">
                                <i class="fa-solid fa-lock mr-1 text-antique-gold"></i> 當下直覺預測 (已安全鎖定)
                            </span>
                            <span class="text-[10px] text-antique-dark bg-white px-2 py-0.5 rounded border border-antique-gold/20 font-bold">防事後諸葛保護中</span>
                        </div>
                        <div id="detail-prediction-text" class="text-sm text-taupe-800 whitespace-pre-wrap leading-relaxed min-h-[80px]"></div>
                        <div class="pt-2 border-t border-parchment-200 text-xs text-taupe-700">
                            <strong>組合解讀筆記：</strong>
                            <p id="detail-pairing-text" class="mt-1 text-taupe-600"></p>
                        </div>
                    </div>

                    <div class="space-y-3 bg-parchment-50 p-4 rounded-xl border border-antique-gold/40 shadow-sm">
                        <div class="flex items-center justify-between">
                            <span class="text-xs font-occult uppercase tracking-wider text-taupe-900 font-bold">
                                <i class="fa-solid fa-star mr-1 text-antique-gold"></i> 實際復盤與星空評分
                            </span>
                            <span id="detail-review-timestamp" class="text-[10px] text-taupe-600 font-medium"></span>
                        </div>

                        <div class="space-y-1">
                            <label class="block text-xs text-taupe-700 font-medium">實際發生狀況與走勢驗證 (Actual Outcome)</label>
                            <textarea id="review-actual-input" rows="3" placeholder="後續實際發展如何？與牌面哪張牌呼應？"
                                class="w-full bg-white border border-parchment-300 rounded-xl p-2.5 text-xs text-taupe-900 focus:outline-none focus:border-antique-gold transition resize-none shadow-sm"></textarea>
                        </div>

                        <div class="space-y-1">
                            <label class="block text-xs text-taupe-700 font-medium">直覺與預測準確度評分</label>
                            <div class="flex items-center space-x-2 py-1 flex-wrap" id="star-rating-container">
                                <i class="fa-solid fa-star text-lg cursor-pointer text-taupe-300 hover:text-antique-gold transition" onclick="setReviewRating(1)"></i>
                                <i class="fa-solid fa-star text-lg cursor-pointer text-taupe-300 hover:text-antique-gold transition" onclick="setReviewRating(2)"></i>
                                <i class="fa-solid fa-star text-lg cursor-pointer text-taupe-300 hover:text-antique-gold transition" onclick="setReviewRating(3)"></i>
                                <i class="fa-solid fa-star text-lg cursor-pointer text-taupe-300 hover:text-antique-gold transition" onclick="setReviewRating(4)"></i>
                                <i class="fa-solid fa-star text-lg cursor-pointer text-taupe-300 hover:text-antique-gold transition" onclick="setReviewRating(5)"></i>
                                <span id="rating-text-label" class="text-xs text-antique-dark ml-2 font-occult font-bold">未評分</span>
                            </div>
                        </div>

                        <div class="space-y-1">
                            <label class="block text-xs text-taupe-700 font-medium">復盤反思心得 (Reflection Notes)</label>
                            <textarea id="review-reflection-input" rows="2" placeholder="您從這次占卜學到了什麼牌陣技巧或心態盲點？"
                                class="w-full bg-white border border-parchment-300 rounded-xl p-2.5 text-xs text-taupe-900 focus:outline-none focus:border-antique-gold transition resize-none shadow-sm"></textarea>
                        </div>

                        <button onclick="saveReviewData()" class="w-full py-2.5 bg-antique-gold text-white rounded-xl font-occult font-bold text-xs hover:bg-antique-light transition shadow-md flex items-center justify-center space-x-2">
                            <i class="fa-solid fa-stamp"></i>
                            <span>雲端同步復盤時間戳記與儲存</span>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <div id="view-analytics" class="hidden space-y-6">
            <div class="text-center max-w-2xl mx-auto space-y-2 py-2">
                <div class="inline-block text-antique-gold text-xs sm:text-sm tracking-widest font-occult uppercase border-b border-antique-gold/40 pb-1">Wisdom Analytics</div>
                <h2 class="text-2xl font-occult font-bold text-taupe-900">直覺與命運統計殿堂</h2>
                <p class="text-xs sm:text-sm text-taupe-700 font-light">追蹤您的復盤完成率，掌握待補的占卜紀錄，精進直覺感應。</p>
            </div>

            <!-- 核心指標卡片 -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                <div class="bg-white border border-parchment-300 rounded-2xl p-5 shadow-sm space-y-1">
                    <span class="text-xs font-occult uppercase text-taupe-600 tracking-wider">總占卜次數</span>
                    <div id="stat-card-total" class="text-2xl sm:text-3xl font-occult font-bold text-antique-dark">0</div>
                </div>
                <div class="bg-white border border-parchment-300 rounded-2xl p-5 shadow-sm space-y-1">
                    <span class="text-xs font-occult uppercase text-taupe-600 tracking-wider">尚未復盤數量</span>
                    <div id="stat-card-unreviewed" class="text-2xl sm:text-3xl font-occult font-bold text-amber-700">0</div>
                </div>
                <div class="bg-white border border-parchment-300 rounded-2xl p-5 shadow-sm space-y-1">
                    <span class="text-xs font-occult uppercase text-taupe-600 tracking-wider">已完成復盤筆數</span>
                    <div id="stat-card-reviewed" class="text-2xl sm:text-3xl font-occult font-bold text-antique-dark">0</div>
                </div>
                <div class="bg-white border border-parchment-300 rounded-2xl p-5 shadow-sm space-y-1">
                    <span class="text-xs font-occult uppercase text-taupe-600 tracking-wider">復盤完成率</span>
                    <div id="stat-card-rate" class="text-2xl sm:text-3xl font-occult font-bold text-antique-dark">0%</div>
                </div>
            </div>

            <!-- 待復盤清單專區 -->
            <div class="bg-white border border-antique-gold/40 rounded-2xl p-6 shadow-md space-y-4">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2 border-b border-parchment-200 pb-3">
                    <h3 class="font-occult font-bold text-sm sm:text-base text-taupe-900 flex items-center">
                        <i class="fa-solid fa-triangle-exclamation mr-2 text-antique-gold"></i> 尚未進行復盤的占卜紀錄 (<span id="unreviewed-count-badge">0</span>)
                    </h3>
                    <span class="text-xs text-taupe-600">完成復盤能大幅提升直覺預測準確度</span>
                </div>
                <div id="unreviewed-records-list" class="space-y-3 max-h-72 overflow-y-auto pr-1">
                    <!-- 動態生成待復盤清單 -->
                </div>
                <div id="empty-unreviewed-state" class="hidden text-center py-6 text-xs text-taupe-600 font-medium">
                    <i class="fa-solid fa-circle-check text-emerald-600 text-lg mb-1"></i>
                    <p>太棒了！所有雲端占卜紀錄皆已完成復盤筆記。</p>
                </div>
            </div>

            <!-- 標籤與高頻牌卡分佈 -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="bg-white border border-parchment-300 rounded-2xl p-6 shadow-sm space-y-4">
                    <h3 class="font-occult font-bold text-sm text-taupe-900 flex items-center">
                        <i class="fa-solid fa-tags mr-2 text-antique-gold"></i> 熱門主題標籤分佈
                    </h3>
                    <div id="analytics-tags-container" class="space-y-3">
                        <!-- 動態生成標籤比例 -->
                    </div>
                </div>

                <div class="bg-white border border-parchment-300 rounded-2xl p-6 shadow-sm space-y-4">
                    <h3 class="font-occult font-bold text-sm text-taupe-900 flex items-center">
                        <i class="fa-solid fa-ranking-star mr-2 text-antique-gold"></i> 高頻出現代表牌卡 Top 5
                    </h3>
                    <div id="analytics-topcards-container" class="space-y-3">
                        <!-- 動態生成高頻牌卡 -->
                    </div>
                </div>
            </div>
        </div>

    </main>

    <div id="export-modal" class="fixed inset-0 z-50 bg-taupe-900/40 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="bg-white border border-antique-gold/50 rounded-2xl max-w-lg w-full p-6 space-y-6 shadow-2xl relative">
            <button onclick="closeExportModal()" class="absolute top-4 right-4 text-taupe-600 hover:text-taupe-900 text-xl font-bold">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <div class="flex items-center space-x-3 border-b border-parchment-200 pb-3">
                <div class="w-8 h-8 rounded-full bg-parchment-100 border border-antique-gold flex items-center justify-center text-antique-gold">
                    <i class="fa-solid fa-vault"></i>
                </div>
                <div>
                    <h3 class="font-occult font-bold text-base text-taupe-900">資料安全保險箱 (JSON 備份與還原)</h3>
                    <p class="text-[11px] text-taupe-600">雲端資料之外，您也可隨時下載備份檔保存</p>
                </div>
            </div>

            <div class="space-y-4">
                <div class="space-y-2">
                    <label class="block text-xs font-occult uppercase text-taupe-800 font-semibold">1. 匯出備份 (Export Backup)</label>
                    <p class="text-xs text-taupe-600">將雲端所有紀錄打包為 JSON 檔案下載。</p>
                    <button onclick="exportDataJSON()" class="w-full py-2.5 bg-parchment-50 border border-antique-gold text-antique-dark rounded-xl text-xs hover:bg-parchment-100 transition flex items-center justify-center space-x-2 font-occult font-bold shadow-sm">
                        <i class="fa-solid fa-download"></i>
                        <span>下載完整雲端資料備份 (.json)</span>
                    </button>
                </div>

                <div class="border-t border-parchment-200 pt-4 space-y-2">
                    <label class="block text-xs font-occult uppercase text-taupe-800 font-semibold">2. 匯入還原 (Import Restore)</label>
                    <p class="text-xs text-taupe-600">上傳先前備份的 JSON 檔案並同步至雲端。</p>
                    <input type="file" id="import-file-input" accept=".json" class="w-full text-xs text-taupe-600 file:mr-4 file:py-2 file:px-4 file:rounded-xl file:border-0 file:text-xs file:font-bold file:bg-parchment-50 file:text-antique-dark file:border file:border-parchment-300 hover:file:bg-parchment-100 cursor-pointer">
                    <button onclick="importDataJSON()" class="w-full py-2.5 bg-antique-gold text-white rounded-xl text-xs hover:bg-antique-light transition flex items-center justify-center space-x-2 font-occult font-bold shadow-sm">
                        <i class="fa-solid fa-upload"></i>
                        <span>確認讀取並同步至雲端</span>
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast-notification" class="fixed bottom-6 right-6 z-50 transform translate-y-20 opacity-0 transition-all duration-300 bg-white border border-antique-gold text-taupe-900 px-4 py-3 rounded-xl shadow-xl flex items-center space-x-3 max-w-xs">
        <i id="toast-icon" class="fa-solid fa-circle-check text-antique-gold text-lg flex-shrink-0"></i>
        <span id="toast-message" class="text-xs font-medium">通知訊息內容</span>
    </div>

    <!-- Firebase SDK 導入與雲端資料同步邏輯 -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, doc, setDoc, deleteDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        const lenormandDeck = [
            { id: 1, name: "騎士", meaning: "訊息、來訪、動態", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M20 70 L50 40 L80 70 Z" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="50" cy="30" r="12" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M35 55 L65 55" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 2, name: "三葉草", meaning: "幸運、機會、短暫快樂", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="40" cy="45" r="12" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="60" cy="45" r="12" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="50" cy="63" r="12" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M50 72 L50 85" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 3, name: "航船", meaning: "旅行、遠行、進展", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M25 65 Q50 85 75 65 L65 50 L35 50 Z" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="50" y1="50" x2="50" y2="25" stroke="#7d611b" stroke-width="4"/><path d="M50 25 L70 37 L50 45" fill="none" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 4, name: "房屋", meaning: "家庭、房產、穩定", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><polyline points="20,50 50,25 80,50" fill="none" stroke="#7d611b" stroke-width="4"/><rect x="30" y="50" width="40" height="35" fill="none" stroke="#7d611b" stroke-width="4"/><rect x="42" y="65" width="16" height="20" fill="none" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 5, name: "樹木", meaning: "健康、生命力、根基", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><rect x="44" y="55" width="12" height="30" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="50" cy="40" r="22" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M38 45 Q50 25 62 45" fill="none" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 6, name: "雲朵", meaning: "困惑、模糊、暫時陰霾", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M30 65 Q20 65 20 52 Q20 40 35 40 Q40 25 60 30 Q75 30 78 45 Q88 48 85 62 Q85 70 70 70 Z" fill="none" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 7, name: "長蛇", meaning: "複雜、嫉妒、智慧、轉折", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M25 75 Q40 50 50 70 Q60 90 75 60 Q85 40 70 25" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="68" cy="22" r="5" fill="none" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 8, name: "棺材", meaning: "結束、轉變、停滯", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><polygon points="35,25 65,25 75,45 65,85 35,85 25,45" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="35" y1="25" x2="65" y2="25" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 9, name: "鮮花", meaning: "禮物、喜悅、美麗、邀請", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="50" cy="45" r="10" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="35" cy="35" r="8" fill="none" stroke="#7d611b" stroke-width="3"/><circle cx="65" cy="35" r="8" fill="none" stroke="#7d611b" stroke-width="3"/><circle cx="35" cy="55" r="8" fill="none" stroke="#7d611b" stroke-width="3"/><circle cx="65" cy="55" r="8" fill="none" stroke="#7d611b" stroke-width="3"/><path d="M50 55 L50 85" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 10, name: "鐮刀", meaning: "突發、決定、切割、收成", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M25 75 Q70 70 75 30 Q75 60 45 78 Z" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M45 78 L30 90" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 11, name: "皮鞭", meaning: "衝突、重複、爭執、鍛鍊", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M25 25 Q60 25 50 55 Q40 85 75 75" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="70" y1="70" x2="80" y2="80" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 12, name: "飛鳥", meaning: "交談、焦慮、雙胞、耳語", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M20 45 Q35 25 50 45 Q65 25 80 45 Q50 65 20 45 Z" fill="none" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 13, name: "小孩子", meaning: "新開始、純真、小孩、小型", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="50" cy="35" r="12" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="50" cy="62" r="18" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M42 27 L58 27" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 14, name: "狐狸", meaning: "工作、策略、小心、謊言", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><polygon points="30,70 50,30 70,70" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="50" cy="55" r="8" fill="none" stroke="#7d611b" stroke-width="3"/><path d="M35 30 L25 15" stroke="#7d611b" stroke-width="4"/><path d="M65 30 L75 15" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 15, name: "熊", meaning: "力量、財務、權威、母親", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="50" cy="55" r="22" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="33" cy="38" r="8" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="67" cy="38" r="8" fill="none" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 16, name: "星星", meaning: "希望、指引、靈感、清晰", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><polygon points="50,20 60,40 80,50 60,60 50,80 40,60 20,50 40,40" fill="none" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 17, name: "鸛鳥", meaning: "搬遷、改變、改善、新氣象", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M30 75 Q40 40 60 45 L75 30" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="72" cy="25" r="6" fill="none" stroke="#7d611b" stroke-width="3"/><path d="M45 60 L60 85" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 18, name: "忠犬", meaning: "朋友、忠誠、信任、陪伴", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><rect x="35" y="45" width="30" height="35" rx="8" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="50" cy="30" r="12" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M40 22 L35 15" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 19, name: "高塔", meaning: "機構、孤立、法律、遠見", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><rect x="38" y="25" width="24" height="60" fill="none" stroke="#7d611b" stroke-width="4"/><polyline points="32,25 50,15 68,25" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="38" y1="45" x2="62" y2="45" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 20, name: "花園", meaning: "社交、公眾、群體、聚會", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="50" cy="40" r="15" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M25 80 Q50 60 75 80" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="50" y1="55" x2="50" y2="80" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 21, name: "高山", meaning: "阻礙、挑戰、延遲、冷漠", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><polygon points="20,80 50,25 80,80" fill="none" stroke="#7d611b" stroke-width="4"/><polyline points="40,80 60,45 80,80" fill="none" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 22, name: "十字路口", meaning: "選擇、分岔口、多重選項", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M50 80 L50 20 M50 20 L25 45 M50 20 L75 45" fill="none" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 23, name: "老鼠", meaning: "壓力、損耗、焦慮、偷竊", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><ellipse cx="50" cy="55" rx="18" ry="14" fill="none" stroke="#7d611b" stroke-width="4"/><circle cx="35" cy="45" r="8" fill="none" stroke="#7d611b" stroke-width="3"/><path d="M68 55 Q85 75 80 40" fill="none" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 24, name: "愛心", meaning: "愛情、情感、熱情、和諧", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M50 78 C25 55 15 40 15 28 C15 18 24 12 33 12 C42 12 50 22 50 22 C50 22 58 12 67 12 C76 12 85 18 85 28 C85 40 75 55 50 78 Z" fill="none" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 25, name: "戒指", meaning: "承諾、合約、婚姻、循環", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="50" cy="50" r="22" fill="none" stroke="#7d611b" stroke-width="6"/><circle cx="50" cy="30" r="5" fill="none" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 26, name: "書本", meaning: "知識、秘密、學習、檔案", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M20 30 Q50 20 80 30 L80 75 Q50 65 20 75 Z" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="50" y1="23" x2="50" y2="70" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 27, name: "信件", meaning: "文件、通知、書面合約", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><rect x="20" y="30" width="60" height="40" rx="4" fill="none" stroke="#7d611b" stroke-width="4"/><polyline points="20,30 50,55 80,30" fill="none" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 28, name: "紳士", meaning: "男性代表、問卜者或伴侶", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="50" cy="35" r="12" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M25 80 L35 55 L65 55 L75 80" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="45" y1="55" x2="55" y2="75" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 29, name: "女士", meaning: "女性代表、問卜者或伴侶", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="50" cy="35" r="12" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M30 80 Q50 50 70 80" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M38 55 Q50 65 62 55" fill="none" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 30, name: "百合花", meaning: "成熟、平和、性愛、家族", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M50 80 L50 25 M30 40 Q50 20 70 40 M35 55 Q50 35 65 55" fill="none" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 31, name: "太陽", meaning: "成功、活力、光明、能量", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="50" cy="50" r="15" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="50" y1="20" x2="50" y2="10" stroke="#7d611b" stroke-width="4"/><line x1="50" y1="80" x2="50" y2="90" stroke="#7d611b" stroke-width="4"/><line x1="20" y1="50" x2="10" y2="50" stroke="#7d611b" stroke-width="4"/><line x1="80" y1="50" x2="90" y2="50" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 32, name: "月亮", meaning: "情感、潛意識、名譽、直覺", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M60 20 A30 30 0 1 1 40 80 A25 25 0 1 0 60 20 Z" fill="none" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 33, name: "鑰匙", meaning: "解答、解方、重要突破", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="35" cy="50" r="14" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="49" y1="50" x2="80" y2="50" stroke="#7d611b" stroke-width="4"/><line x1="70" y1="50" x2="70" y2="62" stroke="#7d611b" stroke-width="3"/><line x1="60" y1="50" x2="60" y2="60" stroke="#7d611b" stroke-width="3"/></svg>' },
            { id: 34, name: "魚類", meaning: "財富、金錢、流動、商業", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><path d="M20 50 Q50 20 75 50 Q50 80 20 50 Z" fill="none" stroke="#7d611b" stroke-width="4"/><path d="M75 35 L90 20 L85 50 L90 80 L75 65" fill="none" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 35, name: "錨", meaning: "穩定, 安全, 長久, 工作", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><circle cx="50" cy="25" r="8" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="50" y1="33" x2="50" y2="80" stroke="#7d611b" stroke-width="4"/><path d="M30 65 Q50 90 70 65" fill="none" stroke="#7d611b" stroke-width="4"/><line x1="35" y1="50" x2="65" y2="50" stroke="#7d611b" stroke-width="4"/></svg>' },
            { id: 36, name: "十字架", meaning: "試煉, 負擔, 宿命, 信仰", svg: '<svg viewBox="0 0 100 100" class="lenormand-card-svg"><line x1="50" y1="15" x2="50" y2="85" stroke="#7d611b" stroke-width="6"/><line x1="30" y1="35" x2="70" y2="35" stroke="#7d611b" stroke-width="6"/></svg>' }
        ];

        let currentSpread = '3';
        let currentSlotsCount = 3;
        let cardAssignments = {};
        let significatorSlots = new Set();
        let activeSelectedSlot = null;
        let recordsList = [];
        let currentEditingRecordId = null;
        let currentReviewRating = 0;

        let db, auth, userId;
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-lenormand-app';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : null;

        window.addEventListener('DOMContentLoaded', async () => {
            initQuickPicker();
            setSpread('3');
            setDefaultDeadline();

            if (firebaseConfig) {
                try {
                    const app = initializeApp(firebaseConfig);
                    db = getFirestore(app);
                    auth = getAuth(app);

                    if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                        await signInWithCustomToken(auth, __initial_auth_token);
                    } else {
                        await signInAnonymously(auth);
                    }

                    userId = auth.currentUser?.uid || crypto.randomUUID();
                    initFirestoreListener();
                } catch (e) {
                    console.warn("雲端連線失敗，自動轉為離線儲存模式", e);
                    loadRecordsFromLocalStorage();
                    renderRecordsList();
                }
            } else {
                loadRecordsFromLocalStorage();
                renderRecordsList();
            }

            const inputs = document.querySelectorAll('input, textarea');
            inputs.forEach(el => {
                el.addEventListener('focus', function() {
                    setTimeout(() => {
                        this.scrollIntoView({ behavior: 'smooth', block: 'center' });
                    }, 300);
                });
            });
        });

        function initFirestoreListener() {
            if (!db || !userId) return;
            const colRef = collection(db, 'artifacts', appId, 'users', userId, 'records');
            onSnapshot(colRef, (snapshot) => {
                recordsList = [];
                snapshot.forEach((docSnap) => {
                    recordsList.push({ id: docSnap.id, ...docSnap.data() });
                });
                recordsList.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
                renderRecordsList();
                document.getElementById('cloud-sync-status').innerHTML = `<i class="fa-solid fa-cloud-arrow-up mr-1 text-[8px]"></i> 雲端同步完成`;
            }, (error) => {
                console.error("Firestore sync error:", error);
                document.getElementById('cloud-sync-status').innerHTML = `<i class="fa-solid fa-triangle-exclamation mr-1 text-[8px] text-amber-600"></i> 雲端連線異常`;
                loadRecordsFromLocalStorage();
                renderRecordsList();
            });
        }

        function setDefaultDeadline() {
            const d = new Date();
            d.setDate(d.getDate() + 30);
            document.getElementById('input-deadline').value = d.toISOString().split('T')[0];
        }

        function setSpread(spreadType) {
            currentSpread = spreadType;
            if (spreadType === '3') currentSlotsCount = 3;
            else if (spreadType === '4') currentSlotsCount = 4;
            else if (spreadType === '5') currentSlotsCount = 5;
            else if (spreadType === '9') currentSlotsCount = 9;
            else if (spreadType === '36') currentSlotsCount = 36;

            document.querySelectorAll('.spread-btn').forEach(btn => {
                if(btn.dataset.spread === spreadType) {
                    btn.classList.add('border-antique-gold', 'bg-parchment-200', 'text-taupe-900', 'font-bold');
                    btn.classList.remove('border-parchment-300', 'bg-parchment-50', 'text-taupe-700');
                } else {
                    btn.classList.remove('border-antique-gold', 'bg-parchment-200', 'text-taupe-900', 'font-bold');
                    btn.classList.add('border-parchment-300', 'bg-parchment-50', 'text-taupe-700');
                }
            });

            const tableauPanel = document.getElementById('tableau-import-panel');
            if (spreadType === '36') {
                tableauPanel.classList.remove('hidden');
            } else {
                tableauPanel.classList.add('hidden');
            }

            cardAssignments = {};
            significatorSlots.clear();
            activeSelectedSlot = null;
            document.getElementById('current-selected-slot-label').innerText = "尚未選取 (請先點上方牌位)";

            renderSlotsContainer();
            updateSignificatorCounter();
        }

        function renderSlotsContainer() {
            const container = document.getElementById('card-slots-container');
            container.innerHTML = '';

            if (currentSpread === '36') {
                container.className = "flex flex-col items-center gap-2 p-2 sm:p-3 bg-white rounded-xl border border-parchment-300 max-h-[520px] overflow-y-auto overflow-x-auto shadow-inner w-full";
                
                let currentRowDiv = document.createElement('div');
                currentRowDiv.className = "grid grid-cols-4 sm:grid-cols-8 gap-1.5 sm:gap-2 w-full justify-center min-w-[360px]";
                
                for (let i = 0; i < 36; i++) {
                    if (i > 0 && i % 8 === 0) {
                        container.appendChild(currentRowDiv);
                        currentRowDiv = document.createElement('div');
                        if (i === 32) {
                            currentRowDiv.className = "grid grid-cols-2 sm:grid-cols-4 gap-1.5 sm:gap-2 w-3/4 sm:w-1/2 justify-center mx-auto pt-1.5 min-w-[200px]";
                        } else {
                            currentRowDiv.className = "grid grid-cols-4 sm:grid-cols-8 gap-1.5 sm:gap-2 w-full justify-center min-w-[360px]";
                        }
                    }

                    const slotEl = createCardSlotElement(i, currentSpread);
                    currentRowDiv.appendChild(slotEl);
                }
                container.appendChild(currentRowDiv);
                return;
            } else if (currentSpread === '9') {
                container.className = "grid grid-cols-3 gap-2.5 sm:gap-3 p-3 sm:p-4 bg-white rounded-xl border border-parchment-300 max-w-md mx-auto shadow-inner";
            } else {
                container.className = "flex flex-wrap gap-3 sm:gap-4 justify-center p-3 sm:p-4 bg-white rounded-xl border border-parchment-300 shadow-inner";
            }

            for (let i = 0; i < currentSlotsCount; i++) {
                const slotEl = createCardSlotElement(i, currentSpread);
                container.appendChild(slotEl);
            }
        }

        function createCardSlotElement(i, spreadType) {
            const assignedCardId = cardAssignments[i];
            const cardData = assignedCardId ? lenormandDeck.find(c => c.id === assignedCardId) : null;
            const isSig = significatorSlots.has(i);
            const isSelected = activeSelectedSlot === i;

            const slotEl = document.createElement('div');
            slotEl.className = `relative flex flex-col items-center justify-between rounded-xl border transition-all cursor-pointer select-none shadow-sm ${
                spreadType === '36' ? 'h-24 sm:h-28 p-1' : spreadType === '9' ? 'h-28 sm:h-32 p-1.5' : 'w-24 sm:w-28 h-36 sm:h-40 p-2'
            } ${
                isSelected ? 'border-antique-gold ring-2 ring-antique-gold/50 bg-parchment-200' : 
                isSig ? 'border-antique-gold card-glow-active bg-parchment-100' : 
                cardData ? 'border-parchment-300 bg-white hover:border-antique-gold' : 
                'border-dashed border-parchment-300 bg-parchment-50 hover:border-antique-gold'
            }`;

            slotEl.onclick = () => selectSlot(i);

            let contentHTML = `<span class="absolute top-1 left-1.5 text-[9px] sm:text-[10px] text-taupe-600 font-occult font-bold z-10">#${i+1}</span>`;
            
            if (isSig) {
                contentHTML += `<span class="absolute top-1 right-1.5 text-[9px] sm:text-[10px] text-antique-gold z-10"><i class="fa-solid fa-star"></i></span>`;
            }

            if (cardData) {
                if (spreadType === '36') {
                    contentHTML += `
                        <div class="w-8 h-8 sm:w-10 sm:h-10 my-auto">${cardData.svg}</div>
                        <div class="text-[9px] sm:text-[10px] font-occult text-taupe-900 font-semibold truncate w-full text-center">${cardData.id}.${cardData.name}</div>
                    `;
                } else if (spreadType === '9') {
                    contentHTML += `
                        <div class="w-10 h-10 sm:w-12 sm:h-12 my-auto">${cardData.svg}</div>
                        <div class="text-[10px] sm:text-xs font-occult text-taupe-900 font-bold truncate w-full text-center">${cardData.id}.${cardData.name}</div>
                    `;
                } else {
                    contentHTML += `
                        <div class="w-14 h-14 sm:w-18 sm:h-18 my-auto">${cardData.svg}</div>
                        <div class="text-xs sm:text-sm font-occult text-taupe-900 font-bold text-center">${cardData.id}. ${cardData.name}</div>
                        <div class="hidden sm:block text-[9px] text-taupe-600 truncate w-full text-center">${cardData.meaning.split(',')[0]}</div>
                    `;
                }
            } else {
                contentHTML += `
                    <div class="my-auto flex flex-col items-center justify-center text-taupe-600">
                        <i class="fa-solid fa-plus text-xs sm:text-sm"></i>
                        <span class="text-[9px] sm:text-[10px] mt-0.5">指派牌</span>
                    </div>
                `;
            }

            slotEl.innerHTML = contentHTML;
            return slotEl;
        }

        function selectSlot(index) {
            activeSelectedSlot = index;
            document.getElementById('current-selected-slot-label').innerText = `已選中牌位 #${index + 1}`;
            renderSlotsContainer();
        }

        function initQuickPicker() {
            const picker = document.getElementById('deck-quick-picker');
            picker.innerHTML = '';
            lenormandDeck.forEach(card => {
                const btn = document.createElement('button');
                btn.type = 'button';
                btn.className = "flex flex-col items-center justify-center p-2 rounded-xl bg-white border border-parchment-300 hover:border-antique-gold hover:bg-parchment-200 transition text-center shadow-xs space-y-1";
                btn.onclick = () => assignCardToActiveSlot(card.id);
                btn.innerHTML = `
                    <div class="w-8 h-8 sm:w-10 sm:h-10">${card.svg}</div>
                    <span class="text-[9px] sm:text-[10px] text-taupe-900 font-occult font-semibold truncate w-full">${card.id}.${card.name}</span>
                `;
                picker.appendChild(btn);
            });
        }

        function assignCardToActiveSlot(cardId) {
            if (activeSelectedSlot === null) {
                showToast("請先點選上方其中一個牌位格！", "error");
                return;
            }
            cardAssignments[activeSelectedSlot] = cardId;
            renderSlotsContainer();

            if (activeSelectedSlot < currentSlotsCount - 1) {
                activeSelectedSlot++;
                document.getElementById('current-selected-slot-label').innerText = `已選中牌位 #${activeSelectedSlot + 1}`;
            }
            renderSlotsContainer();
        }

        document.getElementById('card-slots-container').addEventListener('contextmenu', (e) => {
            e.preventDefault();
            const target = e.target.closest('div.relative');
            if (!target) return;
            const allSlots = Array.from(document.querySelectorAll('#card-slots-container div.relative'));
            const index = allSlots.indexOf(target);
            if (index !== -1) {
                toggleSignificator(index);
            }
        });

        function toggleSignificator(index) {
            if (significatorSlots.has(index)) {
                significatorSlots.delete(index);
            } else {
                if (significatorSlots.size >= 2) {
                    showToast("大藍圖或牌陣最多只能標記 2 張核心代表牌 (Significator)！", "error");
                    return;
                }
                significatorSlots.add(index);
            }
            updateSignificatorCounter();
            renderSlotsContainer();
        }

        function updateSignificatorCounter() {
            document.getElementById('active-significator-count').innerText = `${significatorSlots.size} / 2`;
        }

        function randomFillTableau() {
            let deckCopy = [...Array(36).keys()].map(i => i + 1);
            for (let i = deckCopy.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [deckCopy[i], deckCopy[j]] = [deckCopy[j], deckCopy[i]];
            }
            cardAssignments = {};
            for (let i = 0; i < 36; i++) {
                cardAssignments[i] = deckCopy[i];
            }
            renderSlotsContainer();
            showToast("已隨機洗牌並完美填滿 36 張大藍圖！", "success");
        }

        function parseTableauText() {
            const rawText = document.getElementById('tableau-paste-input').value.trim();
            const feedback = document.getElementById('import-feedback');
            if (!rawText) {
                feedback.innerHTML = `<span class="text-red-600 font-medium">請先輸入或貼上牌卡清單文字。</span>`;
                return;
            }

            const items = rawText.split(/[\n,\s、]+/).filter(item => item.trim() !== "");
            let assignedCount = 0;
            let errors = [];

            items.forEach((item, idx) => {
                if (idx >= 36) return;
                let cleanStr = item.replace(/^\d+[\.\-、\s]*/, "").trim();
                let foundCard = lenormandDeck.find(c => c.id == cleanStr || c.name === cleanStr || c.name.includes(cleanStr));
                if (foundCard) {
                    cardAssignments[idx] = foundCard.id;
                    assignedCount++;
                } else {
                    errors.push(`第 ${idx+1} 項("${item}")無法辨識`);
                }
            });

            renderSlotsContainer();
            if (errors.length > 0) {
                feedback.innerHTML = `<span class="text-amber-700 font-medium">成功帶入 ${assignedCount} 張牌。部分異常: ${errors.slice(0, 3).join(', ')}</span>`;
                showToast(`智慧解析完成，成功帶入 ${assignedCount} 張牌`, "success");
            } else {
                feedback.innerHTML = `<span class="text-antique-dark font-bold"><i class="fa-solid fa-circle-check"></i> 成功完美解析並帶入 36 張大藍圖 (8×4+4) 牌面！</span>`;
                showToast("大藍圖 36 張牌自動對號入座成功！", "success");
            }
        }

        async function handleFormSubmit(e) {
            e.preventDefault();
            const question = document.getElementById('input-question').value.trim();
            const tag = document.getElementById('input-tag').value;
            const deadline = document.getElementById('input-deadline').value;
            const prediction = document.getElementById('input-prediction').value.trim();
            const pairing = document.getElementById('input-pairing').value.trim();

            if (!question || !prediction) {
                showToast("請完整填寫問題與當下直覺預測！", "error");
                return;
            }

            if (Object.keys(cardAssignments).length === 0) {
                showToast("請至少配置一張雷諾曼牌卡！", "error");
                return;
            }

            const recordId = 'rec_' + Date.now();
            const newRecord = {
                createdAt: new Date().toISOString(),
                question: question,
                tag: tag,
                deadline: deadline,
                spreadType: currentSpread,
                cardAssignments: { ...cardAssignments },
                significatorSlots: Array.from(significatorSlots),
                prediction: prediction,
                pairing: pairing,
                status: 'Active',
                actualOutcome: '',
                rating: 0,
                reflection: '',
                reviewedAt: null,
                lastEditedCardsAt: new Date().toISOString()
            };

            try {
                if (db && userId) {
                    const docRef = doc(db, 'artifacts', appId, 'users', userId, 'records', recordId);
                    await setDoc(docRef, newRecord);
                } else {
                    newRecord.id = recordId;
                    recordsList.unshift(newRecord);
                    saveRecordsToLocalStorage();
                }
                showToast("占卜誓約與牌局配置已成功封存至雲端！", "success");
            } catch (err) {
                console.error("Cloud save failed:", err);
                showToast("雲端儲存失敗，已改存於本機", "error");
                newRecord.id = recordId;
                recordsList.unshift(newRecord);
                saveRecordsToLocalStorage();
            }
            
            document.getElementById('divination-form').reset();
            setSpread('3');
            setDefaultDeadline();
            switchTab('records');
        }

        function switchTab(tabName) {
            const divView = document.getElementById('view-divination');
            const recView = document.getElementById('view-records');
            const detailView = document.getElementById('view-detail');
            const analyticsView = document.getElementById('view-analytics');
            
            const divBtn = document.getElementById('nav-divination-btn');
            const recBtn = document.getElementById('nav-records-btn');
            const analyticsBtn = document.getElementById('nav-analytics-btn');

            divView.classList.add('hidden');
            recView.classList.add('hidden');
            detailView.classList.add('hidden');
            analyticsView.classList.add('hidden');

            divBtn.className = "px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm font-occult rounded-xl border border-parchment-300 text-taupe-700 hover:text-taupe-900 transition bg-white shadow-sm font-medium";
            recBtn.className = "px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm font-occult rounded-xl border border-parchment-300 text-taupe-700 hover:text-taupe-900 transition bg-white shadow-sm font-medium";
            analyticsBtn.className = "px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm font-occult rounded-xl border border-parchment-300 text-taupe-700 hover:text-taupe-900 transition bg-white shadow-sm font-medium";

            if (tabName === 'divination') {
                divView.classList.remove('hidden');
                divBtn.className = "px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm font-occult rounded-xl bg-antique-gold text-white font-bold transition shadow-md flex items-center space-x-1";
            } else if (tabName === 'records') {
                recView.classList.remove('hidden');
                recBtn.className = "px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm font-occult rounded-xl bg-antique-gold text-white font-bold transition shadow-md flex items-center space-x-1";
                renderRecordsList();
            } else if (tabName === 'detail') {
                detailView.classList.remove('hidden');
                recBtn.className = "px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm font-occult rounded-xl bg-antique-gold text-white font-bold transition shadow-md flex items-center space-x-1";
            } else if (tabName === 'analytics') {
                analyticsView.classList.remove('hidden');
                analyticsBtn.className = "px-2.5 py-1.5 sm:px-3.5 sm:py-2 text-xs sm:text-sm font-occult rounded-xl bg-antique-gold text-white font-bold transition shadow-md flex items-center space-x-1";
                renderAnalytics();
            }
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function updateRecordStatuses() {
            const today = new Date().toISOString().split('T')[0];
            recordsList.forEach(rec => {
                if (rec.status !== 'Archived') {
                    if (rec.deadline && rec.deadline < today && rec.rating === 0) {
                        rec.status = 'Due';
                    } else if (rec.rating > 0) {
                        rec.status = 'Active';
                    }
                }
            });
        }

        function renderRecordsList() {
            updateRecordStatuses();
            const keyword = document.getElementById('search-keyword').value.toLowerCase();
            const statusFilter = document.getElementById('filter-status').value;
            const tagFilter = document.getElementById('filter-tag').value;

            const grid = document.getElementById('records-grid');
            const emptyState = document.getElementById('empty-records-state');
            grid.innerHTML = '';

            const filtered = recordsList.filter(rec => {
                const matchKeyword = rec.question.toLowerCase().includes(keyword) || rec.prediction.toLowerCase().includes(keyword);
                const matchStatus = statusFilter === 'ALL' || rec.status === statusFilter;
                const matchTag = tagFilter === 'ALL' || rec.tag === tagFilter;
                return matchKeyword && matchStatus && matchTag;
            });

            document.getElementById('stats-total').innerText = recordsList.length;
            document.getElementById('record-count-badge').innerText = recordsList.length;

            if (filtered.length === 0) {
                emptyState.classList.remove('hidden');
                return;
            } else {
                emptyState.classList.add('hidden');
            }

            filtered.forEach(rec => {
                const cardEl = document.createElement('div');
                
                let statusBadgeHTML = '';
                let borderClass = 'border-parchment-300';
                if (rec.status === 'Due') {
                    statusBadgeHTML = `<span class="px-2 py-0.5 rounded text-[10px] bg-amber-100 text-amber-800 border border-amber-300 font-bold animate-pulse"><i class="fa-solid fa-bell"></i> 待驗證 (Due)</span>`;
                    borderClass = 'border-amber-400 card-glow';
                } else if (rec.status === 'Archived') {
                    statusBadgeHTML = `<span class="px-2 py-0.5 rounded text-[10px] bg-parchment-200 text-taupe-700 font-medium">長期封存</span>`;
                } else if (rec.rating > 0) {
                    statusBadgeHTML = `<span class="px-2 py-0.5 rounded text-[10px] bg-emerald-100 text-emerald-800 border border-emerald-300 font-medium"><i class="fa-solid fa-check"></i> 已復盤 (${rec.rating}⭐)</span>`;
                } else {
                    statusBadgeHTML = `<span class="px-2 py-0.5 rounded text-[10px] bg-parchment-100 text-antique-dark border border-antique-gold/30 font-bold">追蹤中 (Active)</span>`;
                }

                let previewCardsHTML = '';
                const assignedEntries = Object.entries(rec.cardAssignments);
                const previewLimit = rec.spreadType === '36' ? 6 : 3;
                assignedEntries.slice(0, previewLimit).forEach(([slotIdx, cardId]) => {
                    const cData = lenormandDeck.find(c => c.id === cardId);
                    if (cData) {
                        const isSig = rec.significatorSlots && rec.significatorSlots.includes(parseInt(slotIdx));
                        previewCardsHTML += `
                            <div class="px-2.5 py-1 bg-parchment-50 border ${isSig ? 'border-antique-gold text-antique-dark font-bold' : 'border-parchment-300 text-taupe-800'} rounded-lg text-[11px] font-occult flex items-center space-x-1.5 shadow-xs">
                                <div class="w-4 h-4">${cData.svg}</div>
                                <span class="truncate max-w-[60px] sm:max-w-[70px]">${cData.name}</span>
                                ${isSig ? '<i class="fa-solid fa-star text-[9px] text-antique-gold"></i>' : ''}
                            </div>
                        `;
                    }
                });

                cardEl.className = `bg-white border ${borderClass} rounded-2xl p-4 sm:p-5 shadow-sm transition hover:border-antique-gold flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4`;
                cardEl.innerHTML = `
                    <div class="space-y-2 flex-grow min-w-0 w-full">
                        <div class="flex flex-wrap items-center gap-1.5">
                            <span class="px-2 py-0.5 rounded text-[10px] bg-parchment-100 text-antique-dark font-occult border border-antique-gold/20 font-bold">${rec.tag}</span>
                            <span class="text-[11px] sm:text-xs text-taupe-600">${rec.createdAt.split('T')[0]}</span>
                            <span class="text-[11px] sm:text-xs text-taupe-600">驗證日: ${rec.deadline || '未設'}</span>
                            ${statusBadgeHTML}
                        </div>
                        <h4 class="font-occult font-bold text-sm sm:text-base text-taupe-900 hover:text-antique-dark cursor-pointer truncate" onclick="openDetailView('${rec.id}')">${rec.question}</h4>
                        <div class="flex flex-wrap gap-1.5 pt-1">
                            ${previewCardsHTML}
                            ${assignedEntries.length > previewLimit ? `<span class="text-[10px] text-taupe-600 self-center">+${assignedEntries.length - previewLimit} 張牌</span>` : ''}
                        </div>
                    </div>
                    <div class="flex items-center space-x-2 self-end sm:self-center flex-shrink-0 w-full sm:w-auto justify-end">
                        <button onclick="openDetailView('${rec.id}')" class="w-full sm:w-auto px-4 py-2 bg-parchment-100 hover:bg-parchment-200 border border-antique-gold/40 text-antique-dark rounded-xl text-xs font-occult font-bold transition flex items-center justify-center space-x-1.5 shadow-sm">
                            <i class="fa-solid fa-eye"></i>
                            <span>進入復盤</span>
                        </button>
                    </div>
                `;
                grid.appendChild(cardEl);
            });
        }

        function openDetailView(id) {
            currentEditingRecordId = id;
            const rec = recordsList.find(r => r.id === id);
            if (!rec) return;

            document.getElementById('detail-tag-badge').innerText = rec.tag;
            document.getElementById('detail-date-badge').innerText = rec.createdAt.replace('T', ' ').substring(0, 16);
            document.getElementById('detail-question-title').innerText = rec.question;
            
            const statusBadge = document.getElementById('detail-status-badge');
            if (rec.status === 'Archived') {
                statusBadge.className = "px-2 py-0.5 rounded text-[10px] bg-parchment-200 text-taupe-700 font-bold";
                statusBadge.innerText = "長期封存";
            } else if (rec.rating > 0) {
                statusBadge.className = "px-2 py-0.5 rounded text-[10px] bg-emerald-100 text-emerald-800 font-bold border border-emerald-300";
                statusBadge.innerText = `已完成復盤 (${rec.rating}⭐)`;
            } else {
                statusBadge.className = "px-2 py-0.5 rounded text-[10px] bg-parchment-100 text-antique-dark font-bold border border-antique-gold/30";
                statusBadge.innerText = "追蹤中 (Active)";
            }

            renderDetailCards(rec);

            document.getElementById('detail-prediction-text').innerText = rec.prediction;
            document.getElementById('detail-pairing-text').innerText = rec.pairing || "無特別筆記";

            document.getElementById('review-actual-input').value = rec.actualOutcome || '';
            document.getElementById('review-reflection-input').value = rec.reflection || '';
            setReviewRating(rec.rating || 0);

            const timestampEl = document.getElementById('detail-review-timestamp');
            if (rec.reviewedAt) {
                timestampEl.innerText = `復盤時間戳記: ${rec.reviewedAt.replace('T', ' ').substring(0, 16)}`;
            } else {
                timestampEl.innerText = "尚未蓋上復盤時間戳記";
            }

            switchTab('detail');
        }

        function renderDetailCards(rec) {
            const container = document.getElementById('detail-cards-display');
            container.innerHTML = '';

            const createdTime = new Date(rec.createdAt).getTime();
            const now = new Date().getTime();
            const hoursDiff = (now - createdTime) / (1000 * 60 * 60);
            const canEditCards = hoursDiff < 24;

            const bufferStatusEl = document.getElementById('detail-edit-buffer-status');
            if (canEditCards) {
                bufferStatusEl.innerHTML = `<span class="text-emerald-700 font-medium"><i class="fa-solid fa-clock"></i> 牌面 24h 編輯緩衝期內 (剩餘 ${Math.max(0, (24 - hoursDiff)).toFixed(1)} 小時)</span>`;
            } else {
                bufferStatusEl.innerHTML = `<span class="text-taupe-600">牌面配置已永久鎖定 (超過24小時)</span>`;
            }

            if (rec.spreadType === '36') {
                container.className = "flex flex-col items-center gap-2 p-2 sm:p-3 bg-parchment-50 rounded-xl border border-parchment-300 max-h-[480px] overflow-y-auto overflow-x-auto shadow-inner w-full";
                
                let currentRowDiv = document.createElement('div');
                currentRowDiv.className = "grid grid-cols-4 sm:grid-cols-8 gap-1.5 sm:gap-2 w-full justify-center min-w-[360px]";
                
                for (let i = 0; i < 36; i++) {
                    if (i > 0 && i % 8 === 0) {
                        container.appendChild(currentRowDiv);
                        currentRowDiv = document.createElement('div');
                        if (i === 32) {
                            currentRowDiv.className = "grid grid-cols-2 sm:grid-cols-4 gap-1.5 sm:gap-2 w-3/4 sm:w-1/2 justify-center mx-auto pt-1.5 min-w-[200px]";
                        } else {
                            currentRowDiv.className = "grid grid-cols-4 sm:grid-cols-8 gap-1.5 sm:gap-2 w-full justify-center min-w-[360px]";
                        }
                    }

                    const cardEl = createDetailCardSlot(rec, i, true);
                    currentRowDiv.appendChild(cardEl);
                }
                container.appendChild(currentRowDiv);
                return;
            }

            container.className = "flex flex-wrap gap-2.5 sm:gap-3 justify-center p-3 sm:p-4 bg-parchment-50 rounded-xl border border-parchment-300 shadow-inner";
            const totalSlots = parseInt(rec.spreadType);
            for (let i = 0; i < totalSlots; i++) {
                const cardEl = createDetailCardSlot(rec, i, false);
                container.appendChild(cardEl);
            }
        }

        function createDetailCardSlot(rec, i, isTableau) {
            const cardId = rec.cardAssignments[i];
            const cardData = cardId ? lenormandDeck.find(c => c.id === cardId) : null;
            const isSig = rec.significatorSlots && rec.significatorSlots.includes(i);

            const slotEl = document.createElement('div');
            slotEl.className = `flex flex-col items-center justify-between p-1.5 rounded-xl border shadow-xs ${
                isTableau ? 'h-24 sm:h-28 text-[9px]' : 'w-24 h-36 sm:w-28 sm:h-40 p-2'
            } ${
                isSig ? 'border-antique-gold card-glow-active bg-parchment-100' : 
                cardData ? 'border-parchment-300 bg-white' : 'border-dashed border-parchment-300 bg-parchment-50'
            }`;

            if (cardData) {
                slotEl.innerHTML = `
                    <span class="text-[8px] sm:text-[9px] text-taupe-600 font-bold self-start">#${i+1}</span>
                    <div class="${isTableau ? 'w-8 h-8 sm:w-10 sm:h-10 my-auto' : 'w-14 h-14 sm:w-18 sm:h-18 my-auto'}">${cardData.svg}</div>
                    <div class="font-occult text-taupe-900 font-bold truncate w-full text-center text-[9px] sm:text-xs">${cardData.name}</div>
                    ${isSig ? '<i class="fa-solid fa-star text-[8px] text-antique-gold absolute top-1 right-1"></i>' : ''}
                `;
            } else {
                slotEl.innerHTML = `
                    <span class="text-[8px] sm:text-[9px] text-taupe-600 font-bold self-start">#${i+1}</span>
                    <div class="text-taupe-600/40 text-[9px] sm:text-[10px] my-auto">無</div>
                    <div></div>
                `;
            }
            return slotEl;
        }

        function setReviewRating(rating) {
            currentReviewRating = rating;
            const stars = document.querySelectorAll('#star-rating-container i');
            stars.forEach((star, idx) => {
                if (idx < rating) {
                    star.className = "fa-solid fa-star text-base sm:text-lg cursor-pointer text-antique-gold transition";
                } else {
                    star.className = "fa-solid fa-star text-base sm:text-lg cursor-pointer text-taupe-300 hover:text-antique-dark transition";
                }
            });

            const labels = ["未評分", "1★ 擦身而過", "2★ 些許微光", "3★ 中度吻合", "4★ 高度靈犀", "5★ 命運神準奇蹟"];
            document.getElementById('rating-text-label').innerText = labels[rating] || "";
        }

        async function saveReviewData() {
            if (!currentEditingRecordId) return;
            const rec = recordsList.find(r => r.id === currentEditingRecordId);
            if (!rec) return;

            const actualOutcome = document.getElementById('review-actual-input').value.trim();
            const reflection = document.getElementById('review-reflection-input').value.trim();

            rec.actualOutcome = actualOutcome;
            rec.reflection = reflection;
            rec.rating = currentReviewRating;
            rec.reviewedAt = new Date().toISOString();
            rec.status = 'Active';

            try {
                if (db && userId) {
                    const docRef = doc(db, 'artifacts', appId, 'users', userId, 'records', rec.id);
                    await setDoc(docRef, rec);
                } else {
                    saveRecordsToLocalStorage();
                }
                showToast("復盤結果與時間戳記已成功封存！", "success");
            } catch (err) {
                console.error("Cloud review save failed:", err);
                showToast("雲端儲存失敗，已改存本機", "error");
                saveRecordsToLocalStorage();
            }

            openDetailView(rec.id);
        }

        async function toggleArchiveCurrentRecord() {
            if (!currentEditingRecordId) return;
            const rec = recordsList.find(r => r.id === currentEditingRecordId);
            if (!rec) return;

            if (rec.status === 'Archived') {
                rec.status = 'Active';
                showToast("已解除封存，恢復追蹤狀態", "success");
            } else {
                rec.status = 'Archived';
                showToast("已放入長期封存殿堂，釋放心理壓力", "success");
            }

            try {
                if (db && userId) {
                    const docRef = doc(db, 'artifacts', appId, 'users', userId, 'records', rec.id);
                    await setDoc(docRef, rec);
                } else {
                    saveRecordsToLocalStorage();
                }
            } catch (err) {
                saveRecordsToLocalStorage();
            }

            openDetailView(rec.id);
        }

        async function deleteCurrentRecord() {
            if (!confirm("確定要永久刪除這筆占卜與復盤紀錄嗎？此動作無法復原。")) return;
            const idToDelete = currentEditingRecordId;

            try {
                if (db && userId) {
                    const docRef = doc(db, 'artifacts', appId, 'users', userId, 'records', idToDelete);
                    await deleteDoc(docRef);
                } else {
                    recordsList = recordsList.filter(r => r.id !== idToDelete);
                    saveRecordsToLocalStorage();
                }
                switchTab('records');
                showToast("雲端紀錄已永久移除", "success");
            } catch (err) {
                showToast("刪除失敗", "error");
            }
        }

        function renderAnalytics() {
            const total = recordsList.length;
            const reviewedList = recordsList.filter(r => r.rating > 0);
            const reviewedCount = reviewedList.length;
            const unreviewedList = recordsList.filter(r => (!r.rating || r.rating === 0) && r.status !== 'Archived');
            const unreviewedCount = unreviewedList.length;
            
            const rate = total > 0 ? Math.round((reviewedCount / total) * 100) : 0;

            document.getElementById('stat-card-total').innerText = total;
            document.getElementById('stat-card-unreviewed').innerText = unreviewedCount;
            document.getElementById('stat-card-reviewed').innerText = reviewedCount;
            document.getElementById('stat-card-rate').innerText = rate + '%';

            document.getElementById('unreviewed-count-badge').innerText = unreviewedCount;
            
            const unreviewedContainer = document.getElementById('unreviewed-records-list');
            const emptyUnreviewedState = document.getElementById('empty-unreviewed-state');
            unreviewedContainer.innerHTML = '';

            if (unreviewedList.length === 0) {
                emptyUnreviewedState.classList.remove('hidden');
            } else {
                emptyUnreviewedState.classList.add('hidden');
                unreviewedList.forEach(rec => {
                    const itemEl = document.createElement('div');
                    itemEl.className = "flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2 p-3 bg-parchment-50 rounded-xl border border-parchment-300 hover:border-antique-gold transition";
                    itemEl.innerHTML = `
                        <div class="space-y-1 min-w-0">
                            <div class="flex items-center space-x-2">
                                <span class="px-2 py-0.2 text-[10px] bg-parchment-200 text-antique-dark font-bold rounded">${rec.tag}</span>
                                <span class="text-[11px] text-taupe-600">${rec.createdAt.split('T')[0]} 建立</span>
                            </div>
                            <h4 class="text-xs sm:text-sm font-occult font-bold text-taupe-900 truncate">${rec.question}</h4>
                        </div>
                        <button onclick="openDetailView('${rec.id}')" class="px-3 py-1.5 bg-antique-gold text-white rounded-xl text-xs font-occult font-bold hover:bg-antique-light transition shadow-sm flex-shrink-0 flex items-center space-x-1">
                            <i class="fa-solid fa-stamp"></i>
                            <span>前往填寫復盤</span>
                        </button>
                    `;
                    unreviewedContainer.appendChild(itemEl);
                });
            }

            const tagCounts = {};
            recordsList.forEach(r => {
                tagCounts[r.tag] = (tagCounts[r.tag] || 0) + 1;
            });

            const tagsContainer = document.getElementById('analytics-tags-container');
            tagsContainer.innerHTML = '';
            if (Object.keys(tagCounts).length === 0) {
                tagsContainer.innerHTML = `<p class="text-xs text-taupe-600">尚無標籤數據</p>`;
            } else {
                Object.entries(tagCounts).sort((a,b) => b[1] - a[1]).forEach(([tag, count]) => {
                    const pct = Math.round((count / total) * 100);
                    tagsContainer.innerHTML += `
                        <div class="space-y-1">
                            <div class="flex justify-between text-xs font-medium text-taupe-800">
                                <span>${tag}</span>
                                <span>${count} 筆 (${pct}%)</span>
                            </div>
                            <div class="w-full bg-parchment-200 rounded-full h-2 overflow-hidden">
                                <div class="bg-antique-gold h-2 rounded-full" style="width: ${pct}%"></div>
                            </div>
                        </div>
                    `;
                });
            }

            const cardCounts = {};
            recordsList.forEach(r => {
                if (r.cardAssignments) {
                    Object.values(r.cardAssignments).forEach(cId => {
                        cardCounts[cId] = (cardCounts[cId] || 0) + 1;
                    });
                }
            });

            const topCardsContainer = document.getElementById('analytics-topcards-container');
            topCardsContainer.innerHTML = '';
            const sortedCards = Object.entries(cardCounts).sort((a,b) => b[1] - a[1]).slice(0, 5);
            
            if (sortedCards.length === 0) {
                topCardsContainer.innerHTML = `<p class="text-xs text-taupe-600">尚無牌卡頻率數據</p>`;
            } else {
                sortedCards.forEach(([cId, count]) => {
                    const cardData = lenormandDeck.find(c => c.id == cId);
                    if (cardData) {
                        topCardsContainer.innerHTML += `
                            <div class="flex items-center justify-between p-2.5 bg-parchment-50 rounded-xl border border-parchment-300">
                                <div class="flex items-center space-x-3">
                                    <div class="w-8 h-8">${cardData.svg}</div>
                                    <span class="font-occult text-xs font-bold text-taupe-900">${cardData.id}. ${cardData.name}</span>
                                </div>
                                <span class="text-xs font-semibold text-antique-dark bg-white px-2 py-1 rounded border border-antique-gold/30">出現 ${count} 次</span>
                            </div>
                        `;
                    }
                });
            }
        }

        function saveRecordsToLocalStorage() {
            localStorage.setItem('aethelgard_lenormand_records', JSON.stringify(recordsList));
        }

        function loadRecordsFromLocalStorage() {
            const data = localStorage.getItem('aethelgard_lenormand_records');
            if (data) {
                try {
                    recordsList = JSON.parse(data);
                } catch(e) {
                    recordsList = [];
                }
            } else {
                recordsList = [
                    {
                        id: 'rec_sample_1',
                        createdAt: new Date(Date.now() - 86400000 * 5).toISOString(),
                        question: '近期靈性成長與內在覺察的方向指引為何？',
                        tag: '#靈性成長',
                        deadline: new Date(Date.now() + 86400000 * 10).toISOString().split('T')[0],
                        spreadType: '3',
                        cardAssignments: { 0: 16, 1: 5, 2: 33 },
                        significatorSlots: [1],
                        prediction: '星星(16)代表清晰指引與希望；樹木(5)象徵扎根與深層生命力；鑰匙(33)代表重要突破與解答。預示近期將有靈性上的深刻體悟。',
                        pairing: '星星 + 樹木 = 靈性扎根與願景實現；樹木 + 鑰匙 = 長期健康與核心解方。',
                        status: 'Active',
                        actualOutcome: '',
                        rating: 0,
                        reflection: '',
                        reviewedAt: null,
                        lastEditedCardsAt: new Date().toISOString()
                    }
                ];
                saveRecordsToLocalStorage();
            }
        }

        function openExportModal() {
            document.getElementById('export-modal').classList.remove('hidden');
        }

        function closeExportModal() {
            document.getElementById('export-modal').classList.add('hidden');
        }

        function exportDataJSON() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(recordsList, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", `Aethelgard_Lenormand_Cloud_Backup_${new Date().toISOString().split('T')[0]}.json`);
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
            showToast("完整 JSON 資料備份已成功下載！", "success");
        }

        async function importDataJSON() {
            const fileInput = document.getElementById('import-file-input');
            if (fileInput.files.length === 0) {
                showToast("請先選擇要還原的 JSON 備份檔案！", "error");
                return;
            }
            const file = fileInput.files[0];
            const reader = new FileReader();
            reader.onload = async function(e) {
                try {
                    const imported = JSON.parse(e.target.result);
                    if (Array.isArray(imported)) {
                        for (const rec of imported) {
                            if (!rec.id) rec.id = 'rec_' + Math.random().toString(36).substr(2, 9);
                            if (db && userId) {
                                const docRef = doc(db, 'artifacts', appId, 'users', userId, 'records', rec.id);
                                await setDoc(docRef, rec);
                            }
                        }
                        recordsList = imported;
                        if (!db) saveRecordsToLocalStorage();
                        renderRecordsList();
                        closeExportModal();
                        showToast(`成功還原並同步 ${imported.length} 筆占卜紀錄！`, "success");
                    } else {
                        showToast("JSON 檔案格式不符，無法解析。", "error");
                    }
                } catch(err) {
                    showToast("解析 JSON 檔案失敗，檔案可能損毀。", "error");
                }
            };
            reader.readAsText(file);
        }

        function showToast(message, type = 'success') {
            const toast = document.getElementById('toast-notification');
            const msgEl = document.getElementById('toast-message');
            const iconEl = document.getElementById('toast-icon');

            msgEl.innerText = message;
            if (type === 'error') {
                iconEl.className = "fa-solid fa-triangle-exclamation text-red-600 text-lg flex-shrink-0";
            } else {
                iconEl.className = "fa-solid fa-circle-check text-antique-gold text-lg flex-shrink-0";
            }

            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3500);
        }

        window.setSpread = setSpread;
        window.selectSlot = selectSlot;
        window.assignCardToActiveSlot = assignCardToActiveSlot;
        window.toggleSignificator = toggleSignificator;
        window.randomFillTableau = randomFillTableau;
        window.parseTableauText = parseTableauText;
        window.handleFormSubmit = handleFormSubmit;
        window.switchTab = switchTab;
        window.renderRecordsList = renderRecordsList;
        window.openDetailView = openDetailView;
        window.setReviewRating = setReviewRating;
        window.saveReviewData = saveReviewData;
        window.toggleArchiveCurrentRecord = toggleArchiveCurrentRecord;
        window.deleteCurrentRecord = deleteCurrentRecord;
        window.openExportModal = openExportModal;
        window.closeExportModal = closeExportModal;
        window.exportDataJSON = exportDataJSON;
        window.importDataJSON = importDataJSON;
    </script>
</body>
</html>
