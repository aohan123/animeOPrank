[oprank.index.html](https://github.com/user-attachments/files/26859737/oprank.index.html)

<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>🎵 动画OP大赏 · 排行榜</title>
    <script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #f9f3e6 0%, #ffe6cc 100%);
            font-family: 'Segoe UI', 'Helvetica Neue', system-ui, sans-serif;
            padding: 2rem 1.5rem;
            color: #2c241a;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            margin-bottom: 2rem;
        }

        .header h1 {
            font-size: 2.5rem;
            background: linear-gradient(135deg, #e65c00, #ff9a3c);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
        }

        .badge-info {
            background: #fce5c1;
            display: inline-block;
            padding: 0.2rem 1rem;
            border-radius: 40px;
            font-size: 0.85rem;
            margin-top: 0.5rem;
        }

        .search-section {
            background: rgba(255, 248, 235, 0.9);
            border-radius: 56px;
            padding: 0.2rem;
            max-width: 700px;
            margin: 0 auto 2rem auto;
            box-shadow: 0 8px 20px rgba(0,0,0,0.08);
            position: relative;
        }
        .search-wrapper {
            display: flex;
            background: white;
            border-radius: 56px;
            overflow: hidden;
            border: 1px solid #ffd8ae;
        }
        .search-wrapper input {
            flex: 1;
            padding: 1rem 1.5rem;
            border: none;
            outline: none;
            font-size: 1rem;
        }
        .search-wrapper button {
            background: #ff8c42;
            border: none;
            padding: 0 1.8rem;
            color: white;
            font-weight: bold;
            cursor: pointer;
        }
        .search-results {
            position: absolute;
            background: white;
            border-radius: 28px;
            max-height: 380px;
            overflow-y: auto;
            z-index: 100;
            display: none;
            width: calc(100% - 2rem);
            left: 1rem;
            box-shadow: 0 12px 28px rgba(0,0,0,0.2);
        }
        .search-results.show { display: block; }
        .result-item {
            display: flex;
            gap: 14px;
            padding: 12px 20px;
            cursor: pointer;
            border-bottom: 1px solid #f7e9db;
        }
        .result-item:hover { background: #fff2e4; }
        .result-img {
            width: 48px;
            height: 68px;
            object-fit: cover;
            border-radius: 8px;
        }

        .selection-header {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            flex-wrap: wrap;
            margin: 1.5rem 0 1rem;
            border-bottom: 2px dashed #ffd2a5;
            padding-bottom: 0.75rem;
        }
        .counter {
            background: #ffdec2;
            padding: 0.3rem 1rem;
            border-radius: 60px;
            font-weight: bold;
        }
        .anime-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 1.5rem;
            margin: 1.5rem 0 1.5rem;
        }

        .anime-card {
            background: white;
            border-radius: 28px;
            overflow: hidden;
            box-shadow: 0 8px 18px rgba(0,0,0,0.08);
            border: 1px solid #ffe0bd;
            display: flex;
            flex-direction: column;
        }
        .rank-control {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: #fff7ef;
            padding: 8px 16px;
            border-bottom: 1px solid #ffebd2;
        }
        .rank-number {
            font-weight: 800;
            font-size: 1.3rem;
            background: #ffb470;
            color: white;
            width: 38px;
            height: 38px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            border-radius: 60px;
            box-shadow: inset 0 -1px 0 rgba(0,0,0,0.1);
        }
        .move-buttons {
            display: flex;
            gap: 10px;
        }
        .move-btn {
            background: #f0e1cf;
            border: none;
            padding: 5px 12px;
            border-radius: 30px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.8rem;
            transition: 0.1s;
        }
        .move-btn:hover { background: #e6cdb2; }
        .card-media {
            display: flex;
            gap: 14px;
            padding: 1rem;
        }
        .card-cover {
            width: 80px;
            height: 110px;
            object-fit: cover;
            border-radius: 14px;
        }
        .card-info {
            flex: 1;
        }
        .card-info h3 {
            font-size: 1rem;
            font-weight: 800;
            margin-bottom: 6px;
        }
        select {
            width: 100%;
            margin-top: 6px;
            padding: 8px;
            border-radius: 40px;
            border: 1px solid #ffcf9a;
            background: #fffaf2;
        }
        .delete-btn {
            background: #fae1cf;
            border: none;
            color: #b1511a;
            padding: 6px 12px;
            border-radius: 60px;
            margin: 0 12px 12px auto;
            cursor: pointer;
            width: fit-content;
        }

        .action-bar {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
            margin: 1rem 0 1.5rem;
        }
        .primary-btn, .rank-btn {
            border: none;
            padding: 0.8rem 1.8rem;
            font-weight: bold;
            border-radius: 60px;
            cursor: pointer;
            font-size: 1rem;
            transition: 0.1s;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        .primary-btn {
            background: #ff7b2c;
            color: white;
        }
        .rank-btn {
            background: #9b6a3e;
            color: white;
        }
        .primary-btn:active, .rank-btn:active { transform: scale(0.97); }
        .disabled-btn {
            opacity: 0.5;
            pointer-events: none;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 2000;
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(4px);
        }
        .modal-content {
            background: #fffaf2;
            width: 90%;
            max-width: 1000px;
            max-height: 85vh;
            border-radius: 48px;
            padding: 1.5rem;
            overflow: auto;
            position: relative;
            box-shadow: 0 25px 40px rgba(0,0,0,0.3);
        }
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid #ffdebc;
            padding-bottom: 12px;
            margin-bottom: 20px;
        }
        .close-modal {
            font-size: 2rem;
            cursor: pointer;
            font-weight: bold;
            background: none;
            border: none;
        }
        .rank-table {
            width: 100%;
            border-collapse: collapse;
        }
        .rank-table th, .rank-table td {
            padding: 12px 8px;
            text-align: left;
            border-bottom: 1px solid #f0e0ce;
            vertical-align: middle;
        }
        .rank-table th {
            background: #ffefdf;
            position: sticky;
            top: 0;
        }
        .rank-cover {
            width: 48px;
            height: 64px;
            object-fit: cover;
            border-radius: 8px;
        }
        .footer {
            text-align: center;
            font-size: 0.7rem;
            margin-top: 2rem;
            color: #b48b5a;
        }
        @media (max-width: 680px) {
            .anime-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>
<div class="container">
    <div class="header">
        <h1>🎶 动画OP大赏 · 排行榜</h1>
        <div class="badge-info">✨ 为动画排序(1最爱) → 上传榜单 → 影响全站OP人气榜 ✨</div>
    </div>

    <div class="search-section">
        <div class="search-wrapper">
            <input type="text" id="searchInput" placeholder="🔍 搜索动画 (仅限英文名！国漫可以试试拼音)" autocomplete="off">
            <button id="searchBtn">搜 索</button>
        </div>
        <div id="searchResults" class="search-results"></div>
    </div>

    <div class="selection-header">
        <h2>🎵 我的OP歌单 <span style="font-size:0.8rem;">(可拖拽排序↑↓)</span></h2>
        <div class="counter"><span id="selectedCount">0</span> / 9 (最少3部)</div>
    </div>

    <div id="animeListContainer" class="anime-grid"></div>

    <div class="action-bar">
        <button id="uploadRankBtn" class="primary-btn">📤 上传我的选择 → 更新排行榜</button>
        <button id="viewRankBtn" class="rank-btn">🏆 查看全站OP排行榜</button>
        <button id="generateBtn" class="primary-btn">📸 生成分享图片</button>
    </div>
    <div class="footer">
        ※ 通过上下按钮调整动画排名 (第1名为最爱)，上传后每个OP的人气+1，平均排名根据所有用户的排名位置计算。<br>
        💡 同一动画的不同OP可以分别添加多次，但同一动画的同一OP不能重复出现在列表中。
    </div>
</div>

<div id="rankModal" class="modal">
    <div class="modal-content">
        <div class="modal-header">
            <h2>🏅 OP人气总榜 (平均排名↓ & 总人气↑)</h2>
            <button class="close-modal" id="closeRankModal">&times;</button>
        </div>
        <div id="rankTableContainer">
            <table class="rank-table" id="rankTable">
                <thead>
                    <tr><th>动画 & 封面</th><th>OP名</th><th>平均排名</th><th>总人气</th></tr>
                </thead>
                <tbody id="rankTbody"></tbody>
            </table>
        </div>
    </div>
</div>

<script>
    (function(){
        // ---------- 全局变量 ----------
        let selectedAnimes = [];      // 存储 { uid, id, title, imageUrl, openingsList, selectedOp }
        let nextUid = 1;
        const JIKAN_API = 'https://api.jikan.moe/v4';
        let debounceTimer;

        // DOM 元素
        const searchInput = document.getElementById('searchInput');
        const searchBtn = document.getElementById('searchBtn');
        const resultsDiv = document.getElementById('searchResults');
        const animeContainer = document.getElementById('animeListContainer');
        const selectedCountSpan = document.getElementById('selectedCount');
        const generateBtn = document.getElementById('generateBtn');
        const uploadRankBtn = document.getElementById('uploadRankBtn');
        const viewRankBtn = document.getElementById('viewRankBtn');
        const rankModal = document.getElementById('rankModal');
        const closeRankModal = document.getElementById('closeRankModal');

        // 排行榜存储 KEY
        const RANK_STORAGE_KEY = 'anime_op_rankings_v2';
        const DEVICE_ID_KEY = 'anime_op_device_id';

        // 获取或生成设备唯一ID
        function getDeviceId() {
            let deviceId = localStorage.getItem(DEVICE_ID_KEY);
            if (!deviceId) {
                deviceId = 'dev_' + Date.now() + '_' + Math.random().toString(36).substr(2, 8);
                localStorage.setItem(DEVICE_ID_KEY, deviceId);
            }
            return deviceId;
        }

        // 获取所有排行榜记录
        function getAllRankRecords() {
            const stored = localStorage.getItem(RANK_STORAGE_KEY);
            if (!stored) return [];
            try {
                return JSON.parse(stored);
            } catch(e) { return []; }
        }

        // 保存排行榜记录（完全替换该设备的所有记录）
        function saveUserRanking(rankingList) {
            const deviceId = getDeviceId();
            let allRecords = getAllRankRecords();
            // 删除该设备之前的所有记录
            allRecords = allRecords.filter(rec => rec.deviceId !== deviceId);
            // 添加新记录，每条记录附带 deviceId
            const newRecords = rankingList.map(item => ({
                ...item,
                deviceId: deviceId,
                timestamp: Date.now()
            }));
            allRecords.push(...newRecords);
            localStorage.setItem(RANK_STORAGE_KEY, JSON.stringify(allRecords));
        }

        // 上传前的重复检查：列表中不能有相同的 (动画ID + OP名)
        function hasDuplicateAnimeOp() {
            const seen = new Set();
            for (let ani of selectedAnimes) {
                const key = `${ani.id}|${ani.selectedOp}`;
                if (seen.has(key)) return true;
                seen.add(key);
            }
            return false;
        }

        // 计算排行榜聚合数据
        function computeLeaderboard() {
            const records = getAllRankRecords();
            const map = new Map(); // key: `${animeId}|${opName}`
            for (let rec of records) {
                const key = `${rec.animeId}|${rec.opName}`;
                if (!map.has(key)) {
                    map.set(key, {
                        animeId: rec.animeId,
                        animeTitle: rec.animeTitle,
                        animeImage: rec.animeImage,
                        opName: rec.opName,
                        totalRank: rec.rank,
                        count: 1
                    });
                } else {
                    const entry = map.get(key);
                    entry.totalRank += rec.rank;
                    entry.count += 1;
                }
            }
            const result = [];
            for (let entry of map.values()) {
                const avgRank = entry.totalRank / entry.count;
                result.push({
                    animeId: entry.animeId,
                    animeTitle: entry.animeTitle,
                    animeImage: entry.animeImage,
                    opName: entry.opName,
                    avgRank: avgRank,
                    totalPopularity: entry.count
                });
            }
            // 排序: 总人气降序，平均排名升序
            result.sort((a,b) => {
                if (a.totalPopularity !== b.totalPopularity) return b.totalPopularity - a.totalPopularity;
                return a.avgRank - b.avgRank;
            });
            return result;
        }

        function renderRankModal() {
            const leaderboard = computeLeaderboard();
            const tbody = document.getElementById('rankTbody');
            if (!tbody) return;
            if (leaderboard.length === 0) {
                tbody.innerHTML = '<tr><td colspan="4" style="text-align:center;">📭 暂无排行榜数据，快上传你的榜单吧！</td></tr>';
                return;
            }
            let html = '';
            for (let item of leaderboard) {
                html += `
                    <tr>
                        <td style="display: flex; align-items: center; gap: 10px;">
                            <img class="rank-cover" src="${item.animeImage}" onerror="this.src='https://via.placeholder.com/48x64'">
                            <strong>${escapeHtml(item.animeTitle)}</strong>
                        </td>
                        <td>🎵 ${escapeHtml(item.opName)}</td>
                        <td>${item.avgRank.toFixed(2)}</td>
                        <td>🔥 ${item.totalPopularity}</td>
                    </tr>
                `;
            }
            tbody.innerHTML = html;
        }

        // 上传当前榜单
        function uploadCurrentSelection() {
            const len = selectedAnimes.length;
            if (len < 3 || len > 9) {
                alert(`请选择3~9部动画，当前数量: ${len}`);
                return;
            }
            // 检查每个动画是否已选择有效OP
            for (let i = 0; i < selectedAnimes.length; i++) {
                const ani = selectedAnimes[i];
                if (!ani.selectedOp || ani.selectedOp === '加载OP中...' || ani.openingsList.length === 0) {
                    alert(`动画「${ani.title}」未选择有效OP，请在下拉框中选择主题曲`);
                    return;
                }
            }
            // 检查是否有重复的 (动画ID + OP名)
            if (hasDuplicateAnimeOp()) {
                alert('❌ 列表中存在相同的动画和OP组合！每个动画的同一OP只能出现一次。请删除重复项后再上传。');
                return;
            }

            const rankingToUpload = [];
            for (let i = 0; i < selectedAnimes.length; i++) {
                const ani = selectedAnimes[i];
                const rank = i + 1;
                rankingToUpload.push({
                    animeId: ani.id,
                    animeTitle: ani.title,
                    animeImage: ani.imageUrl,
                    opName: ani.selectedOp,
                    rank: rank,
                });
            }
            saveUserRanking(rankingToUpload);
            alert(`✅ 上传成功！你的 ${selectedAnimes.length} 部动画排名已加入全站OP排行榜（已覆盖本设备之前的记录）。`);
            if (rankModal.style.display === 'flex') {
                renderRankModal();
            }
        }

        // ---------- 以下为 UI 相关函数，与之前相同，但保留了添加时允许重复动画但会检查重复OP? 实际上在添加时不做限制，只在上传时检查。----------
        function updateCounterUI() {
            const len = selectedAnimes.length;
            selectedCountSpan.innerText = len;
            const validLen = (len >= 3 && len <= 9);
            if (validLen) {
                generateBtn.disabled = false;
                uploadRankBtn.disabled = false;
                generateBtn.classList.remove('disabled-btn');
                uploadRankBtn.classList.remove('disabled-btn');
            } else {
                generateBtn.disabled = true;
                uploadRankBtn.disabled = true;
                generateBtn.classList.add('disabled-btn');
                uploadRankBtn.classList.add('disabled-btn');
            }
        }

        function renderSelectedCards() {
            if (!animeContainer) return;
            if (selectedAnimes.length === 0) {
                animeContainer.innerHTML = `<div style="grid-column:1/-1; text-align:center; padding: 2rem;">✨ 暂无动画，快去搜索添加吧 (3~9部，可排序) ✨</div>`;
                updateCounterUI();
                return;
            }

            let html = '';
            for (let i = 0; i < selectedAnimes.length; i++) {
                const ani = selectedAnimes[i];
                const rank = i + 1;
                const openings = ani.openingsList || [];
                let optionsHtml = '';
                if (openings.length === 0) {
                    optionsHtml = '<option disabled>⚠️ 暂无OP数据</option>';
                } else {
                    openings.forEach(op => {
                        const selectedAttr = (ani.selectedOp === op) ? 'selected' : '';
                        let displayOp = op.length > 45 ? op.substring(0, 42) + '...' : op;
                        optionsHtml += `<option value="${escapeHtml(op)}" ${selectedAttr}>${escapeHtml(displayOp)}</option>`;
                    });
                }

                html += `
                    <div class="anime-card" data-uid="${ani.uid}">
                        <div class="rank-control">
                            <span class="rank-number">#${rank}</span>
                            <div class="move-buttons">
                                <button class="move-btn up-btn" data-uid="${ani.uid}" ${i === 0 ? 'disabled style="opacity:0.4;"' : ''}>▲ 上移</button>
                                <button class="move-btn down-btn" data-uid="${ani.uid}" ${i === selectedAnimes.length-1 ? 'disabled style="opacity:0.4;"' : ''}>▼ 下移</button>
                            </div>
                        </div>
                        <div class="card-media">
                            <img class="card-cover" src="${ani.imageUrl}" alt="${escapeHtml(ani.title)}" onerror="this.src='https://via.placeholder.com/80x110?text=No+Image'">
                            <div class="card-info">
                                <h3>${escapeHtml(ani.title)}</h3>
                                <div class="op-selector">
                                    <label>🎤 选择OP</label>
                                    <select class="op-dropdown" data-uid="${ani.uid}">
                                        ${optionsHtml}
                                    </select>
                                </div>
                            </div>
                        </div>
                        <button class="delete-btn" data-uid="${ani.uid}">🗑 删除</button>
                    </div>
                `;
            }
            animeContainer.innerHTML = html;
            updateCounterUI();

            document.querySelectorAll('.op-dropdown').forEach(select => {
                select.removeEventListener('change', handleOpChange);
                select.addEventListener('change', handleOpChange);
            });
            document.querySelectorAll('.delete-btn').forEach(btn => {
                btn.removeEventListener('click', handleDelete);
                btn.addEventListener('click', handleDelete);
            });
            document.querySelectorAll('.up-btn').forEach(btn => {
                btn.removeEventListener('click', handleMoveUp);
                btn.addEventListener('click', handleMoveUp);
            });
            document.querySelectorAll('.down-btn').forEach(btn => {
                btn.removeEventListener('click', handleMoveDown);
                btn.addEventListener('click', handleMoveDown);
            });
        }

        function handleOpChange(e) {
            const selectEl = e.target;
            const uid = parseInt(selectEl.getAttribute('data-uid'));
            const selectedOpValue = selectEl.value;
            const animeIndex = selectedAnimes.findIndex(a => a.uid === uid);
            if (animeIndex !== -1) {
                selectedAnimes[animeIndex].selectedOp = selectedOpValue;
            }
        }

        function handleDelete(e) {
            const uid = parseInt(e.target.getAttribute('data-uid'));
            const idx = selectedAnimes.findIndex(a => a.uid === uid);
            if (idx !== -1) {
                selectedAnimes.splice(idx, 1);
                renderSelectedCards();
            }
        }

        function handleMoveUp(e) {
            const uid = parseInt(e.currentTarget.getAttribute('data-uid'));
            const idx = selectedAnimes.findIndex(a => a.uid === uid);
            if (idx > 0) {
                [selectedAnimes[idx-1], selectedAnimes[idx]] = [selectedAnimes[idx], selectedAnimes[idx-1]];
                renderSelectedCards();
            }
        }

        function handleMoveDown(e) {
            const uid = parseInt(e.currentTarget.getAttribute('data-uid'));
            const idx = selectedAnimes.findIndex(a => a.uid === uid);
            if (idx < selectedAnimes.length - 1 && idx !== -1) {
                [selectedAnimes[idx+1], selectedAnimes[idx]] = [selectedAnimes[idx], selectedAnimes[idx+1]];
                renderSelectedCards();
            }
        }

        function escapeHtml(str) {
            if (!str) return '';
            return str.replace(/[&<>]/g, function(m) {
                if (m === '&') return '&amp;';
                if (m === '<') return '&lt;';
                if (m === '>') return '&gt;';
                return m;
            });
        }

        async function fetchAnimeThemes(animeId) {
            try {
                const response = await fetch(`${JIKAN_API}/anime/${animeId}/themes`);
                if (!response.ok) throw new Error();
                const data = await response.json();
                let openings = data.data?.openings || [];
                openings = openings.filter(op => op && op.trim().length > 0);
                return openings;
            } catch (err) {
                return [];
            }
        }

        async function addAnime(anime) {
            if (selectedAnimes.length >= 9) {
                alert('最多只能选择9部动画');
                return false;
            }

            const uid = nextUid++;
            const newAnime = {
                uid: uid,
                id: anime.id,
                title: anime.title,
                imageUrl: anime.imageUrl || 'https://via.placeholder.com/80x110?text=Cover',
                openingsList: [],
                selectedOp: '加载OP中...',
            };
            selectedAnimes.push(newAnime);
            renderSelectedCards();

            const openings = await fetchAnimeThemes(anime.id);
            const idx = selectedAnimes.findIndex(a => a.uid === uid);
            if (idx !== -1) {
                if (openings.length === 0) {
                    selectedAnimes.splice(idx, 1);
                    renderSelectedCards();
                    alert(`「${anime.title}」没有收录主题曲(OP)信息，无法添加`);
                    return false;
                } else {
                    selectedAnimes[idx].openingsList = openings;
                    selectedAnimes[idx].selectedOp = openings[0];
                    renderSelectedCards();
                }
            }
            return true;
        }

        async function searchAnime(query) {
            if (!query.trim()) { resultsDiv.classList.remove('show'); return; }
            try {
                const url = `${JIKAN_API}/anime?q=${encodeURIComponent(query)}&limit=8&sfw`;
                const resp = await fetch(url);
                const data = await resp.json();
                const results = data.data || [];
                if (results.length === 0) {
                    resultsDiv.innerHTML = '<div class="result-item">未找到相关动画</div>';
                    resultsDiv.classList.add('show');
                    return;
                }
                let html = '';
                for (let item of results) {
                    const image = item.images?.jpg?.image_url || 'https://via.placeholder.com/48x68';
                    html += `
                        <div class="result-item" data-id="${item.mal_id}" data-title="${escapeHtml(item.title)}" data-image="${image}">
                            <img class="result-img" src="${image}" onerror="this.src='https://via.placeholder.com/48x68'">
                            <div class="result-info"><h4>${escapeHtml(item.title)}</h4><p>${item.year || ''}</p></div>
                        </div>
                    `;
                }
                resultsDiv.innerHTML = html;
                resultsDiv.classList.add('show');
                document.querySelectorAll('.result-item').forEach(el => {
                    el.addEventListener('click', () => {
                        const id = parseInt(el.getAttribute('data-id'));
                        const title = el.getAttribute('data-title');
                        const image = el.querySelector('.result-img')?.src || '';
                        addAnime({ id, title, imageUrl: image });
                        resultsDiv.classList.remove('show');
                        searchInput.value = '';
                    });
                });
            } catch (err) {
                resultsDiv.innerHTML = '<div class="result-item">搜索失败，请重试</div>';
                resultsDiv.classList.add('show');
            }
        }

        searchInput.addEventListener('input', () => {
            clearTimeout(debounceTimer);
            const val = searchInput.value.trim();
            if (!val) { resultsDiv.classList.remove('show'); return; }
            debounceTimer = setTimeout(() => searchAnime(val), 400);
        });
        searchBtn.addEventListener('click', () => searchAnime(searchInput.value.trim()));
        document.addEventListener('click', (e) => {
            if (!searchInput.contains(e.target) && !resultsDiv.contains(e.target)) resultsDiv.classList.remove('show');
        });

        async function generateShareImage() {
            if (selectedAnimes.length < 3 || selectedAnimes.length > 9) {
                alert(`请选择3~9部动画 (当前${selectedAnimes.length})`);
                return;
            }
            for (let ani of selectedAnimes) {
                if (!ani.selectedOp || ani.selectedOp === '加载OP中...' || ani.openingsList.length === 0) {
                    alert(`请为动画「${ani.title}」选择有效OP`);
                    return;
                }
            }
            const shareContainer = document.getElementById('sharePreviewContainer') || (() => { let div = document.createElement('div'); div.id = 'sharePreviewContainer'; div.style.position='fixed'; div.style.top='-9999px'; document.body.appendChild(div); return div; })();
            shareContainer.innerHTML = '';
            const previewDiv = document.createElement('div');
            previewDiv.style.background = '#FDF3E6';
            previewDiv.style.padding = '28px 24px';
            previewDiv.style.borderRadius = '48px';
            previewDiv.style.width = '800px';
            const gridDiv = document.createElement('div');
            gridDiv.style.display = 'grid';
            gridDiv.style.gridTemplateColumns = 'repeat(3, 1fr)';
            gridDiv.style.gap = '20px';
            for (let ani of selectedAnimes) {
                const card = document.createElement('div');
                card.style.background = 'white';
                card.style.borderRadius = '28px';
                card.style.padding = '16px';
                card.style.textAlign = 'center';
                const img = document.createElement('img');
                img.src = ani.imageUrl;
                img.style.width = '100%';
                img.style.aspectRatio = '3/4';
                img.style.objectFit = 'cover';
                img.style.borderRadius = '20px';
                const title = document.createElement('div');
                title.innerText = ani.title;
                title.style.fontWeight = 'bold';
                const opDiv = document.createElement('div');
                opDiv.innerText = `♪ ${ani.selectedOp}`;
                opDiv.style.fontSize = '0.75rem';
                opDiv.style.background = '#fff0e0';
                opDiv.style.display = 'inline-block';
                opDiv.style.padding = '4px 12px';
                opDiv.style.borderRadius = '40px';
                card.appendChild(img);
                card.appendChild(title);
                card.appendChild(opDiv);
                gridDiv.appendChild(card);
            }
            const watermark = document.createElement('div');
            watermark.innerText = '🎵 最喜欢的动画OP | 我的专属歌单';
            watermark.style.textAlign = 'center';
            watermark.style.marginTop = '20px';
            previewDiv.appendChild(gridDiv);
            previewDiv.appendChild(watermark);
            shareContainer.appendChild(previewDiv);
            shareContainer.style.position = 'fixed';
            shareContainer.style.top = '0';
            shareContainer.style.left = '0';
            shareContainer.style.opacity = '1';
            shareContainer.style.pointerEvents = 'none';
            shareContainer.style.zIndex = '9999';
            const images = previewDiv.querySelectorAll('img');
            await Promise.all(Array.from(images).map(img => img.complete ? Promise.resolve() : new Promise(resolve => { img.onload = resolve; img.onerror = resolve; })));
            await new Promise(r => setTimeout(r, 100));
            try {
                const canvas = await html2canvas(previewDiv, { scale: 2.5, backgroundColor: '#FDF3E6', useCORS: true });
                const link = document.createElement('a');
                link.download = 'anime_op_collection.png';
                link.href = canvas.toDataURL();
                link.click();
            } catch(e) { alert('生成失败'); }
            finally {
                shareContainer.style.top = '-9999px';
                shareContainer.innerHTML = '';
            }
        }

        function openRankModal() {
            renderRankModal();
            rankModal.style.display = 'flex';
        }
        closeRankModal.onclick = () => rankModal.style.display = 'none';
        window.onclick = (e) => { if (e.target === rankModal) rankModal.style.display = 'none'; };

        uploadRankBtn.addEventListener('click', uploadCurrentSelection);
        viewRankBtn.addEventListener('click', openRankModal);
        generateBtn.addEventListener('click', generateShareImage);

        renderSelectedCards();
    })();
</script>
<div id="sharePreviewContainer" style="position:fixed; top:-9999px; left:-9999px;"></div>
</body>
</html>
```
