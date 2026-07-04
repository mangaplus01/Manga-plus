<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
    <title>📚 Manga+ Premium</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, 'Segoe UI', system-ui, sans-serif;
            background: #0a0a0f;
            color: #e2e2e6;
            min-height: 100vh;
            padding: 16px;
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0 20px;
            flex-wrap: wrap;
            gap: 12px;
            position: sticky;
            top: 0;
            background: #0a0a0f;
            z-index: 50;
        }

        .logo {
            font-size: 24px;
            font-weight: 800;
            background: linear-gradient(135deg, #f472b6, #8b5cf6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .logo span {
            font-weight: 300;
            -webkit-text-fill-color: #6b7280;
        }

        .header-actions {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .premium-badge {
            background: linear-gradient(135deg, #f59e0b, #f472b6);
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 700;
            color: #fff;
            letter-spacing: 0.3px;
            cursor: pointer;
            border: none;
            white-space: nowrap;
        }

        .premium-badge.free {
            background: rgba(255, 255, 255, 0.06);
            color: #9ca3af;
        }

        .search-box {
            display: flex;
            gap: 8px;
            flex: 1;
            max-width: 380px;
            min-width: 160px;
        }

        .search-box input {
            flex: 1;
            padding: 10px 16px;
            background: rgba(255, 255, 255, 0.06);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 12px;
            color: #fff;
            font-size: 14px;
            transition: 0.2s;
        }

        .search-box input:focus {
            outline: none;
            border-color: #8b5cf6;
            background: rgba(255, 255, 255, 0.08);
        }

        .search-box input::placeholder {
            color: #4b5563;
        }

        .search-box button {
            padding: 10px 18px;
            background: linear-gradient(135deg, #8b5cf6, #6366f1);
            border: none;
            border-radius: 12px;
            color: #fff;
            font-weight: 600;
            cursor: pointer;
            font-size: 14px;
            transition: 0.2s;
            white-space: nowrap;
        }

        .search-box button:active {
            transform: scale(0.95);
        }

        .categories {
            display: flex;
            gap: 8px;
            overflow-x: auto;
            padding: 4px 0 20px;
            scrollbar-width: none;
            -webkit-overflow-scrolling: touch;
        }

        .categories::-webkit-scrollbar {
            display: none;
        }

        .cat-btn {
            padding: 6px 18px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.06);
            border-radius: 20px;
            color: #9ca3af;
            font-size: 13px;
            font-weight: 500;
            cursor: pointer;
            white-space: nowrap;
            transition: 0.2s;
        }

        .cat-btn.active {
            background: rgba(139, 92, 246, 0.2);
            border-color: #8b5cf6;
            color: #c4b5fd;
        }

        .cat-btn:active {
            transform: scale(0.95);
        }

        .premium-banner {
            background: linear-gradient(135deg, rgba(139, 92, 246, 0.1), rgba(244, 114, 182, 0.1));
            border: 1px solid rgba(139, 92, 246, 0.15);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 20px;
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            gap: 16px;
        }

        .premium-banner p {
            font-size: 14px;
            color: #c4b5fd;
            margin: 0;
        }

        .premium-banner p strong {
            color: #f472b6;
        }

        .plan-buttons {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }

        .btn-premium {
            border: none;
            padding: 10px 24px;
            border-radius: 12px;
            color: #fff;
            font-weight: 700;
            font-size: 14px;
            cursor: pointer;
            transition: 0.2s;
            text-decoration: none;
            display: inline-block;
        }

        .btn-premium:active {
            transform: scale(0.95);
        }

        .btn-premium.basic {
            background: linear-gradient(135deg, #6366f1, #8b5cf6);
        }

        .btn-premium.premium {
            background: linear-gradient(135deg, #f59e0b, #f472b6);
        }

        .btn-premium.manage {
            background: rgba(255, 255, 255, 0.1);
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 16px;
            padding: 8px 0 30px;
        }

        .manga-card {
            background: rgba(255, 255, 255, 0.03);
            border-radius: 16px;
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.04);
            transition: 0.25s;
            cursor: pointer;
            position: relative;
        }

        .manga-card:active {
            transform: scale(0.96);
        }

        .manga-card.locked::after {
            content: '🔒';
            position: absolute;
            top: 8px;
            right: 8px;
            font-size: 18px;
            background: rgba(0, 0, 0, 0.6);
            padding: 4px 8px;
            border-radius: 8px;
        }

        .manga-card.premium-unlocked {
            border-color: rgba(139, 92, 246, 0.3);
        }

        .manga-cover {
            width: 100%;
            aspect-ratio: 2/3;
            background: linear-gradient(145deg, #1a1a2e, #2a1a3e);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 48px;
            font-weight: 300;
            color: rgba(255, 255, 255, 0.1);
            position: relative;
        }

        .manga-cover .premium-tag {
            position: absolute;
            bottom: 8px;
            right: 8px;
            background: linear-gradient(135deg, #f59e0b, #f472b6);
            font-size: 9px;
            padding: 2px 10px;
            border-radius: 10px;
            color: #fff;
            font-weight: 700;
            letter-spacing: 0.3px;
        }

        .manga-info {
            padding: 12px 14px 14px;
        }

        .manga-title {
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 4px;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            overflow: hidden;
            line-height: 1.3;
        }

        .manga-meta {
            display: flex;
            justify-content: space-between;
            font-size: 11px;
            color: #6b7280;
        }

        .manga-meta .chap {
            color: #8b5cf6;
            font-weight: 500;
        }

        #reader {
            display: none;
            position: fixed;
            inset: 0;
            background: #0a0a0f;
            z-index: 1000;
            overflow-y: auto;
            padding: 16px;
            -webkit-overflow-scrolling: touch;
        }

        #reader.open {
            display: block;
        }

        .reader-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 0 16px;
            position: sticky;
            top: 0;
            background: #0a0a0f;
            z-index: 10;
        }

        .reader-header h2 {
            font-size: 18px;
            font-weight: 600;
        }

        .reader-header .close-btn {
            background: rgba(255, 255, 255, 0.06);
            border: none;
            color: #fff;
            font-size: 24px;
            width: 44px;
            height: 44px;
            border-radius: 12px;
            cursor: pointer;
            transition: 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .reader-header .close-btn:active {
            background: rgba(255, 255, 255, 0.12);
        }

        .reader-lock {
            text-align: center;
            padding: 80px 20px;
            color: #6b7280;
        }

        .reader-lock .lock-icon {
            font-size: 64px;
            display: block;
            margin-bottom: 16px;
        }

        .reader-lock h3 {
            color: #e2e2e6;
            margin-bottom: 8px;
        }

        .reader-lock p {
            font-size: 14px;
            margin-bottom: 20px;
        }

        .page-img {
            width: 100%;
            max-width: 800px;
            margin: 0 auto 8px;
            display: block;
            border-radius: 8px;
            background: #1a1a2e;
            min-height: 200px;
        }

        .reader-nav {
            display: flex;
            gap: 12px;
            justify-content: center;
            padding: 16px 0 30px;
            position: sticky;
            bottom: 0;
            background: #0a0a0f;
        }

        .reader-nav button {
            padding: 10px 28px;
            background: rgba(255, 255, 255, 0.06);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 12px;
            color: #fff;
            font-size: 14px;
            font-weight: 500;
            cursor: pointer;
            transition: 0.2s;
        }

        .reader-nav button:active {
            background: rgba(255, 255, 255, 0.12);
            transform: scale(0.95);
        }

        .reader-nav button:disabled {
            opacity: 0.3;
            cursor: not-allowed;
        }

        .toast {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.9);
            padding: 12px 24px;
            border-radius: 14px;
            color: #fff;
            font-size: 14px;
            z-index: 3000;
            display: none;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.06);
            max-width: 90%;
            text-align: center;
        }

        .toast.show {
            display: block;
            animation: slideUp 0.3s ease;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateX(-50%) translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateX(-50%) translateY(0);
            }
        }

        .empty {
            text-align: center;
            padding: 60px 20px;
            color: #4b5563;
            font-size: 15px;
        }

        .empty span {
            font-size: 48px;
            display: block;
            margin-bottom: 12px;
        }

        @media (max-width: 500px) {
            .header {
                flex-direction: column;
                align-items: stretch;
            }
            .search-box {
                max-width: 100%;
            }
            .grid {
                grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
                gap: 12px;
            }
            .manga-title {
                font-size: 13px;
            }
            .premium-banner {
                flex-direction: column;
                text-align: center;
            }
            .plan-buttons {
                justify-content: center;
            }
        }
    </style>
</head>
<body>

    <!-- ═══ TOAST ═══ -->
    <div id="toast" class="toast"></div>

    <!-- ═══ HEADER ═══ -->
    <div class="header">
        <div class="logo">📚 Manga<span>+</span></div>
        <div class="header-actions">
            <button class="premium-badge free" id="premiumStatusBtn">⭐ Free</button>
        </div>
        <div class="search-box">
            <input type="text" id="searchInput" placeholder="Search manga..." />
            <button id="searchBtn">🔍</button>
        </div>
    </div>

    <!-- ═══ CATEGORIES ═══ -->
    <div class="categories" id="categories">
        <button class="cat-btn active" data-cat="all">🔥 All</button>
        <button class="cat-btn" data-cat="action">⚔️ Action</button>
        <button class="cat-btn" data-cat="adventure">🗺️ Adventure</button>
        <button class="cat-btn" data-cat="comedy">😂 Comedy</button>
        <button class="cat-btn" data-cat="drama">🎭 Drama</button>
        <button class="cat-btn" data-cat="fantasy">🐉 Fantasy</button>
        <button class="cat-btn" data-cat="romance">💕 Romance</button>
        <button class="cat-btn" data-cat="sci-fi">🤖 Sci-Fi</button>
        <button class="cat-btn" data-cat="sports">🏀 Sports</button>
    </div>

    <!-- ═══ PREMIUM BANNER (Two Plans) ═══ -->
    <div class="premium-banner" id="premiumBanner">
        <p>🔓 <strong>Choose Your Plan</strong> — Unlock ALL manga!</p>
        <div class="plan-buttons">
            <a href="https://rzp.io/rzp/M6KAphX" target="_blank" class="btn-premium basic">
                ⭐ Basic — ₹49/mo
            </a>
            <a href="https://rzp.io/rzp/8cIIBwr" target="_blank" class="btn-premium premium">
                ⭐ Premium — ₹99/mo
            </a>
        </div>
    </div>

    <!-- ═══ MANGA GRID ═══ -->
    <div id="grid" class="grid"></div>

    <!-- ═══ READER ═══ -->
    <div id="reader">
        <div class="reader-header">
            <h2 id="readerTitle">Manga</h2>
            <button class="close-btn" id="closeReader">✕</button>
        </div>
        <div id="pagesContainer"></div>
        <div class="reader-nav">
            <button id="prevPage">◀ Prev</button>
            <span id="pageCounter" style="color:#6b7280;font-size:14px;display:flex;align-items:center;">1 / 1</span>
            <button id="nextPage">Next ▶</button>
        </div>
    </div>

    <script>
        // ────────────────────────────────────────────────────────
        //  📚 MANGA DATA
        // ────────────────────────────────────────────────────────
        const MANGA_DB = [
            { id: 1, title: "One Piece", category: "adventure", chapters: 1089, cover: "🏴‍☠️", pages: 12, premium: false },
            { id: 2, title: "Naruto", category: "action", chapters: 700, cover: "🍥", pages: 10, premium: false },
            { id: 3, title: "Bleach", category: "action", chapters: 686, cover: "⚔️", pages: 14, premium: false },
            { id: 4, title: "Attack on Titan", category: "action", chapters: 139, cover: "🏰", pages: 16, premium: false },
            { id: 5, title: "Death Note", category: "drama", chapters: 108, cover: "📓", pages: 8, premium: false },
            { id: 6, title: "Fullmetal Alchemist", category: "fantasy", chapters: 116, cover: "🔮", pages: 12,
            premium: false },
            { id: 7, title: "Dragon Ball Z", category: "action", chapters: 519, cover: "🐉", pages: 14, premium: false },
            { id: 8, title: "Demon Slayer", category: "fantasy", chapters: 205, cover: "🗡️", pages: 10, premium: false },
            { id: 9, title: "My Hero Academia", category: "action", chapters: 410, cover: "🦸", pages: 12,
            premium: false },
            { id: 10, title: "One Punch Man", category: "comedy", chapters: 198, cover: "👊", pages: 9, premium: false },
            { id: 11, title: "Tokyo Ghoul", category: "drama", chapters: 179, cover: "👁️", pages: 11, premium: false },
            { id: 12, title: "Jujutsu Kaisen", category: "fantasy", chapters: 248, cover: "🔮", pages: 13,
            premium: false },
            { id: 13, title: "Chainsaw Man", category: "action", chapters: 167, cover: "⛓️", pages: 10, premium: false },
            { id: 14, title: "Haikyuu!!", category: "sports", chapters: 402, cover: "🏐", pages: 8, premium: false },
            { id: 15, title: "Slam Dunk", category: "sports", chapters: 276, cover: "🏀", pages: 10, premium: false },
            { id: 16, title: "Hunter x Hunter", category: "adventure", chapters: 400, cover: "🎯", pages: 14,
            premium: false },
            { id: 17, title: "Fairy Tail", category: "fantasy", chapters: 545, cover: "🔥", pages: 12, premium: false },
            { id: 18, title: "Gintama", category: "comedy", chapters: 704, cover: "🤣", pages: 15, premium: false },
            { id: 19, title: "Vinland Saga", category: "adventure", chapters: 208, cover: "⚔️", pages: 14,
            premium: true },
            { id: 20, title: "Berserk", category: "drama", chapters: 373, cover: "🗡️", pages: 18, premium: true },
            { id: 21, title: "Sword Art Online", category: "sci-fi", chapters: 180, cover: "🎮", pages: 10,
            premium: true },
            { id: 22, title: "Steins;Gate", category: "sci-fi", chapters: 56, cover: "⏳", pages: 8, premium: true },
            { id: 23, title: "Kaguya-sama", category: "comedy", chapters: 281, cover: "💕", pages: 7, premium: true },
            { id: 24, title: "Rent-A-Girlfriend", category: "romance", chapters: 336, cover: "💖", pages: 8,
            premium: true },
            { id: 25, title: "Horimiya", category: "romance", chapters: 122, cover: "❤️", pages: 7, premium: true },
            { id: 26, title: "Dr. Stone", category: "sci-fi", chapters: 232, cover: "🧪", pages: 11, premium: true },
            { id: 27, title: "Fire Force", category: "fantasy", chapters: 304, cover: "🔥", pages: 12, premium: true },
            { id: 28, title: "Black Clover", category: "fantasy", chapters: 373, cover: "📖", pages: 13, premium: true },
            { id: 29, title: "Boruto", category: "adventure", chapters: 80, cover: "🍥", pages: 9, premium: true },
            { id: 30, title: "Blue Lock", category: "sports", chapters: 267, cover: "⚽", pages: 10, premium: true },
            { id: 31, title: "Vagabond", category: "drama", chapters: 327, cover: "🗡️", pages: 16, premium: true },
            { id: 32, title: "Monster", category: "drama", chapters: 162, cover: "🔪", pages: 14, premium: true },
            { id: 33, title: "20th Century Boys", category: "sci-fi", chapters: 249, cover: "👾", pages: 15,
            premium: true },
            { id: 34, title: "Pluto", category: "sci-fi", chapters: 65, cover: "🤖", pages: 10, premium: true },
            { id: 35, title: "Goodnight Punpun", category: "drama", chapters: 147, cover: "🐦", pages: 12,
            premium: true },
        ];

        // ────────────────────────────────────────────────────────
        //  🧠 STATE
        // ────────────────────────────────────────────────────────
        let isPremium = localStorage.getItem('manga_premium') === 'true';
        let currentManga = null;
        let currentPage = 0;
        let totalPages = 0;
        let currentCategory = 'all';

        const gridEl = document.getElementById('grid');
        const searchInput = document.getElementById('searchInput');
        const searchBtn = document.getElementById('searchBtn');
        const categoriesEl = document.getElementById('categories');
        const readerEl = document.getElementById('reader');
        const readerTitle = document.getElementById('readerTitle');
        const pagesContainer = document.getElementById('pagesContainer');
        const prevBtn = document.getElementById('prevPage');
        const nextBtn = document.getElementById('nextPage');
        const pageCounter = document.getElementById('pageCounter');
        const closeReader = document.getElementById('closeReader');
        const premiumStatusBtn = document.getElementById('premiumStatusBtn');
        const premiumBanner = document.getElementById('premiumBanner');
        const toast = document.getElementById('toast');

        // ────────────────────────────────────────────────────────
        //  🍞 TOAST
        // ────────────────────────────────────────────────────────
        function showToast(msg) {
            toast.textContent = msg;
            toast.className = 'toast show';
            clearTimeout(toast._timer);
            toast._timer = setTimeout(() => {
                toast.className = 'toast';
            }, 3000);
        }

        // ────────────────────────────────────────────────────────
        //  📖 RENDER GRID
        // ────────────────────────────────────────────────────────
        function renderGrid(mangaList) {
            if (!mangaList || mangaList.length === 0) {
                gridEl.innerHTML = `<div class="empty"><span>🔍</span>No manga found 😢</div>`;
                return;
            }

            gridEl.innerHTML = mangaList.map(m => `
                    <div class="manga-card ${!isPremium && m.premium ? 'locked' : ''} ${isPremium && m.premium ? 'premium-unlocked' : ''}" data-id="${m.id}">
                        <div class="manga-cover">
                            ${m.cover}
                            ${m.premium ? '<span class="premium-tag">⭐ PREMIUM</span>' : ''}
                        </div>
                        <div class="manga-info">
                            <div class="manga-title">${m.title}</div>
                            <div class="manga-meta">
                                <span>${m.category}</span>
                                <span class="chap">📖 ${m.chapters} ch</span>
                            </div>
                        </div>
                    </div>
                `).join('');

            document.querySelectorAll('.manga-card').forEach(el => {
                el.addEventListener('click', () => {
                    const id = parseInt(el.dataset.id);
                    const manga = MANGA_DB.find(m => m.id === id);
                    if (manga) {
                        if (manga.premium && !isPremium) {
                            showToast('🔒 Subscribe to unlock premium manga!');
                            return;
                        }
                        openReader(manga);
                    }
                });
            });
        }

        // ────────────────────────────────────────────────────────
        //  🔍 FILTER
        // ────────────────────────────────────────────────────────
        function filterManga() {
            const query = searchInput.value.toLowerCase().trim();
            let filtered = MANGA_DB;

            if (currentCategory !== 'all') {
                filtered = filtered.filter(m => m.category === currentCategory);
            }

            if (query) {
                filtered = filtered.filter(m => m.title.toLowerCase().includes(query));
            }

            renderGrid(filtered);
        }

        // ────────────────────────────────────────────────────────
        //  📚 OPEN READER
        // ────────────────────────────────────────────────────────
        function openReader(manga) {
            currentManga = manga;
            currentPage = 0;
            totalPages = manga.pages || 10;
            readerTitle.textContent = `${manga.title}`;
            readerEl.classList.add('open');
            document.body.style.overflow = 'hidden';
            renderPages();
            updateNav();
        }

        function renderPages() {
            const colors = ['#1a1a2e', '#16213e', '#0f3460', '#1a1a3e', '#2a1a3e', '#1a2a3e', '#3e1a2e', '#2e1a3e'];

            let html = '';
            for (let i = 0; i < totalPages; i++) {
                const color = colors[i % colors.length];
                html += `
                        <div class="page-img" data-index="${i}">
                            <div style="width:100%;aspect-ratio:2/3;background:${color};border-radius:8px;display:flex;align-items:center;justify-content:center;flex-direction:column;color:rgba(255,255,255,0.2);font-size:60px;font-weight:300;">
                                📖
                                <span style="font-size:16px;margin-top:8px;">Page ${i+1}</span>
                                <span style="font-size:12px;color:rgba(255,255,255,0.08);">${currentManga.title}</span>
                            </div>
                        </div>
                    `;
            }
            pagesContainer.innerHTML = html;
            updateNav();
        }

        function updateNav() {
            pageCounter.textContent = `${currentPage + 1} / ${totalPages}`;
            prevBtn.disabled = currentPage === 0;
            nextBtn.disabled = currentPage === totalPages - 1;

            document.querySelectorAll('.page-img').forEach(el => {
                const idx = parseInt(el.dataset.index);
                const distance = Math.abs(idx - currentPage);
                el.style.display = distance < 3 ? 'block' : 'none';
            });

            readerEl.scrollTop = 0;
        }

        function goToPage(delta) {
            const newPage = currentPage + delta;
            if (newPage < 0 || newPage >= totalPages) return;
            currentPage = newPage;
            updateNav();
        }

        // ────────────────────────────────────────────────────────
        //  🎨 UPDATE UI
        // ────────────────────────────────────────────────────────
        function updatePremiumUI() {
            if (isPremium) {
                premiumStatusBtn.textContent = '⭐ Premium';
                premiumStatusBtn.className = 'premium-badge';
                premiumBanner.innerHTML = `
                        <p>✅ <strong>You're Premium!</strong> Enjoy all manga.</p>
                        <div style="display: flex; gap: 12px; flex-wrap: wrap;">
                            <span style="color: #6b7280; font-size: 14px;">Active plan: ₹99/mo</span>
                            <a href="https://rzp.io/rzp/8cIIBwr" target="_blank" class="btn-premium manage">
                                📧 Manage
                            </a>
                        </div>
                    `;
                premiumBanner.style.display = 'flex';
                showToast('🎉 Welcome back, Premium user!');
            } else {
                premiumStatusBtn.textContent = '⭐ Free';
                premiumStatusBtn.className = 'premium-badge free';
                premiumBanner.innerHTML = `
                        <p>🔓 <strong>Choose Your Plan</strong> — Unlock ALL manga!</p>
                        <div class="plan-buttons">
                            <a href="https://rzp.io/rzp/M6KAphX" target="_blank" class="btn-premium basic">
                                ⭐ Basic — ₹49/mo
                            </a>
                            <a href="https://rzp.io/rzp/8cIIBwr" target="_blank" class="btn-premium premium">
                                ⭐ Premium — ₹99/mo
                            </a>
                        </div>
                    `;
                premiumBanner.style.display = 'flex';
            }
            filterManga();
        }

        // ────────────────────────────────────────────────────────
        //  🔓 SIMULATE PREMIUM
        // ────────────────────────────────────────────────────────
        function activatePremium() {
            isPremium = true;
            localStorage.setItem('manga_premium', 'true');
            updatePremiumUI();
            showToast('✅ Premium activated! All manga unlocked! 🎉');
        }

        // ────────────────────────────────────────────────────────
        //  🎮 EVENT LISTENERS
        // ────────────────────────────────────────────────────────

        searchBtn.addEventListener('click', filterManga);
        searchInput.addEventListener('keyup', (e) => {
            if (e.key === 'Enter') filterManga();
        });

        categoriesEl.addEventListener('click', (e) => {
            const btn = e.target.closest('.cat-btn');
            if (!btn) return;
            document.querySelectorAll('.cat-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            currentCategory = btn.dataset.cat;
            filterManga();
        });

        prevBtn.addEventListener('click', () => goToPage(-1));
        nextBtn.addEventListener('click', () => goToPage(1));

        document.addEventListener('keydown', (e) => {
            if (!readerEl.classList.contains('open')) return;
            if (e.key === 'ArrowLeft') goToPage(-1);
            if (e.key === 'ArrowRight') goToPage(1);
            if (e.key === 'Escape') closeReader.click();
        });

        let touchStartX = 0;
        readerEl.addEventListener('touchstart', (e) => {
            touchStartX = e.changedTouches[0].screenX;
        });
        readerEl.addEventListener('touchend', (e) => {
            if (!readerEl.classList.contains('open')) return;
            const diff = touchStartX - e.changedTouches[0].screenX;
            if (Math.abs(diff) > 50) {
                goToPage(diff > 0 ? 1 : -1);
            }
        });

        closeReader.addEventListener('click', () => {
            readerEl.classList.remove('open');
            document.body.style.overflow = '';
        });

        // ────────────────────────────────────────────────────────
        //  🚀 INIT
        // ────────────────────────────────────────────────────────

        const urlParams = new URLSearchParams(window.location.search);
        if (urlParams.get('premium') === 'true') {
            activatePremium();
        }

        window.addEventListener('message', (event) => {
            if (event.data && event.data.premium === true) {
                activatePremium();
            }
        });

        updatePremiumUI();
        renderGrid(MANGA_DB);

        console.log('📚 Manga+ loaded with TWO plans!');
        console.log('🔗 Basic (₹49): https://rzp.io/rzp/M6KAphX');
        console.log('🔗 Premium (₹99): https://rzp.io/rzp/8cIIBwr');
        console.log('💡 To test premium, add ?premium=true to URL');
    </script>
</body>
</html>
