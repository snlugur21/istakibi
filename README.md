```html
<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>İş Takibi — Haftalık Takım Planlayıcı</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>
  <!-- Plus Jakarta Sans Font -->
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Plus Jakarta Sans', sans-serif;
      -webkit-tap-highlight-color: transparent;
    }
    .no-scrollbar::-webkit-scrollbar {
      display: none;
    }
    .no-scrollbar {
      -ms-overflow-style: none;
      scrollbar-width: none;
    }
    .custom-scrollbar::-webkit-scrollbar {
      width: 5px;
      height: 5px;
    }
    .custom-scrollbar::-webkit-scrollbar-track {
      background: transparent;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background: #e2e8f0;
      border-radius: 9999px;
    }
    @keyframes popIn {
      0% { transform: scale(0.95); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }
    .animate-pop {
      animation: popIn 0.2s cubic-bezier(0.16, 1, 0.3, 1) forwards;
    }
  </style>
</head>
<body class="bg-[#FAF9F5] text-slate-800 antialiased min-h-screen flex flex-col selection:bg-amber-200 selection:text-amber-900">

  <!-- REUSABLE SVG DAISY TEMPLATE (Hidden) -->
  <svg class="hidden">
    <symbol id="daisy-icon" viewBox="0 0 64 64">
      <g fill="currentColor">
        <ellipse cx="32" cy="12" rx="6" ry="13" />
        <ellipse cx="32" cy="52" rx="6" ry="13" />
        <ellipse cx="12" cy="32" rx="13" ry="6" />
        <ellipse cx="52" cy="32" rx="13" ry="6" />
        <ellipse cx="17.8" cy="17.8" rx="6" ry="13" transform="rotate(-45 17.8 17.8)" />
        <ellipse cx="46.2" cy="46.2" rx="6" ry="13" transform="rotate(-45 46.2 46.2)" />
        <ellipse cx="46.2" cy="17.8" rx="6" ry="13" transform="rotate(45 46.2 17.8)" />
        <ellipse cx="17.8" cy="46.2" rx="6" ry="13" transform="rotate(45 17.8 46.2)" />
      </g>
      <circle cx="32" cy="32" r="9.5" fill="#F59E0B" />
      <circle cx="30" cy="30" r="3" fill="#FDE68A" opacity="0.7" />
    </symbol>
  </svg>

  <!-- APP WRAPPER -->
  <div id="app" class="flex-grow flex flex-col">

    <!-- ==================== LOGIN SCREEN ==================== -->
    <div id="loginView" class="hidden min-h-screen flex items-center justify-center p-4 bg-gradient-to-b from-[#FFFDF7] via-[#FAF8F1] to-[#F3EFE2] relative overflow-hidden">
      <!-- Subtle Decorative Daisies in Background -->
      <svg class="w-48 h-48 text-amber-200/35 absolute -top-10 -left-10 rotate-12 pointer-events-none">
        <use href="#daisy-icon"></use>
      </svg>
      <svg class="w-64 h-64 text-amber-200/30 absolute -bottom-16 -right-12 -rotate-12 pointer-events-none">
        <use href="#daisy-icon"></use>
      </svg>

      <div class="w-full max-w-md bg-white/95 backdrop-blur-md rounded-3xl shadow-xl shadow-amber-900/5 p-6 sm:p-8 border border-amber-100/80 relative z-10 animate-pop">
        <div class="text-center mb-7">
          <div class="w-16 h-16 bg-amber-50 rounded-2xl flex items-center justify-center mx-auto mb-3.5 border border-amber-200/70 shadow-sm relative">
            <svg class="w-10 h-10 text-amber-300 drop-shadow-sm">
              <use href="#daisy-icon"></use>
            </svg>
          </div>
          <h1 class="text-2xl font-extrabold text-slate-900 tracking-tight">İş Takibi</h1>
          <p class="text-xs sm:text-sm text-slate-500 mt-1">Giriş yapmak için nickname ve şifrenizi girin.</p>
        </div>

        <form id="loginForm" class="space-y-4" onsubmit="handleLogin(event)">
          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1.5 ml-1">Kullanıcı Adı (Nickname)</label>
            <div class="relative">
              <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                <i data-lucide="user" class="w-4 h-4"></i>
              </span>
              <input type="text" id="loginUsername" required autocomplete="username" class="w-full pl-10 pr-4 py-3 bg-slate-50/80 border border-slate-200 rounded-2xl focus:ring-2 focus:ring-amber-400 focus:border-amber-400 focus:bg-white focus:outline-none text-slate-900 font-semibold text-sm transition" placeholder="Nickname">
            </div>
          </div>

          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1.5 ml-1">Şifre</label>
            <div class="relative">
              <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                <i data-lucide="lock" class="w-4 h-4"></i>
              </span>
              <input type="password" id="loginPassword" required autocomplete="current-password" class="w-full pl-10 pr-4 py-3 bg-slate-50/80 border border-slate-200 rounded-2xl focus:ring-2 focus:ring-amber-400 focus:border-amber-400 focus:bg-white focus:outline-none text-slate-900 font-semibold text-sm transition" placeholder="••••••••">
            </div>
          </div>

          <div id="loginError" class="hidden p-3 bg-rose-50 border border-rose-200 rounded-2xl text-rose-600 text-xs font-medium flex items-center gap-2">
            <i data-lucide="alert-circle" class="w-4 h-4 shrink-0"></i>
            <span>Kullanıcı adı veya şifre hatalı. Lütfen kontrol edin.</span>
          </div>

          <button type="submit" class="w-full py-3.5 px-4 bg-slate-900 hover:bg-slate-800 active:scale-[0.99] text-white font-bold rounded-2xl shadow-lg shadow-slate-900/10 transition flex items-center justify-center gap-2 text-sm mt-2">
            <span>Sisteme Giriş Yap</span>
            <i data-lucide="arrow-right" class="w-4 h-4 text-amber-400"></i>
          </button>
        </form>
      </div>
    </div>

    <!-- ==================== MAIN DASHBOARD ==================== -->
    <div id="mainView" class="hidden flex-grow flex flex-col pb-24 md:pb-8">
      
      <!-- GLASSMORPHISM STICKY HEADER -->
      <header class="bg-white/85 backdrop-blur-md border-b border-amber-100/80 sticky top-0 z-30">
        <div class="max-w-7xl mx-auto px-3.5 sm:px-6 lg:px-8">
          <div class="flex items-center justify-between h-14 sm:h-16">
            
            <!-- Brand with Daisy SVG -->
            <div class="flex items-center gap-2.5">
              <div class="w-9 h-9 sm:w-10 sm:h-10 bg-amber-50 border border-amber-200/80 rounded-2xl flex items-center justify-center shadow-xs shrink-0">
                <svg class="w-6 h-6 sm:w-7 sm:h-7 text-amber-300">
                  <use href="#daisy-icon"></use>
                </svg>
              </div>
              <div>
                <div class="flex items-center gap-1.5">
                  <h1 class="font-extrabold text-slate-900 text-base sm:text-lg tracking-tight leading-none">İş Takibi</h1>
                </div>
                <p class="text-[11px] text-slate-400 font-medium mt-0.5 hidden sm:block">Haftalık Takım Ajandası</p>
              </div>
            </div>

            <!-- Right Controls -->
            <div class="flex items-center gap-1.5 sm:gap-2.5">
              <!-- Desktop Add Button -->
              <button onclick="openNewTaskModal()" class="hidden md:inline-flex items-center gap-2 bg-slate-900 hover:bg-slate-800 text-white px-4 py-2 rounded-xl font-bold text-xs shadow-sm transition">
                <i data-lucide="plus" class="w-4 h-4 text-amber-400"></i>
                <span>Yeni İş Ekle</span>
              </button>

              <!-- Active User Pill -->
              <div class="flex items-center gap-2 bg-[#FAF9F5] pl-1.5 pr-2.5 py-1 rounded-full border border-slate-200/80">
                <div class="w-6 h-6 rounded-full bg-amber-400 text-slate-900 flex items-center justify-center text-xs font-extrabold shadow-2xs" id="userAvatar">
                  A
                </div>
                <span class="text-xs font-bold text-slate-700 max-w-[75px] truncate" id="currentUserName">Admin</span>
              </div>

              <!-- Users Management Button -->
              <button onclick="openUsersModal()" title="Üye ve Şifre Yönetimi" class="p-2 text-slate-600 hover:text-amber-700 hover:bg-amber-50 rounded-xl border border-slate-200/80 bg-white transition relative">
                <i data-lucide="users" class="w-4 h-4"></i>
                <span class="sr-only">Üyeler</span>
              </button>

              <!-- Logout Button -->
              <button onclick="logout()" title="Çıkış Yap" class="p-2 text-slate-400 hover:text-rose-600 hover:bg-rose-50 rounded-xl transition">
                <i data-lucide="log-out" class="w-4 h-4"></i>
              </button>
            </div>
          </div>
        </div>
      </header>

      <!-- WEEK NAVIGATION & FILTER TOOLBAR -->
      <section class="bg-white/60 border-b border-slate-200/60 pt-3 pb-3 px-3.5 sm:px-6 lg:px-8">
        <div class="max-w-7xl mx-auto space-y-3">
          
          <!-- Top Row: Week Range & Nav Arrows -->
          <div class="flex items-center justify-between gap-2">
            <div class="flex items-center gap-1.5">
              <button onclick="changeWeek(-1)" aria-label="Önceki Hafta" class="p-2 bg-white hover:bg-amber-50 active:scale-95 border border-slate-200/90 rounded-xl text-slate-700 shadow-2xs transition">
                <i data-lucide="chevron-left" class="w-4 h-4"></i>
              </button>
              <button onclick="goToToday()" class="px-3 py-1.5 bg-amber-50 hover:bg-amber-100 active:scale-95 border border-amber-200/80 rounded-xl text-xs font-bold text-amber-900 transition">
                Bugün
              </button>
              <button onclick="changeWeek(1)" aria-label="Sonraki Hafta" class="p-2 bg-white hover:bg-amber-50 active:scale-95 border border-slate-200/90 rounded-xl text-slate-700 shadow-2xs transition">
                <i data-lucide="chevron-right" class="w-4 h-4"></i>
              </button>
            </div>

            <div class="text-right sm:text-left flex items-center gap-1.5">
              <svg class="w-4 h-4 text-amber-400 hidden sm:inline shrink-0"><use href="#daisy-icon"></use></svg>
              <span class="text-xs sm:text-base font-extrabold text-slate-800 tracking-tight" id="weekRangeText">
                9 - 15 Kasım 2026
              </span>
            </div>
          </div>

          <!-- Second Row: Horizontal Scrollable Filter Pills + Mobile View Mode Toggle -->
          <div class="flex items-center justify-between gap-2">
            <!-- Status / Owner Pills -->
            <div class="flex items-center gap-1.5 overflow-x-auto no-scrollbar py-0.5 flex-grow">
              <button onclick="setQuickFilter('all')" data-qfilter="all" class="qfilter-btn px-3 py-1.5 rounded-full text-xs font-bold whitespace-nowrap transition bg-slate-900 text-white">
                Tümü
              </button>
              <button onclick="setQuickFilter('mine')" data-qfilter="mine" class="qfilter-btn px-3 py-1.5 rounded-full text-xs font-bold whitespace-nowrap transition bg-white text-slate-600 border border-slate-200/90 hover:bg-slate-50">
                Benim İşlerim
              </button>
              <button onclick="setQuickFilter('pending')" data-qfilter="pending" class="qfilter-btn px-3 py-1.5 rounded-full text-xs font-bold whitespace-nowrap transition bg-white text-slate-600 border border-slate-200/90 hover:bg-slate-50">
                Yapılacaklar
              </button>
              <button onclick="setQuickFilter('completed')" data-qfilter="completed" class="qfilter-btn px-3 py-1.5 rounded-full text-xs font-bold whitespace-nowrap transition bg-white text-slate-600 border border-slate-200/90 hover:bg-slate-50">
                Yapılanlar
              </button>

              <!-- Member Select Dropdown -->
              <div class="relative inline-flex items-center shrink-0">
                <select id="memberFilter" onchange="renderCalendar()" class="appearance-none bg-white border border-slate-200/90 text-slate-700 text-xs font-bold rounded-full pl-3 pr-7 py-1.5 focus:outline-none focus:ring-2 focus:ring-amber-400">
                  <option value="all">Kişi: Tümü</option>
                </select>
                <i data-lucide="chevron-down" class="w-3.5 h-3.5 text-slate-400 absolute right-2.5 pointer-events-none"></i>
              </div>
            </div>

            <!-- Mobile View Toggle -->
            <div class="flex md:hidden items-center bg-slate-200/70 p-0.5 rounded-xl shrink-0">
              <button onclick="setMobileMode('day')" id="btnModeDay" class="px-2.5 py-1 rounded-lg text-[11px] font-bold bg-white text-slate-900 shadow-2xs transition">
                Gün
              </button>
              <button onclick="setMobileMode('week')" id="btnModeWeek" class="px-2.5 py-1 rounded-lg text-[11px] font-bold text-slate-600 transition">
                Hafta
              </button>
            </div>
          </div>

          <!-- MOBILE HORIZONTAL DAY PILL STRIP -->
          <div id="mobileDayStrip" class="grid grid-cols-7 gap-1 md:hidden pt-1">
            <!-- JS Populated -->
          </div>

        </div>
      </section>

      <!-- MAIN AGENDA BOARD -->
      <main class="flex-grow px-3.5 sm:px-6 lg:px-8 pt-4 max-w-7xl w-full mx-auto">
        <div id="weekGridContainer" class="grid grid-cols-1 md:grid-cols-7 gap-3.5">
          <!-- Columns 0..6 generated dynamically -->
        </div>
      </main>
    </div>

    <!-- MOBILE FLOATING ACTION BUTTON (FAB) -->
    <button id="mobileFab" onclick="openNewTaskModal()" class="hidden md:hidden fixed bottom-5 right-5 z-40 bg-slate-900 hover:bg-slate-800 active:scale-95 text-white pl-4 pr-5 py-3.5 rounded-full shadow-xl shadow-slate-900/25 flex items-center gap-2 font-bold text-sm border border-slate-700/50 transition">
      <div class="w-6 h-6 rounded-full bg-amber-400 text-slate-900 flex items-center justify-center">
        <i data-lucide="plus" class="w-4 h-4 stroke-[2.5]"></i>
      </div>
      <span>İş Ekle</span>
    </button>

  </div>

  <!-- ==================== TASK MODAL ==================== -->
  <div id="taskModal" class="hidden fixed inset-0 z-50 bg-slate-900/50 backdrop-blur-xs flex items-end sm:items-center justify-center p-0 sm:p-4">
    <div class="bg-white rounded-t-3xl sm:rounded-3xl shadow-2xl max-w-md w-full overflow-hidden border border-slate-100 animate-pop">
      <div class="w-10 h-1 bg-slate-200 rounded-full mx-auto mt-2.5 sm:hidden"></div>
      
      <div class="px-5 py-4 border-b border-slate-100 flex items-center justify-between">
        <h3 class="font-extrabold text-slate-900 text-base sm:text-lg flex items-center gap-2">
          <svg class="w-5 h-5 text-amber-400"><use href="#daisy-icon"></use></svg>
          <span id="taskModalTitle">Yeni İş Ekle</span>
        </h3>
        <button onclick="closeTaskModal()" class="p-1.5 hover:bg-slate-100 text-slate-400 hover:text-slate-700 rounded-full transition">
          <i data-lucide="x" class="w-5 h-5"></i>
        </button>
      </div>

      <form id="taskForm" onsubmit="handleSaveTask(event)" class="p-5 space-y-4">
        <input type="hidden" id="taskId">
        
        <div>
          <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1.5">Yapılacak İş</label>
          <input type="text" id="taskTitle" required class="w-full px-3.5 py-3 bg-slate-50 border border-slate-200 rounded-2xl focus:ring-2 focus:ring-amber-400 focus:bg-white focus:outline-none text-slate-900 font-semibold text-sm transition" placeholder="Örn: Müşteri teklifini gönder">
        </div>

        <div>
          <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1.5">Kısa Not (İsteğe Bağlı)</label>
          <textarea id="taskDesc" rows="2" class="w-full px-3.5 py-2.5 bg-slate-50 border border-slate-200 rounded-2xl focus:ring-2 focus:ring-amber-400 focus:bg-white focus:outline-none text-slate-900 text-sm transition" placeholder="Varsa detay ekleyin..."></textarea>
        </div>

        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1.5">Tarih</label>
            <input type="date" id="taskDate" required class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-2xl focus:ring-2 focus:ring-amber-400 focus:bg-white focus:outline-none text-slate-900 font-semibold text-xs sm:text-sm transition">
          </div>
          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1.5">Öncelik</label>
            <select id="taskPriority" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-2xl focus:ring-2 focus:ring-amber-400 focus:bg-white focus:outline-none text-slate-900 font-semibold text-xs sm:text-sm transition">
              <option value="normal">Normal</option>
              <option value="high">Acil / Önemli</option>
              <option value="low">Düşük</option>
            </select>
          </div>
        </div>

        <div class="pt-3 flex items-center gap-2.5">
          <button type="button" onclick="closeTaskModal()" class="flex-1 py-3 bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold rounded-2xl text-sm transition">Vazgeç</button>
          <button type="submit" class="flex-1 py-3 bg-slate-900 hover:bg-slate-800 text-white font-bold rounded-2xl text-sm shadow-md transition">Kaydet</button>
        </div>
      </form>
    </div>
  </div>

  <!-- ==================== USERS & SETTINGS MODAL ==================== -->
  <div id="usersModal" class="hidden fixed inset-0 z-50 bg-slate-900/50 backdrop-blur-xs flex items-end sm:items-center justify-center p-0 sm:p-4">
    <div class="bg-white rounded-t-3xl sm:rounded-3xl shadow-2xl max-w-md w-full overflow-hidden border border-slate-100 animate-pop">
      <div class="w-10 h-1 bg-slate-200 rounded-full mx-auto mt-2.5 sm:hidden"></div>

      <div class="px-5 py-4 border-b border-slate-100 flex items-center justify-between">
        <h3 class="font-extrabold text-slate-900 text-base sm:text-lg flex items-center gap-2">
          <i data-lucide="users" class="w-5 h-5 text-amber-500"></i>
          <span>Üye & Şifre Yönetimi</span>
        </h3>
        <button onclick="closeUsersModal()" class="p-1.5 hover:bg-slate-100 text-slate-400 hover:text-slate-700 rounded-full transition">
          <i data-lucide="x" class="w-5 h-5"></i>
        </button>
      </div>

      <div class="p-5 space-y-5 max-h-[80vh] overflow-y-auto custom-scrollbar">
        <!-- Add / Edit Member Form -->
        <form id="addUserForm" onsubmit="handleSaveUser(event)" class="bg-[#FAF9F5] p-4 rounded-2xl border border-amber-200/60 space-y-3">
          <h4 id="userFormHeading" class="text-xs font-extrabold uppercase tracking-wider text-slate-700 flex items-center gap-1.5">
            <i data-lucide="user-plus" class="w-4 h-4 text-amber-500"></i> Yeni Üye Oluştur
          </h4>
          <input type="hidden" id="editingUserId">
          <div class="grid grid-cols-2 gap-2">
            <input type="text" id="newUsername" required placeholder="Nickname" class="px-3 py-2.5 bg-white border border-slate-200 rounded-xl text-xs font-semibold focus:ring-2 focus:ring-amber-400 focus:outline-none">
            <input type="text" id="newUserPassword" required placeholder="Şifre belirle" class="px-3 py-2.5 bg-white border border-slate-200 rounded-xl text-xs font-semibold focus:ring-2 focus:ring-amber-400 focus:outline-none">
          </div>
          <div id="userModalAlert" class="hidden text-xs font-semibold text-rose-600"></div>
          <div class="flex gap-2">
            <button type="button" id="cancelUserEditBtn" onclick="resetUserForm()" class="hidden flex-1 py-2 bg-slate-200 hover:bg-slate-300 text-slate-700 font-bold text-xs rounded-xl transition">
              İptal
            </button>
            <button type="submit" id="saveUserBtn" class="flex-1 py-2 bg-slate-900 hover:bg-slate-800 text-white font-bold text-xs rounded-xl transition shadow-xs">
              Üyeyi Kaydet
            </button>
          </div>
        </form>

        <!-- Member List -->
        <div>
          <h4 class="text-xs font-extrabold uppercase tracking-wider text-slate-400 mb-2.5">Kayıtlı Üyeler ve Şifreler</h4>
          <div id="usersListContainer" class="space-y-2">
            <!-- JS Populated -->
          </div>
        </div>

        <!-- Reset Footer -->
        <div class="pt-3 border-t border-slate-100 flex items-center justify-between">
          <span class="text-[11px] text-slate-400">Verileri varsayılana sıfırla:</span>
          <button type="button" onclick="resetData()" class="text-xs font-bold text-rose-600 hover:text-rose-700 bg-rose-50 hover:bg-rose-100 px-3 py-1.5 rounded-xl transition flex items-center gap-1.5">
            <i data-lucide="rotate-ccw" class="w-3.5 h-3.5"></i>
            Sıfırla
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- CUSTOM CONFIRMATION TOAST / MODAL -->
  <div id="confirmBox" class="hidden fixed inset-0 z-50 bg-slate-900/50 backdrop-blur-xs flex items-center justify-center p-4">
    <div class="bg-white rounded-3xl max-w-xs w-full p-5 shadow-2xl border border-slate-100 text-center animate-pop">
      <div class="w-12 h-12 rounded-2xl bg-amber-50 text-amber-500 flex items-center justify-center mx-auto mb-3">
        <i data-lucide="help-circle" class="w-6 h-6"></i>
      </div>
      <p id="confirmMessage" class="text-sm font-bold text-slate-800 mb-4">Emin misiniz?</p>
      <div class="flex gap-2">
        <button id="confirmCancelBtn" class="flex-1 py-2.5 bg-slate-100 text-slate-700 font-bold rounded-xl text-xs">İptal</button>
        <button id="confirmOkBtn" class="flex-1 py-2.5 bg-rose-600 text-white font-bold rounded-xl text-xs">Evet, Onayla</button>
      </div>
    </div>
  </div>

  <!-- ==================== JAVASCRIPT LOGIC ==================== -->
  <script>
    const DAY_NAMES_FULL = ['Pazartesi', 'Salı', 'Çarşamba', 'Perşembe', 'Cuma', 'Cumartesi', 'Pazar'];
    const DAY_NAMES_SHORT = ['Pzt', 'Sal', 'Çar', 'Per', 'Cum', 'Cmt', 'Paz'];

    const DEFAULT_USERS = [
      { id: '1', username: 'admin', password: '4132', role: 'admin', color: 'bg-amber-100 text-amber-800 border-amber-200' },
      { id: '2', username: 'Ahmet', password: '123', role: 'user', color: 'bg-emerald-100 text-emerald-800 border-emerald-200' },
      { id: '3', username: 'Elif', password: '456', role: 'user', color: 'bg-sky-100 text-sky-800 border-sky-200' }
    ];

    const BADGE_PALETTE = [
      'bg-amber-100 text-amber-800 border-amber-200',
      'bg-emerald-100 text-emerald-800 border-emerald-200',
      'bg-sky-100 text-sky-800 border-sky-200',
      'bg-purple-100 text-purple-800 border-purple-200',
      'bg-rose-100 text-rose-800 border-rose-200'
    ];

    function getInitialTasks() {
      const today = new Date();
      const mon = getMonday(today);
      const addDays = (base, d) => {
        const copy = new Date(base);
        copy.setDate(copy.getDate() + d);
        return formatDateKey(copy);
      };

      return [
        {
          id: 't-101',
          title: 'Haftalık stok ve sipariş kontrolü',
          desc: 'Tedarikçilere verilecek liste netleştirilecek.',
          date: addDays(mon, 0),
          createdByName: 'admin',
          completed: true,
          priority: 'high'
        },
        {
          id: 't-102',
          title: 'Müşteri görüşmeleri',
          desc: 'Geçen haftaki teklifler aranıp teyit edilecek.',
          date: addDays(mon, 1),
          createdByName: 'Ahmet',
          completed: false,
          priority: 'normal'
        },
        {
          id: 't-103',
          title: 'Sosyal medya görselleri onaylanacak',
          desc: 'Papatya temalı yeni tasarımlar kontrol edilecek.',
          date: addDays(mon, 2),
          createdByName: 'Elif',
          completed: false,
          priority: 'normal'
        }
      ];
    }

    // APP STATE
    let users = JSON.parse(localStorage.getItem('papatya_users')) || DEFAULT_USERS;
    let tasks = JSON.parse(localStorage.getItem('papatya_tasks')) || getInitialTasks();
    let currentUser = JSON.parse(localStorage.getItem('papatya_current_user')) || null;
    let currentWeekStart = getMonday(new Date());
    let quickFilter = 'all'; 
    let mobileViewMode = 'day'; 
    let selectedMobileDayIndex = getTodayDayIndex();

    function getTodayDayIndex() {
      const day = new Date().getDay();
      return day === 0 ? 6 : day - 1;
    }

    function getMonday(d) {
      const date = new Date(d);
      const day = date.getDay();
      const diff = date.getDate() - day + (day === 0 ? -6 : 1);
      date.setDate(diff);
      date.setHours(0, 0, 0, 0);
      return date;
    }

    function formatDateKey(dateObj) {
      const year = dateObj.getFullYear();
      const month = String(dateObj.getMonth() + 1).padStart(2, '0');
      const day = String(dateObj.getDate()).padStart(2, '0');
      return `${year}-${month}-${day}`;
    }

    function formatTurkishShortDate(dateObj) {
      return dateObj.toLocaleDateString('tr-TR', { day: 'numeric', month: 'short' });
    }

    function saveState() {
      localStorage.setItem('papatya_users', JSON.stringify(users));
      localStorage.setItem('papatya_tasks', JSON.stringify(tasks));
      localStorage.setItem('papatya_current_user', JSON.stringify(currentUser));
    }

    function getUserBadgeClass(username) {
      const idx = users.findIndex(u => u.username.toLowerCase() === username.toLowerCase());
      if (idx !== -1 && users[idx].color) return users[idx].color;
      const hash = username.split('').reduce((acc, ch) => acc + ch.charCodeAt(0), 0);
      return BADGE_PALETTE[hash % BADGE_PALETTE.length];
    }

    // INIT
    window.addEventListener('DOMContentLoaded', () => {
      lucide.createIcons();
      if (currentUser) {
        showMainView();
      } else {
        showLoginView();
      }
    });

    // VIEWS
    function showLoginView() {
      document.getElementById('loginView').classList.remove('hidden');
      document.getElementById('mainView').classList.add('hidden');
      document.getElementById('mobileFab').classList.add('hidden');
      document.getElementById('loginError').classList.add('hidden');
    }

    function showMainView() {
      document.getElementById('loginView').classList.add('hidden');
      document.getElementById('mainView').classList.remove('hidden');
      document.getElementById('mobileFab').classList.remove('hidden');

      document.getElementById('currentUserName').innerText = currentUser.username;
      document.getElementById('userAvatar').innerText = currentUser.username.charAt(0).toUpperCase();

      populateMemberFilter();
      renderCalendar();
    }

    function handleLogin(e) {
      e.preventDefault();
      const nameInput = document.getElementById('loginUsername').value.trim();
      const passInput = document.getElementById('loginPassword').value.trim();

      const foundUser = users.find(
        u => u.username.toLowerCase() === nameInput.toLowerCase() && u.password === passInput
      );

      if (foundUser) {
        currentUser = foundUser;
        saveState();
        showMainView();
      } else {
        document.getElementById('loginError').classList.remove('hidden');
      }
    }

    function logout() {
      currentUser = null;
      saveState();
      showLoginView();
    }

    // NAVIGATION & FILTERS
    function changeWeek(direction) {
      currentWeekStart.setDate(currentWeekStart.getDate() + (direction * 7));
      renderCalendar();
    }

    function goToToday() {
      currentWeekStart = getMonday(new Date());
      selectedMobileDayIndex = getTodayDayIndex();
      renderCalendar();
    }

    function setQuickFilter(filterType) {
      quickFilter = filterType;
      document.querySelectorAll('.qfilter-btn').forEach(btn => {
        if (btn.dataset.qfilter === filterType) {
          btn.className = 'qfilter-btn px-3 py-1.5 rounded-full text-xs font-bold whitespace-nowrap transition bg-slate-900 text-white shadow-2xs';
        } else {
          btn.className = 'qfilter-btn px-3 py-1.5 rounded-full text-xs font-bold whitespace-nowrap transition bg-white text-slate-600 border border-slate-200/90 hover:bg-slate-50';
        }
      });
      renderCalendar();
    }

    function setMobileMode(mode) {
      mobileViewMode = mode;
      const btnDay = document.getElementById('btnModeDay');
      const btnWeek = document.getElementById('btnModeWeek');
      const strip = document.getElementById('mobileDayStrip');

      if (mode === 'day') {
        btnDay.className = 'px-2.5 py-1 rounded-lg text-[11px] font-bold bg-white text-slate-900 shadow-2xs transition';
        btnWeek.className = 'px-2.5 py-1 rounded-lg text-[11px] font-bold text-slate-600 transition';
        strip.classList.remove('hidden');
      } else {
        btnWeek.className = 'px-2.5 py-1 rounded-lg text-[11px] font-bold bg-white text-slate-900 shadow-2xs transition';
        btnDay.className = 'px-2.5 py-1 rounded-lg text-[11px] font-bold text-slate-600 transition';
        strip.classList.add('hidden');
      }
      renderCalendar();
    }

    function selectMobileDay(index) {
      selectedMobileDayIndex = index;
      renderCalendar();
    }

    function populateMemberFilter() {
      const select = document.getElementById('memberFilter');
      const prev = select.value;
      select.innerHTML = '<option value="all">Kişi: Tümü</option>';
      users.forEach(u => {
        const opt = document.createElement('option');
        opt.value = u.username;
        opt.textContent = `Kişi: ${u.username}`;
        select.appendChild(opt);
      });
      if ([...select.options].some(o => o.value === prev)) {
        select.value = prev;
      }
    }

    function getFilteredTasksForDate(dateKey) {
      const memberVal = document.getElementById('memberFilter').value;
      return tasks.filter(t => {
        if (t.date !== dateKey) return false;
        if (quickFilter === 'mine' && t.createdByName !== currentUser.username) return false;
        if (quickFilter === 'pending' && t.completed) return false;
        if (quickFilter === 'completed' && !t.completed) return false;
        if (memberVal !== 'all' && t.createdByName !== memberVal) return false;
        return true;
      });
    }

    // RENDER CALENDAR
    function renderCalendar() {
      const weekDates = [];
      const tempDate = new Date(currentWeekStart);
      for (let i = 0; i < 7; i++) {
        weekDates.push(new Date(tempDate));
        tempDate.setDate(tempDate.getDate() + 1);
      }

      // Header Date Range
      const startStr = formatTurkishShortDate(weekDates[0]);
      const endStr = formatTurkishShortDate(weekDates[6]);
      const yearStr = weekDates[6].getFullYear();
      document.getElementById('weekRangeText').innerText = `${startStr} – ${endStr} ${yearStr}`;

      const todayKey = formatDateKey(new Date());

      // Mobile Day Selector Pills
      const strip = document.getElementById('mobileDayStrip');
      strip.innerHTML = '';
      weekDates.forEach((dateObj, idx) => {
        const dateKey = formatDateKey(dateObj);
        const isToday = dateKey === todayKey;
        const isSelected = idx === selectedMobileDayIndex;
        const dayTasks = getFilteredTasksForDate(dateKey);
        const pendingCount = dayTasks.filter(t => !t.completed).length;
        const doneCount = dayTasks.filter(t => t.completed).length;

        const pill = document.createElement('button');
        pill.type = 'button';
        pill.onclick = () => selectMobileDay(idx);

        let pillStyle = 'bg-white border-slate-200/80 text-slate-700';
        if (isSelected) {
          pillStyle = 'bg-slate-900 border-slate-900 text-white shadow-md scale-[1.02]';
        } else if (isToday) {
          pillStyle = 'bg-amber-50 border-amber-300 text-amber-950';
        }

        pill.className = `flex flex-col items-center py-2 px-1 rounded-2xl border transition ${pillStyle}`;
        pill.innerHTML = `
          <span class="text-[10px] font-bold uppercase ${isSelected ? 'text-amber-300' : 'text-slate-400'}">${DAY_NAMES_SHORT[idx]}</span>
          <span class="text-sm font-extrabold mt-0.5">${dateObj.getDate()}</span>
          <div class="flex items-center gap-0.5 mt-1 h-1.5">
            ${pendingCount > 0 ? `<span class="w-1.5 h-1.5 rounded-full bg-amber-400"></span>` : ''}
            ${doneCount > 0 ? `<span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>` : ''}
          </div>
        `;
        strip.appendChild(pill);
      });

      // Render Day Columns
      const grid = document.getElementById('weekGridContainer');
      grid.innerHTML = '';

      weekDates.forEach((dateObj, dayIndex) => {
        const dateKey = formatDateKey(dateObj);
        const isToday = dateKey === todayKey;
        const isWeekend = dayIndex >= 5;
        const dayTasks = getFilteredTasksForDate(dateKey);

        const visibilityClass = (mobileViewMode === 'day' && dayIndex !== selectedMobileDayIndex)
          ? 'hidden md:flex'
          : 'flex';

        const col = document.createElement('div');
        col.className = `${visibilityClass} flex-col rounded-3xl border transition min-h-[340px] md:min-h-[520px] ${
          isToday
            ? 'bg-white border-amber-300 ring-2 ring-amber-200/60 shadow-md shadow-amber-900/5'
            : isWeekend
              ? 'bg-[#F6F5EF] border-slate-200/80 shadow-2xs'
              : 'bg-white border-slate-200/80 shadow-2xs'
        }`;

        col.innerHTML = `
          <div class="p-3.5 border-b ${isToday ? 'border-amber-100 bg-amber-50/40' : 'border-slate-100'} rounded-t-3xl flex items-center justify-between">
            <div class="flex items-center gap-2">
              <div>
                <div class="flex items-center gap-1.5">
                  <span class="text-xs font-extrabold uppercase tracking-wider ${isToday ? 'text-amber-700' : 'text-slate-400'}">
                    ${DAY_NAMES_FULL[dayIndex]}
                  </span>
                  ${isToday ? '<span class="text-[10px] font-extrabold bg-amber-400 text-slate-900 px-1.5 py-0.5 rounded-md">Bugün</span>' : ''}
                </div>
                <span class="text-sm font-extrabold text-slate-900">${formatTurkishShortDate(dateObj)}</span>
              </div>
            </div>

            <button onclick="openNewTaskModal(${dayIndex})" title="Bu güne iş ekle" class="w-8 h-8 rounded-xl bg-amber-50 hover:bg-amber-100 active:scale-95 text-amber-700 flex items-center justify-center border border-amber-200/70 transition">
              <i data-lucide="plus" class="w-4 h-4 stroke-[2.5]"></i>
            </button>
          </div>

          <div class="flex-grow p-2.5 space-y-2.5 overflow-y-auto custom-scrollbar" id="day-tasks-${dayIndex}"></div>
        `;

        grid.appendChild(col);

        const listContainer = col.querySelector(`#day-tasks-${dayIndex}`);
        if (dayTasks.length === 0) {
          listContainer.innerHTML = `
            <div class="h-full min-h-[180px] flex flex-col items-center justify-center p-4 text-center select-none">
              <svg class="w-10 h-10 text-amber-200/70 mb-2">
                <use href="#daisy-icon"></use>
              </svg>
              <span class="text-xs font-semibold text-slate-400">Planlanmış iş yok</span>
              <button onclick="openNewTaskModal(${dayIndex})" class="mt-2 text-[11px] font-bold text-amber-700 hover:underline">
                + İlk işi ekle
              </button>
            </div>
          `;
        } else {
          dayTasks.forEach(task => {
            listContainer.appendChild(createTaskCard(task));
          });
        }
      });

      lucide.createIcons();
    }

    function createTaskCard(task) {
      const card = document.createElement('div');
      const badgeColor = getUserBadgeClass(task.createdByName);

      let priorityDot = '';
      if (task.priority === 'high') {
        priorityDot = '<span class="inline-block w-2 h-2 rounded-full bg-rose-500 mr-1" title="Önemli"></span>';
      }

      card.className = `p-3 rounded-2xl border transition-all duration-150 ${
        task.completed
          ? 'bg-emerald-50/40 border-emerald-200/70'
          : 'bg-white border-slate-200/90 hover:border-amber-300 shadow-2xs'
      }`;

      card.innerHTML = `
        <div class="flex items-start gap-2.5">
          <button onclick="toggleTaskStatus('${task.id}')" aria-label="Durumu Değiştir" class="mt-0.5 shrink-0 w-6 h-6 rounded-full flex items-center justify-center transition active:scale-90 ${
            task.completed
              ? 'bg-emerald-500 text-white shadow-xs shadow-emerald-200'
              : 'border-2 border-slate-300 hover:border-amber-400 bg-white'
          }">
            ${task.completed
              ? `<svg class="w-4 h-4 text-white"><use href="#daisy-icon"></use></svg>`
              : ''}
          </button>

          <div class="flex-grow min-w-0">
            <div class="flex items-start justify-between gap-1.5">
              <h4 class="text-xs sm:text-[13px] font-bold leading-snug break-words ${
                task.completed ? 'line-through text-slate-400' : 'text-slate-800'
              }">
                ${priorityDot}${escapeHtml(task.title)}
              </h4>

              <div class="flex items-center gap-0.5 shrink-0">
                <button onclick="openEditTaskModal('${task.id}')" title="Düzenle" class="p-1 text-slate-300 hover:text-slate-600 rounded-lg transition">
                  <i data-lucide="pencil" class="w-3.5 h-3.5"></i>
                </button>
                <button onclick="deleteTask('${task.id}')" title="Sil" class="p-1 text-slate-300 hover:text-rose-500 rounded-lg transition">
                  <i data-lucide="trash-2" class="w-3.5 h-3.5"></i>
                </button>
              </div>
            </div>

            ${task.desc ? `
              <p class="text-[11px] mt-1 leading-relaxed break-words ${
                task.completed ? 'text-slate-400' : 'text-slate-500'
              }">${escapeHtml(task.desc)}</p>
            ` : ''}

            <div class="mt-2.5 pt-2 border-t border-slate-100/80 flex items-center justify-between gap-1 flex-wrap">
              <span class="inline-flex items-center gap-1 text-[10px] font-bold px-2 py-0.5 rounded-full border ${badgeColor}">
                <span class="w-3.5 h-3.5 rounded-full bg-white/70 flex items-center justify-center text-[9px] font-extrabold">
                  ${escapeHtml(task.createdByName.charAt(0).toUpperCase())}
                </span>
                ${escapeHtml(task.createdByName)}
              </span>

              <button onclick="toggleTaskStatus('${task.id}')" class="text-[10px] font-extrabold px-2 py-0.5 rounded-full transition ${
                task.completed
                  ? 'bg-emerald-100 text-emerald-700'
                  : 'bg-amber-50 text-amber-700 hover:bg-amber-100'
              }">
                ${task.completed ? '✓ Yapıldı' : 'Yapılacak'}
              </button>
            </div>
          </div>
        </div>
      `;

      return card;
    }

    // TASK CRUD
    function toggleTaskStatus(taskId) {
      const task = tasks.find(t => t.id === taskId);
      if (task) {
        task.completed = !task.completed;
        saveState();
        renderCalendar();
      }
    }

    function deleteTask(taskId) {
      showConfirm('Bu işi silmek istediğinize emin misiniz?', () => {
        tasks = tasks.filter(t => t.id !== taskId);
        saveState();
        renderCalendar();
      });
    }

    function openNewTaskModal(dayIndex = null) {
      document.getElementById('taskForm').reset();
      document.getElementById('taskId').value = '';
      document.getElementById('taskModalTitle').innerText = 'Yeni İş Ekle';

      const targetIndex = dayIndex !== null
        ? dayIndex
        : (window.innerWidth < 768 && mobileViewMode === 'day' ? selectedMobileDayIndex : null);

      if (targetIndex !== null) {
        const d = new Date(currentWeekStart);
        d.setDate(d.getDate() + targetIndex);
        document.getElementById('taskDate').value = formatDateKey(d);
      } else {
        document.getElementById('taskDate').value = formatDateKey(new Date());
      }

      document.getElementById('taskModal').classList.remove('hidden');
      setTimeout(() => document.getElementById('taskTitle').focus(), 50);
    }

    function openEditTaskModal(taskId) {
      const task = tasks.find(t => t.id === taskId);
      if (!task) return;

      document.getElementById('taskId').value = task.id;
      document.getElementById('taskTitle').value = task.title;
      document.getElementById('taskDesc').value = task.desc || '';
      document.getElementById('taskDate').value = task.date;
      document.getElementById('taskPriority').value = task.priority || 'normal';
      document.getElementById('taskModalTitle').innerText = 'İşi Düzenle';

      document.getElementById('taskModal').classList.remove('hidden');
    }

    function closeTaskModal() {
      document.getElementById('taskModal').classList.add('hidden');
    }

    function handleSaveTask(e) {
      e.preventDefault();
      const id = document.getElementById('taskId').value;
      const title = document.getElementById('taskTitle').value.trim();
      const desc = document.getElementById('taskDesc').value.trim();
      const date = document.getElementById('taskDate').value;
      const priority = document.getElementById('taskPriority').value;

      if (!title || !date) return;

      if (id) {
        const idx = tasks.findIndex(t => t.id === id);
        if (idx > -1) {
          tasks[idx] = { ...tasks[idx], title, desc, date, priority };
        }
      } else {
        tasks.push({
          id: 't-' + Date.now(),
          title,
          desc,
          date,
          createdByName: currentUser.username,
          completed: false,
          priority
        });
      }

      const savedDateObj = new Date(date + 'T00:00:00');
      currentWeekStart = getMonday(savedDateObj);
      const dayOfWeek = savedDateObj.getDay();
      selectedMobileDayIndex = dayOfWeek === 0 ? 6 : dayOfWeek - 1;

      saveState();
      closeTaskModal();
      renderCalendar();
    }

    // ENHANCED USER MANAGEMENT (ADD, EDIT, DELETE)
    function openUsersModal() {
      document.getElementById('userModalAlert').classList.add('hidden');
      resetUserForm();
      renderUsersList();
      document.getElementById('usersModal').classList.remove('hidden');
      lucide.createIcons();
    }

    function closeUsersModal() {
      document.getElementById('usersModal').classList.add('hidden');
    }

    function resetUserForm() {
      document.getElementById('addUserForm').reset();
      document.getElementById('editingUserId').value = '';
      document.getElementById('userFormHeading').innerHTML = '<i data-lucide="user-plus" class="w-4 h-4 text-amber-500"></i> Yeni Üye Oluştur';
      document.getElementById('saveUserBtn').innerText = 'Üyeyi Kaydet';
      document.getElementById('cancelUserEditBtn').classList.add('hidden');
      document.getElementById('userModalAlert').classList.add('hidden');
      lucide.createIcons();
    }

    function startEditUser(userId) {
      const u = users.find(x => x.id === userId);
      if (!u) return;

      document.getElementById('editingUserId').value = u.id;
      document.getElementById('newUsername').value = u.username;
      document.getElementById('newUserPassword').value = u.password;
      
      document.getElementById('userFormHeading').innerHTML = '<i data-lucide="edit-3" class="w-4 h-4 text-amber-500"></i> Üyeyi / Şifreyi Düzenle';
      document.getElementById('saveUserBtn').innerText = 'Güncelle';
      document.getElementById('cancelUserEditBtn').classList.remove('hidden');
      document.getElementById('userModalAlert').classList.add('hidden');
      lucide.createIcons();
    }

    function renderUsersList() {
      const container = document.getElementById('usersListContainer');
      container.innerHTML = '';

      users.forEach(u => {
        const isSelf = currentUser && currentUser.username === u.username;
        const badgeColor = getUserBadgeClass(u.username);
        const item = document.createElement('div');
        item.className = 'flex items-center justify-between p-3 bg-slate-50 border border-slate-200/80 rounded-2xl text-xs';

        item.innerHTML = `
          <div class="flex items-center gap-2.5">
            <div class="w-8 h-8 rounded-xl border font-extrabold flex items-center justify-center text-xs ${badgeColor}">
              ${escapeHtml(u.username.charAt(0).toUpperCase())}
            </div>
            <div>
              <div class="font-extrabold text-slate-800 flex items-center gap-1.5">
                <span>${escapeHtml(u.username)}</span>
                ${u.role === 'admin' ? '<span class="text-[9px] font-bold bg-slate-900 text-amber-400 px-1.5 py-0.2 rounded">ADMIN</span>' : ''}
              </div>
              <div class="text-slate-400 text-[11px] font-medium">Şifre: <span class="font-mono text-slate-700 font-bold">${escapeHtml(u.password)}</span></div>
            </div>
          </div>
          <div class="flex items-center gap-1">
            <button onclick="startEditUser('${u.id}')" title="Kullanıcı Adı / Şifre Değiştir" class="p-2 text-slate-500 hover:text-amber-700 hover:bg-amber-100/60 rounded-xl transition">
              <i data-lucide="pencil" class="w-3.5 h-3.5"></i>
            </button>
            ${!isSelf && users.length > 1 ? `
              <button onclick="removeUser('${u.id}')" title="Üyeyi Sil" class="p-2 text-slate-400 hover:text-rose-600 hover:bg-rose-50 rounded-xl transition">
                <i data-lucide="trash-2" class="w-3.5 h-3.5"></i>
              </button>
            ` : ''}
          </div>
        `;
        container.appendChild(item);
      });
      lucide.createIcons();
    }

    function handleSaveUser(e) {
      e.preventDefault();
      const editId = document.getElementById('editingUserId').value;
      const username = document.getElementById('newUsername').value.trim();
      const password = document.getElementById('newUserPassword').value.trim();
      const alertEl = document.getElementById('userModalAlert');

      // Duplicate nickname check
      const duplicate = users.find(u => u.username.toLowerCase() === username.toLowerCase() && u.id !== editId);
      if (duplicate) {
        alertEl.innerText = 'Bu nickname başka bir kullanıcıda kayıtlı.';
        alertEl.classList.remove('hidden');
        return;
      }

      alertEl.classList.add('hidden');

      if (editId) {
        // Edit existing user
        const uIndex = users.findIndex(u => u.id === editId);
        if (uIndex > -1) {
          const oldUsername = users[uIndex].username;
          users[uIndex].username = username;
          users[uIndex].password = password;

          // Update tasks associated with this user if nickname changed
          if (oldUsername !== username) {
            tasks.forEach(t => {
              if (t.createdByName === oldUsername) t.createdByName = username;
            });
            if (currentUser && currentUser.id === editId) {
              currentUser.username = username;
            }
          }
        }
      } else {
        // Add new user
        const color = BADGE_PALETTE[users.length % BADGE_PALETTE.length];
        users.push({
          id: 'u-' + Date.now(),
          username,
          password,
          role: 'user',
          color
        });
      }

      saveState();
      populateMemberFilter();
      renderUsersList();
      resetUserForm();
      renderCalendar();
      if (currentUser) {
        document.getElementById('currentUserName').innerText = currentUser.username;
        document.getElementById('userAvatar').innerText = currentUser.username.charAt(0).toUpperCase();
      }
    }

    function removeUser(userId) {
      showConfirm('Bu üyeyi silmek istediğinize emin misiniz?', () => {
        users = users.filter(u => u.id !== userId);
        saveState();
        populateMemberFilter();
        renderUsersList();
        renderCalendar();
      });
    }

    function resetData() {
      closeUsersModal();
      showConfirm('Tüm görevler ve üyeler varsayılan ayarlara sıfırlansın mı?', () => {
        localStorage.removeItem('papatya_users');
        localStorage.removeItem('papatya_tasks');
        users = JSON.parse(JSON.stringify(DEFAULT_USERS));
        tasks = getInitialTasks();
        currentUser = users[0]; // Admin
        saveState();
        showMainView();
      });
    }

    // CONFIRM DIALOG
    function showConfirm(message, onConfirm) {
      const box = document.getElementById('confirmBox');
      document.getElementById('confirmMessage').innerText = message;
      box.classList.remove('hidden');
      lucide.createIcons();

      const okBtn = document.getElementById('confirmOkBtn');
      const cancelBtn = document.getElementById('confirmCancelBtn');

      const cleanup = () => {
        box.classList.add('hidden');
        okBtn.onclick = null;
        cancelBtn.onclick = null;
      };

      cancelBtn.onclick = cleanup;
      okBtn.onclick = () => {
        cleanup();
        onConfirm();
      };
    }

    function escapeHtml(str) {
      if (!str) return '';
      return str.replace(/[&<>"']/g, m => ({
        '&': '&amp;',
        '<': '&lt;',
        '>': '&gt;',
        '"': '&quot;',
        "'": '&#039;'
      }[m]));
    }
  </script>
</body>
</html>
```
