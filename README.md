btn-info-sidebar {
    background: #4299e1;
    color: white;
}

.btn-info-sidebar:hover {
    background: #3182ce;
    transform: translateY(-1px);
}
/* ========== БЛОК ПРИБЫЛИ ПО КАНАЛАМ ========== */
.profit-channels-container {
    transition: max-height 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.profit-channel-item {
    transition: all 0.3s ease;
}

.profit-channel-item:hover {
    background: rgba(102,126,234,0.05);
    border-radius: 8px;
    padding: 4px;
    margin: -4px;
}

.toggle-channels-profit-btn {
    transition: all 0.2s;
}

.toggle-channels-profit-btn:hover {
    background: rgba(102,126,234,0.1);
    transform: translateY(-1px);
}

.profit-progress-bar {
    transition: width 0.5s ease-out;
}
    </style>
</head>
<body>
    <div id="authContainer" class="auth-container">
        <div class="auth-card">
            <h2 id="authTitle">🔐 Вход в систему</h2>
            <div id="authError" class="error-msg"></div>
            <div id="authSuccess" class="success-msg"></div>
            <input type="text" id="authFio" class="auth-input" placeholder="ФИО" style="display: none;">
            <input type="email" id="authEmail" class="auth-input" placeholder="Email">
            <input type="password" id="authPassword" class="auth-input" placeholder="Пароль">
            <button id="authSubmitBtn" class="auth-btn">Войти</button>
            <div id="authToggle" class="auth-link">Нет аккаунта? Зарегистрироваться</div>
            <button id="resetDataBtn" class="auth-btn reset-btn">🔄 Сбросить данные</button>
        </div>
    </div>

    <div id="adminPanel" class="admin-panel">
        <div class="admin-content">
            <div class="admin-header">
                <h2>👑 Админ-панель</h2>
                <button class="close-admin" id="closeAdminBtn">Закрыть</button>
            </div>
            <h3>Управление пользователями</h3>
            <table class="admin-table" id="adminTable">
                <thead>
                    <tr><th>ФИО</th><th>Email</th><th>Статус</th><th>Действия</th>  </thead>
                <tbody id="adminTableBody"></tbody>
             </table>
        </div>
    </div>

    <div id="mainApp" style="display: none;">
        <div class="header">
            <div class="header-content">
                <div class="logo-section">
                    <div class="logo-icon">📊</div>
                    <div class="logo-text">
                        <h1>Финансовый аналитический дашборд</h1>
                        <p>Полный анализ доходов, расходов, НДС и структуры каналов продаж</p>
                    </div>
                </div>
                <div class="buttons-section">
                    <div class="user-info" id="userInfo"></div>
                    <button class="admin-btn" id="adminBtn" style="display: none;">👑 Админ-панель</button>
                    <button class="logout-btn" id="logoutBtn">🚪 Выйти</button>
                </div>
            </div>
        </div>

        <div class="container">
            <div class="sidebar-nav">
    <div class="nav-title">НАВИГАЦИЯ</div>
    <div class="nav-item has-submenu" id="dashboardMenu">
        <span class="nav-icon">📊</span>
        <span>Дашборд</span>
        <span class="arrow">▶</span>
    </div>
    <div class="nav-submenu" id="channelsSubmenu">
        <div class="nav-subitem" data-channel="wildberries"><span class="nav-icon">🛍️</span><span>Wildberries</span></div>
        <div class="nav-subitem" data-channel="ozon"><span class="nav-icon">📦</span><span>OZON</span></div>
        <div class="nav-subitem" data-channel="detsky-mir"><span class="nav-icon">🧸</span><span>Детский мир</span></div>
        <div class="nav-subitem" data-channel="lamoda"><span class="nav-icon">👗</span><span>Lamoda</span></div>
    </div>
    <div class="nav-item" data-page="ai"><span class="nav-icon">🤖</span><span>AI Аналитик</span></div>
    
    <!-- БЛОК ФИЛЬТРОВ ПОД НАВИГАЦИЕЙ -->
<div class="filters-sidebar" id="filtersSidebar" style="margin-top: 20px; padding-top: 20px; border-top: 1px solid rgba(102,126,234,0.3);">
    <div class="filters-sidebar-header">
        <span class="filters-sidebar-icon">🔍</span>
        <span>Фильтры</span>
        <button class="filters-sidebar-toggle" id="filtersSidebarToggle">
            <span class="toggle-icon">▲</span>
        </button>
    </div>
    <div class="filters-sidebar-content" id="filtersSidebarContent">
        <div class="filter-group-sidebar">
            <label>🏢 Компания</label>
            <select id="companyFilter">
                <option value="">Все компании</option>
            </select>
        </div>
        <div class="filter-group-sidebar">
            <label>📅 Год</label>
            <select id="yearFilter">
                <option value="">Все годы</option>
            </select>
        </div>
        <div class="filter-group-sidebar">
            <label>📆 Месяц (можно выбрать несколько)</label>
            <select id="monthFilter" multiple size="4"></select>
        </div>
        <div class="filter-actions-sidebar">
            <button class="btn-sidebar btn-danger-sidebar" id="resetFilters">
                <span>🔄</span> Сбросить
            </button>
            <button class="btn-sidebar btn-info-sidebar" id="changeDataBtn">
                <span>📁</span> Сменить данные
            </button>
        </div>
    </div>
</div>
    
    <div class="theme-toggle"><span class="theme-toggle-label">🌙 Темная тема</span><div class="toggle-switch active" id="themeToggle"><div class="slider"></div></div></div>
</div>

            <div class="main-content">
                <div id="uploadArea" class="upload-card">
                    <div class="upload-icon">📊</div>
                    <div class="upload-title">Загрузите Excel файл с финансовыми данными</div>
                    <div class="upload-text">Поддерживаются форматы .xlsx, .xls</div>
                    <input type="file" id="fileInput" accept=".xlsx,.xls">
                </div>
                
                <div id="dataSourceInfo" style="display: none; margin-bottom: 20px;">
                    <div class="data-source" id="dataSourceText"></div>
                </div>
                
                <div id="page-dashboard" class="page-content active">
                    <div id="dashboardMetrics"></div>
                    <div id="aiInsights" class="ai-agent-card" style="margin-top: 24px;"></div>
                </div>
                <div id="page-channel-wildberries" class="page-content"><div id="channelWildberriesMetrics"></div></div>
                <div id="page-channel-ozon" class="page-content"><div id="channelOzonMetrics"></div></div>
                <div id="page-channel-detsky-mir" class="page-content"><div id="channelDetskyMirMetrics"></div></div>
                <div id="page-channel-lamoda" class="page-content"><div id="channelLamodaMetrics"></div></div>
                <div id="page-ai" class="page-content">
                    <div class="ai-agent-card">
                        <div class="ai-header"><div class="ai-icon">🤖</div><div><div class="ai-title">AI Финансовый Аналитик</div><div class="ai-subtitle">Задайте вопрос о ваших данных или получите автоматический анализ</div></div></div>
                        <div id="aiChatMessages" class="ai-chat-messages" style="max-height: 400px; overflow-y: auto; margin-bottom: 16px;"><div class="ai-message assistant">👋 Здравствуйте! Я AI финансовый аналитик. Задайте вопрос о данных.</div></div>
                        <div class="ai-suggestions" id="aiSuggestions">
                            <span class="ai-suggestion" data-question="analyze">📊 Анализ общих показателей</span>
                            <span class="ai-suggestion" data-question="bestChannel">🏆 Самый прибыльный канал</span>
                            <span class="ai-suggestion" data-question="expenses">💰 Основные расходы</span>
                            <span class="ai-suggestion" data-question="recommend">💡 Рекомендации</span>
                        </div>
                        <div class="ai-input-area">
                            <textarea id="aiInput" class="ai-input" rows="2" placeholder="Задайте вопрос о данных..."></textarea>
                            <button id="aiSendBtn" class="btn btn-primary">Отправить</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // ========== АВТОРИЗАЦИЯ ==========
        let currentUser = null;
        
        function resetAllData() {
            localStorage.clear();
            alert('Все данные сброшены! Обновите страницу.');
            location.reload();
        }
        
        function loadUsers() {
            const users = localStorage.getItem('dashboard_users');
            if (!users) {
                const defaultUsers = {
                    'admin@dashboard.com': {
                        fio: 'Администратор',
                        email: 'admin@dashboard.com',
                        password: 'admin123',
                        isAdmin: true,
                        blocked: false,
                        createdAt: new Date().toISOString()
                    }
                };
                localStorage.setItem('dashboard_users', JSON.stringify(defaultUsers));
                return defaultUsers;
            }
            return JSON.parse(users);
        }
        
        function saveUsers(users) { localStorage.setItem('dashboard_users', JSON.stringify(users)); }
        
        function register(fio, email, password) {
            const users = loadUsers();
            if (users[email]) return { success: false, error: 'Пользователь с таким email уже существует' };
            if (password.length < 6) return { success: false, error: 'Пароль должен быть не менее 6 символов' };
            users[email] = { fio, email, password, isAdmin: false, blocked: false, createdAt: new Date().toISOString() };
            saveUsers(users);
            return { success: true };
        }
        
        function login(email, password) {
            const users = loadUsers();
            const user = users[email];
            if (!user) return { success: false, error: 'Пользователь не найден' };
            if (user.password !== password) return { success: false, error: 'Неверный пароль' };
            if (user.blocked) return { success: false, error: 'Ваш аккаунт заблокирован' };
            return { success: true, user };
        }
        
        function updateAdminTable() {
            const users = loadUsers();
            const tbody = document.getElementById('adminTableBody');
            if (!tbody) return;
            tbody.innerHTML = '';
            for (const [email, user] of Object.entries(users)) {
                const row = tbody.insertRow();
                row.insertCell(0).textContent = user.fio;
                row.insertCell(1).textContent = email;
                row.insertCell(2).textContent = user.blocked ? '🔴 Заблокирован' : '🟢 Активен';
                const actionCell = row.insertCell(3);
                if (email !== 'admin@dashboard.com') {
                    const btn = document.createElement('button');
                    btn.textContent = user.blocked ? 'Разблокировать' : 'Заблокировать';
                    btn.className = user.blocked ? 'unblock-btn' : 'block-btn';
                    btn.onclick = () => {
                        const usersData = loadUsers();
                        usersData[email].blocked = !usersData[email].blocked;
                        saveUsers(usersData);
                        updateAdminTable();
                        if (currentUser && currentUser.email === email) {
                            alert('Ваш статус изменен. Вы будете выйдены из системы.');
                            logout();
                        }
                    };
                    actionCell.appendChild(btn);
                } else {
                    actionCell.textContent = 'Администратор';
                }
            }
        }
        
        function showAdminPanel() {
            if (currentUser && currentUser.isAdmin) {
                updateAdminTable();
                document.getElementById('adminPanel').classList.add('active');
            } else {
                alert('Доступ запрещен. Только для администратора.');
            }
        }
        
        function logout() {
            currentUser = null;
            localStorage.removeItem('dashboard_current_user');
            document.getElementById('mainApp').style.display = 'none';
            document.getElementById('authContainer').style.display = 'flex';
            document.getElementById('authEmail').value = '';
            document.getElementById('authPassword').value = '';
            document.getElementById('authFio').value = '';
 = '';
                document.getElementById('authFio').value = '';
            };
            
            authSubmitBtn.onclick = () => {
                const email = document.getElementById('authEmail').value.trim();
                const password = document.getElementById('authPassword').value;
                authError.textContent = '';
                authSuccess.textContent = '';
                
                if (!email || !password) {
                    authError.textContent = 'Заполните все поля';
                    return;
                }
                
                if (isLogin) {
                    const result = login(email, password);
                    if (result.success) {
                        currentUser = result.user;
                        localStorage.setItem('dashboard_current_user', JSON.stringify({ email: currentUser.email }));
                        document.getElementById('mainApp').style.display = 'block';
                        document.getElementById('authContainer').style.display = 'none';
                        document.getElementById('userInfo').innerHTML = `👤 ${currentUser.fio} ${currentUser.isAdmin ? '(Админ)' : ''}`;
                        if (currentUser.isAdmin) document.getElementById('adminBtn').style.display = 'block';
                        initApp();
                    } else {
                        authError.textContent = result.error;
                    }
                } else {
                    const fio = document.getElementById('authFio').value.trim();
                    if (!fio) { authError.textContent = 'Введите ФИО'; return; }
                    if (password.length < 6) { authError.textContent = 'Пароль должен быть не менее 6 символов'; return; }
                    const result = register(fio, email, password);
                    if (result.success) {
                        authSuccess.textContent = 'Регистрация успешна! Теперь войдите.';
                        authToggle.click();
                        document.getElementById('authEmail').value = '';
                        document.getElementById('authPassword').value = '';
                        document.getElementById('authFio').value = '';
                    } else {
                        authError.textContent = result.error;
                    }
                }
            };
        }
        
        // ========== ОСНОВНОЙ ДАШБОРД ========== 
        let originalData = [], currentData = [];
        let currentChannel = null;
        let currentFilters = { company: '', year: '', month: [] };
        let isRendering = false;
        
        const monthsOrder = ['январь', 'февраль', 'март', 'апрель', 'май', 'июнь', 'июль', 'август', 'сентябрь', 'октябрь', 'ноябрь', 'декабрь'];
        
        const channelMapping = {
            'wildberries': { name: '1.1 Wildberries', displayName: 'Wildberries', prefix: '1.', ndsArticle: 'НДС от выручки 1.1' },
            'ozon': { name: '2.1 OZON', displayName: 'OZON', prefix: '2.', ndsArticle: 'НДС от выручки 2.1' },
            'detsky-mir': { name: '3.1 Детский мир', displayName: 'Детский мир', prefix: '3.', ndsArticle: 'НДС от выручки 3.1' },
            'lamoda': { name: '4.1 Lamoda', displayName: 'Lamoda', prefix: '4.', ndsArticle: 'НДС от выручки 4.1' }
        };
        
        function readExcelFile(file) {
            return new Promise((resolve, reject) => {
                if (typeof XLSX === 'undefined') {
                    reject(new Error('XLSX библиотека не загружена. Проверьте интернет-соединение.'));
                    return;
                }
                const reader = new FileReader();
                reader.onload = function(e) {
                    try {
                        const data = new Uint8Array(e.target.result);
                        const workbook = XLSX.read(data, { type: 'array', cellFormula: false, cellText: false });
                        const firstSheet = workbook.Sheets[workbook.SheetNames[0]];
                        const jsonData = XLSX.utils.sheet_to_json(firstSheet, { defval: "", raw: true, blankrows: false });
                        console.log('Найдено строк в Excel:', jsonData.length);
                        const processed = [];
                        
                        for (const row of jsonData) {
                            let company = row['компания'] || row['Компания'] || '';
                            let year = row['год'] || row['Год'] || '';
                            let month = row['месяц'] || row['Месяц'] || '';
                            let type = row['Статья'] || row['статья'] || '';
                            let channel = row['канал'] || row['Канал'] || '';
                            let subCategory = row['подканал'] || row['Подканал'] || '';
                            let amount = parseFloat(row['сумма'] || row['Сумма'] || 0);
                            
                            company = String(company).trim(); 
                            year = String(year).trim(); 
                            month = String(month).trim();
                            type = String(type).trim();
                            channel = String(channel).trim();
                            subCategory = String(subCategory).trim();
                            
                            if (!type || !year || !month) continue;
                            if (isNaN(amount) || amount === 0) continue;
                            
                            let mappedType = '';
                            if (type === 'Доход') mappedType = 'Доход';
                            else if (type === 'Расход') mappedType = 'Расход';
                            else if (type === 'НДС Исх' || type === 'НДС Вх') mappedType = 'НДС';
                            else if (type === 'Справочно') mappedType = 'Справочная';
                            else continue;
                            
                            processed.push({ 
                                компания: company || 'A', 
                                год: year, 
                                месяц: month, 
                                статья: subCategory,
                                канал: channel,
                                подканал: subCategory,
                                тип: mappedType,
                                сумма: amount 
                            });
                        }
                        
                        console.log('Обработано строк:', processed.length);
                        console.log('Пример первых 5 строк:', processed.slice(0, 5));
                        
                        if (processed.length === 0) {
                            reject(new Error('Не найдено данных для анализа. Проверьте структуру файла.'));
                        } else {
                            resolve(processed);
                        }
                    } catch (error) { 
                        console.error('Ошибка парсинга:', error);
                        reject(error); 
                    }
                };
                reader.onerror = (error) => { reject(error); };
                reader.readAsArrayBuffer(file);
            });
        }
        
        function formatCurrency(value) { return new Intl.NumberFormat('ru-RU', { style: 'currency', currency: 'RUB', minimumFractionDigits: 0 }).format(Math.abs(value)); }
        
        function renderMiniChart(elementId, data, color) {
            if (!data || data.length === 0) return;
            const trace = { y: data, type: 'scatter', mode: 'lines+markers', line: { color, width: 2 }, fill: 'tozeroy', fillcolor: color + '20' };
            const layout = { margin: { t: 5, l: 5, r: 5, b: 5 }, height: 40, xaxis: { showticklabels: false, showgrid: false }, yaxis: { showticklabels: false, showgrid: false }, paper_bgcolor: 'rgba(0,0,0,0)', plot_bgcolor: 'rgba(0,0,0,0)' };
            Plotly.newPlot(elementId, [trace], layout, { displayModeBar: false });
        }
        
        function calculateFinancials(data, channelKey = null) {
            let totalRevenue = 0, totalNDS = 0, totalExpenses = 0;
            let filtered = data;
            if (channelKey && channelMapping[channelKey]) {
                const channel = channelMapping[channelKey];
                filtered = data.filter(row => {
                    if (row.статья.startsWith(channel.prefix)) return true;
                    if (row.статья === channel.ndsArticle) return true;
                    return false;
                });
            }
            filtered.forEach(row => {
                if (row.тип === 'Доход') totalRevenue += row.сумма;
                else if (row.тип === 'НДС') totalNDS += row.сумма;
                else if (row.тип === 'Расход') totalExpenses += Math.abs(row.сумма);
            });
            const netRevenue = totalRevenue - totalNDS;
            const profit = netRevenue - totalExpenses;
            const profitability = netRevenue > 0 ? (profit / netRevenue) * 100 : 0;
            return { totalRevenue, netRevenue, totalNDS, totalExpenses, profit, profitability };
        }

        function generateProfitByChannels(f, revenueChannels, expenseChannels) {
    // Собираем данные по каналам
    const channelsProfit = [];
    
    // Все возможные каналы
    const allChannels = ['Wildberries', 'OZON', 'Детский мир', 'Lamoda', 'Оптовики', 'Фулфилмент'];
    
    allChannels.forEach(channel => {
        const revenueData = revenueChannels.find(r => r.name === channel);
        const expenseData = expenseChannels.find(e => e.name === channel);
        
        const revenue = revenueData ? revenueData.total : 0;
        const expense = expenseData ? expenseData.total : 0;
        const profit = revenue - expense;
        const profitability = revenue > 0 ? (profit / revenue) * 100 : 0;
        
        // Показываем только каналы с ненулевой прибылью или убытком
        if (profit !== 0 && revenue > 0) {
            channelsProfit.push({
                name: channel,
                revenue: revenue,
                expense: expense,
                profit: profit,
                profitability: profitability
            });
        }
    });
    
    // Сортируем по прибыли (от большей к меньшей)
    channelsProfit.sort((a, b) => b.profit - a.profit);
    
    if (channelsProfit.length === 0) {
        return '<div style="text-align: center; padding: 16px; color: var(--text-secondary);">Нет данных по каналам</div>';
    }
    
    // Генерируем HTML для каждого канала
    const channelsHtml = channelsProfit.map((channel, idx) => {
        const profitClass = channel.profit >= 0 ? 'positive' : 'negative';
        const profitIcon = channel.profit >= 0 ? '📈' : '📉';
        const profitPercent = (channel.profit / f.totalProfit) * 100;
        
        return `
            <div class="profit-channel-item" style="margin-bottom: 16px; opacity: 0; transform: translateX(-10px); transition: all 0.3s ease; transition-delay: ${idx * 0.05}s;">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px;">
                    <div style="display: flex; align-items: center; gap: 8px;">
                        <span style="font-size: 16px;">${getChannelIcon(channel.name)}</span>
                        <span style="font-weight: 600; font-size: 14px;">${channel.name}</span>
                    </div>
                    <div style="display: flex; align-items: center; gap: 12px;">
                        <span class="${profitClass}" style="font-weight: 600; font-size: 14px;">${profitIcon} ${formatCurrency(channel.profit)}</span>
                        <span style="font-size: 12px; color: var(--text-secondary); background: rgba(102,126,234,0.15); padding: 2px 8px; border-radius: 12px;">
                            ${profitPercent.toFixed(1)}% от общей
                        </span>
                    </div>
                </div>
                <div style="margin-bottom: 4px;">
                    <div style="display: flex; justify-content: space-between; font-size: 11px; color: var(--text-secondary); margin-bottom: 4px;">
                        <span>Рентабельность: ${channel.profitability.toFixed(1)}%</span>
                        <span>Выручка: ${formatCurrency(channel.revenue)}</span>
                        <span>Расходы: ${formatCurrency(channel.expense)}</span>
                    </div>
                </div>
                <div style="background: rgba(102,126,234,0.1); height: 6px; border-radius: 3px; overflow: hidden;">
                    <div class="profit-progress-bar" style="width: ${Math.abs(profitPercent)}%; height: 100%; background: ${channel.profit >= 0 ? 'linear-gradient(90deg, #48bb78, #38a169)' : 'linear-gradient(90deg, #f56565, #ed8936)'}; border-radius: 3px;"></div>
                </div>
            </div>
        `;
    }).join('');
    
    return `
        <div class="profit-channels-list">
            <div style="margin-bottom: 12px; padding-bottom: 8px; border-bottom: 1px solid rgba(102,126,234,0.2);">
                <span style="font-size: 12px; font-weight: 600; color: #667eea;">РАЗБИВКА ПО КАНАЛАМ</span>
            </div>
            ${channelsHtml}
        </div>
    `;
}

