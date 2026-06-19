# jjina654-wq.io

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>도란도란 - 고등학교 학습 소모임 커뮤니티</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts (Noto Sans KR) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700;900&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Noto Sans KR', sans-serif;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
        /* Float pulse animation */
        @keyframes pulse-soft {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        .animate-pulse-soft {
            animation: pulse-soft 2s infinite ease-in-out;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col pb-24 md:pb-8 relative">

    <!-- REAL-NAME AUTHENTICATION OVERLAY (For High Schoolers) -->
    <div id="authOverlay" class="fixed inset-0 bg-slate-900/80 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 shadow-2xl border border-slate-100 transform transition-all">
            <div class="text-center mb-5">
                <div class="w-16 h-16 bg-gradient-to-tr from-amber-400 to-amber-600 rounded-3xl flex items-center justify-center shadow-lg shadow-amber-500/30 text-white font-black text-3xl mx-auto mb-3">
                    도
                </div>
                <h3 class="text-xl font-bold text-slate-900">도란도란 가입 (고등학생용)</h3>
                <p class="text-xs text-slate-500 mt-1">우리 동아리는 신뢰성 있는 공부 분위기 조성을 위해<br><span class="font-bold text-amber-600">실명제 및 희망학과 연동</span>을 시행하고 있습니다.</p>
            </div>

            <div class="space-y-3.5">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1"><i class="fa-solid fa-signature mr-1 text-slate-400"></i>본명 (실명)</label>
                    <input type="text" id="authRealName" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-amber-500" placeholder="홍길동 (실명만 가능)">
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1"><i class="fa-solid fa-graduation-cap mr-1 text-slate-400"></i>학년</label>
                        <select id="authGrade" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-amber-500">
                            <option value="1">1학년</option>
                            <option value="2">2학년</option>
                            <option value="3">3학년</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1"><i class="fa-solid fa-hashtag mr-1 text-slate-400"></i>반/번호</label>
                        <input type="text" id="authClassId" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-amber-500" placeholder="예: 3반 12번">
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1 flex justify-between items-center">
                        <span><i class="fa-solid fa-heart-pulse mr-1 text-slate-400"></i>목표/희망 학과</span>
                        <span class="text-[10px] text-slate-400 font-normal">선택사항</span>
                    </label>
                    <input type="text" id="authTargetMajor" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-amber-500" placeholder="예: 컴퓨터공학과, 의예과 (미입력 시 '미정')">
                </div>
                <div class="flex items-start space-x-2 bg-slate-50 p-3 rounded-xl border border-slate-100">
                    <input type="checkbox" id="authAgree" class="mt-0.5 rounded text-amber-500 focus:ring-amber-500">
                    <label for="authAgree" class="text-[10px] text-slate-500 leading-normal font-medium">본인은 고등학교 소모임 부원으로서 실명을 투명하게 밝히며, 선플과 정직한 정보 기재에 성실히 응할 것을 서약합니다.</label>
                </div>
            </div>

            <button onclick="submitRealNameAuth()" class="w-full mt-5 py-3 bg-gradient-to-r from-amber-500 to-orange-500 hover:from-amber-600 hover:to-orange-600 text-white font-bold rounded-xl text-xs transition shadow-lg shadow-amber-500/20">
                실명 가입 완료 및 입장
            </button>
        </div>
    </div>

    <!-- Top Navigation Bar -->
    <header class="bg-white border-b border-slate-100 sticky top-0 z-40 shadow-sm">
        <div class="max-w-5xl mx-auto px-4 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 bg-gradient-to-tr from-amber-500 to-orange-500 rounded-2xl flex items-center justify-center shadow-md shadow-amber-500/20 text-white font-black text-xl">
                    도
                </div>
                <div>
                    <h1 class="text-lg font-bold tracking-tight text-slate-900">도란도란</h1>
                    <p class="text-[10px] text-amber-600 font-bold">고등학교 연합 학습 커뮤니티</p>
                </div>
            </div>
            
            <!-- User Profile Quick Info -->
            <button onclick="openProfileModal()" class="flex items-center space-x-2 bg-slate-50 hover:bg-slate-100 transition p-1.5 pr-3 rounded-full border border-slate-100">
                <div id="userBadgeIcon" class="w-7 h-7 rounded-full bg-amber-500 text-white flex items-center justify-center text-sm">
                    🌱
                </div>
                <div class="text-left hidden sm:block">
                    <div class="flex items-center space-x-1">
                        <span id="userNameText" class="text-xs font-bold text-slate-700">홍길동</span>
                        <span id="userLevelText" class="bg-amber-100 text-amber-800 text-[9px] px-1.5 py-0.2 rounded font-bold">새싹🌱</span>
                    </div>
                    <p id="userExpBar" class="text-[8px] text-slate-400">EXP 0/10</p>
                </div>
                <span class="text-[10px] bg-emerald-500 text-white px-1.5 py-0.5 rounded-full font-bold"><i class="fa-solid fa-user-shield"></i> 고교실명</span>
            </button>
        </div>
    </header>

    <!-- Main Content Grid with Sidebar -->
    <div class="max-w-5xl w-full mx-auto p-4 flex flex-col md:flex-row gap-6">
        
        <!-- SIDEBAR FOR LARGE DEVICES -->
        <aside class="hidden md:block w-64 shrink-0 space-y-4">
            <div class="bg-white p-5 rounded-2xl border border-slate-100 shadow-sm text-center">
                <div id="sidebarBadgeIcon" class="w-14 h-14 bg-gradient-to-tr from-amber-100 to-amber-200 text-3xl flex items-center justify-center rounded-2xl mx-auto mb-2 shadow-inner">
                    🌱
                </div>
                <h3 class="font-bold text-slate-900 text-sm flex items-center justify-center gap-1">
                    <span id="sidebarName">홍길동</span>
                    <span id="sidebarLevelBadge" class="text-xs bg-amber-100 text-amber-800 px-1.5 py-0.5 rounded">새싹</span>
                </h3>
                <p class="text-[10px] text-slate-400 mt-0.5">목표: <span id="sidebarTargetMajor" class="font-bold text-slate-600">컴퓨터공학</span></p>
                
                <!-- Experience bar -->
                <div class="mt-3 space-y-1">
                    <div class="flex justify-between text-[9px] text-slate-400">
                        <span>성장 경험치</span>
                        <span id="sidebarExpRatio">0%</span>
                    </div>
                    <div class="w-full bg-slate-100 h-1.5 rounded-full overflow-hidden">
                        <div id="sidebarExpProgress" class="bg-amber-500 h-full rounded-full" style="width: 0%"></div>
                    </div>
                </div>
            </div>

            <!-- Side Nav Category Buttons -->
            <div class="bg-white rounded-2xl border border-slate-100 p-2 shadow-sm space-y-1">
                <button onclick="switchTab('mentor')" id="aside-mentor" class="aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-bold transition text-amber-600 bg-amber-50">
                    <i class="fa-solid fa-graduation-cap text-base"></i>
                    <span>멘토 멘티 & 프로필</span>
                </button>
                <button onclick="switchTab('study')" id="aside-study" class="aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-semibold transition text-slate-600 hover:bg-slate-50">
                    <i class="fa-solid fa-user-group text-base"></i>
                    <span>스터디 모집방</span>
                </button>
                <button onclick="switchTab('resource')" id="aside-resource" class="aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-semibold transition text-slate-600 hover:bg-slate-50">
                    <i class="fa-solid fa-folder-open text-base"></i>
                    <span>학습자료 공유방</span>
                </button>
                <button onclick="switchTab('freeboard')" id="aside-freeboard" class="aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-semibold transition text-slate-600 hover:bg-slate-50">
                    <i class="fa-solid fa-comments text-base"></i>
                    <span>자율 게시판</span>
                </button>
                <button onclick="switchTab('planner')" id="aside-planner" class="aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-semibold transition text-slate-600 hover:bg-slate-50">
                    <i class="fa-solid fa-calendar-check text-base"></i>
                    <span>스터디 플래너</span>
                </button>
                <button onclick="switchTab('timer')" id="aside-timer" class="aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-semibold transition text-slate-600 hover:bg-slate-50">
                    <i class="fa-solid fa-stopwatch text-base text-rose-500"></i>
                    <span>공부 타이머 & 뽀모도로</span>
                </button>
                <button onclick="switchTab('incorrect')" id="aside-incorrect" class="aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-semibold transition text-slate-600 hover:bg-slate-50">
                    <i class="fa-solid fa-book-open text-base text-indigo-500"></i>
                    <span>유사 오답노트</span>
                </button>
                <button onclick="switchTab('graph')" id="aside-graph" class="aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-semibold transition text-slate-600 hover:bg-slate-50">
                    <i class="fa-solid fa-chart-line text-base text-emerald-500"></i>
                    <span>성적 성장곡선</span>
                </button>
                <button onclick="switchTab('compliment')" id="aside-compliment" class="aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-semibold transition text-slate-600 hover:bg-slate-50">
                    <i class="fa-solid fa-envelope-open-text text-base text-rose-500"></i>
                    <span>칭찬 우체통 (익명)</span>
                </button>
            </div>
        </aside>

        <!-- MAIN WINDOW VIEWPORT -->
        <main class="flex-1 min-w-0 space-y-6">
            
            <!-- Attendance & Exam Countdown Panels -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                
                <!-- Countdown Dashboard -->
                <div class="bg-gradient-to-br from-indigo-600 to-purple-600 rounded-3xl p-5 text-white shadow-lg relative overflow-hidden">
                    <div class="absolute right-0 bottom-0 opacity-10 translate-x-2 translate-y-2 text-8xl font-bold"><i class="fa-regular fa-clock"></i></div>
                    <div class="relative z-10 flex flex-col justify-between h-full">
                        <div class="flex items-center justify-between">
                            <span class="bg-white/25 text-[10px] px-2.5 py-1 rounded-full font-bold">🎯 시험 카운트다운</span>
                            <button onclick="openExamModal()" class="text-white/80 hover:text-white text-xs"><i class="fa-solid fa-gear"></i> 일정 변경</button>
                        </div>
                        <div class="my-3">
                            <h3 class="text-xl font-bold" id="examDdayTitle">시험을 등록해주세요</h3>
                            <div class="text-4xl font-black mt-1" id="examDdayValue">D-Day</div>
                        </div>
                        <p class="text-[10px] text-indigo-100" id="examTargetDate">목표일: 미정</p>
                    </div>
                </div>

                <!-- Fast Stamp CheckIn panel -->
                <div class="bg-gradient-to-br from-amber-500 to-orange-500 rounded-3xl p-5 text-white shadow-lg relative overflow-hidden flex flex-col justify-between">
                    <div>
                        <span class="bg-white/20 text-[10px] px-2.5 py-1 rounded-full font-bold">📍 등교/출석 도장</span>
                        <h3 class="text-sm font-bold mt-3 leading-snug" id="greetingMessage">오늘도 공부할 준비 되셨나요?</h3>
                        <p class="text-[10px] text-amber-100 mt-1">출석체크 시 등급 성장을 위한 경험치 +2가 지급됩니다!</p>
                    </div>
                    <div class="flex items-center justify-between mt-4">
                        <div class="text-xs font-semibold">누적 인증: <span class="font-extrabold" id="totalAttendanceText">0</span>회</div>
                        <button id="btnAttendanceQuick" onclick="doAttendance()" class="bg-white text-amber-600 hover:bg-amber-50 font-bold text-xs px-3.5 py-1.5 rounded-xl shadow-sm transition">
                            <i class="fa-solid fa-stamp mr-1"></i>출석하기
                        </button>
                    </div>
                </div>
            </div>

            <!-- Attendance Mini log banner -->
            <div class="bg-white p-3.5 rounded-2xl border border-slate-150 shadow-sm flex flex-col sm:flex-row sm:items-center justify-between gap-3">
                <div class="flex items-center space-x-2 shrink-0">
                    <span class="text-lg">📢</span>
                    <span class="text-xs font-bold text-slate-800">오늘 공부실 입장 목록 <span id="todayAttendanceCount" class="text-amber-500">(0명)</span>:</span>
                </div>
                <div id="todayAttendanceList" class="flex flex-wrap gap-1.5 items-center">
                    <p class="text-xs text-slate-400" id="noAttendanceMsg">아직 오늘의 첫 입장 학우가 없습니다.</p>
                </div>
            </div>

            <!-- TAB 1: MENTOR/MENTEE & DETAILED PROFILE -->
            <section id="content-mentor" class="tab-content space-y-4">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 border-b border-slate-100 pb-3">
                    <div>
                        <h3 class="text-base font-bold text-slate-900">멘토 멘티 & 선배 매칭</h3>
                        <p class="text-xs text-slate-500">희망 학과 및 입시 특기를 기입해 상호 협력하는 학습 채널입니다.</p>
                    </div>
                    <div class="flex space-x-2">
                        <button onclick="openMentorRegModal()" class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-xs px-3.5 py-2.5 rounded-xl transition flex items-center space-x-1.5">
                            <i class="fa-solid fa-user-graduate"></i>
                            <span>멘토 등록</span>
                        </button>
                        <button onclick="openMentorCreateModal()" class="bg-amber-500 hover:bg-amber-600 text-white font-bold text-xs px-3.5 py-2.5 rounded-xl transition flex items-center space-x-1.5">
                            <i class="fa-solid fa-plus"></i>
                            <span>매칭글 작성</span>
                        </button>
                    </div>
                </div>

                <div class="flex space-x-2 bg-slate-150/60 p-1 rounded-xl w-fit">
                    <button id="subtab-m-posts" onclick="switchMentorSubTab('posts')" class="text-xs font-bold px-3.5 py-1.5 rounded-lg bg-white shadow-sm text-slate-800">멘토링 매칭 게시글</button>
                    <button id="subtab-m-profiles" onclick="switchMentorSubTab('profiles')" class="text-xs font-semibold px-3.5 py-1.5 rounded-lg text-slate-600 hover:text-slate-800">멘토 리스트 프로필</button>
                </div>

                <div id="mentor-posts-container" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <!-- Cards -->
                </div>

                <div id="mentor-profiles-container" class="grid grid-cols-1 md:grid-cols-2 gap-4 hidden">
                    <!-- Profiles -->
                </div>
            </section>

            <!-- TAB 2: STUDY GROUP -->
            <section id="content-study" class="tab-content hidden space-y-4">
                <div class="flex justify-between items-center">
                    <div>
                        <h3 class="text-base font-bold text-slate-900">스터디 모집방</h3>
                        <p class="text-xs text-slate-500">정기적으로 모여 문제 풀고 플래너를 대조해 볼 파티원을 구해봅니다.</p>
                    </div>
                    <button onclick="openStudyCreateModal()" class="bg-orange-500 hover:bg-orange-600 text-white font-bold text-xs px-4 py-2.5 rounded-xl transition">
                        스터디 개설
                    </button>
                </div>
                <div id="studyList" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <!-- Cards -->
                </div>
            </section>

            <!-- TAB 3: STUDY RESOURCE -->
            <section id="content-resource" class="tab-content hidden space-y-4">
                <div class="flex justify-between items-center">
                    <div>
                        <h3 class="text-base font-bold text-slate-900">학습자료 공유방</h3>
                        <p class="text-xs text-slate-500">정리 요점, 인강 교재 요약, 필기 정리 등 공공 자료를 아카이빙합니다.</p>
                    </div>
                    <button onclick="openResourceCreateModal()" class="bg-emerald-500 hover:bg-emerald-600 text-white font-bold text-xs px-4 py-2.5 rounded-xl transition">
                        자료 업로드
                    </button>
                </div>
                <div id="resourceList" class="space-y-3">
                    <!-- Items -->
                </div>
            </section>

            <!-- TAB 4: FREE BOARD -->
            <section id="content-freeboard" class="tab-content hidden space-y-4">
                <div class="flex justify-between items-center">
                    <div>
                        <h3 class="text-base font-bold text-slate-900">자율 게시판</h3>
                        <p class="text-xs text-slate-500">고등학교 일상 소통, 학우 고민 상담 등 프리 토크 라운지입니다.</p>
                    </div>
                    <button onclick="openFreePostModal()" class="bg-sky-500 hover:bg-sky-600 text-white font-bold text-xs px-4 py-2.5 rounded-xl transition">
                        새 글 쓰기
                    </button>
                </div>
                <div id="freeBoardList" class="space-y-4">
                    <!-- Items -->
                </div>
            </section>

            <!-- TAB 5: PLANNER -->
            <section id="content-planner" class="tab-content hidden space-y-4">
                <div>
                    <h3 class="text-base font-bold text-slate-900">스터디 플래너</h3>
                    <p class="text-xs text-slate-500">공부 분량을 효율적으로 쪼개어 계획하고 성공률을 추적합니다.</p>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
                    <div class="bg-white border border-slate-150 p-5 rounded-2xl h-fit shadow-sm space-y-3">
                        <h4 class="text-xs font-bold text-slate-700">📌 오늘 공부 분량 등록</h4>
                        <input type="text" id="plannerTaskInput" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="예: 영단어 50개 암기">
                        <button onclick="addPlannerTask()" class="w-full py-2.5 bg-indigo-600 hover:bg-indigo-700 text-white font-bold rounded-xl text-xs transition">
                            추가
                        </button>
                    </div>
                    <div class="md:col-span-2 bg-white border border-slate-100 rounded-2xl p-5 shadow-sm space-y-4">
                        <div class="flex justify-between items-center">
                            <h4 class="text-xs font-bold text-slate-700">성취 지표</h4>
                            <span class="text-xs font-bold text-indigo-600" id="plannerProgressText">0% 완료</span>
                        </div>
                        <div class="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                            <div class="bg-indigo-500 h-full rounded-full transition-all duration-300" style="width: 0%" id="plannerProgressBar"></div>
                        </div>
                        <div id="plannerTaskList" class="space-y-2 pt-2">
                            <!-- Tasks -->
                        </div>
                    </div>
                </div>
            </section>

            <!-- TAB 6: STUDY TIMER (공부 타이머) -->
            <section id="content-timer" class="tab-content hidden space-y-4">
                <div>
                    <h3 class="text-base font-bold text-slate-900">집중 공부 타이머</h3>
                    <p class="text-xs text-slate-500">순공 시간을 정확히 기록해 성적의 밀도를 강화하세요. 뽀모도로 세션도 활용 가능합니다.</p>
                </div>
                
                <div class="bg-white border border-slate-100 rounded-3xl p-8 shadow-sm text-center max-w-md mx-auto space-y-6">
                    <div class="text-5xl font-black tracking-widest text-slate-800" id="timerDisplay">00:00:00</div>
                    
                    <div class="flex justify-center space-x-3">
                        <button onclick="startTimer()" id="btnTimerStart" class="bg-rose-500 hover:bg-rose-600 text-white font-bold text-xs px-5 py-2.5 rounded-xl shadow-md transition flex items-center space-x-1">
                            <i class="fa-solid fa-play"></i>
                            <span>시작</span>
                        </button>
                        <button onclick="pauseTimer()" id="btnTimerPause" class="bg-slate-500 hover:bg-slate-600 text-white font-bold text-xs px-5 py-2.5 rounded-xl shadow-md transition flex items-center space-x-1" disabled>
                            <i class="fa-solid fa-pause"></i>
                            <span>일시정지</span>
                        </button>
                        <button onclick="resetTimer()" class="bg-slate-200 hover:bg-slate-300 text-slate-700 font-bold text-xs px-5 py-2.5 rounded-xl transition">
                            초기화
                        </button>
                    </div>

                    <div class="bg-slate-50 p-3.5 rounded-2xl border border-slate-100">
                        <p class="text-[11px] text-slate-500 font-medium">💡 타이머를 실행한 후 다른 탭이나 자율 게시판으로 이동해도 우측 하단에 미니 플로팅 타이머가 지속 추적됩니다.</p>
                    </div>
                </div>
            </section>

            <!-- TAB 7: AUTOMATIC INCORRECT NOTE (유사 오답노트 자동생성) -->
            <section id="content-incorrect" class="tab-content hidden space-y-4">
                <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                    <div>
                        <h3 class="text-base font-bold text-slate-900">오답노트 & AI 유사 문제 발전소</h3>
                        <p class="text-xs text-slate-500">틀린 문제 유형을 입력하면 유사한 변형 문제를 즉시 도출하여 극복 훈련을 시켜드립니다.</p>
                    </div>
                    <button onclick="openIncorrectModal()" class="bg-indigo-500 hover:bg-indigo-600 text-white font-bold text-xs px-3.5 py-2 rounded-xl transition flex items-center space-x-1">
                        <i class="fa-solid fa-circle-plus"></i>
                        <span>오답 등록하기</span>
                    </button>
                </div>

                <div id="incorrectList" class="space-y-4">
                    <!-- Cards with auto generated questions will build here -->
                </div>
            </section>

            <!-- TAB 8: GROWTH GRAPH -->
            <section id="content-graph" class="tab-content hidden space-y-4">
                <div>
                    <h3 class="text-base font-bold text-slate-900">학기별 성적 성장곡선</h3>
                    <p class="text-xs text-slate-500">내 모의고사나 내신 원점수를 기입하면 실시간으로 성장의 추이를 그라데이션 곡선 차트로 증명합니다.</p>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
                    <div class="bg-white border border-slate-150 p-5 rounded-2xl h-fit shadow-sm space-y-3">
                        <h4 class="text-xs font-bold text-slate-700">📊 성적 정보 기입</h4>
                        <div>
                            <label class="block text-[10px] font-bold text-slate-400 mb-1">시험 회차 (예: 1학년 6월 모평)</label>
                            <input type="text" id="scoreTerm" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-emerald-500" placeholder="예: 2학년 1학기 기말">
                        </div>
                        <div>
                            <label class="block text-[10px] font-bold text-slate-400 mb-1">평균 성적 점수 (0 ~ 100)</label>
                            <input type="number" id="scoreNum" min="0" max="100" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-emerald-500" placeholder="예: 92">
                        </div>
                        <button onclick="addScoreData()" class="w-full py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl text-xs transition">
                            등록
                        </button>
                    </div>
                    <div class="md:col-span-2 bg-white border border-slate-100 rounded-2xl p-5 shadow-sm space-y-4">
                        <div class="flex items-center justify-between">
                            <h4 class="text-xs font-bold text-slate-700">성장 성적 도식</h4>
                            <button onclick="resetScores()" class="text-[10px] text-rose-500 hover:underline"><i class="fa-solid fa-rotate-left mr-1"></i>초기화</button>
                        </div>
                        <div class="w-full h-48 bg-slate-50 border border-slate-100 rounded-xl flex items-center justify-center p-2">
                            <svg id="growthGraphSvg" class="w-full h-full" viewBox="0 0 500 150" preserveAspectRatio="none"></svg>
                        </div>
                        <div id="scoreLabelsList" class="flex flex-wrap gap-2"></div>
                    </div>
                </div>
            </section>

            <!-- TAB 9: COMPLIMENT -->
            <section id="content-compliment" class="tab-content hidden space-y-4">
                <div class="bg-rose-50 border border-rose-100/60 p-4 rounded-2xl">
                    <p class="text-xs text-rose-800 leading-relaxed">익명으로 칭찬 메시지를 보내보세요. 욕설이나 비방 단어(바보, 쓰레기 등) 입력 시 등록이 원천 차단됩니다.</p>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
                    <div class="bg-white border border-rose-100 p-5 rounded-2xl h-fit shadow-sm space-y-4">
                        <h4 class="text-sm font-bold text-slate-900"><i class="fa-solid fa-paper-plane text-rose-500 mr-1"></i>엽서 쓰기</h4>
                        <div>
                            <label class="block text-[11px] font-bold text-slate-500 mb-1">전달할 학년</label>
                            <select id="complimentTargetGrade" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-rose-500">
                                <option value="all">전체 학우</option>
                                <option value="1">1학년</option>
                                <option value="2">2학년</option>
                                <option value="3">3학년</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-[11px] font-bold text-slate-500 mb-1">칭찬할 내용</label>
                            <textarea id="complimentText" rows="4" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-rose-500 resize-none" placeholder="익명으로 학우에게 용기를 주는 칭찬을 작성하세요..."></textarea>
                        </div>
                        <button onclick="submitCompliment()" class="w-full py-2.5 bg-rose-500 hover:bg-rose-600 text-white font-bold rounded-xl text-xs transition">
                            보내기
                        </button>
                    </div>
                    <div class="md:col-span-2 space-y-3">
                        <h4 class="text-xs font-bold text-slate-700">도착한 칭찬 메시지</h4>
                        <div id="complimentList" class="space-y-3 max-h-[400px] overflow-y-auto pr-1"></div>
                    </div>
                </div>
            </section>
        </main>
    </div>

    <!-- PERSISTENT FLOATING MINI TIMER (PIP MODE) -->
    <div id="floatingTimer" onclick="switchTab('timer')" class="fixed bottom-20 right-4 md:bottom-6 md:right-6 bg-rose-500 hover:bg-rose-600 text-white p-3 rounded-full shadow-2xl flex items-center justify-center space-x-2 cursor-pointer z-50 border-2 border-white animate-pulse-soft hidden transition-all duration-300">
        <i class="fa-solid fa-stopwatch text-base"></i>
        <span id="floatingTimeText" class="text-xs font-black">00:00:00</span>
    </div>

    <!-- MOBILE NAVIGATION TAB BAR -->
    <nav class="md:hidden fixed bottom-0 left-0 right-0 bg-white border-t border-slate-200 py-2.5 px-4 flex justify-around items-center z-40 shadow-[0_-2px_10px_rgba(0,0,0,0.05)] overflow-x-auto gap-3">
        <button onclick="switchTab('mentor')" id="mobile-tab-mentor" class="flex flex-col items-center shrink-0 space-y-1 text-amber-500">
            <i class="text-base fa-solid fa-graduation-cap"></i>
            <span class="text-[9px] font-bold">멘토</span>
        </button>
        <button onclick="switchTab('study')" id="mobile-tab-study" class="flex flex-col items-center shrink-0 space-y-1 text-slate-400">
            <i class="text-base fa-solid fa-user-group"></i>
            <span class="text-[9px] font-semibold">스터디</span>
        </button>
        <button onclick="switchTab('resource')" id="mobile-tab-resource" class="flex flex-col items-center shrink-0 space-y-1 text-slate-400">
            <i class="text-base fa-solid fa-folder-open"></i>
            <span class="text-[9px] font-semibold">자료방</span>
        </button>
        <button onclick="switchTab('freeboard')" id="mobile-tab-freeboard" class="flex flex-col items-center shrink-0 space-y-1 text-slate-400">
            <i class="text-base fa-solid fa-comments"></i>
            <span class="text-[9px] font-semibold">자율방</span>
        </button>
        <button onclick="switchTab('planner')" id="mobile-tab-planner" class="flex flex-col items-center shrink-0 space-y-1 text-slate-400">
            <i class="text-base fa-solid fa-calendar-check"></i>
            <span class="text-[9px] font-semibold">플래너</span>
        </button>
        <button onclick="switchTab('timer')" id="mobile-tab-timer" class="flex flex-col items-center shrink-0 space-y-1 text-slate-400">
            <i class="text-base fa-solid fa-stopwatch text-rose-500"></i>
            <span class="text-[9px] font-semibold">타이머</span>
        </button>
        <button onclick="switchTab('incorrect')" id="mobile-tab-incorrect" class="flex flex-col items-center shrink-0 space-y-1 text-slate-400">
            <i class="text-base fa-solid fa-book-open"></i>
            <span class="text-[9px] font-semibold">오답노트</span>
        </button>
    </nav>

    <!-- MODAL LAYOUTS -->

    <!-- INCORRECT NOTE SUBMISSION MODAL -->
    <div id="incorrectRegModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-4">
                <h4 class="text-base font-bold text-slate-900">오답노트 등록</h4>
                <button onclick="closeIncorrectModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">교과목 / 유형</label>
                    <input type="text" id="incSubject" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="예: 고등 수학I - 수열">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">내가 원래 틀렸던 문제 기입</label>
                    <textarea id="incOriginal" rows="3" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-indigo-500 resize-none" placeholder="예: 다음 등차수열의 제 10항을 구하시오..."></textarea>
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">나의 오답 원인 분석</label>
                    <input type="text" id="incMistake" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="예: 공차 d를 더하는 과정에서 덧셈 실수가 있었음">
                </div>
            </div>
            <div class="flex space-x-2 mt-5">
                <button onclick="closeIncorrectModal()" class="flex-1 py-2.5 bg-slate-100 text-slate-700 font-bold rounded-xl text-xs">취소</button>
                <button onclick="submitIncorrect()" class="flex-1 py-2.5 bg-indigo-600 text-white font-bold rounded-xl text-xs transition">자동 변형문제 생성</button>
            </div>
        </div>
    </div>

    <!-- SET TARGET EXAM DATE MODAL -->
    <div id="examModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-sm w-full p-6 shadow-2xl">
            <div class="flex justify-between items-center mb-4">
                <h4 class="text-base font-bold text-slate-900">목표 시험 디데이 등록</h4>
                <button onclick="closeExamModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">시험 명칭</label>
                    <input type="text" id="inputExamName" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="예: 고3 9월 평가원 모의고사">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">시험 날짜</label>
                    <input type="date" id="inputExamDate" class="w-full px-3 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-indigo-500">
                </div>
            </div>
            <div class="flex space-x-2 mt-5">
                <button onclick="closeExamModal()" class="flex-1 py-2.5 bg-slate-100 text-slate-700 font-bold rounded-xl text-xs">취소</button>
                <button onclick="saveExamDday()" class="flex-1 py-2.5 bg-indigo-600 text-white font-bold rounded-xl text-xs transition">저장</button>
            </div>
        </div>
    </div>

    <!-- MODALS FROM PREVIOUS VERSIONS (Profile, Mentors, Studies, Free detail) -->
    <!-- MENTOR REGISTRATION -->
    <div id="mentorRegModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-4">
                <h4 class="text-base font-bold text-slate-900">정식 멘토 등록</h4>
                <button onclick="closeMentorRegModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">나의 학습 주전공 / 전문 멘토링 과목</label>
                    <input type="text" id="mentorRegSpecialty" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs" placeholder="예: 영어 구문 독해, 생명과학 유전 파트 요약">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">특기, 수상실적 또는 동기부여 요소 (콤마구분)</label>
                    <input type="text" id="mentorRegCertificates" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs" placeholder="예: 모평 전과목 1등급, 영어 올림피아드 입상">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">멘토 인사말</label>
                    <textarea id="mentorRegIntro" rows="3" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs resize-none" placeholder="후배들을 가르칠 다정한 소개글을 적어주세요."></textarea>
                </div>
            </div>
            <div class="flex space-x-2 mt-5">
                <button onclick="closeMentorRegModal()" class="flex-1 py-2.5 bg-slate-100 text-slate-700 font-bold rounded-xl text-xs">취소</button>
                <button onclick="submitMentorProfile()" class="flex-1 py-2.5 bg-indigo-600 text-white font-bold rounded-xl text-xs">등록</button>
            </div>
        </div>
    </div>

    <!-- MENTOR POSTS -->
    <div id="mentorCreateModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-4">
                <h4 class="text-base font-bold text-slate-900">구인글 쓰기</h4>
                <button onclick="closeMentorCreateModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1.5">선택 구분</label>
                    <div class="grid grid-cols-2 gap-2">
                        <button onclick="setMentoringRole('mentor')" id="role-opt-mentor" class="role-opt py-2 border rounded-xl font-bold text-xs border-amber-500 bg-amber-50 text-amber-700">멘토를 모십니다</button>
                        <button onclick="setMentoringRole('mentee')" id="role-opt-mentee" class="role-opt py-2 border rounded-xl font-bold text-xs border-slate-200 hover:border-slate-300">멘티를 모십니다</button>
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1.5">희망 학습 과목</label>
                    <input type="text" id="mentorSubject" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-sm" placeholder="예: 수학II 미분 파트 격파">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1.5">상세 내용 기재</label>
                    <textarea id="mentorDetail" rows="4" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-sm resize-none" placeholder="만날 요일, 방식 등 적어주세요."></textarea>
                </div>
            </div>
            <div class="flex space-x-2 mt-6">
                <button onclick="closeMentorCreateModal()" class="flex-1 py-3 bg-slate-100 text-slate-700 font-bold rounded-xl text-xs">취소</button>
                <button onclick="createMentoringPost()" class="flex-1 py-3 bg-amber-500 text-white font-bold rounded-xl text-xs">등록</button>
            </div>
        </div>
    </div>

    <!-- STUDY GROUP CREATE -->
    <div id="studyCreateModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-4">
                <h4 class="text-base font-bold text-slate-900">새 스터디 모임 개설</h4>
                <button onclick="closeStudyCreateModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">스터디 명칭</label>
                    <input type="text" id="studyTitle" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs" placeholder="예: 자습 매일 3시간 체크">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">과제 테마</label>
                    <input type="text" id="studyTopic" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs" placeholder="예: 영어 기출 / 사탐 / 정시파이터">
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">모집 최대 인원</label>
                        <input type="number" id="studyMaxMembers" min="2" max="10" value="4" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">주기</label>
                        <select id="studyCycle" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs">
                            <option value="매일">매일</option>
                            <option value="주 2회">주 2회</option>
                            <option value="주 3회">주 3회</option>
                            <option value="자율">자율</option>
                        </select>
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">모임 규칙</label>
                    <textarea id="studyDetail" rows="3" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs resize-none" placeholder="간단한 공부 규칙"></textarea>
                </div>
            </div>
            <div class="flex space-x-2 mt-6">
                <button onclick="closeStudyCreateModal()" class="flex-1 py-3 bg-slate-100 text-slate-700 font-bold rounded-xl text-xs">취소</button>
                <button onclick="createStudyPost()" class="flex-1 py-3 bg-orange-500 text-white font-bold rounded-xl text-xs">개설 완료</button>
            </div>
        </div>
    </div>

    <!-- STUDY RESOURCE CREATE -->
    <div id="resourceCreateModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-4">
                <h4 class="text-base font-bold text-slate-900">학습 자료 아카이브</h4>
                <button onclick="closeResourceCreateModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">자료 명칭</label>
                    <input type="text" id="resourceTitle" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs" placeholder="예: 영어 구문 7개 암기 카드">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">학과 / 계열</label>
                    <input type="text" id="resourceCategory" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs" placeholder="예: 영어 / 교양 / 학술">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">다운로드 링크 (구글 등)</label>
                    <input type="text" id="resourceLink" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs" placeholder="자료 공유 클라우드 링크">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">해설 / 노트정리</label>
                    <textarea id="resourceDetail" rows="3" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs resize-none" placeholder="공부 방법 제언"></textarea>
                </div>
            </div>
            <div class="flex space-x-2 mt-6">
                <button onclick="closeResourceCreateModal()" class="flex-1 py-3 bg-slate-100 text-slate-700 font-bold rounded-xl text-xs">취소</button>
                <button onclick="createResourcePost()" class="flex-1 py-3 bg-emerald-500 text-white font-bold rounded-xl text-xs">등록</button>
            </div>
        </div>
    </div>

    <!-- FREE POST MODAL -->
    <div id="freePostModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl">
            <div class="flex justify-between items-center mb-4">
                <h4 class="text-base font-bold text-slate-900">자율게시판 글쓰기</h4>
                <button onclick="closeFreePostModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">글 제목</label>
                    <input type="text" id="freePostTitle" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs" placeholder="제목 기입">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">본문</label>
                    <textarea id="freePostContent" rows="5" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs resize-none" placeholder="자유로운 소통"></textarea>
                </div>
            </div>
            <div class="flex space-x-2 mt-6">
                <button onclick="closeFreePostModal()" class="flex-1 py-2.5 bg-slate-100 text-slate-700 font-bold rounded-xl text-xs">취소</button>
                <button onclick="createFreePost()" class="flex-1 py-2.5 bg-sky-500 text-white font-bold rounded-xl text-xs">글 올리기</button>
            </div>
        </div>
    </div>

    <!-- FREE POST DETAIL & COMMENTS -->
    <div id="freeDetailModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-3">
                <span class="text-[10px] bg-slate-100 px-2 py-0.5 rounded font-bold" id="detailPostGrade">1학년</span>
                <button onclick="closeFreeDetailModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="space-y-3 pb-4 border-b border-slate-100">
                <h4 class="text-base font-bold text-slate-900" id="detailPostTitle">제목</h4>
                <div class="flex items-center space-x-2 text-[10px] text-slate-400">
                    <span id="detailPostAuthor" class="font-bold text-slate-700">홍길동</span>
                    <span id="detailPostDate">2026.06.12</span>
                </div>
                <p class="text-xs text-slate-700 leading-relaxed whitespace-pre-line bg-slate-50 p-3.5 rounded-xl" id="detailPostContent">내용</p>
            </div>
            <div class="pt-4 space-y-3">
                <h5 class="text-xs font-bold text-slate-800">댓글달기</h5>
                <div class="flex space-x-2">
                    <input type="text" id="commentInput" class="flex-1 px-3 py-2 border border-slate-200 rounded-xl text-xs" placeholder="선한 칭찬의 문장을 남겨봐요.">
                    <button onclick="submitComment()" class="px-3.5 py-2 bg-sky-500 hover:bg-sky-600 text-white font-bold rounded-xl text-xs transition">등록</button>
                </div>
                <div class="space-y-2 pt-2" id="detailCommentsList"></div>
            </div>
        </div>
    </div>

    <!-- PROFILE/MYPAGE -->
    <div id="profileModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl">
            <div class="flex justify-between items-center mb-4">
                <h4 class="text-sm font-bold text-slate-900"><i class="fa-solid fa-user-gear text-amber-500 mr-1.5"></i>학적부 및 마이페이지</h4>
                <button onclick="closeProfileModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-400 mb-1">인증 실명 (수정불가)</label>
                    <input type="text" id="editUserName" class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs text-slate-500 font-semibold cursor-not-allowed" disabled>
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-400 mb-1">목표 희망학과 (수정불가)</label>
                    <input type="text" id="editUserTargetMajor" class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs text-slate-500 font-semibold cursor-not-allowed" disabled>
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-bold text-slate-400 mb-1">학년</label>
                        <input type="text" id="editUserGrade" class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs text-slate-500 font-semibold cursor-not-allowed" disabled>
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-400 mb-1">반/번호</label>
                        <input type="text" id="editUserClassId" class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs text-slate-500 font-semibold cursor-not-allowed" disabled>
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">나의 한마디 소개글</label>
                    <input type="text" id="editUserBio" class="w-full px-3.5 py-2 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-amber-500">
                </div>
            </div>
            <div class="flex space-x-2 mt-6">
                <button onclick="closeProfileModal()" class="flex-1 py-3 bg-slate-100 text-slate-700 font-bold rounded-xl text-xs">취소</button>
                <button onclick="saveUserProfile()" class="flex-1 py-3 bg-amber-500 text-white font-bold rounded-xl text-xs">소개글 저장</button>
            </div>
        </div>
    </div>

    <!-- Toast Overlay -->
    <div id="toastMessage" class="fixed top-20 left-1/2 -translate-x-1/2 bg-slate-900 text-white text-xs font-bold py-3 px-6 rounded-full shadow-lg opacity-0 transition-opacity duration-300 pointer-events-none z-50 flex items-center space-x-2">
        <span id="toastIcon"></span>
        <span id="toastText">처리되었습니다.</span>
    </div>

    <script>
        // --- 1. STATE & DEFAULT DB ---
        let currentUser = null;
        let currentTab = 'mentor';
        let currentMentorSubTab = 'posts';
        let gradeFilter = 'all';
        let searchQuery = '';
        let selectedMentoringRole = "mentor";
        let activePostIdForComment = null;

        // Banned words
        const bannedWords = ["바보", "짜증", "새끼", "시발", "개새", "존나", "쓰레기", "닥쳐", "등신", "미친", "호구", "지랄", "씨발", "꺼져", "썅", "개같은"];

        // Highschool Default Seed Exam D-day
        let targetExam = JSON.parse(localStorage.getItem("doran_exam_dday")) || {
            title: "2학기 수능 대비 평가원 모의고사",
            date: "2026-09-03"
        };

        // Seeds
        const defaultMentorProfiles = [
            {
                id: "p-1",
                name: "김수현",
                grade: "3",
                major: "컴퓨터학부 목표",
                specialty: "수학I 삼각함수 완전 공략 & 미적분 입문",
                certificates: "모의고사 수학 1등급, 수학경시대회 장려상",
                intro: "의외로 수능 수학은 공식 연상 훈련만 되면 2등급 이상은 쉽습니다. 기초가 약한 1, 2학년 학우들을 따뜻하게 도와드릴게요!"
            }
        ];

        const defaultMentors = [
            {
                id: "m-1",
                role: "mentor",
                author: "김수현",
                grade: "3",
                subject: "영어 어법 구문 독해 빈칸추론 격파",
                detail: "어려운 장문 영어 독해에서 막히는 후배님들을 위해 매주 수요일 저녁 Zoom 스터디를 준비했습니다. 관심 있는 학우는 매칭 신청하세요!",
                subscribers: [],
                likedBy: ["이지은", "강동우"],
                date: "2026.06.10"
            }
        ];

        const defaultStudies = [
            {
                id: "s-1",
                title: "매일 아침 7:30 영단어 100개 인증방",
                topic: "영어 / EBS 연계",
                author: "이지은",
                grade: "2",
                maxMembers: 5,
                members: ["이지은"],
                cycle: "매일",
                detail: "EBS 수능특강 핵심 영단어를 매일 무조건 자가 테스트하고 스크린샷 올리는 강제성 스터디입니다.",
                date: "2026.06.11"
            }
        ];

        const defaultResources = [
            {
                id: "r-1",
                title: "한국사 근현대사 흐름 요약 타임라인 지도",
                category: "역사 / 공통",
                author: "김수현",
                grade: "3",
                link: "https://drive.google.com/drive/folders/resource-demo1",
                detail: "한눈에 흐름을 파악하기 힘든 개항기 및 임시정부 역사를 한 장짜리 연표로 기획 구성한 일러스트 노트입니다.",
                likedBy: ["이지은", "박민지", "최현우"],
                downloads: 48,
                date: "2026.06.09"
            }
        ];

        const defaultFreePosts = [
            {
                id: "f-1",
                title: "오늘 모의고사 피드백 다들 어떠셨어요?",
                content: "생각보다 영어 시간 배분이 너무 타이트했네요... 빈칸 31~34번 라인은 역시 악랄했습니다. 다들 화이팅해서 다음 기말고사 잘 봐요!",
                author: "이지은",
                grade: "2",
                date: "2026.06.12",
                likedBy: ["김수현", "강태경"],
                comments: [
                    { author: "김수현", grade: "3", text: "시간 관리 훈련을 하려면 실전 모의고사를 평소 65분 타이머 맞춰두고 풀어보는 습관이 아주 요긴합니다!" }
                ]
            }
        ];

        const defaultCompliments = [
            {
                id: "c-1",
                targetGrade: "1",
                text: "저번에 야간 자율학습 끝날 때 독서실 형광등 다 꺼주시고 창문 닫아주신 착한 학우분, 항상 칭찬하고 고맙게 생각해요!",
                date: "2026.06.12",
                likedBy: ["민경찬", "이지현"]
            }
        ];

        const defaultTasks = [
            { id: "t-1", task: "오늘 오답노트에서 AI 유사 문제 1회 해결하기", completed: false },
            { id: "t-2", task: "순공 집중 타이머 1시간 채우기", completed: true }
        ];

        const defaultScores = [
            { term: "1학년 1학기 중간", score: 72 },
            { term: "1학년 1학기 기말", score: 79 },
            { term: "1학년 2학기 중간", score: 86 },
            { term: "1학년 2학기 기말", score: 91 }
        ];

        const defaultIncorrectNotes = [
            {
                id: "inc-1",
                subject: "수학 - 등차수열",
                originalQuestion: "첫째항이 3이고, 제 5항이 15인 등차수열의 공차를 구하시오.",
                mistakeReason: "공차 d를 더하는 과정에서 연산 실수로 15 - 3 = 12를 4로 나누지 않고 5로 나눔.",
                generatedQuestion: "첫째항이 5이고, 제 6항이 25인 새로운 등차수열의 공차를 구하시오.",
                generatedAnswer: "정답: 4",
                generatedExplanation: "제 6항은 a + 5d = 25 이므로, 5 + 5d = 25 ➔ 5d = 20이 되어 공차 d는 4가 됩니다.",
                resolved: false
            }
        ];

        // Load Databases
        let mentors = JSON.parse(localStorage.getItem("doran_mentors")) || defaultMentors;
        let mentorProfiles = JSON.parse(localStorage.getItem("doran_mentor_profiles")) || defaultMentorProfiles;
        let studies = JSON.parse(localStorage.getItem("doran_studies")) || defaultStudies;
        let resources = JSON.parse(localStorage.getItem("doran_resources")) || defaultResources;
        let freePosts = JSON.parse(localStorage.getItem("doran_free_posts")) || defaultFreePosts;
        let compliments = JSON.parse(localStorage.getItem("doran_compliments")) || defaultCompliments;
        let plannerTasks = JSON.parse(localStorage.getItem("doran_planner_tasks")) || defaultTasks;
        let growthScores = JSON.parse(localStorage.getItem("doran_growth_scores")) || defaultScores;
        let incorrectNotes = JSON.parse(localStorage.getItem("doran_incorrect_notes")) || defaultIncorrectNotes;

        // DATA MIGRATION: Ensure all likes fields are converted to likedBy arrays
        function migrateLikes(list) {
            list.forEach(item => {
                if (typeof item.likedBy === 'undefined' || !Array.isArray(item.likedBy)) {
                    item.likedBy = [];
                }
            });
        }
        migrateLikes(mentors);
        migrateLikes(resources);
        migrateLikes(freePosts);
        migrateLikes(compliments);

        let todayStr = new Date().toISOString().slice(0, 10);
        let attendances = JSON.parse(localStorage.getItem("doran_attendances"));
        if (!attendances || attendances.date !== todayStr) {
            attendances = {
                date: todayStr,
                list: [
                    { name: "김수현", grade: "3", time: "08:15" },
                    { name: "이지은", grade: "2", time: "08:42" }
                ]
            };
        }

        // --- STUDY TIMER VARIABLES ---
        let timerInterval = null;
        let secondsElapsed = parseInt(localStorage.getItem("doran_seconds_elapsed")) || 0;
        let timerRunning = false;

        // --- 2. VERIFY REGISTERED HIGH SCHOOL USER ---
        currentUser = JSON.parse(localStorage.getItem("doran_user"));

        window.onload = function() {
            if (!currentUser) {
                document.getElementById("authOverlay").classList.remove("hidden");
            } else {
                completeStartSession();
            }
        };

        function submitRealNameAuth() {
            const realName = document.getElementById("authRealName").value.trim();
            const grade = document.getElementById("authGrade").value;
            const classId = document.getElementById("authClassId").value.trim();
            const targetMajor = document.getElementById("authTargetMajor").value.trim();
            const agree = document.getElementById("authAgree").checked;

            if (!realName || realName.length < 2) {
                showToast("실명을 정확히 기재해 주세요.", "error");
                return;
            }
            if (!classId) {
                showToast("반/번호 정보를 채워주세요.", "error");
                return;
            }
            if (!agree) {
                showToast("실명 인증 약관 동의가 필요합니다.", "error");
                return;
            }

            currentUser = {
                name: realName,
                grade: grade,
                classId: classId,
                major: targetMajor || "미정", // targetMajor is now fully optional, default to "미정"
                bio: "반갑습니다! 오늘부터 도란도란과 함께 달릴 예정입니다.",
                exp: 0,
                totalAttendance: 0,
                lastAttendanceDate: ""
            };

            localStorage.setItem("doran_user", JSON.stringify(currentUser));
            document.getElementById("authOverlay").classList.add("hidden");
            showToast("실명 매핑 등록에 가입되었습니다! 즐거운 학습 되세요.");
            completeStartSession();
        }

        function completeStartSession() {
            updateUserInfoUI();
            updateAttendanceUI();
            calculateExamDday();
            initTimerStatusOnLoad();
            renderAll();
        }

        // --- 3. EXP & LEVELING MECHANISM ---
        function addExperience(amount) {
            if (!currentUser) return;
            currentUser.exp = (currentUser.exp || 0) + amount;
            saveToStorage();
            updateUserInfoUI();
            showToast(`경험치가 +${amount} 증가했습니다! ✨`);
        }

        function getLevelDetails(exp) {
            if (exp <= 10) {
                return { name: "새싹🌱", level: 1, maxExp: 10, current: exp, min: 0 };
            } else if (exp <= 30) {
                return { name: "도전자📚", level: 2, maxExp: 30, current: exp, min: 11 };
            } else if (exp <= 70) {
                return { name: "성장러🚀", level: 3, maxExp: 70, current: exp, min: 31 };
            } else {
                return { name: "마스터👑", level: 4, maxExp: 999, current: exp, min: 71 };
            }
        }

        // --- 4. TOASTS & SAVER ---
        function showToast(message, type = 'success') {
            const toast = document.getElementById("toastMessage");
            const text = document.getElementById("toastText");
            const icon = document.getElementById("toastIcon");

            text.textContent = message;
            if (type === 'success') {
                icon.innerHTML = `<i class="fa-solid fa-circle-check text-emerald-500 text-base"></i>`;
            } else if (type === 'error') {
                icon.innerHTML = `<i class="fa-solid fa-triangle-exclamation text-rose-500 text-base"></i>`;
            } else {
                icon.innerHTML = `<i class="fa-solid fa-circle-info text-blue-500 text-base"></i>`;
            }

            toast.classList.remove("opacity-0", "pointer-events-none");
            toast.classList.add("opacity-100");

            setTimeout(() => {
                toast.classList.remove("opacity-100");
                toast.classList.add("opacity-0", "pointer-events-none");
            }, 2500);
        }

        function saveToStorage() {
            localStorage.setItem("doran_mentors", JSON.stringify(mentors));
            localStorage.setItem("doran_mentor_profiles", JSON.stringify(mentorProfiles));
            localStorage.setItem("doran_studies", JSON.stringify(studies));
            localStorage.setItem("doran_resources", JSON.stringify(resources));
            localStorage.setItem("doran_free_posts", JSON.stringify(freePosts));
            localStorage.setItem("doran_compliments", JSON.stringify(compliments));
            localStorage.setItem("doran_planner_tasks", JSON.stringify(plannerTasks));
            localStorage.setItem("doran_growth_scores", JSON.stringify(growthScores));
            localStorage.setItem("doran_incorrect_notes", JSON.stringify(incorrectNotes));
            localStorage.setItem("doran_user", JSON.stringify(currentUser));
            localStorage.setItem("doran_attendances", JSON.stringify(attendances));
            localStorage.setItem("doran_exam_dday", JSON.stringify(targetExam));
            localStorage.setItem("doran_seconds_elapsed", secondsElapsed);
        }

        // --- 5. VIEW PORTION CONTROL ---
        function switchTab(tabName) {
            currentTab = tabName;
            const tabs = ['mentor', 'study', 'resource', 'freeboard', 'planner', 'timer', 'incorrect', 'graph', 'compliment'];
            
            tabs.forEach(t => {
                const asideBtn = document.getElementById(`aside-${t}`);
                const mobEl = document.getElementById(`mobile-tab-${t}`);
                const contentSec = document.getElementById(`content-${t}`);

                if (t === tabName) {
                    if (asideBtn) asideBtn.className = "aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-bold transition text-amber-600 bg-amber-50";
                    if (mobEl) mobEl.className = "flex flex-col items-center shrink-0 space-y-1 text-amber-500";
                    if (contentSec) contentSec.classList.remove('hidden');
                } else {
                    if (asideBtn) asideBtn.className = "aside-btn w-full flex items-center space-x-3 px-4 py-2.5 rounded-xl text-left text-xs font-semibold transition text-slate-600 hover:bg-slate-50";
                    if (mobEl) mobEl.className = "flex flex-col items-center shrink-0 space-y-1 text-slate-400";
                    if (contentSec) contentSec.classList.add('hidden');
                }
            });

            updateFloatingTimerVisibility();
            renderAll();
        }

        function switchMentorSubTab(sub) {
            currentMentorSubTab = sub;
            const btnPosts = document.getElementById("subtab-m-posts");
            const btnProfiles = document.getElementById("subtab-m-profiles");
            const postsContainer = document.getElementById("mentor-posts-container");
            const profilesContainer = document.getElementById("mentor-profiles-container");

            if (sub === 'posts') {
                btnPosts.className = "text-xs font-bold px-3.5 py-1.5 rounded-lg bg-white shadow-sm text-slate-800";
                btnProfiles.className = "text-xs font-semibold px-3.5 py-1.5 rounded-lg text-slate-600 hover:text-slate-800";
                postsContainer.classList.remove("hidden");
                profilesContainer.classList.add("hidden");
            } else {
                btnProfiles.className = "text-xs font-bold px-3.5 py-1.5 rounded-lg bg-white shadow-sm text-slate-800";
                btnPosts.className = "text-xs font-semibold px-3.5 py-1.5 rounded-lg text-slate-600 hover:text-slate-800";
                profilesContainer.classList.remove("hidden");
                postsContainer.classList.add("hidden");
            }
            renderAll();
        }

        // --- 6. CORE UI RENDERING ---
        function updateUserInfoUI() {
            if (!currentUser) return;
            const exp = currentUser.exp || 0;
            const lvl = getLevelDetails(exp);

            document.getElementById("userBadgeIcon").innerText = lvl.level === 1 ? '🌱' : (lvl.level === 2 ? '📚' : (lvl.level === 3 ? '🚀' : '👑'));
            document.getElementById("userNameText").innerText = currentUser.name;
            document.getElementById("userLevelText").innerText = lvl.name;
            document.getElementById("userExpBar").innerText = `EXP ${lvl.current}/${lvl.maxExp}`;

            // Sidebar
            const sidebarIcon = document.getElementById("sidebarBadgeIcon");
            if (sidebarIcon) {
                sidebarIcon.innerText = lvl.level === 1 ? '🌱' : (lvl.level === 2 ? '📚' : (lvl.level === 3 ? '🚀' : '👑'));
            }
            document.getElementById("sidebarName").innerText = currentUser.name;
            document.getElementById("sidebarLevelBadge").innerText = lvl.name;
            document.getElementById("sidebarTargetMajor").innerText = currentUser.major;

            // Exp ratio calculation
            const expRange = lvl.maxExp - lvl.min + 1;
            const relativeExp = lvl.current - lvl.min;
            const ratio = lvl.level === 4 ? 100 : Math.round((relativeExp / expRange) * 100);
            
            document.getElementById("sidebarExpRatio").innerText = `${ratio}%`;
            document.getElementById("sidebarExpProgress").style.width = `${ratio}%`;

            // Greeting
            document.getElementById("greetingMessage").innerText = `오늘도 ${currentUser.name} 학우의 꿈(${currentUser.major})을 향해 달리자!`;

            // Profile Edit Modal setup
            document.getElementById("editUserName").value = currentUser.name;
            document.getElementById("editUserTargetMajor").value = currentUser.major;
            document.getElementById("editUserGrade").value = currentUser.grade + "학년";
            document.getElementById("editUserClassId").value = currentUser.classId;
            document.getElementById("editUserBio").value = currentUser.bio;
        }

        function calculateExamDday() {
            if (!targetExam || !targetExam.date) return;

            const targetDate = new Date(targetExam.date + "T00:00:00");
            const today = new Date();
            today.setHours(0,0,0,0);

            const diffTime = targetDate - today;
            const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));

            document.getElementById("examDdayTitle").innerText = targetExam.title;
            document.getElementById("examTargetDate").innerText = `시험 날짜: ${targetExam.date}`;

            const ddayLabel = document.getElementById("examDdayValue");
            if (diffDays === 0) {
                ddayLabel.innerText = "D-Day 🎉";
                ddayLabel.className = "text-4xl font-black mt-1 text-yellow-300 animate-bounce";
            } else if (diffDays > 0) {
                ddayLabel.innerText = `D-${diffDays}`;
                ddayLabel.className = "text-4xl font-black mt-1 text-white";
            } else {
                ddayLabel.innerText = `D+${Math.abs(diffDays)}`;
                ddayLabel.className = "text-4xl font-black mt-1 text-slate-300";
            }
        }

        function renderAll() {
            if (!currentUser) return;
            if (currentTab === 'mentor') {
                if (currentMentorSubTab === 'posts') renderMentorPosts();
                else renderMentorProfiles();
            }
            if (currentTab === 'study') renderStudies();
            if (currentTab === 'resource') renderResources();
            if (currentTab === 'freeboard') renderFreeBoard();
            if (currentTab === 'planner') renderPlanner();
            if (currentTab === 'timer') updateTimerDisplay();
            if (currentTab === 'incorrect') renderIncorrectNotes();
            if (currentTab === 'graph') renderGrowthGraph();
            if (currentTab === 'compliment') renderCompliments();
        }

        // --- STUDY TIMER CONTROLS ---
        function initTimerStatusOnLoad() {
            const wasRunning = localStorage.getItem("doran_timer_running") === "true";
            if (wasRunning) {
                const pauseTime = parseInt(localStorage.getItem("doran_timer_paused_at")) || Date.now();
                const now = Date.now();
                const offlineSecs = Math.floor((now - pauseTime) / 1000);
                secondsElapsed += offlineSecs;
                startTimer();
            }
            updateTimerDisplay();
            updateFloatingTimerVisibility();
        }

        function formatTime(totalSeconds) {
            const hrs = String(Math.floor(totalSeconds / 3600)).padStart(2, '0');
            const mins = String(Math.floor((totalSeconds % 3600) / 60)).padStart(2, '0');
            const secs = String(totalSeconds % 60).padStart(2, '0');
            return `${hrs}:${mins}:${secs}`;
        }

        function updateTimerDisplay() {
            const timeStr = formatTime(secondsElapsed);
            const timerText = document.getElementById("timerDisplay");
            const floatingText = document.getElementById("floatingTimeText");

            if (timerText) timerText.innerText = timeStr;
            if (floatingText) floatingText.innerText = timeStr;
        }

        function updateFloatingTimerVisibility() {
            const panel = document.getElementById("floatingTimer");
            if (timerRunning && currentTab !== 'timer') {
                panel.classList.remove("hidden");
            } else {
                panel.classList.add("hidden");
            }
        }

        function startTimer() {
            if (timerRunning) return;
            timerRunning = true;
            localStorage.setItem("doran_timer_running", "true");

            document.getElementById("btnTimerStart").disabled = true;
            document.getElementById("btnTimerPause").disabled = false;

            timerInterval = setInterval(() => {
                secondsElapsed++;
                updateTimerDisplay();
                saveToStorage();
            }, 1000);

            showToast("공부 시간 측정을 시작합니다. 열공하세요! 🔥", "info");
            updateFloatingTimerVisibility();
        }

        function pauseTimer() {
            if (!timerRunning) return;
            timerRunning = false;
            clearInterval(timerInterval);
            localStorage.setItem("doran_timer_running", "false");
            localStorage.setItem("doran_timer_paused_at", Date.now());

            document.getElementById("btnTimerStart").disabled = false;
            document.getElementById("btnTimerPause").disabled = true;

            if (secondsElapsed >= 3600) {
                const hourlyExp = Math.floor(secondsElapsed / 3600) * 3;
                addExperience(hourlyExp);
            }

            saveToStorage();
            showToast("타이머가 일시정지되었습니다.");
            updateFloatingTimerVisibility();
        }

        function resetTimer() {
            timerRunning = false;
            clearInterval(timerInterval);
            localStorage.setItem("doran_timer_running", "false");
            
            secondsElapsed = 0;
            saveToStorage();

            document.getElementById("btnTimerStart").disabled = false;
            document.getElementById("btnTimerPause").disabled = true;

            updateTimerDisplay();
            updateFloatingTimerVisibility();
            showToast("타이머가 초기화되었습니다.");
        }

        // --- AUTOMATIC INCORRECT NOTES & SIMULATOR ---
        function openIncorrectModal() {
            document.getElementById("incorrectRegModal").classList.remove("hidden");
            document.getElementById("incSubject").value = "";
            document.getElementById("incOriginal").value = "";
            document.getElementById("incMistake").value = "";
        }
        function closeIncorrectModal() {
            document.getElementById("incorrectRegModal").classList.add("hidden");
        }

        function generatePlausibleVariant(subject, originalQuestion) {
            const subjLower = subject.toLowerCase();
            const qLower = originalQuestion.toLowerCase();

            if (subjLower.includes("수학") || subjLower.includes("math")) {
                const numbers = originalQuestion.match(/\d+/g);
                if (numbers && numbers.length >= 2) {
                    const n1 = parseInt(numbers[0]) + 2;
                    const n2 = parseInt(numbers[1]) * 2;
                    return {
                        question: `[실력 극복 변형 문제] 첫째항이 ${n1}이고, 제 6항이 ${n2}인 새로운 등차수열의 공차를 구하시오.`,
                        answer: `정답: ${(n2 - n1)/5}`,
                        explanation: `a + 5d = ${n2} 식에 첫째항 ${n1}을 집어넣어 전개하면 5d = ${n2 - n1}이 되므로 d는 ${(n2 - n1)/5}가 도출됩니다.`
                    };
                }
                return {
                    question: "[변형] 아래 2차방정식 x^2 - 6x + 8 = 0 의 두 근의 합과 곱을 각각 연산하시오.",
                    answer: "정답: 합 6, 곱 8",
                    explanation: "근과 계수의 관계에 의하여 합은 -(-6)/1 = 6이며, 곱은 8/1 = 8입니다."
                };
            } else if (subjLower.includes("영어") || subjLower.includes("english")) {
                return {
                    question: "[변형 어휘 추론] 다음 문장 빈칸에 들어갈 가장 알맞은 어휘를 고르시오:\n'The scientific community suggests that climate change requires a _______ effort from all nations.'\n1) unilateral  2) collaborative  3) superficial  4) temporary",
                    answer: "정답: 2 (collaborative)",
                    explanation: "문맥상 기후 변화 해결을 위해 모든 국가의 '공동의, 협력적인(collaborative)' 노력이 요구되므로 2번이 적절합니다."
                }
            } else {
                return {
                    question: `[변형 기출] ${subject} 영역에서 다루어지는 핵심 개념 요소 중, 이전 시험 출제 메커니즘을 토대로 변형된 주관식 서술형 질문에 답하시오.`,
                    answer: "정답: 핵심 핵심 개념 요소의 유기적 매칭",
                    explanation: "시험 범위의 핵심 단어를 유기적으로 결합하여 암기하는 것이 오답을 방지하는 필수 비결입니다."
                }
            }
        }

        function submitIncorrect() {
            const subject = document.getElementById("incSubject").value.trim();
            const original = document.getElementById("incOriginal").value.trim();
            const mistake = document.getElementById("incMistake").value.trim();

            if (!subject || !original || !mistake) {
                showToast("모든 항목을 올바르게 채워주세요.", "error");
                return;
            }

            const sim = generatePlausibleVariant(subject, original);

            incorrectNotes.unshift({
                id: "inc-" + Date.now(),
                subject: subject,
                originalQuestion: original,
                mistakeReason: mistake,
                generatedQuestion: sim.question,
                generatedAnswer: sim.answer,
                generatedExplanation: sim.explanation,
                resolved: false
            });

            addExperience(4);

            saveToStorage();
            closeIncorrectModal();
            renderIncorrectNotes();
            showToast("유사 변형 문항이 성공적으로 오답노트에 생성되었습니다!");
        }

        function renderIncorrectNotes() {
            const container = document.getElementById("incorrectList");
            if (incorrectNotes.length === 0) {
                container.innerHTML = `
                    <div class="bg-white p-12 rounded-2xl border border-slate-100 text-center flex flex-col items-center justify-center">
                        <div class="w-16 h-16 bg-indigo-50 text-indigo-400 rounded-full flex items-center justify-center text-2xl mb-3">
                            <i class="fa-solid fa-book-open"></i>
                        </div>
                        <p class="text-sm font-bold text-slate-700">오답노트가 비어있습니다.</p>
                        <p class="text-xs text-slate-400 mt-1">상단의 등록하기 단추를 눌러 AI 기반 극복 훈련을 수행해 보세요!</p>
                    </div>
                `;
                return;
            }

            container.innerHTML = incorrectNotes.map(item => {
                return `
                    <div class="bg-white border ${item.resolved ? 'border-emerald-200 bg-emerald-50/10' : 'border-slate-150'} rounded-2xl p-5 space-y-4">
                        <div class="flex items-center justify-between">
                            <span class="bg-indigo-100 text-indigo-800 text-[10px] font-bold px-2 py-0.5 rounded-md">${item.subject}</span>
                            <div class="flex items-center space-x-2">
                                <span class="text-xs ${item.resolved ? 'text-emerald-600 font-bold' : 'text-amber-500 font-bold'}">
                                    ${item.resolved ? '<i class="fa-solid fa-square-check"></i> 해결완료' : '🔴 훈련 대기중'}
                                </span>
                                <button onclick="deleteIncorrect('${item.id}')" class="text-slate-400 hover:text-rose-500 text-xs"><i class="fa-solid fa-trash-can"></i></button>
                            </div>
                        </div>

                        <div class="space-y-1 bg-slate-50 p-3 rounded-xl border border-slate-100">
                            <span class="text-[10px] text-rose-500 font-black">원래 틀린 문제:</span>
                            <p class="text-xs text-slate-700 font-medium">${item.originalQuestion}</p>
                            <span class="text-[9px] text-slate-400 block mt-1">⚠️ 내 실수 원인: ${item.mistakeReason}</span>
                        </div>

                        <div class="border-2 border-dashed border-indigo-200 bg-indigo-50/20 p-4 rounded-xl space-y-3">
                            <span class="text-[10px] bg-indigo-600 text-white px-2 py-0.5 rounded font-bold">🤖 자동 유사 변형 문제</span>
                            <p class="text-xs text-slate-800 font-bold whitespace-pre-line">${item.generatedQuestion}</p>
                            
                            <div id="solverArea-${item.id}" class="space-y-2">
                                <button onclick="revealIncorrectAnswer('${item.id}')" class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-[10px] px-3.5 py-1.5 rounded-lg transition shadow-sm">
                                    해설 및 모범 답안 보기
                                </button>
                                
                                <div id="answerSheet-${item.id}" class="hidden space-y-2 bg-white border border-indigo-100 p-3 rounded-lg text-xs animate-fade-in">
                                    <strong class="text-emerald-600">${item.generatedAnswer}</strong>
                                    <p class="text-slate-600 text-[11px] leading-relaxed">${item.generatedExplanation}</p>
                                    
                                    ${!item.resolved ? `
                                        <button onclick="resolveIncorrect('${item.id}')" class="w-full py-1.5 bg-emerald-500 hover:bg-emerald-600 text-white font-bold rounded-lg text-[10px] transition mt-2">
                                            정답을 완벽히 이해했습니다 (해결 처리)
                                        </button>
                                    ` : ''}
                                </div>
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }

        function revealIncorrectAnswer(id) {
            const el = document.getElementById(`answerSheet-${id}`);
            el.classList.toggle("hidden");
        }

        function resolveIncorrect(id) {
            const item = incorrectNotes.find(i => i.id === id);
            if (item) {
                item.resolved = true;
                addExperience(6); 
                saveToStorage();
                renderIncorrectNotes();
            }
        }

        function deleteIncorrect(id) {
            incorrectNotes = incorrectNotes.filter(i => i.id !== id);
            saveToStorage();
            renderIncorrectNotes();
        }

        // --- STUDY PLANNERS ---
        function renderPlanner() {
            const list = document.getElementById("plannerTaskList");
            if (plannerTasks.length === 0) {
                list.innerHTML = `<p class="text-xs text-slate-400 py-6 text-center">오늘 등록한 학습 계획 목표가 없습니다.</p>`;
                updatePlannerProgress(0);
                return;
            }

            list.innerHTML = plannerTasks.map(item => {
                const checkedClass = item.completed ? 'line-through text-slate-400' : 'text-slate-700 font-medium';
                const checkedIcon = item.completed ? '<i class="fa-solid fa-circle-check text-indigo-600 text-base"></i>' : '<i class="fa-regular fa-circle text-slate-300 text-base"></i>';

                return `
                    <div class="flex items-center justify-between p-3 bg-slate-50 rounded-xl hover:bg-slate-100/70 transition">
                        <button onclick="toggleTask('${item.id}')" class="flex items-center space-x-3 text-left">
                            <span>${checkedIcon}</span>
                            <span class="text-xs ${checkedClass}">${item.task}</span>
                        </button>
                        <button onclick="deleteTask('${item.id}')" class="text-slate-400 hover:text-rose-500 text-xs p-1"><i class="fa-solid fa-trash-can"></i></button>
                    </div>
                `;
            }).join('');

            const completedCount = plannerTasks.filter(t => t.completed).length;
            const percent = Math.round((completedCount / plannerTasks.length) * 100) || 0;
            updatePlannerProgress(percent);
        }

        function updatePlannerProgress(percent) {
            document.getElementById("plannerProgressText").innerText = `${percent}% 완료`;
            document.getElementById("plannerProgressBar").style.width = `${percent}%`;
        }

        function addPlannerTask() {
            const input = document.getElementById("plannerTaskInput");
            const text = input.value.trim();

            if (!text) return;

            plannerTasks.push({
                id: "t-" + Date.now(),
                task: text,
                completed: false
            });

            addExperience(1);
            saveToStorage();
            input.value = "";
            renderPlanner();
        }

        function toggleTask(id) {
            const task = plannerTasks.find(t => t.id === id);
            if (!task) return;
            task.completed = !task.completed;
            if (task.completed) {
                addExperience(2); 
            }
            saveToStorage();
            renderPlanner();
        }

        function deleteTask(id) {
            plannerTasks = plannerTasks.filter(t => t.id !== id);
            saveToStorage();
            renderPlanner();
        }

        // --- ATTENDANCE SYSTEM ---
        function updateAttendanceUI() {
            if (!currentUser) return;
            document.getElementById("totalAttendanceText").innerText = currentUser.totalAttendance || 0;
            document.getElementById("todayAttendanceCount").innerText = `(${attendances.list.length}명)`;

            const container = document.getElementById("todayAttendanceList");
            const noMsg = document.getElementById("noAttendanceMsg");

            if (attendances.list.length === 0) {
                noMsg.classList.remove("hidden");
                container.innerHTML = "";
            } else {
                noMsg.classList.add("hidden");
                container.innerHTML = attendances.list.map(u => {
                    const gradeColor = u.grade === '1' ? 'bg-emerald-50 text-emerald-700' : (u.grade === '2' ? 'bg-sky-50 text-sky-700' : 'bg-purple-50 text-purple-700');
                    return `
                        <span class="${gradeColor} text-[10px] font-bold px-2 py-0.5 rounded-full border border-slate-100 flex items-center space-x-1 shadow-sm animate-fade-in">
                            <span>📍</span><span>${u.name}</span><span class="text-[8px] font-normal opacity-75">${u.time}</span>
                        </span>
                    `;
                }).join('');
            }

            const hasCheckedIn = attendances.list.some(u => u.name === currentUser.name);
            const btn = document.getElementById("btnAttendanceQuick");
            if (hasCheckedIn) {
                btn.innerHTML = `<i class="fa-solid fa-circle-check text-emerald-500 mr-1"></i>출석완료`;
                btn.disabled = true;
                btn.className = "bg-emerald-50 text-emerald-700 font-bold text-xs px-3.5 py-1.5 rounded-xl cursor-default border border-emerald-100 shadow-none";
            } else {
                btn.innerHTML = `<i class="fa-solid fa-stamp mr-1"></i>출석하기`;
                btn.disabled = false;
                btn.className = "bg-white text-amber-600 hover:bg-amber-50 font-bold text-xs px-3.5 py-1.5 rounded-xl shadow-sm transition";
            }
        }

        function doAttendance() {
            const alreadyChecked = attendances.list.some(u => u.name === currentUser.name);
            if (alreadyChecked) return;

            const timeStr = new Date().toTimeString().slice(0, 5);
            attendances.list.push({
                name: currentUser.name,
                grade: currentUser.grade,
                time: timeStr
            });

            currentUser.totalAttendance = (currentUser.totalAttendance || 0) + 1;
            currentUser.lastAttendanceDate = todayStr;

            addExperience(2); 
            saveToStorage();
            updateAttendanceUI();
            showToast("오늘 등교 출석 도장을 찍었습니다!");
        }

        // --- SUBMIT EXAM DDAY CONTROLS ---
        function openExamModal() {
            document.getElementById("examModal").classList.remove("hidden");
            document.getElementById("inputExamName").value = targetExam.title;
            document.getElementById("inputExamDate").value = targetExam.date;
        }
        function closeExamModal() {
            document.getElementById("examModal").classList.add("hidden");
        }
        function saveExamDday() {
            const title = document.getElementById("inputExamName").value.trim();
            const dateStr = document.getElementById("inputExamDate").value;

            if (!title || !dateStr) {
                showToast("시험 일정 이름과 날짜를 채워주세요.", "error");
                return;
            }

            targetExam.title = title;
            targetExam.date = dateStr;

            saveToStorage();
            calculateExamDday();
            closeExamModal();
            showToast("목표 시험 D-Day 일정이 변경 저장되었습니다.");
        }

        // --- MENTORING SECTIONS ---
        function renderMentorPosts() {
            const listContainer = document.getElementById("mentor-posts-container");
            const data = getFilteredData(mentors);

            if (data.length === 0) {
                listContainer.innerHTML = `<div class="col-span-full py-12 text-center text-slate-400 text-xs">매칭 구인 게시글이 존재하지 않습니다.</div>`;
                return;
            }

            listContainer.innerHTML = data.map(item => {
                const isMentor = item.role === 'mentor';
                const hasApplied = item.subscribers.includes(currentUser.name);
                const roleBadge = isMentor 
                    ? `<span class="bg-indigo-50 text-indigo-700 text-[10px] px-2 py-0.5 rounded-md font-bold border border-indigo-100"><i class="fa-solid fa-crown mr-1"></i>멘토 구함</span>` 
                    : `<span class="bg-amber-50 text-amber-700 text-[10px] px-2 py-0.5 rounded-md font-bold border border-amber-100"><i class="fa-solid fa-circle-nodes mr-1"></i>멘티 구함</span>`;
                
                const gradeBadgeColor = item.grade === '1' ? 'bg-emerald-50 text-emerald-700' : (item.grade === '2' ? 'bg-sky-50 text-sky-700' : 'bg-purple-50 text-purple-700');
                
                const hasLiked = item.likedBy && item.likedBy.includes(currentUser.name);
                const likesCount = item.likedBy ? item.likedBy.length : 0;
                const heartIcon = hasLiked 
                    ? `<i class="fa-solid fa-heart text-rose-500 scale-110 transition duration-150"></i>` 
                    : `<i class="fa-regular fa-heart text-slate-400 hover:text-rose-500 transition duration-150"></i>`;

                return `
                    <div class="bg-white border border-slate-100 hover:border-amber-200 hover:shadow-md transition duration-200 p-5 rounded-2xl flex flex-col justify-between">
                        <div>
                            <div class="flex items-center justify-between mb-3">
                                <div class="flex items-center space-x-2">
                                    ${roleBadge}
                                    <span class="${gradeBadgeColor} text-[10px] px-2 py-0.5 rounded-md font-bold">${item.grade}학년</span>
                                </div>
                                <span class="text-[10px] text-slate-400 font-medium">${item.date}</span>
                            </div>
                            <h4 class="text-base font-bold text-slate-900 mb-1">${item.subject}</h4>
                            <p class="text-xs text-slate-500 font-semibold mb-3"><i class="fa-solid fa-user-check text-emerald-500 text-[10px]"></i> 실명: ${item.author}</p>
                            <p class="text-xs text-slate-600 leading-relaxed bg-slate-50 p-3 rounded-xl mb-4 whitespace-pre-line min-h-[60px]">${item.detail}</p>
                        </div>
                        <div class="flex items-center justify-between pt-3 border-t border-slate-100">
                            <button onclick="likeMentor('${item.id}')" class="flex items-center space-x-1.5 text-slate-500 hover:text-rose-500 transition">
                                ${heartIcon}
                                <span class="text-xs font-semibold text-slate-600">${likesCount}</span>
                            </button>
                            <div class="flex items-center space-x-2">
                                ${item.author === currentUser.name ? 
                                    `<button onclick="deleteMentor('${item.id}')" class="text-slate-400 hover:text-rose-500 text-xs"><i class="fa-solid fa-trash-can"></i> 삭제</button>` : 
                                    `<button onclick="applyMentor('${item.id}')" class="text-xs font-bold px-3 py-1.5 rounded-lg transition ${
                                        hasApplied ? 'bg-emerald-100 text-emerald-700' : 'bg-amber-500 hover:bg-amber-600 text-white'
                                    }">${hasApplied ? '신청완료' : '매칭신청'}</button>`
                                }
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }

        function renderMentorProfiles() {
            const container = document.getElementById("mentor-profiles-container");
            const data = getFilteredData(mentorProfiles);

            if (data.length === 0) {
                container.innerHTML = `<div class="col-span-full py-12 text-center text-slate-400 text-xs">등록된 정식 멘토 프로필이 없습니다.</div>`;
                return;
            }

            container.innerHTML = data.map(profile => {
                const gradeText = `${profile.grade}학년`;
                const certsList = profile.certificates.split(',').map(c => c.trim()).filter(Boolean);

                return `
                    <div class="bg-white border border-slate-100 hover:border-indigo-100 hover:shadow-md transition p-5 rounded-2xl space-y-3 relative overflow-hidden">
                        <div class="absolute right-0 top-0 bg-indigo-600 text-white text-[9px] font-bold px-3 py-1 rounded-bl-xl shadow-sm">
                            공부 멘토
                        </div>
                        <div class="flex items-center space-x-3">
                            <div class="w-10 h-10 rounded-xl bg-indigo-50 flex items-center justify-center text-indigo-600 text-lg font-bold">
                                ${profile.name.charAt(0)}
                            </div>
                            <div>
                                <h4 class="text-sm font-bold text-slate-900">${profile.name} <span class="text-[10px] text-slate-400 font-semibold">(${profile.major})</span></h4>
                                <span class="bg-indigo-50 text-indigo-800 text-[9px] font-bold px-1.5 py-0.5 rounded border border-indigo-100">${gradeText}</span>
                            </div>
                        </div>
                        
                        <div class="space-y-1.5 text-xs">
                            <p class="text-slate-500"><strong class="text-slate-800"><i class="fa-solid fa-star text-amber-500 mr-1"></i>가르칠 수 있는 분야:</strong> ${profile.specialty}</p>
                            
                            <div class="flex flex-wrap gap-1 items-center">
                                <strong class="text-slate-800 text-[11px] shrink-0"><i class="fa-solid fa-certificate text-indigo-500 mr-1"></i>특기/실적:</strong>
                                ${certsList.length > 0 ? certsList.map(c => `<span class="bg-slate-100 text-slate-600 text-[9px] font-bold px-2 py-0.5 rounded-full">${c}</span>`).join('') : '<span class="text-slate-400 text-[10px]">미기입</span>'}
                            </div>
                        </div>

                        <p class="text-xs text-slate-600 bg-slate-50 p-3 rounded-xl whitespace-pre-line">${profile.intro}</p>
                    </div>
                `;
            }).join('');
        }

        // --- STUDY GROUP ---
        function renderStudies() {
            const listContainer = document.getElementById("studyList");
            const data = getFilteredData(studies);

            if (data.length === 0) {
                listContainer.innerHTML = `<div class="col-span-full py-12 text-center text-slate-400 text-xs">개설된 스터디방이 없습니다.</div>`;
                return;
            }

            listContainer.innerHTML = data.map(item => {
                const isMember = item.members.includes(currentUser.name);
                const isFull = item.members.length >= item.maxMembers;
                const progressPercent = Math.min(100, (item.members.length / item.maxMembers) * 100);

                return `
                    <div class="bg-white border border-slate-100 p-5 rounded-2xl flex flex-col justify-between animate-fade-in">
                        <div>
                            <div class="flex items-center justify-between mb-3">
                                <span class="bg-orange-50 text-orange-700 text-[10px] px-2 py-0.5 rounded-md font-bold">${item.topic}</span>
                                <span class="text-xs font-semibold text-slate-400">${item.cycle}</span>
                            </div>
                            <h4 class="text-base font-bold text-slate-900 mb-1">${item.title}</h4>
                            <p class="text-xs text-slate-400 mb-3 font-semibold">스터디장: ${item.author}</p>
                            <p class="text-xs text-slate-600 leading-relaxed bg-slate-50 p-3 rounded-xl mb-4 whitespace-pre-line">${item.detail}</p>
                        </div>
                        <div>
                            <div class="mb-3">
                                <div class="flex justify-between items-center text-xs mb-1">
                                    <span class="text-slate-500 font-semibold">진척도</span>
                                    <span class="text-orange-600 font-bold">${item.members.length} / ${item.maxMembers}명</span>
                                </div>
                                <div class="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                                    <div class="bg-orange-500 h-full rounded-full" style="width: ${progressPercent}%"></div>
                                </div>
                            </div>
                            <div class="flex items-center justify-between pt-2 border-t border-slate-100">
                                <span class="text-[10px] text-slate-400">참여자: ${item.members.join(', ')}</span>
                                <div class="flex space-x-1">
                                    ${item.author === currentUser.name ? 
                                        `<button onclick="deleteStudy('${item.id}')" class="text-rose-500 text-xs p-1">삭제</button>` :
                                        `<button onclick="toggleStudyJoin('${item.id}')" class="text-xs font-bold px-3 py-1 rounded-lg ${
                                            isMember ? 'bg-rose-50 text-rose-600' : 'bg-orange-500 hover:bg-orange-600 text-white'
                                        }">${isMember ? '탈퇴' : '참여'}</button>`
                                    }
                                </div>
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }

        // --- STUDY RESOURCES ---
        function renderResources() {
            const listContainer = document.getElementById("resourceList");
            const data = getFilteredData(resources);

            if (data.length === 0) {
                listContainer.innerHTML = `<div class="py-12 text-center text-slate-400 text-xs">자료방이 비어있습니다.</div>`;
                return;
            }

            listContainer.innerHTML = data.map(item => {
                const hasLiked = item.likedBy && item.likedBy.includes(currentUser.name);
                const likesCount = item.likedBy ? item.likedBy.length : 0;
                const heartIcon = hasLiked 
                    ? `<i class="fa-solid fa-heart text-rose-500 scale-110"></i>` 
                    : `<i class="fa-regular fa-heart text-slate-400 hover:text-rose-500"></i>`;

                return `
                    <div class="bg-white border border-slate-100 rounded-2xl p-4 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3 animate-fade-in">
                        <div class="space-y-1">
                            <div class="flex items-center space-x-2">
                                <span class="bg-emerald-50 text-emerald-700 text-[9px] font-bold px-2 py-0.5 rounded">${item.category}</span>
                                <span class="text-[10px] text-slate-400">${item.date}</span>
                            </div>
                            <h4 class="text-sm font-bold text-slate-900 flex items-center gap-1.5">
                                <i class="fa-solid fa-file-pdf text-rose-500 text-base"></i>
                                <span>${item.title}</span>
                            </h4>
                            <p class="text-xs text-slate-600">${item.detail}</p>
                            <span class="text-[10px] text-slate-400 block">제공자: ${item.author} | 다운로드: ${item.downloads}회</span>
                        </div>
                        <div class="flex items-center space-x-2 w-full sm:w-auto justify-end">
                            <a href="${item.link}" target="_blank" onclick="incrementDownload('${item.id}')" class="bg-emerald-500 hover:bg-emerald-600 text-white text-xs font-bold px-4 py-2 rounded-xl transition">자료 보기</a>
                            
                            <button onclick="likeResource('${item.id}')" class="bg-slate-50 p-2 rounded-lg text-slate-500 hover:text-rose-500 text-xs flex items-center space-x-1 transition">
                                ${heartIcon}
                                <span>${likesCount}</span>
                            </button>
                            ${item.author === currentUser.name ? `<button onclick="deleteResource('${item.id}')" class="text-slate-400 text-xs hover:text-rose-500">삭제</button>` : ''}
                        </div>
                    </div>
                `;
            }).join('');
        }

        // --- FREE BOARD ---
        function renderFreeBoard() {
            const listContainer = document.getElementById("freeBoardList");
            const data = getFilteredData(freePosts);

            if (data.length === 0) {
                listContainer.innerHTML = `<div class="py-12 text-center text-slate-400 text-xs">첫 게시글을 써보세요!</div>`;
                return;
            }

            listContainer.innerHTML = data.map(item => {
                const commentCount = item.comments ? item.comments.length : 0;
                
                const hasLiked = item.likedBy && item.likedBy.includes(currentUser.name);
                const likesCount = item.likedBy ? item.likedBy.length : 0;
                const heartIcon = hasLiked 
                    ? `<i class="fa-solid fa-heart text-rose-500 scale-110"></i>` 
                    : `<i class="fa-regular fa-heart text-slate-400 hover:text-rose-500"></i>`;

                return `
                    <div class="bg-white border border-slate-100 hover:border-sky-100 hover:shadow-sm rounded-2xl p-5 space-y-3 transition duration-150 animate-fade-in">
                        <div class="flex justify-between items-center text-[10px] text-slate-400">
                            <span class="font-bold text-slate-700">${item.author} (${item.grade}학년)</span>
                            <span>${item.date}</span>
                        </div>
                        <h4 class="text-sm font-bold text-slate-900 leading-snug">${item.title}</h4>
                        <p class="text-xs text-slate-600 whitespace-pre-line line-clamp-3">${item.content}</p>

                        <div class="flex items-center justify-between pt-2 border-t border-slate-50">
                            <button onclick="likeFreePost('${item.id}')" class="flex items-center space-x-1 text-slate-500 hover:text-rose-500 transition text-xs font-bold">
                                ${heartIcon}
                                <span>공감 ${likesCount}</span>
                            </button>
                            <div class="flex space-x-2">
                                <button onclick="openFreeDetail('${item.id}')" class="text-xs bg-sky-50 text-sky-700 px-3.5 py-1.5 rounded-lg font-bold hover:bg-sky-100 transition">
                                    댓글 (${commentCount})
                                </button>
                                ${item.author === currentUser.name ? `<button onclick="deleteFreePost('${item.id}')" class="text-xs text-slate-400 hover:text-rose-500 px-1">삭제</button>` : ''}
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }

        function openFreeDetail(id) {
            const post = freePosts.find(f => f.id === id);
            if (!post) return;

            activePostIdForComment = id;
            document.getElementById("detailPostGrade").innerText = `${post.grade}학년`;
            document.getElementById("detailPostTitle").innerText = post.title;
            document.getElementById("detailPostAuthor").innerText = post.author;
            document.getElementById("detailPostDate").innerText = post.date;
            document.getElementById("detailPostContent").innerText = post.content;

            renderComments(post);
            document.getElementById("freeDetailModal").classList.remove("hidden");
        }

        function renderComments(post) {
            const list = document.getElementById("detailCommentsList");
            if (!post.comments || post.comments.length === 0) {
                list.innerHTML = `<p class="text-[10px] text-slate-400 py-4 text-center">댓글이 없습니다.</p>`;
                return;
            }

            list.innerHTML = post.comments.map(c => `
                <div class="bg-slate-50 p-2.5 rounded-xl text-xs space-y-1 animate-fade-in">
                    <div class="flex justify-between items-center text-[9px] text-slate-400">
                        <span class="font-bold text-slate-700">${c.author} (${c.grade || '2'}학년)</span>
                    </div>
                    <p class="text-slate-600 leading-normal">${c.text}</p>
                </div>
            `).join('');
        }

        function submitComment() {
            if (!activePostIdForComment) return;
            const input = document.getElementById("commentInput");
            const text = input.value.trim();

            if (!text) return;

            const textLower = text.toLowerCase();
            const containsBanned = bannedWords.some(word => textLower.includes(word));
            if (containsBanned) {
                showToast("비속어가 감지되었습니다. 아름다운 단어들을 사용해 보아요.", "error");
                return;
            }

            const post = freePosts.find(f => f.id === activePostIdForComment);
            if (!post) return;

            if (!post.comments) post.comments = [];
            post.comments.push({
                author: currentUser.name,
                grade: currentUser.grade,
                text: text
            });

            addExperience(1);
            saveToStorage();
            input.value = "";
            renderComments(post);
            renderFreeBoard();
            showToast("선행 댓글이 저장되었습니다.");
        }

        function closeFreeDetailModal() {
            document.getElementById("freeDetailModal").classList.add("hidden");
            activePostIdForComment = null;
        }

        // --- GROWTH GRAPH ENGINE (GRADIENT SVGCURVE) ---
        function renderGrowthGraph() {
            const svg = document.getElementById("growthGraphSvg");
            const list = document.getElementById("scoreLabelsList");

            if (growthScores.length === 0) {
                svg.innerHTML = `<text x="50%" y="50%" dominant-baseline="middle" text-anchor="middle" font-size="11" fill="#94a3b8">아직 등록된 성적이 없습니다.</text>`;
                list.innerHTML = `<p class="text-xs text-slate-400 py-3">학기 성적 평균을 추가해 보세요!</p>`;
                return;
            }

            list.innerHTML = growthScores.map((s, idx) => `
                <div class="bg-emerald-50 text-emerald-800 text-[10px] font-bold px-2 py-1 rounded-lg border border-emerald-100 flex items-center space-x-1 animate-fade-in">
                    <span>${s.term}: <strong>${s.score}점</strong></span>
                    <button onclick="deleteScore(${idx})" class="text-rose-500 hover:text-rose-700 ml-1">×</button>
                </div>
            `).join('');

            const svgWidth = 500;
            const svgHeight = 150;
            const paddingX = 40;
            const paddingY = 20;

            const chartWidth = svgWidth - 2 * paddingX;
            const chartHeight = svgHeight - 2 * paddingY;

            let innerHTML = '';

            const guideY = [100, 75, 50, 25, 0];
            guideY.forEach(scoreVal => {
                const ratio = scoreVal / 100;
                const y = paddingY + chartHeight - (ratio * chartHeight);
                innerHTML += `
                    <line x1="${paddingX}" y1="${y}" x2="${svgWidth - paddingX}" y2="${y}" stroke="#f1f5f9" stroke-width="1" />
                    <text x="${paddingX - 10}" y="${y + 3}" font-size="8" fill="#94a3b8" text-anchor="end">${scoreVal}</text>
                `;
            });

            const points = growthScores.map((s, i) => {
                const ratioX = growthScores.length > 1 ? (i / (growthScores.length - 1)) : 0.5;
                const ratioY = s.score / 100;

                const x = paddingX + (ratioX * chartWidth);
                const y = paddingY + chartHeight - (ratioY * chartHeight);
                return { x, y, score: s.score, label: s.term };
            });

            if (points.length > 0) {
                let pathD = '';
                let areaD = `M ${points[0].x} ${svgHeight - paddingY}`;

                if (points.length === 1) {
                    pathD = `M ${points[0].x} ${points[0].y}`;
                    areaD += ` L ${points[0].x} ${points[0].y} L ${points[0].x} ${svgHeight - paddingY}`;
                } else {
                    pathD = `M ${points[0].x} ${points[0].y}`;
                    for (let i = 0; i < points.length - 1; i++) {
                        const p0 = points[i];
                        const p1 = points[i + 1];
                        const cpX1 = p0.x + (p1.x - p0.x) / 3;
                        const cpY1 = p0.y;
                        const cpX2 = p0.x + 2 * (p1.x - p0.x) / 3;
                        const cpY2 = p1.y;

                        pathD += ` C ${cpX1} ${cpY1}, ${cpX2} ${cpY2}, ${p1.x} ${p1.y}`;
                    }

                    for (let i = 0; i < points.length - 1; i++) {
                        const p0 = points[i];
                        const p1 = points[i + 1];
                        const cpX1 = p0.x + (p1.x - p0.x) / 3;
                        const cpY1 = p0.y;
                        const cpX2 = p0.x + 2 * (p1.x - p0.x) / 3;
                        const cpY2 = p1.y;
                        areaD += ` C ${cpX1} ${cpY1}, ${cpX2} ${cpY2}, ${p1.x} ${p1.y}`;
                    }
                    areaD += ` L ${points[points.length - 1].x} ${svgHeight - paddingY} Z`;
                }

                innerHTML += `
                    <defs>
                        <linearGradient id="curveGradient" x1="0" y1="0" x2="0" y2="1">
                            <stop offset="0%" stop-color="#10b981" stop-opacity="0.3" />
                            <stop offset="100%" stop-color="#10b981" stop-opacity="0.0" />
                        </linearGradient>
                    </defs>
                    <path d="${areaD}" fill="url(#curveGradient)" />
                    <path d="${pathD}" fill="none" stroke="#10b981" stroke-width="2.5" stroke-linecap="round" />
                `;

                points.forEach(p => {
                    innerHTML += `
                        <circle cx="${p.x}" cy="${p.y}" r="4" fill="#ffffff" stroke="#10b981" stroke-width="2" />
                        <text x="${p.x}" y="${p.y - 8}" font-size="8" font-weight="bold" fill="#047857" text-anchor="middle">${p.score}점</text>
                        <text x="${p.x}" y="${svgHeight - paddingY + 12}" font-size="8" fill="#64748b" text-anchor="middle">${p.label}</text>
                    `;
                });
            }

            svg.innerHTML = innerHTML;
        }

        function addScoreData() {
            const term = document.getElementById("scoreTerm").value.trim();
            const val = parseInt(document.getElementById("scoreNum").value);

            if (!term || isNaN(val) || val < 0 || val > 100) {
                showToast("올바른 성적과 차수를 입력해주세요.", "error");
                return;
            }

            growthScores.push({ term: term, score: val });
            addExperience(3);
            saveToStorage();
            
            document.getElementById("scoreTerm").value = "";
            document.getElementById("scoreNum").value = "";
            renderGrowthGraph();
            showToast("성적 차트 데이터가 갱신되었습니다.");
        }

        function deleteScore(idx) {
            growthScores.splice(idx, 1);
            saveToStorage();
            renderGrowthGraph();
        }

        function resetScores() {
            growthScores = [];
            saveToStorage();
            renderGrowthGraph();
        }

        // --- COMPLIMENTS ---
        function renderCompliments() {
            const listContainer = document.getElementById("complimentList");
            const data = getFilteredData(compliments);

            if (data.length === 0) {
                listContainer.innerHTML = `<p class="text-xs text-slate-400 py-6 text-center">우편함에 편지가 존재하지 않습니다.</p>`;
                return;
            }

            listContainer.innerHTML = data.map(item => {
                const targetText = item.targetGrade === 'all' ? '전체 학우에게' : `${item.targetGrade}학년 학우에게`;
                
                const hasLiked = item.likedBy && item.likedBy.includes(currentUser.name);
                const likesCount = item.likedBy ? item.likedBy.length : 0;
                const heartIcon = hasLiked 
                    ? `<i class="fa-solid fa-heart text-rose-500 scale-110"></i>` 
                    : `<i class="fa-regular fa-heart text-slate-400 hover:text-rose-500"></i>`;

                return `
                    <div class="bg-white border border-rose-50 rounded-xl p-4 shadow-sm space-y-2 relative animate-fade-in">
                        <div class="flex items-center justify-between text-[10px] text-slate-400">
                            <span class="bg-rose-50 text-rose-700 font-bold px-2 py-0.5 rounded-full">${targetText}</span>
                            <span>${item.date}</span>
                        </div>
                        <p class="text-xs text-slate-700 leading-relaxed whitespace-pre-line">${item.text}</p>
                        <div class="flex justify-end pt-1 border-t border-slate-50">
                            <button onclick="likeCompliment('${item.id}')" class="text-slate-400 hover:text-rose-500 text-[10px] font-semibold flex items-center space-x-1 transition">
                                ${heartIcon}
                                <span>공감 ${likesCount}</span>
                            </button>
                        </div>
                    </div>
                `;
            }).join('');
        }

        function submitCompliment() {
            const target = document.getElementById("complimentTargetGrade").value;
            const text = document.getElementById("complimentText").value.trim();

            if (!text) return;

            const textLower = text.toLowerCase();
            const containsBanned = bannedWords.some(word => textLower.includes(word));
            if (containsBanned) {
                showToast("욕설 및 부적절 표현 감지로 발송할 수 없습니다.", "error");
                return;
            }

            compliments.unshift({
                id: "c-" + Date.now(),
                targetGrade: target,
                text: text,
                likedBy: [],
                date: new Date().toISOString().slice(0, 10).replace(/-/g, '.')
            });

            addExperience(2);
            saveToStorage();
            
            document.getElementById("complimentText").value = "";
            renderCompliments();
            showToast("익명의 칭찬 엽서가 발송되었습니다. 📮");
        }

        // --- UNIQUE TOGGLABLE LIKING LOGIC (NO EXP GAIN) ---
        function likeMentor(id) {
            const item = mentors.find(m => m.id === id);
            if (!item) return;
            if (!item.likedBy) item.likedBy = [];

            const userIndex = item.likedBy.indexOf(currentUser.name);
            if (userIndex !== -1) {
                item.likedBy.splice(userIndex, 1);
                showToast("구인글 공감을 취소했습니다.", "info");
            } else {
                item.likedBy.push(currentUser.name);
                // Experience addition removed completely from liking actions!
                showToast("구인글에 공감했습니다! ❤️");
            }
            saveToStorage();
            renderMentorPosts();
        }

        function likeResource(id) {
            const item = resources.find(r => r.id === id);
            if (!item) return;
            if (!item.likedBy) item.likedBy = [];

            const userIndex = item.likedBy.indexOf(currentUser.name);
            if (userIndex !== -1) {
                item.likedBy.splice(userIndex, 1);
                showToast("학습 자료 공감을 취소했습니다.", "info");
            } else {
                item.likedBy.push(currentUser.name);
                // Experience addition removed completely from liking actions!
                showToast("자료가 유익하셨군요! 공감이 반영되었습니다. ❤️");
            }
            saveToStorage();
            renderResources();
        }

        function likeFreePost(id) {
            const item = freePosts.find(f => f.id === id);
            if (!item) return;
            if (!item.likedBy) item.likedBy = [];

            const userIndex = item.likedBy.indexOf(currentUser.name);
            if (userIndex !== -1) {
                item.likedBy.splice(userIndex, 1);
                showToast("게시글 공감을 취소했습니다.", "info");
            } else {
                item.likedBy.push(currentUser.name);
                // Experience addition removed completely from liking actions!
                showToast("게시글에 공감했습니다! ❤️");
            }
            saveToStorage();
            renderFreeBoard();
        }

        function likeCompliment(id) {
            const item = compliments.find(c => c.id === id);
            if (!item) return;
            if (!item.likedBy) item.likedBy = [];

            const userIndex = item.likedBy.indexOf(currentUser.name);
            if (userIndex !== -1) {
                item.likedBy.splice(userIndex, 1);
                showToast("엽서 공감을 취소했습니다.", "info");
            } else {
                item.likedBy.push(currentUser.name);
                // Experience addition removed completely from liking actions!
                showToast("따뜻한 마음에 한 표 공감했습니다! ❤️");
            }
            saveToStorage();
            renderCompliments();
        }

        // --- MENTOR CONTROLS ---
        function openMentorRegModal() {
            document.getElementById("mentorRegModal").classList.remove("hidden");
            document.getElementById("mentorRegSpecialty").value = "";
            document.getElementById("mentorRegCertificates").value = "";
            document.getElementById("mentorRegIntro").value = "";
        }
        function closeMentorRegModal() {
            document.getElementById("mentorRegModal").classList.add("hidden");
        }
        function submitMentorProfile() {
            const spec = document.getElementById("mentorRegSpecialty").value.trim();
            const certs = document.getElementById("mentorRegCertificates").value.trim();
            const intro = document.getElementById("mentorRegIntro").value.trim();

            if (!spec || !intro) {
                showToast("정보들을 알맞게 채워주세요.", "error");
                return;
            }

            mentorProfiles.unshift({
                id: "p-" + Date.now(),
                name: currentUser.name,
                grade: currentUser.grade,
                major: currentUser.major,
                specialty: spec,
                certificates: certs,
                intro: intro
            });

            addExperience(5);
            saveToStorage();
            closeMentorRegModal();
            switchMentorSubTab('profiles');
            showToast("공부 멘토 프로필이 등록 완료되었습니다!");
        }

        function openMentorCreateModal() {
            document.getElementById("mentorCreateModal").classList.remove("hidden");
            document.getElementById("mentorSubject").value = "";
            document.getElementById("mentorDetail").value = "";
            setMentoringRole("mentor");
        }
        function closeMentorCreateModal() {
            document.getElementById("mentorCreateModal").classList.add("hidden");
        }
        function setMentoringRole(role) {
            selectedMentoringRole = role;
            const mentorBtn = document.getElementById("role-opt-mentor");
            const menteeBtn = document.getElementById("role-opt-mentee");

            if (role === 'mentor') {
                mentorBtn.className = "role-opt py-2 border rounded-xl font-bold text-xs border-amber-500 bg-amber-50 text-amber-700";
                menteeBtn.className = "role-opt py-2 border rounded-xl font-bold text-xs border-slate-200 hover:border-slate-300";
            } else {
                mentorBtn.className = "role-opt py-2 border rounded-xl font-bold text-xs border-slate-200 hover:border-slate-300";
                menteeBtn.className = "role-opt py-2 border rounded-xl font-bold text-xs border-amber-500 bg-amber-50 text-amber-700";
            }
        }

        function createMentoringPost() {
            const subject = document.getElementById("mentorSubject").value.trim();
            const detail = document.getElementById("mentorDetail").value.trim();

            if (!subject || !detail) return;

            mentors.unshift({
                id: "m-" + Date.now(),
                role: selectedMentoringRole,
                author: currentUser.name,
                grade: currentUser.grade,
                subject: subject,
                detail: detail,
                subscribers: [],
                likedBy: [],
                date: new Date().toISOString().slice(0, 10).replace(/-/g, '.')
            });

            addExperience(3);
            saveToStorage();
            closeMentorCreateModal();
            switchMentorSubTab('posts');
            showToast("구인 매칭글이 작성되었습니다.");
        }

        function deleteMentor(id) {
            mentors = mentors.filter(m => m.id !== id);
            saveToStorage();
            renderMentorPosts();
        }
        function applyMentor(id) {
            const item = mentors.find(m => m.id === id);
            if (!item) return;

            const hasApplied = item.subscribers.includes(currentUser.name);
            if (hasApplied) {
                item.subscribers = item.subscribers.filter(u => u !== currentUser.name);
                showToast("신청이 취소되었습니다.");
            } else {
                item.subscribers.push(currentUser.name);
                showToast("멘토링 신청이 접수되었습니다!");
            }
            saveToStorage();
            renderMentorPosts();
        }

        // --- STUDY GROUP ---
        function openStudyCreateModal() {
            document.getElementById("studyCreateModal").classList.remove("hidden");
            document.getElementById("studyTitle").value = "";
            document.getElementById("studyTopic").value = "";
            document.getElementById("studyDetail").value = "";
        }
        function closeStudyCreateModal() {
            document.getElementById("studyCreateModal").classList.add("hidden");
        }
        function createStudyPost() {
            const title = document.getElementById("studyTitle").value.trim();
            const topic = document.getElementById("studyTopic").value.trim();
            const maxM = parseInt(document.getElementById("studyMaxMembers").value) || 4;
            const cycle = document.getElementById("studyCycle").value;
            const detail = document.getElementById("studyDetail").value.trim();

            if (!title || !topic || !detail) return;

            studies.unshift({
                id: "s-" + Date.now(),
                title: title,
                topic: topic,
                author: currentUser.name,
                grade: currentUser.grade,
                maxMembers: maxM,
                members: [currentUser.name],
                cycle: cycle,
                detail: detail,
                date: new Date().toISOString().slice(0, 10).replace(/-/g, '.')
            });

            addExperience(4);
            saveToStorage();
            closeStudyCreateModal();
            renderStudies();
            showToast("새 자습 스터디방이 열렸습니다!");
        }
        function toggleStudyJoin(id) {
            const item = studies.find(s => s.id === id);
            if (!item) return;

            const isMember = item.members.includes(currentUser.name);
            if (isMember) {
                item.members = item.members.filter(u => u !== currentUser.name);
                showToast("참여를 탈퇴했습니다.");
            } else {
                if (item.members.length >= item.maxMembers) {
                    showToast("모집 정원이 초과되었습니다.", "error");
                    return;
                }
                item.members.push(currentUser.name);
                showToast("참여가 완료되었습니다!");
            }
            saveToStorage();
            renderStudies();
        }
        function deleteStudy(id) {
            studies = studies.filter(s => s.id !== id);
            saveToStorage();
            renderStudies();
        }

        // --- RESOURCES ---
        function openResourceCreateModal() {
            document.getElementById("resourceCreateModal").classList.remove("hidden");
            document.getElementById("resourceTitle").value = "";
            document.getElementById("resourceCategory").value = "";
            document.getElementById("resourceLink").value = "";
            document.getElementById("resourceDetail").value = "";
        }
        function closeResourceCreateModal() {
            document.getElementById("resourceCreateModal").classList.add("hidden");
        }
        function createResourcePost() {
            const title = document.getElementById("resourceTitle").value.trim();
            const cat = document.getElementById("resourceCategory").value.trim();
            const link = document.getElementById("resourceLink").value.trim();
            const detail = document.getElementById("resourceDetail").value.trim();

            if (!title || !cat || !link || !detail) return;

            resources.unshift({
                id: "r-" + Date.now(),
                title: title,
                category: cat,
                author: currentUser.name,
                grade: currentUser.grade,
                link: link,
                detail: detail,
                likedBy: [],
                downloads: 0,
                date: new Date().toISOString().slice(0, 10).replace(/-/g, '.')
            });

            addExperience(3);
            saveToStorage();
            closeResourceCreateModal();
            renderResources();
            showToast("학습 자료 나눔에 동참해주셔서 감사합니다!");
        }
        function incrementDownload(id) {
            const item = resources.find(r => r.id === id);
            if (item) {
                item.downloads += 1;
                saveToStorage();
                setTimeout(renderResources, 100);
            }
        }
        function deleteResource(id) {
            resources = resources.filter(r => r.id !== id);
            saveToStorage();
            renderResources();
        }

        // --- FREE POST ---
        function openFreePostModal() {
            document.getElementById("freePostModal").classList.remove("hidden");
            document.getElementById("freePostTitle").value = "";
            document.getElementById("freePostContent").value = "";
        }
        function closeFreePostModal() {
            document.getElementById("freePostModal").classList.add("hidden");
        }
        function createFreePost() {
            const title = document.getElementById("freePostTitle").value.trim();
            const content = document.getElementById("freePostContent").value.trim();

            if (!title || !content) return;

            const textLower = (title + ' ' + content).toLowerCase();
            const containsBanned = bannedWords.some(word => textLower.includes(word));
            if (containsBanned) {
                showToast("부적절한 단어가 본문에 기재되어 게시가 거부되었습니다.", "error");
                return;
            }

            freePosts.unshift({
                id: "f-" + Date.now(),
                title: title,
                content: content,
                author: currentUser.name,
                grade: currentUser.grade,
                likedBy: [],
                comments: [],
                date: new Date().toISOString().slice(0, 10).replace(/-/g, '.')
            });

            addExperience(2);
            saveToStorage();
            closeFreePostModal();
            renderFreeBoard();
            showToast("자율방 일상이 등록되었습니다.");
        }
        function deleteFreePost(id) {
            freePosts = freePosts.filter(f => f.id !== id);
            saveToStorage();
            renderFreeBoard();
        }

        // --- PROFILE EDIT ---
        function openProfileModal() {
            document.getElementById("profileModal").classList.remove("hidden");
            updateUserInfoUI();
        }
        function closeProfileModal() {
            document.getElementById("profileModal").classList.add("hidden");
        }
        function saveUserProfile() {
            const bio = document.getElementById("editUserBio").value.trim();
            currentUser.bio = bio || "화이팅!";
            saveToStorage();
            closeProfileModal();
            updateUserInfoUI();
            showToast("한마디 소개가 수정되었습니다.");
        }

        function getFilteredData(list) {
            return list.filter(item => {
                const gradeMatch = (gradeFilter === 'all') || (item.grade === gradeFilter) || (item.targetGrade === gradeFilter);
                let searchMatch = true;
                if (searchQuery) {
                    const textSource = [
                        item.title || '',
                        item.subject || '',
                        item.detail || '',
                        item.author || '',
                        item.category || '',
                        item.topic || '',
                        item.name || '',
                        item.specialty || '',
                        item.certificates || '',
                        item.text || ''
                    ].join(' ').toLowerCase();
                    searchMatch = textSource.includes(searchQuery);
                }
                return gradeMatch && searchMatch;
            });
        }
    </script>
</body>
</html>

```

