
[index.html](https://github.com/user-attachments/files/30982819/index.html)
<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Daily Check-in | 打卡系統</title>
  <!-- Google Fonts: Noto Sans TC & Inter -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500&family=Noto+Sans+TC:wght@300;400;500&display=swap" rel="stylesheet">

  <style>
    /* CSS Rest & Minimal Style Definition */
    :root {
      --bg-color: #f7f5f0;
      --card-bg: #ffffff;
      --primary-color: #7d6e63;
      --primary-hover: #63564d;
      --text-main: #4a403a;
      --text-muted: #9e938a;
      --border-color: #eae5df;
      --shadow: 0 10px 25px rgba(0, 0, 0, 0.03);
      --radius: 16px;

      /* 類別色彩定義 */
      --tag-work-bg: #e8f3ec;
      --tag-work-text: #3d7a5a;
      --tag-off-bg: #fbeee9;
      --tag-off-text: #b56247;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Inter', 'Noto Sans TC', sans-serif;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-main);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 20px;
    }

    .container {
      width: 100%;
      max-width: 440px;
      background: var(--card-bg);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding: 32px 28px;
      border: 1px solid var(--border-color);
    }

    .header {
      text-align: center;
      margin-bottom: 20px;
    }

    .header .date-display {
      font-size: 0.9rem;
      font-weight: 500;
      color: var(--primary-color);
      margin-bottom: 8px;
      letter-spacing: 0.5px;
    }

    .header h1 {
      font-size: 1.5rem;
      font-weight: 500;
      letter-spacing: 1px;
      color: var(--primary-color);
      margin-bottom: 4px;
    }

    .header p {
      font-size: 0.85rem;
      color: var(--text-muted);
    }

    /* 主分頁頁籤 */
    .nav-tabs {
      display: flex;
      border-bottom: 1px solid var(--border-color);
      margin-bottom: 24px;
    }

    .tab-btn {
      flex: 1;
      padding: 12px 0;
      background: none;
      border: none;
      color: var(--text-muted);
      font-size: 0.95rem;
      font-weight: 500;
      cursor: pointer;
      position: relative;
      transition: color 0.2s ease;
    }

    .tab-btn.active {
      color: var(--primary-color);
    }

    .tab-btn.active::after {
      content: '';
      position: absolute;
      bottom: -1px;
      left: 0;
      width: 100%;
      height: 2px;
      background-color: var(--primary-color);
    }

    /* 分頁區塊顯示/隱藏 */
    .tab-content {
      display: none;
    }

    .tab-content.active {
      display: block;
    }

    .form-group {
      margin-bottom: 18px;
    }

    label {
      display: block;
      font-size: 0.85rem;
      color: var(--primary-color);
      margin-bottom: 6px;
      font-weight: 500;
    }

    input, select {
      width: 100%;
      padding: 12px 14px;
      border: 1px solid var(--border-color);
      border-radius: 8px;
      background-color: #faf9f7;
      color: var(--text-main);
      font-size: 0.95rem;
      outline: none;
      transition: all 0.2s ease;
    }

    input:focus, select:focus {
      border-color: var(--primary-color);
      background-color: #ffffff;
    }

    .time-select-group {
      display: flex;
      gap: 8px;
    }

    .time-select-group select {
      flex: 1;
    }

    .type-toggle-group {
      display: flex;
      gap: 10px;
    }

    .type-btn {
      flex: 1;
      padding: 12px;
      border: 1px solid var(--border-color);
      background-color: #faf9f7;
      color: var(--text-muted);
      border-radius: 8px;
      font-size: 0.95rem;
      font-weight: 500;
      cursor: pointer;
      transition: all 0.2s ease;
      text-align: center;
    }

    .type-btn.active[data-type="上班"] {
      background-color: var(--tag-work-bg);
      color: var(--tag-work-text);
      border-color: var(--tag-work-text);
    }

    .type-btn.active[data-type="下班"] {
      background-color: var(--tag-off-bg);
      color: var(--tag-off-text);
      border-color: var(--tag-off-text);
    }

    .btn-submit {
      width: 100%;
      padding: 14px;
      background-color: var(--primary-color);
      color: #ffffff;
      border: none;
      border-radius: 8px;
      font-size: 1rem;
      font-weight: 500;
      letter-spacing: 1px;
      cursor: pointer;
      margin-top: 10px;
      transition: background-color 0.2s ease;
    }

    .btn-submit:hover {
      background-color: var(--primary-hover);
    }

    /* 紀錄頁面時間篩選器 */
    .filter-group {
      display: flex;
      gap: 4px;
      margin-bottom: 16px;
    }

    .filter-btn {
      flex: 1;
      padding: 8px 0;
      background-color: #faf9f7;
      border: 1px solid var(--border-color);
      border-radius: 6px;
      color: var(--text-muted);
      font-size: 0.75rem;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .filter-btn.active {
      background-color: var(--primary-color);
      color: #ffffff;
      border-color: var(--primary-color);
    }

    .record-list {
      list-style: none;
      max-height: 320px;
      overflow-y: auto;
    }

    .record-item {
      padding: 12px 14px;
      border: 1px solid var(--border-color);
      border-radius: 8px;
      margin-bottom: 10px;
      background-color: #faf9f7;
      display: flex;
      justify-content: space-between;
      align-items: center;
      transition: all 0.2s ease;
    }

    .record-info {
      font-size: 0.85rem;
      line-height: 1.5;
    }

    .record-info strong {
      color: var(--primary-color);
      font-weight: 500;
    }

    .tag {
      display: inline-block;
      padding: 2px 8px;
      border-radius: 6px;
      font-size: 0.75rem;
      font-weight: 500;
      margin-left: 6px;
    }

    .tag-上班 {
      background-color: var(--tag-work-bg);
      color: var(--tag-work-text);
    }

    .tag-下班 {
      background-color: var(--tag-off-bg);
      color: var(--tag-off-text);
    }

    /* 文字式按鈕組 */
    .action-btns {
      display: flex;
      align-items: center;
      font-size: 0.8rem;
      color: var(--text-muted);
    }

    .btn-action {
      background: none;
      border: none;
      color: var(--text-muted);
      cursor: pointer;
      font-size: 0.8rem;
      padding: 2px 4px;
      transition: color 0.2s ease;
    }

    .btn-share:hover {
      color: var(--primary-color);
    }

    .btn-delete:hover {
      color: #d9534f;
    }

    .action-divider {
      margin: 0 2px;
      color: var(--border-color);
    }

    .empty-msg {
      text-align: center;
      color: var(--text-muted);
      font-size: 0.85rem;
      padding: 24px 0;
    }
  </style>
</head>
<body>

  <div class="container">
    <div class="header">
      <div id="todayDate" class="date-display"></div>
      <h1>DAILY CHECK-IN</h1>
      <p>打卡系統</p>
    </div>

    <!-- 主頁籤導覽 -->
    <div class="nav-tabs">
      <button class="tab-btn active" onclick="switchTab('checkin')">新增打卡</button>
      <button class="tab-btn" onclick="switchTab('records')">打卡紀錄</button>
    </div>

    <!-- 分頁一：打卡表單 -->
    <div id="checkinTab" class="tab-content active">
      <form id="checkinForm">
        <div class="form-group">
          <label for="userName">姓名 *</label>
          <input type="text" id="userName" placeholder="請輸入姓名" required>
        </div>

        <div class="form-group">
          <label>打卡類別 *</label>
          <div class="type-toggle-group">
            <button type="button" class="type-btn active" data-type="上班" onclick="selectType('上班')">上班 Check-in</button>
            <button type="button" class="type-btn" data-type="下班" onclick="selectType('下班')">下班 Check-out</button>
          </div>
        </div>

        <div class="form-group">
          <label>時間 *</label>
          <div class="time-select-group">
            <select id="hour"></select>
            <select id="minute"></select>
          </div>
        </div>

        <div class="form-group">
          <label for="location">地點 *</label>
          <input type="text" id="location" placeholder="例如：OW、八度、飛龍" required>
        </div>

        <div class="form-group">
          <label for="note">備註</label>
          <input type="text" id="note" placeholder="例如：自收、客人算XX小時">
        </div>

        <button type="submit" class="btn-submit">完成打卡</button>
      </form>
    </div>

    <!-- 分頁二：打卡紀錄與查詢篩選 -->
    <div id="recordsTab" class="tab-content">
      <div class="filter-group">
        <button class="filter-btn active" onclick="setFilter('daily', this)">每日</button>
        <button class="filter-btn" onclick="setFilter('weekly', this)">本週</button>
        <button class="filter-btn" onclick="setFilter('3months', this)">近三個月</button>
        <button class="filter-btn" onclick="setFilter('all', this)">全部</button>
      </div>

      <ul id="recordList" class="record-list">
        <!-- 動態帶入紀錄 -->
      </ul>
    </div>
  </div>

  <script>
    let selectedType = '上班';
    let currentFilter = 'daily';

    // 設定頂部日期
    function initDateDisplay() {
      const now = new Date();
      const options = { year: 'numeric', month: 'long', day: 'numeric', weekday: 'long' };
      document.getElementById('todayDate').innerText = now.toLocaleDateString('zh-TW', options);
    }

    // 主分頁切換
    function switchTab(tabName) {
      const tabs = document.querySelectorAll('.tab-btn');
      const contents = document.querySelectorAll('.tab-content');

      tabs.forEach(tab => tab.classList.remove('active'));
      contents.forEach(content => content.classList.remove('active'));

      if (tabName === 'checkin') {
        tabs[0].classList.add('active');
        document.getElementById('checkinTab').classList.add('active');
      } else {
        tabs[1].classList.add('active');
        document.getElementById('recordsTab').classList.add('active');
        renderRecords();
      }
    }

    // 初始化 24小時制時間下拉選單
    function initTimeOptions() {
      const hourSelect = document.getElementById('hour');
      const minuteSelect = document.getElementById('minute');

      hourSelect.innerHTML = '';
      minuteSelect.innerHTML = '';

      for (let i = 0; i < 24; i++) {
        const val = i < 10 ? '0' + i : '' + i;
        hourSelect.innerHTML += `<option value="${val}">${val} 時</option>`;
      }

      for (let i = 0; i < 60; i++) {
        const val = i < 10 ? '0' + i : '' + i;
        minuteSelect.innerHTML += `<option value="${val}">${val} 分</option>`;
      }

      setNowTime();
    }

    // 設置下拉選單為當前系統時間
    function setNowTime() {
      const now = new Date();
      const hours = now.getHours();
      const minutes = now.getMinutes();

      document.getElementById('hour').value = hours < 10 ? '0' + hours : '' + hours;
      document.getElementById('minute').value = minutes < 10 ? '0' + minutes : '' + minutes;
    }

    // 切換上班/下班類別
    function selectType(type) {
      selectedType = type;
      const buttons = document.querySelectorAll('.type-btn');
      buttons.forEach(btn => {
        if (btn.getAttribute('data-type') === type) {
          btn.classList.add('active');
        } else {
          btn.classList.remove('active');
        }
      });
    }

    // LocalStorage 操作
    function getRecords() {
      return JSON.parse(localStorage.getItem('checkin_records')) || [];
    }

    function saveRecords(records) {
      localStorage.setItem('checkin_records', JSON.stringify(records));
    }

    // 紀錄篩選邏輯
    function setFilter(filterType, btnElement) {
      currentFilter = filterType;
      const filterBtns = document.querySelectorAll('.filter-btn');
      filterBtns.forEach(btn => btn.classList.remove('active'));
      btnElement.classList.add('active');

      renderRecords();
    }

    function filterRecords(records) {
      if (currentFilter === 'all') return records;

      const now = new Date();
      const todayStr = `${now.getFullYear()}-${(now.getMonth()+1).toString().padStart(2, '0')}-${now.getDate().toString().padStart(2, '0')}`;

      return records.filter(item => {
        const recordDate = new Date(item.date);

        if (currentFilter === 'daily') {
          return item.date === todayStr;
        }

        if (currentFilter === 'weekly') {
          const oneWeekAgo = new Date();
          oneWeekAgo.setDate(now.getDate() - 7);
          return recordDate >= oneWeekAgo && recordDate <= now;
        }

        if (currentFilter === '3months') {
          const threeMonthsAgo = new Date();
          threeMonthsAgo.setDate(now.getDate() - 90);
          return recordDate >= threeMonthsAgo && recordDate <= now;
        }

        return true;
      });
    }

    // 渲染打卡紀錄列表
    function renderRecords() {
      const recordList = document.getElementById('recordList');
      const allRecords = getRecords();
      const filteredRecords = filterRecords(allRecords);

      recordList.innerHTML = '';

      if (filteredRecords.length === 0) {
        recordList.innerHTML = '<li class="empty-msg">尚無符合條件的打卡紀錄</li>';
        return;
      }

      filteredRecords.forEach((item) => {
        const originalIndex = allRecords.findIndex(r => r === item);
        const li = document.createElement('li');
        li.className = 'record-item';

        const noteText = item.note ? ` | 📝 ${item.note}` : '';

        li.innerHTML = `
          <div class="record-info">
            <div>
              <strong>${item.name}</strong> 
              <span class="tag tag-${item.type}">${item.type}</span>
            </div>
            <div style="color: var(--text-muted); font-size: 0.8rem; margin-top: 2px;">
              📅 ${item.date} | ⏰ ${item.time} | 📍 ${item.location}${noteText}
            </div>
          </div>
          <div class="action-btns">
            <button class="btn-action btn-share" onclick="shareRecord(${originalIndex})">分享</button>
            <span class="action-divider">|</span>
            <button class="btn-action btn-delete" onclick="deleteRecord(${originalIndex})">刪除</button>
          </div>
        `;
        recordList.appendChild(li);
      });
    }

    // 分享單筆打卡紀錄 (格式：上班/下班 姓名 日期及時間 地點 備註)
    async function shareRecord(index) {
      const records = getRecords();
      const item = records[index];
      if (!item) return;

      const noteStr = item.note ? ` 備註：${item.note}` : '';
      const shareText = `${item.type} ${item.name} ${item.date} ${item.time} ${item.location}${noteStr}`;

      if (navigator.share) {
        try {
          await navigator.share({
            text: shareText
          });
        } catch (err) {
          // 使用者取消分享不動作
        }
      } else {
        try {
          await navigator.clipboard.writeText(shareText);
          alert('已複製紀錄至剪貼簿！');
        } catch (err) {
          alert('複製失敗，請手動複製文字：\n\n' + shareText);
        }
      }
    }

    // 送出表單
    document.getElementById('checkinForm').addEventListener('submit', function(e) {
      e.preventDefault();

      const name = document.getElementById('userName').value.trim();
      const type = selectedType;
      const hour = document.getElementById('hour').value;
      const minute = document.getElementById('minute').value;
      const timeStr = `${hour}:${minute}`;

      const now = new Date();
      const dateStr = `${now.getFullYear()}-${(now.getMonth()+1).toString().padStart(2, '0')}-${now.getDate().toString().padStart(2, '0')}`;
      const location = document.getElementById('location').value.trim();
      const note = document.getElementById('note').value.trim();

      if (!name || !location) {
        alert('請完整填寫所有欄位！');
        return;
      }

      const newRecord = { name, type, date: dateStr, time: timeStr, location, note };
      const records = getRecords();
      records.unshift(newRecord);

      saveRecords(records);

      document.getElementById('location').value = '';
      document.getElementById('note').value = '';
      setNowTime();
      switchTab('records');
    });

    // 刪除單筆紀錄
    function deleteRecord(index) {
      const records = getRecords();
      records.splice(index, 1);
      saveRecords(records);
      renderRecords();
    }

    // 初始化
    window.onload = function() {
      initDateDisplay();
      initTimeOptions();
      renderRecords();
    };
  </script>
</body>
</html>