function getChannelIcon(channelName) {
    const icons = {
        'Wildberries': '🛍️',
        'OZON': '📦',
        'Детский мир': '🧸',
        'Lamoda': '👗',
        'Оптовики': '📊',
        'Фулфилмент': '🚚'
    };
    return icons[channelName] || '📁';
}
        
        function renderDashboard() {
            if (isRendering) {
                console.log('Рендер уже выполняется, пропускаем');
                return;
            }
            isRendering = true;
            
            try {
                if (!currentData.length) { 
                    document.getElementById('dashboardMetrics').innerHTML = '<div class="loading">Нет данных</div>'; 
                    isRendering = false;
                    return; 
                }
                
                const companyFilter = document.getElementById('companyFilter');
                const yearFilter = document.getElementById('yearFilter');
                const monthSelect = document.getElementById('monthFilter');
                const selectedMonths = monthSelect ? Array.from(monthSelect.selectedOptions).map(o => o.value) : [];
                
                currentFilters.company = companyFilter ? companyFilter.value : '';
                currentFilters.year = yearFilter ? yearFilter.value : '';
                currentFilters.month = selectedMonths;
                
                function getPreviousMonths(months, count = 1) {
                    const prevMonths = [];
                    for (const month of months) {
                        const monthIndex = monthsOrder.indexOf(month);
                        if (monthIndex !== -1) {
                            let prevIndex = monthIndex - count;
                            let yearOffset = 0;
                            while (prevIndex < 0) {
                                prevIndex += 12;
                                yearOffset--;
                            }
                            prevMonths.push(monthsOrder[prevIndex % 12]);
                        }
                    }
                    return prevMonths;
                }
                
                const prevMonths = getPreviousMonths(selectedMonths, 1);
                let prevData = [];
                if (prevMonths.length > 0 && currentFilters.year) {
                    let prevYear = parseInt(currentFilters.year);
                    if (prevMonths[0] === 'декабрь' && selectedMonths[0] === 'январь') {
                        prevYear = prevYear - 1;
                    }
                    prevData = originalData.filter(row => {
                        if (currentFilters.company && row.компания !== currentFilters.company) return false;
                        if (row.год != prevYear) return false;
                        if (!prevMonths.includes(row.месяц)) return false;
                        return true;
                    });
                }
                
                const f = calculateFinancials(currentData);
                const fPrev = prevData.length > 0 ? calculateFinancials(prevData) : null;
                
                function getChangePercent(current, previous) {
                    if (!previous || previous === 0) return null;
                    const change = ((current - previous) / previous) * 100;
                    return { percent: change, isPositive: change >= 0, formatted: `${change > 0 ? '+' : ''}${change.toFixed(1)}%` };
                }
                
                const revenueChange = fPrev ? getChangePercent(f.totalRevenue, fPrev.totalRevenue) : null;
                const ndsChange = fPrev ? getChangePercent(f.totalNDS, fPrev.totalNDS) : null;
                const netRevenueChange = fPrev ? getChangePercent(f.netRevenue, fPrev.netRevenue) : null;
                const expensesChange = fPrev ? getChangePercent(f.totalExpenses, fPrev.totalExpenses) : null;
                const profitChange = fPrev ? getChangePercent(f.profit, fPrev.profit) : null;
                const profitabilityChange = fPrev ? getChangePercent(f.profitability, fPrev.profitability) : null;
                
                // Собираем данные для метрик продаж и себестоимости
const salesData = currentData
    .filter(d => d.статья === 'Продажи шт.')
    .reduce((sum, d) => sum + (d.сумма || 0), 0);

const costData = currentData
    .filter(d => d.статья === 'Себестоимость сырья')
    .reduce((sum, d) => sum + Math.abs(d.сумма || 0), 0);

const avgCheck = salesData > 0 ? f.netRevenue / salesData : 0;
const avgCost = salesData > 0 ? costData / salesData : 0;

// Данные за предыдущий период для продаж и себестоимости
const prevSalesData = prevData.length > 0 
    ? prevData.filter(d => d.статья === 'Продажи шт.').reduce((sum, d) => sum + (d.сумма || 0), 0) 
    : 0;
    
const prevCostData = prevData.length > 0 
    ? prevData.filter(d => d.статья === 'Себестоимость сырья').reduce((sum, d) => sum + Math.abs(d.сумма || 0), 0) 
    : 0;
    
const prevNetRevenue = fPrev ? fPrev.netRevenue : 0;
const prevAvgCheck = prevSalesData > 0 ? prevNetRevenue / prevSalesData : 0;
const prevAvgCost = prevSalesData > 0 ? prevCostData / prevSalesData : 0;
                
                const salesChange = fPrev ? getChangePercent(salesData, prevSalesData) : null;
                const avgCheckChange = fPrev ? getChangePercent(avgCheck, prevAvgCheck) : null;
                const costChange = fPrev ? getChangePercent(costData, prevCostData) : null;
                const avgCostChange = fPrev ? getChangePercent(avgCost, prevAvgCost) : null;
                
                const efficiency = f.profit / (f.totalExpenses || 1);
                const prevEfficiency = fPrev ? fPrev.profit / (fPrev.totalExpenses || 1) : 0;
                const efficiencyChange = fPrev ? getChangePercent(efficiency, prevEfficiency) : null;
                
                const monthlyExpenses = {};
                currentData.forEach(d => {
                    if (d.месяц && d.год && d.тип === 'Расход') {
                        const monthIndex = monthsOrder.indexOf(d.месяц);
                        if (monthIndex === -1) return;
                        const key = `${d.год}-${monthIndex}`;
                        monthlyExpenses[key] = (monthlyExpenses[key] || 0) + Math.abs(d.сумма || 0);
                    }
                });
                const expensesTrend = Object.values(monthlyExpenses);
                
                // Анализ расходов по каналам
                const expensesByChannel = {};
                currentData.forEach(d => {
                    if (d.тип === 'Расход' && d.канал) {
                        let channel = d.канал;
                        if (channel === 'Wildberries') channel = 'Wildberries';
                        else if (channel === 'Ozon') channel = 'OZON';
                        else if (channel === 'Детский мир') channel = 'Детский мир';
                        else if (channel === 'Lamoda') channel = 'Lamoda';
                        else if (channel === 'Оптовики') channel = 'Оптовики';
                        
                        if (!expensesByChannel[channel]) expensesByChannel[channel] = { total: 0, items: {} };
                        const amount = Math.abs(d.сумма);
                        expensesByChannel[channel].total += amount;
                        expensesByChannel[channel].items[d.подканал] = (expensesByChannel[channel].items[d.подканал] || 0) + amount;
                    }
                });
                
                // Анализ доходов по каналам - ТОЛЬКО ДОХОДЫ
                const revenueByChannel = {};
                currentData.forEach(d => {
                    if (d.тип === 'Доход' && d.канал) {
                        let channel = d.канал;
                        if (channel === 'Wildberries') channel = 'Wildberries';
                        else if (channel === 'Ozon') channel = 'OZON';
                        else if (channel === 'Детский мир') channel = 'Детский мир';
                        else if (channel === 'Lamoda') channel = 'Lamoda';
                        else if (channel === 'Оптовики') channel = 'Оптовики';
                        else if (channel === 'Фулфилмент') channel = 'Фулфилмент';
                        
                        if (!revenueByChannel[channel]) revenueByChannel[channel] = { total: 0, items: {} };
                        revenueByChannel[channel].total += d.сумма;
                        revenueByChannel[channel].items[d.подканал] = (revenueByChannel[channel].items[d.подканал] || 0) + d.сумма;
                    }
                });
                
                console.log('=== ДОХОДЫ ПО КАНАЛАМ ===');
                Object.entries(revenueByChannel).forEach(([channel, data]) => {
                    console.log(`${channel}: ${formatCurrency(data.total)}`);
                    console.log('  Статьи:', data.items);
                });
                
                const revenueChannelsList = Object.entries(revenueByChannel)
                    .filter(([_, data]) => data.total > 0)
                    .sort((a, b) => b[1].total - a[1].total)
                    .map(([name, data]) => ({
                        name,
                        total: data.total,
                        items: Object.entries(data.items).map(([itemName, amount]) => ({ name: itemName, amount })).sort((a, b) => b.amount - a.amount)
                    }));
                
                const expenseChannelsList = Object.entries(expensesByChannel)
                    .filter(([_, data]) => data.total > 0)
                    .sort((a, b) => b[1].total - a[1].total)
                    .map(([name, data]) => ({
                        name,
                        total: data.total,
                        items: Object.entries(data.items).map(([itemName, amount]) => ({ name: itemName, amount })).sort((a, b) => b.amount - a.amount)
                    }));
                
                const oldData = {
                    totalRevenue: f.totalRevenue, totalNDS: f.totalNDS, netRevenue: f.netRevenue,
                    totalExpenses: f.totalExpenses, profit: f.profit, profitability: f.profitability,
                    totalProfit: f.profit,
                    salesData: salesData, avgCheck: avgCheck, costData: costData, avgCost: avgCost,
                    efficiency: efficiency, expensesTrend: expensesTrend,
                    expenseChannels: expenseChannelsList, revenueChannels: revenueChannelsList
                };
                
                function animateNumber(element, start, end, duration = 600, isCurrency = true, isPercent = false) {
                    if (!element) return Promise.resolve();
                    if (element._animationFrame) cancelAnimationFrame(element._animationFrame);
                    return new Promise((resolve) => {
                        const startTime = performance.now();
                        function update(currentTime) {
                            const elapsed = currentTime - startTime;
                            const progress = Math.min(elapsed / duration, 1);
                            const easeOutCubic = 1 - Math.pow(1 - progress, 3);
                            const currentValue = start + (end - start) * easeOutCubic;
                            if (isPercent) element.innerHTML = currentValue.toFixed(1);
                            else if (isCurrency) element.innerHTML = formatCurrency(currentValue);
                            else element.innerHTML = currentValue.toFixed(2);
                            if (progress < 1) element._animationFrame = requestAnimationFrame(update);
                            else { 
                                if (isPercent) element.innerHTML = end.toFixed(1);
                                else if (isCurrency) element.innerHTML = formatCurrency(end);
                                else element.innerHTML = end.toFixed(2);
                                delete element._animationFrame;
                                resolve();
                            }
                        }
                        element._animationFrame = requestAnimationFrame(update);
                    });
                }
                
                function animateProgressBar(bar, oldPercent, newPercent, duration = 500) {
                    if (!bar) return Promise.resolve();
                    if (bar._animationFrame) cancelAnimationFrame(bar._animationFrame);
                    return new Promise((resolve) => {
                        const startTime = performance.now();
                        function update(currentTime) {
                            const elapsed = currentTime - startTime;
                            const progress = Math.min(elapsed / duration, 1);
                            const easeOutCubic = 1 - Math.pow(1 - progress, 3);
                            const currentPercent = oldPercent + (newPercent - oldPercent) * easeOutCubic;
                            bar.style.width = `${currentPercent}%`;
                            if (progress < 1) {
                                bar._animationFrame = requestAnimationFrame(update);
                            } else {
                                bar.style.width = `${newPercent}%`;
                                delete bar._animationFrame;
                                resolve();
                            }
                        }
                        bar._animationFrame = requestAnimationFrame(update);
                    });
                }
                
                function getChangeHtml(change, isExpense = false) {
                    if (!change) return '<span style="font-size: 11px; color: var(--text-secondary);">нет данных для сравнения</span>';
                    let isPositive = change.isPositive;
                    if (isExpense) isPositive = !isPositive;
                    const colorClass = isPositive ? 'change-positive' : 'change-negative';
                    return `<span class="metric-change ${colorClass}" style="font-size: 11px; padding: 2px 6px; border-radius: 12px; display: inline-block;">${change.formatted}</span>`;
                }
                
                function createCollapsibleBlock(title, icon, total, totalChange, channels, isExpense = false) {
    const channelItemsHtml = channels.map((channel, channelIdx) => {
        const channelPercent = (channel.total / total) * 100;
        const sortedItems = [...channel.items].sort((a, b) => b.amount - a.amount);
        const itemsHtml = sortedItems.map((item, itemIdx) => {
            const itemPercentOfTotal = (item.amount / total) * 100;
            const itemPercentOfChannel = (item.amount / channel.total) * 100;
            // Градиент для подканалов
            const gradient = isExpense 
                ? 'linear-gradient(90deg, #f56565, #ed8936)'  // красный/оранжевый для расходов
                : 'linear-gradient(90deg, #48bb78, #8dd934)'; // зеленый для доходов
            return `
                <div class="sub-item" data-item-name="${item.name}" style="margin-bottom: 12px; opacity: 0; transform: translateX(-10px); transition: all 0.3s ease; transition-delay: ${itemIdx * 0.03}s;">
                    <div style="display: flex; justify-content: space-between; margin-bottom: 6px; flex-wrap: wrap; gap: 8px;">
                        <span style="font-size: 13px; font-weight: 500;">${item.name}</span>
                        <div style="display: flex; gap: 12px; flex-wrap: wrap;">
                            <span style="font-size: 13px; font-weight: 600;">${formatCurrency(item.amount)}</span>
                            <span style="font-size: 12px; color: var(--text-secondary); background: rgba(102,126,234,0.1); padding: 2px 8px; border-radius: 12px;">
                                ${itemPercentOfTotal.toFixed(1)}% от дохода
                            </span>
                        </div>
                    </div>
                    <div style="background: rgba(102,126,234,0.15); height: 6px; border-radius: 3px; overflow: hidden;">
                        <div class="sub-progress-bar" style="width: ${itemPercentOfChannel}%; height: 100%; background: ${gradient}; border-radius: 3px;"></div>
                    </div>
                </div>
            `;
        }).join('');
        
        // Градиент для основного прогресс-бара канала
        const channelGradient = isExpense 
            ? 'linear-gradient(90deg, #f56565, #ed8936)'
            : 'linear-gradient(90deg, #48bb78, #8dd934)';
        
        return `
            <div class="channel-item" data-channel-name="${channel.name}" style="margin-bottom: 20px; border-bottom: 1px solid rgba(102,126,234,0.2); padding-bottom: 16px;">
                <div class="channel-header" style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; cursor: pointer;">
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <span class="channel-icon" style="font-size: 20px;">${channel.name === 'Wildberries' ? '🛍️' : channel.name === 'OZON' ? '📦' : channel.name === 'Детский мир' ? '🧸' : channel.name === 'Lamoda' ? '👗' : channel.name === 'Оптовики' ? '📊' : '📁'}</span>
                        <span style="font-weight: 700; font-size: 15px;">${channel.name}</span>
                    </div>
                    <div style="display: flex; align-items: center; gap: 12px;">
                        <span class="channel-total" style="font-size: 14px; font-weight: 600;">${formatCurrency(channel.total)}</span>
                        <span class="channel-percent" style="font-size: 12px; color: var(--text-secondary); background: rgba(102,126,234,0.15); padding: 2px 8px; border-radius: 12px;">
                            ${channelPercent.toFixed(1)}%
                        </span>
                        <span class="expand-icon" style="font-size: 14px; transition: transform 0.3s; cursor: pointer;">▶</span>
                    </div>
                </div>
                <div style="background: rgba(102,126,234,0.1); height: 8px; border-radius: 4px; margin-bottom: 12px; overflow: hidden;">
                    <div class="channel-progress-bar" style="width: ${channelPercent}%; height: 100%; background: ${channelGradient}; border-radius: 4px;"></div>
                </div>
                <div class="channel-details" style="max-height: 0; overflow: hidden; transition: max-height 0.4s cubic-bezier(0.4, 0, 0.2, 1);">
                    <div style="padding-top: 12px; padding-left: 30px;">${itemsHtml}</div>
                </div>
            </div>
        `;
    }).join('');
    
    return `
        <div class="metric-card" style="overflow: hidden; padding: 20px; height: 100%; display: flex; flex-direction: column;">
            <div class="metric-title" style="display: flex; align-items: center; gap: 8px; margin-bottom: 16px;">
                <span style="font-size: 20px;">${icon}</span>
                <span style="font-size: 16px; font-weight: 700;">${title}</span>
            </div>
            <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 12px; margin-bottom: 16px; padding-bottom: 12px; border-bottom: 1px solid rgba(102,126,234,0.2);">
                <div>
                    <div class="metric-value" id="${isExpense ? 'expensesTotal' : 'revenueTotal'}" style="font-size: 28px;">${formatCurrency(total)}</div>
                    ${getChangeHtml(totalChange, isExpense)}
                </div>
                <div style="display: flex; align-items: center; gap: 12px;">
                    <div class="mini-chart" id="${isExpense ? 'expensesMiniChart' : 'revenueMiniChart'}" style="width: 100px; height: 40px;"></div>
                    <div class="metric-sub">общая сумма</div>
                </div>
            </div>
            <div class="channels-container" style="flex: 1; overflow-y: visible; padding-right: 5px;">
                ${channelItemsHtml}
            </div>
            <button class="toggle-all-channels-btn" style="margin-top: 16px; background: none; border: none; color: #667eea; cursor: pointer; font-size: 13px; display: flex; align-items: center; gap: 6px; padding: 8px 0; width: 100%; justify-content: center;">
                <span>▶</span> Показать все подканалы
            </button>
        </div>
    `;
}
                
                const revenueHtml = createCollapsibleBlock('Доходы по каналам', '💰', f.totalRevenue, revenueChange, revenueChannelsList, false);
                const expensesHtml = createCollapsibleBlock('Расходы по каналам', '📉', f.totalExpenses, expensesChange, expenseChannelsList, true);
                
                document.getElementById('dashboardMetrics').innerHTML = `
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 24px;">
        ${revenueHtml}
        ${expensesHtml}
    </div>
    <div class="metrics-grid" style="margin-top: 24px;">
        <div class="metric-card">
            <div class="metric-title" style="display: flex; align-items: center; justify-content: space-between; margin-bottom: 16px;">
                <div style="display: flex; align-items: center; gap: 8px;">
                    <span style="font-size: 18px;">📈</span>
                    <span>Маржинальная прибыль</span>
                </div>
                <button class="toggle-channels-profit-btn" style="background: none; border: none; color: #667eea; cursor: pointer; font-size: 12px; display: flex; align-items: center; gap: 4px; padding: 4px 8px; border-radius: 8px; transition: all 0.2s;">
                    <span>▶</span> Показать по каналам
                </button>
            </div>
            <div><div class="metric-value ${f.profit>=0?'positive':'negative'}" id="mainProfitValue">${formatCurrency(f.profit)}</div>${getChangeHtml(profitChange)}</div>
            <div class="metric-sub" style="margin-top: 4px;">Рентабельность: <span id="mainProfitabilityValue">${f.profitability.toFixed(1)}</span>% ${getChangeHtml(profitabilityChange)}</div>
            <div class="mini-chart" id="miniProfitChart" style="margin-top: 12px;"></div>
            <div class="profit-channels-container" style="max-height: 0; overflow: hidden; transition: max-height 0.4s cubic-bezier(0.4, 0, 0.2, 1); margin-top: 16px; border-top: 1px solid rgba(102,126,234,0.2);">
                <div style="padding-top: 16px;">
                    ${generateProfitByChannels(f, revenueChannelsList, expenseChannelsList)}
                </div>
            </div>
        </div>
        <div class="metric-card"><div class="metric-title">💸 НДС</div><div><div class="metric-value" id="mainNdsValue">${formatCurrency(f.totalNDS)}</div>${getChangeHtml(ndsChange)}</div></div>
        <div class="metric-card"><div class="metric-title">📊 Выручка чистая</div><div><div class="metric-value" id="mainNetRevenueValue">${formatCurrency(f.netRevenue)}</div>${getChangeHtml(netRevenueChange)}</div><div class="mini-chart" id="miniNetRevenueChart"></div></div>
        <div class="metric-card"><div class="metric-title">📊 Эффективность</div><div><div class="metric-value" id="mainEfficiencyValue">${(f.profit / (f.totalExpenses || 1)).toFixed(2)} ₽</div>${getChangeHtml(efficiencyChange)}</div><div class="metric-sub">прибыли на 1 рубль расходов</div></div>
    </div>
    <div class="metrics-grid" style="margin-top: 24px;">
        <div class="metric-card"><div class="metric-title">📦 Продажи (шт)</div><div><div class="metric-value" id="mainSalesValue">${new Intl.NumberFormat('ru-RU').format(salesData)}</div>${getChangeHtml(salesChange)}</div><div class="mini-chart" id="dashboardSalesChart"></div><div class="metric-sub">всего за период</div></div>
        <div class="metric-card"><div class="metric-title">💰 Средний чек</div><div><div class="metric-value" id="mainAvgCheckValue">${formatCurrency(avgCheck)}</div>${getChangeHtml(avgCheckChange)}</div><div class="metric-sub">на 1 продажу</div></div>
        <div class="metric-card"><div class="metric-title">🏭 Себестоимость сырья</div><div><div class="metric-value" id="mainCostValue">${formatCurrency(costData)}</div>${getChangeHtml(costChange, true)}</div><div class="mini-chart" id="dashboardCostChart"></div><div class="metric-sub">общая за период</div></div>
        <div class="metric-card"><div class="metric-title">📊 Себестоимость 1 шт</div><div><div class="metric-value" id="mainAvgCostValue">${formatCurrency(avgCost)}</div>${getChangeHtml(avgCostChange, true)}</div><div class="metric-sub">на единицу товара</div></div>
    </div>
`;

// Добавляем обработчик для кнопки "Показать по каналам"
setTimeout(() => {
    const toggleProfitBtn = document.querySelector('.toggle-channels-profit-btn');
    const profitChannelsContainer = document.querySelector('.profit-channels-container');
    
    if (toggleProfitBtn && profitChannelsContainer) {
        toggleProfitBtn.onclick = () => {
            if (profitChannelsContainer.style.maxHeight && profitChannelsContainer.style.maxHeight !== '0px') {
                profitChannelsContainer.style.maxHeight = '0';
                toggleProfitBtn.innerHTML = '<span>▶</span> Показать по каналам';
            } else {
                profitChannelsContainer.style.maxHeight = profitChannelsContainer.scrollHeight + 'px';
                toggleProfitBtn.innerHTML = '<span>▼</span> Скрыть по каналам';
                
                const items = profitChannelsContainer.querySelectorAll('.profit-channel-item');
                items.forEach((item, idx) => {
                    setTimeout(() => {
                        item.style.opacity = '1';
                        item.style.transform = 'translateX(0)';
                    }, idx * 50);
                });
            }
        };
    }
}, 150);

      
                
                const monthlyRevenue = {};
                currentData.forEach(d => {
                    if (d.месяц && d.год && d.тип === 'Доход') {
                        const monthIndex = monthsOrder.indexOf(d.месяц);
                        if (monthIndex === -1) return;
                        const key = `${d.год}-${monthIndex}`;
                        monthlyRevenue[key] = (monthlyRevenue[key] || 0) + (d.сумма || 0);
                    }
                });
                
                const animations = [
                    animateNumber(document.getElementById('mainNdsValue'), oldData.totalNDS, f.totalNDS, 600),
                    animateNumber(document.getElementById('mainNetRevenueValue'), oldData.netRevenue, f.netRevenue, 600),
                    animateNumber(document.getElementById('mainProfitValue'), oldData.profit, f.profit, 600),
                    animateNumber(document.getElementById('mainEfficiencyValue'), oldData.efficiency, f.profit / (f.totalExpenses || 1), 600, false, false),
                    animateNumber(document.getElementById('mainSalesValue'), oldData.salesData, salesData, 600),
                    animateNumber(document.getElementById('mainAvgCheckValue'), oldData.avgCheck, avgCheck, 600),
                    animateNumber(document.getElementById('mainCostValue'), oldData.costData, costData, 600),
                    animateNumber(document.getElementById('mainAvgCostValue'), oldData.avgCost, avgCost, 600),
                    animateNumber(document.getElementById('mainProfitabilityValue'), oldData.profitability, f.profitability, 600, false, true)
                ];
                
                Promise.all(animations).then(() => {
    console.log('Анимации завершены');
    // Анимация прогресс-баров временно отключена для проверки
    // setTimeout(() => {
    //     revenueChannelsList.forEach((channel, idx) => {
    //         const oldChannel = oldData.revenueChannels.find(c => c.name === channel.name);
    //         const oldPercent = oldChannel ? (oldChannel.total / oldData.totalRevenue) * 100 : 0;
    //         const newPercent = (channel.total / f.totalRevenue) * 100;
    //         const channelDiv = document.querySelector(`#dashboardMetrics .channel-item[data-channel-name="${channel.name}"]`);
    //         if (channelDiv) {
    //             const progressBar = channelDiv.querySelector('.channel-progress-bar');
    //             const totalSpan = channelDiv.querySelector('.channel-total');
    //             const percentSpan = channelDiv.querySelector('.channel-percent');
    //             if (totalSpan) animateNumber(totalSpan, oldChannel?.total || 0, channel.total, 400);
    //             if (percentSpan) animateNumber(percentSpan, oldPercent, newPercent, 400, false, true);
    //             if (progressBar) animateProgressBar(progressBar, oldPercent, newPercent, 400);
    //         }
    //     });
    //     expenseChannelsList.forEach((channel, idx) => {
    //         const oldChannel = oldData.expenseChannels.find(c => c.name === channel.name);
    //         const oldPercent = oldChannel ? (oldChannel.total / oldData.totalExpenses) * 100 : 0;
    //         const newPercent = (channel.total / f.totalExpenses) * 100;
    //         const channelDiv = document.querySelector(`#dashboardMetrics .channel-item[data-channel-name="${channel.name}"]`);
    //         if (channelDiv) {
    //             const progressBar = channelDiv.querySelector('.channel-progress-bar');
    //             const totalSpan = channelDiv.querySelector('.channel-total');
    //             const percentSpan = channelDiv.querySelector('.channel-percent');
    //             if (totalSpan) animateNumber(totalSpan, oldChannel?.total || 0, channel.total, 400);
    //             if (percentSpan) animateNumber(percentSpan, oldPercent, newPercent, 400, false, true);
    //             if (progressBar) animateProgressBar(progressBar, oldPercent, newPercent, 400);
    //         }
    //     });
    // }, 50);
});
                
                setTimeout(() => {
                    const channelHeaders = document.querySelectorAll('.channel-header');
                    channelHeaders.forEach(header => {
                        const channelDiv = header.closest('.channel-item');
                        const detailsDiv = channelDiv.querySelector('.channel-details');
                        const expandIcon = header.querySelector('.expand-icon');
                        const channelName = channelDiv.dataset.channelName;
                        
                        if (window._openChannels && window._openChannels[channelName]) {
                            detailsDiv.style.maxHeight = detailsDiv.scrollHeight + 'px';
                            if (expandIcon) expandIcon.style.transform = 'rotate(90deg)';
                            const items = detailsDiv.querySelectorAll('.sub-item');
                            items.forEach((item, idx) => {
                                setTimeout(() => { item.style.opacity = '1'; item.style.transform = 'translateX(0)'; }, idx * 30);
                            });
                        }
                        
                        header.removeEventListener('click', header._clickHandler);
                        const handler = (e) => {
                            e.stopPropagation();
                            const currentChannelDiv = header.closest('.channel-item');
                            const currentDetailsDiv = currentChannelDiv.querySelector('.channel-details');
                            const currentExpandIcon = header.querySelector('.expand-icon');
                            const currentChannelName = currentChannelDiv.dataset.channelName;
                            if (!window._openChannels) window._openChannels = {};
                            if (currentDetailsDiv.style.maxHeight && currentDetailsDiv.style.maxHeight !== '0px') {
                                currentDetailsDiv.style.maxHeight = '0';
                                if (currentExpandIcon) currentExpandIcon.style.transform = 'rotate(0deg)';
                                window._openChannels[currentChannelName] = false;
                            } else {
                                currentDetailsDiv.style.maxHeight = currentDetailsDiv.scrollHeight + 'px';
                                if (currentExpandIcon) currentExpandIcon.style.transform = 'rotate(90deg)';
                                window._openChannels[currentChannelName] = true;
                                const items = currentDetailsDiv.querySelectorAll('.sub-item');
                                items.forEach((item, idx) => {
                                    setTimeout(() => { item.style.opacity = '1'; item.style.transform = 'translateX(0)'; }, idx * 30);
                                });
                            }
                        };
                        header._clickHandler = handler;
                        header.addEventListener('click', handler);
                    });
                    
                    const toggleAllBtns = document.querySelectorAll('.toggle-all-channels-btn');
                    toggleAllBtns.forEach(btn => {
                        btn.removeEventListener('click', btn._toggleHandler);
                        const handler = (e) => {
                            e.stopPropagation();
                            const container = btn.closest('.metric-card').querySelector('.channels-container');
                            const allChannelItems = container.querySelectorAll('.channel-item');
                            const allExpandIcons = container.querySelectorAll('.expand-icon');
                            const allDetailsDivs = container.querySelectorAll('.channel-details');
                            const allOpen = Array.from(allDetailsDivs).every(details => details.style.maxHeight && details.style.maxHeight !== '0px');
                            if (allOpen) {
                                allDetailsDivs.forEach(details => details.style.maxHeight = '0');
                                allExpandIcons.forEach(icon => icon.style.transform = 'rotate(0deg)');
                                btn.innerHTML = '<span>▶</span> Показать все подканалы';
                                allChannelItems.forEach(item => { if (window._openChannels) window._openChannels[item.dataset.channelName] = false; });
                            } else {
                                allDetailsDivs.forEach(details => { details.style.maxHeight = details.scrollHeight + 'px'; });
                                allExpandIcons.forEach(icon => icon.style.transform = 'rotate(90deg)');
                                btn.innerHTML = '<span>▼</span> Скрыть все подканалы';
                                allDetailsDivs.forEach((details, idx) => {
                                    const items = details.querySelectorAll('.sub-item');
                                    items.forEach((item, itemIdx) => {
                                        setTimeout(() => { item.style.opacity = '1'; item.style.transform = 'translateX(0)'; }, idx * 50 + itemIdx * 30);
                                    });
                                });
                                allChannelItems.forEach(item => { if (window._openChannels) window._openChannels[item.dataset.channelName] = true; });
                            }
                        };
                        btn._toggleHandler = handler;
                        btn.addEventListener('click', handler);
                    });
                }, 150);
                
                const monthlyNDS = {};
                currentData.forEach(d => {
                    if (d.месяц && d.год && d.тип === 'НДС') {
                        const monthIndex = monthsOrder.indexOf(d.месяц);
                        if (monthIndex === -1) return;
                        const key = `${d.год}-${monthIndex}`;
                        monthlyNDS[key] = (monthlyNDS[key] || 0) + (d.сумма || 0);
                    }
                });
                
                if (document.getElementById('revenueMiniChart')) {
                    const revenueData = Object.values(monthlyRevenue).sort((a, b) => a - b);
                    renderMiniChart('revenueMiniChart', revenueData, '#48bb78');
                }
                if (document.getElementById('expensesMiniChart')) {
                    const expensesData = Object.values(monthlyExpenses).sort((a, b) => a - b);
                    renderMiniChart('expensesMiniChart', expensesData, '#f56565');
                }
                if (document.getElementById('miniNetRevenueChart')) {
                    const sortedKeys = Object.keys(monthlyRevenue).sort();
                    const netRevenueData = sortedKeys.map(key => {
                        const revenue = monthlyRevenue[key] || 0;
                        const nds = monthlyNDS[key] || 0;
                        return revenue - nds;
                    });
                    renderMiniChart('miniNetRevenueChart', netRevenueData, '#4299e1');
                }
                
                const monthlySales = {}, monthlyCost = {};
                currentData.forEach(d => {
                    if (d.месяц && d.год) {
                        const monthIndex = monthsOrder.indexOf(d.месяц);
                        if (monthIndex === -1) return;
                        const key = `${d.год}-${monthIndex}`;
                        if (d.статья === 'Продажи шт.') monthlySales[key] = (monthlySales[key] || 0) + (d.сумма || 0);
                        if (d.статья === 'Себестоимость сырья') monthlyCost[key] = (monthlyCost[key] || 0) + Math.abs(d.сумма || 0);
                    }
                });
                renderMiniChart('dashboardSalesChart', Object.values(monthlySales), '#48bb78');
                renderMiniChart('dashboardCostChart', Object.values(monthlyCost), '#f56565');
                
                const aiInsightsDiv = document.getElementById('aiInsights');
                if (aiInsightsDiv) {
                    const expensesText = expenseChannelsList.map(channel => {
                        const percent = (channel.total / f.totalExpenses) * 100;
                        return `• ${channel.name}: ${formatCurrency(channel.total)} (${percent.toFixed(1)}%)`;
                    }).join('\n');
                    aiInsightsDiv.innerHTML = `<div class="ai-header"><div class="ai-icon" style="background: #48bb78;">🤖</div><div><div class="ai-title">AI Аналитика</div><div class="ai-subtitle">Автоматический анализ ваших данных</div></div></div>
                    <div class="ai-message assistant">📊 **Общий анализ:**\nВыручка: ${formatCurrency(f.totalRevenue)}\nПрибыль: ${formatCurrency(f.profit)}\nРентабельность: ${f.profitability.toFixed(1)}%\nПродажи: ${new Intl.NumberFormat('ru-RU').format(salesData)} шт\nСредний чек: ${formatCurrency(avgCheck)}\nСебестоимость 1 шт: ${formatCurrency(avgCost)}\n\n💰 **Структура доходов по каналам:**\n${revenueChannelsList.map(ch => `• ${ch.name}: ${formatCurrency(ch.total)} (${(ch.total/f.totalRevenue*100).toFixed(1)}%)`).join('\n')}\n\n📉 **Структура расходов по каналам:**\n${expensesText}</div>
                    <div style="margin-top: 12px;"><button id="askAIBtn" class="btn btn-info">💬 Задать вопрос AI</button></div>`;
                    document.getElementById('askAIBtn')?.addEventListener('click', () => { 
                        document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
                        document.querySelectorAll('.nav-subitem').forEach(n => n.classList.remove('active'));
                        document.querySelector('.nav-item[data-page="ai"]').classList.add('active');
                        document.querySelectorAll('.page-content').forEach(c => c.classList.remove('active'));
                        document.getElementById('page-ai').classList.add('active');
                    });
                }
            } finally {
                isRendering = false;
            }
        }
        
        function renderChannelPage(channelKey) {
            const channel = channelMapping[channelKey];
            if (!channel) return;
            const f = calculateFinancials(currentData, channelKey);
            const salesData = currentData.find(d => d.статья === 'Продажи шт.')?.сумма || 0;
            const costData = Math.abs(currentData.find(d => d.статья === 'Себестоимость сырья')?.сумма || 0);
            const avgCheck = salesData > 0 ? f.netRevenue / salesData : 0;
            const avgCost = salesData > 0 ? costData / salesData : 0;
            
            const content = `
                <div class="metrics-grid">
                    <div class="metric-card"><div class="metric-title">💰 Выручка (с НДС)</div><div class="metric-value">${formatCurrency(f.totalRevenue)}</div><div class="mini-chart" id="chRevenueChart"></div></div>
                    <div class="metric-card"><div class="metric-title">💸 НДС</div><div class="metric-value">${formatCurrency(f.totalNDS)}</div><div class="mini-chart" id="chNdsChart"></div></div>
                    <div class="metric-card"><div class="metric-title">📊 Выручка чистая</div><div class="metric-value">${formatCurrency(f.netRevenue)}</div><div class="mini-chart" id="chNetRevenueChart"></div></div>
                    <div class="metric-card"><div class="metric-title">📉 Расходы</div><div class="metric-value">${formatCurrency(f.totalExpenses)}</div><div class="metric-sub">${((f.totalExpenses/f.netRevenue)*100).toFixed(1)}%</div></div>
                    <div class="metric-card"><div class="metric-title">📈 Прибыль</div><div class="metric-value ${f.profit>=0?'positive':'negative'}">${formatCurrency(f.profit)}</div><div class="metric-sub">Рентабельность: ${f.profitability.toFixed(1)}%</div></div>
                    <div class="metric-card"><div class="metric-title">📊 Маржинальность</div><div class="metric-value">${f.profitability.toFixed(1)}%</div></div>
                </div>
                <div class="metrics-grid" style="margin-top:20px">
                    <div class="metric-card"><div class="metric-title">📦 Продажи (шт)</div><div class="metric-value">${new Intl.NumberFormat('ru-RU').format(salesData)}</div><div class="mini-chart" id="chSalesChart"></div></div>
                    <div class="metric-card"><div class="metric-title">💰 Средний чек</div><div class="metric-value">${formatCurrency(avgCheck)}</div></div>
                    <div class="metric-card"><div class="metric-title">🏭 Себестоимость</div><div class="metric-value">${formatCurrency(costData)}</div><div class="mini-chart" id="chCostChart"></div></div>
                    <div class="metric-card"><div class="metric-title">📊 Себестоимость 1 шт</div><div class="metric-value">${formatCurrency(avgCost)}</div></div>
                </div>
            `;
            document.getElementById(`channel${channelKey.charAt(0).toUpperCase() + channelKey.slice(1)}Metrics`).innerHTML = content;
            renderMiniChart('chRevenueChart', [f.totalRevenue], '#48bb78');
            renderMiniChart('chNdsChart', [f.totalNDS], '#f59e0b');
            renderMiniChart('chNetRevenueChart', [f.netRevenue], '#4299e1');
            renderMiniChart('chProfitChart', [f.profit], '#667eea');
            renderMiniChart('chSalesChart', [salesData], '#48bb78');
            renderMiniChart('chCostChart', [costData], '#f56565');
        }
        
        function initApp() {
    // Проверяем существование всех необходимых элементов
    const fileInput = document.getElementById('fileInput');
    const uploadArea = document.getElementById('uploadArea');
    const changeDataBtn = document.getElementById('changeDataBtn');
    const resetFiltersBtn = document.getElementById('resetFilters');
    const companyFilter = document.getElementById('companyFilter');
    const yearFilter = document.getElementById('yearFilter');
    const monthFilter = document.getElementById('monthFilter');
    
    if (!companyFilter || !yearFilter || !monthFilter) {
        console.error('Не найдены элементы фильтров');
        return;
    }
    
    // Добавляем обработчик для сворачивания фильтров с проверкой
    setTimeout(() => {
        const filtersSidebarToggle = document.getElementById('filtersSidebarToggle');
        const filtersSidebarContent = document.getElementById('filtersSidebarContent');
        
        if (filtersSidebarToggle && filtersSidebarContent) {
            const toggleIconSidebar = filtersSidebarToggle.querySelector('.toggle-icon');
            filtersSidebarToggle.onclick = () => {
                filtersSidebarContent.classList.toggle('collapsed');
                if (toggleIconSidebar) {
                    toggleIconSidebar.style.transform = filtersSidebarContent.classList.contains('collapsed') ? 'rotate(180deg)' : 'rotate(0deg)';
                }
            };
        } else {
            console.log('Элементы фильтров не найдены, пропускаем настройку');
        }
    }, 100);
    
    function loadData(data) {
        originalData = data;
        currentData = [...data];
        document.getElementById('dataSourceText').innerHTML = `📊 Данные загружены (${data.length} записей)`;
        document.getElementById('dataSourceInfo').style.display = 'block';
        updateFilters();
        renderDashboard();
        uploadArea.style.display = 'none';
        // filtersBar и periodSelector теперь в боковой панели, убираем старые ссылки
    }
    
    async function loadFile(file) {
        try {
            const data = await readExcelFile(file);
            loadData(data);
        } catch (error) { alert('Ошибка: ' + error.message); }
    }
    
    fileInput.onchange = (e) => { if (e.target.files[0]) loadFile(e.target.files[0]); };
    uploadArea.onclick = () => fileInput.click();
    changeDataBtn.onclick = () => {
        uploadArea.style.display = 'block';
        document.getElementById('dataSourceInfo').style.display = 'none';
        originalData = [];
    };
    resetFiltersBtn.onclick = () => { 
        companyFilter.value = ''; 
        yearFilter.value = ''; 
        Array.from(monthFilter.options).forEach(o => o.selected = false);
        applyFilters(); 
    };
    
    function updateFilters() {
        const companies = [...new Set(originalData.map(d => d.компания))];
        const years = [...new Set(originalData.map(d => d.год))].sort();
        const months = [...new Set(originalData.map(d => d.месяц))].sort((a,b) => monthsOrder.indexOf(a)-monthsOrder.indexOf(b));
        companyFilter.innerHTML = '<option value="">Все компании</option>' + companies.map(c => `<option value="${c}">${c}</option>`).join('');
        yearFilter.innerHTML = '<option value="">Все годы</option>' + years.map(y => `<option value="${y}">${y}</option>`).join('');
        monthFilter.innerHTML = months.map(m => `<option value="${m}">${m}</option>`).join('');
        monthFilter.setAttribute('multiple', 'multiple');
        monthFilter.size = 4;
    }
    
    function applyFilters() {
        currentFilters.company = companyFilter.value;
        currentFilters.year = yearFilter.value;
        const selectedMonths = Array.from(monthFilter.selectedOptions).map(o => o.value);
        currentFilters.month = selectedMonths;
        
        currentData = originalData.filter(row => {
            if (companyFilter.value && row.компания !== companyFilter.value) return false;
            if (yearFilter.value && row.год != yearFilter.value) return false;
            const selectedMonths = Array.from(monthFilter.selectedOptions).map(o => o.value);
            if (selectedMonths.length > 0 && !selectedMonths.includes(row.месяц)) return false;
            return true;
        });
        renderDashboard();
        if (currentChannel) renderChannelPage(currentChannel);
    }
    
    const debouncedApply = () => setTimeout(applyFilters, 300);
    companyFilter.onchange = debouncedApply;
    yearFilter.onchange = debouncedApply;
    monthFilter.onchange = debouncedApply;
    
    const dashboardMenu = document.getElementById('dashboardMenu');
    const channelsSubmenu = document.getElementById('channelsSubmenu');
    const arrow = dashboardMenu.querySelector('.arrow');
    
    dashboardMenu.onclick = (e) => {
        e.stopPropagation();
        channelsSubmenu.classList.toggle('show');
        arrow.classList.toggle('open');
        if (!channelsSubmenu.classList.contains('show')) {
            currentChannel = null;
            document.querySelectorAll('.nav-subitem').forEach(n => n.classList.remove('active'));
            document.querySelectorAll('.page-content').forEach(c => c.classList.remove('active'));
            document.getElementById('page-dashboard').classList.add('active');
            renderDashboard();
        }
    };
    
    document.querySelectorAll('.nav-subitem').forEach(item => {
        item.onclick = () => {
            const channel = item.dataset.channel;
            currentChannel = channel;
            document.querySelectorAll('.nav-subitem').forEach(n => n.classList.remove('active'));
            item.classList.add('active');
            document.querySelectorAll('.page-content').forEach(c => c.classList.remove('active'));
            document.getElementById(`page-channel-${channel}`).classList.add('active');
            renderChannelPage(channel);
        };
    });
    
    const aiNavItem = document.querySelector('.nav-item[data-page="ai"]');
    const dashboardNavItem = document.getElementById('dashboardMenu');
    
    aiNavItem.onclick = () => {
        currentChannel = null;
        document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
        document.querySelectorAll('.nav-subitem').forEach(n => n.classList.remove('active'));
        aiNavItem.classList.add('active');
        channelsSubmenu.classList.remove('show');
        arrow.classList.remove('open');
        document.querySelectorAll('.page-content').forEach(c => c.classList.remove('active'));
        document.getElementById('page-ai').classList.add('active');
    };
    
    dashboardNavItem.onclick = (e) => {
        e.stopPropagation();
        if (channelsSubmenu.classList.contains('show')) {
            channelsSubmenu.classList.remove('show');
            arrow.classList.remove('open');
            currentChannel = null;
            document.querySelectorAll('.nav-subitem').forEach(n => n.classList.remove('active'));
            document.querySelectorAll('.page-content').forEach(c => c.classList.remove('active'));
            document.getElementById('page-dashboard').classList.add('active');
            renderDashboard();
        } else {
            channelsSubmenu.classList.add('show');
            arrow.classList.add('open');
        }
    };
    
    const aiSendBtn = document.getElementById('aiSendBtn');
    const aiInput = document.getElementById('aiInput');
    const aiChatMessages = document.getElementById('aiChatMessages');
    function addAIMessage(text, isUser) { const div = document.createElement('div'); div.className = `ai-message ${isUser ? 'user' : 'assistant'}`; div.style.whiteSpace = 'pre-line'; div.innerHTML = text; aiChatMessages.appendChild(div); aiChatMessages.scrollTop = aiChatMessages.scrollHeight; }
    function getAIResponse(question) {
        const f = calculateFinancials(currentData);
        if (question === 'analyze' || question.includes('анализ')) return `📊 **Анализ:**\nВыручка: ${formatCurrency(f.totalRevenue)}\nНДС: ${formatCurrency(f.totalNDS)}\nРасходы: ${formatCurrency(f.totalExpenses)}\nПрибыль: ${formatCurrency(f.profit)}\nРентабельность: ${f.profitability.toFixed(1)}%`;
        if (question === 'bestChannel' || question.includes('прибыльн')) return `🏆 Wildberries: ${formatCurrency(calculateFinancials(currentData, 'wildberries').profit)}\nOZON: ${formatCurrency(calculateFinancials(currentData, 'ozon').profit)}`;
        if (question === 'expenses' || question.includes('расход')) return `💰 Расходы: ${formatCurrency(f.totalExpenses)} (${((f.totalExpenses/f.netRevenue)*100).toFixed(1)}% от выручки)`;
        if (question === 'recommend' || question.includes('рекоменд')) return `💡 **Рекомендации:**\n1. Оптимизируйте логистику\n2. Увеличьте маржинальность\n3. Диверсифицируйте каналы`;
        return `🔍 Задайте вопрос о выручке, расходах или каналах.`;
    }
    aiSendBtn.onclick = () => {
        const q = aiInput.value.trim();
        if (!q) return;
        addAIMessage(q, true);
        aiInput.value = '';
        setTimeout(() => addAIMessage(getAIResponse(q), false), 300);
    };
    document.querySelectorAll('.ai-suggestion').forEach(s => {
        s.onclick = () => { aiInput.value = s.dataset.question; aiSendBtn.click(); };
    });
    
    const themeToggle = document.getElementById('themeToggle');
    const body = document.body;
    themeToggle.onclick = () => {
        if (body.classList.contains('dark')) { body.classList.remove('dark'); body.classList.add('light'); themeToggle.classList.remove('active'); }
        else { body.classList.remove('light'); body.classList.add('dark'); themeToggle.classList.add('active'); }
    };
    body.classList.add('dark');
}
        
        document.getElementById('adminBtn')?.addEventListener('click', showAdminPanel);
        document.getElementById('closeAdminBtn')?.addEventListener('click', () => document.getElementById('adminPanel').classList.remove('active'));
        document.getElementById('logoutBtn')?.addEventListener('click', logout);
        
        initAuth();
    </script>
</body>
</html>
