<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>記憶実験 - 自由研究</title>
    <!-- Tailwind CSS CDN for mobile-first responsive styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        /* iPhone Safari & Mobile Touch UX optimizations */
        -webkit-touch-callout: none;
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            -webkit-font-smoothing: antialiased;
            touch-action: manipulation;
        }
        .no-select {
            -webkit-touch-callout: none;
            -webkit-user-select: none;
            user-select: none;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col justify-between">

    <!-- Header -->
    <header class="bg-indigo-600 text-white p-4 shadow-md sticky top-0 z-50">
        <div class="max-w-md mx-auto flex justify-between items-center">
            <h1 class="text-lg font-bold tracking-wide flex items-center gap-2" id="header-title">
                <i data-lucide="brain"></i> 記憶実験
            </h1>
            <div class="flex items-center gap-2">
                <button onclick="openAiModal('menu')" class="text-xs bg-indigo-500 hover:bg-indigo-400 active:scale-95 text-white px-2.5 py-1 rounded-full flex items-center gap-1 transition shadow-sm font-medium">
                    <i data-lucide="sparkles" class="w-3.5 h-3.5 text-amber-300"></i> Gemini AI
                </button>
                <span id="session-badge" class="text-xs bg-indigo-700 px-2.5 py-1 rounded-full font-mono text-indigo-100 hidden"></span>
            </div>
        </div>
    </header>

    <!-- Main Dynamic Content Area -->
    <main class="flex-grow p-4 max-w-md mx-auto w-full flex flex-col justify-center">

        <!-- VIEW 1: TOP PORTAL (index.html mode) -->
        <div id="view-portal" class="space-y-6">
            <div class="text-center space-y-2">
                <div class="inline-block p-3 bg-indigo-100 text-indigo-600 rounded-full mb-1">
                    <i data-lucide="file-question" class="w-10 h-10"></i>
                </div>
                <h2 class="text-2xl font-bold text-slate-800">記憶の正確さ実験</h2>
                <p class="text-sm text-slate-600">中学3年 自由研究プロジェクト</p>
            </div>

            <div class="bg-white p-5 rounded-2xl shadow-sm border border-slate-200 space-y-4">
                <h3 class="font-bold text-slate-700 border-b pb-2 flex items-center gap-2">
                    <i data-lucide="play-circle" class="w-5 h-5 text-indigo-600"></i> 実験を始める
                </h3>
                <p class="text-xs text-slate-500 leading-relaxed">
                    参加者の方は、担当者から送られたURLまたは以下の該当するボタンから実験を開始してください。
                </p>

                <div class="space-y-3 pt-2">
                    <button onclick="startExperiment('with-info')" class="w-full bg-indigo-600 hover:bg-indigo-700 active:scale-[0.98] text-white font-bold py-3.5 px-4 rounded-xl shadow transition duration-150 text-base flex items-center justify-center gap-2">
                        事前情報あり
                    </button>
                    <button onclick="startExperiment('without-info')" class="w-full bg-slate-700 hover:bg-slate-800 active:scale-[0.98] text-white font-bold py-3.5 px-4 rounded-xl shadow transition duration-150 text-base flex items-center justify-center gap-2">
                        事前情報なし
                    </button>
                </div>
            </div>

            <!-- Gemini AI Assistant Card -->
            <div class="bg-gradient-to-br from-indigo-900 to-purple-900 text-white p-5 rounded-2xl shadow-md border border-indigo-700/50 space-y-3">
                <div class="flex items-center justify-between">
                    <h3 class="font-bold text-sm flex items-center gap-2 text-indigo-100">
                        <i data-lucide="sparkles" class="w-4 h-4 text-amber-300"></i> Gemini AI 自由研究サポート
                    </h3>
                    <span class="text-[10px] bg-amber-400/20 text-amber-300 px-2 py-0.5 rounded-full font-semibold border border-amber-300/30">AI Powered</span>
                </div>
                <p class="text-xs text-indigo-200 leading-relaxed">
                    Gemini APIを活用して、記憶実験用画像の自動生成や心理学的なAI考察レポートのドラフト生成が可能です。
                </p>
                <div class="grid grid-cols-2 gap-2 pt-1">
                    <button onclick="openAiModal('image')" class="bg-white/10 hover:bg-white/20 active:scale-95 text-xs text-indigo-100 py-2 px-3 rounded-xl border border-white/20 flex items-center justify-center gap-1.5 transition">
                        <i data-lucide="image-plus" class="w-3.5 h-3.5 text-amber-300"></i> AI画像生成
                    </button>
                    <button onclick="openAiModal('tutor')" class="bg-white/10 hover:bg-white/20 active:scale-95 text-xs text-indigo-100 py-2 px-3 rounded-xl border border-white/20 flex items-center justify-center gap-1.5 transition">
                        <i data-lucide="messages-square" class="w-3.5 h-3.5 text-cyan-300"></i> 心理学AI質問
                    </button>
                </div>
            </div>

            <!-- GitHub Pages Export & Files Generator Guide -->
            <div class="bg-slate-100 p-5 rounded-2xl border border-slate-300 space-y-3">
                <h3 class="font-bold text-slate-700 text-sm flex items-center gap-2">
                    <i data-lucide="folder-archive" class="w-4 h-4 text-slate-600"></i> GitHub Pages 設置用ファイル構成
                </h3>
                <p class="text-xs text-slate-600 leading-relaxed">
                    GitHub Pagesで複数ファイル形式としてデプロイする場合は、以下のボタンから必要なファイルコードを一括表示・コピーできます。
                </p>
                <button onclick="toggleFileExporter()" class="w-full bg-white hover:bg-slate-50 text-slate-700 font-semibold py-2 px-3 rounded-lg border border-slate-300 text-xs flex items-center justify-center gap-1">
                    <i data-lucide="code" class="w-4 h-4"></i> ファイルコード取得・生成ツールを開く
                </button>
            </div>
        </div>

        <!-- VIEW 2: CHECKLIST -->
        <div id="view-checklist" class="hidden space-y-5">
            <div class="bg-indigo-50 border border-indigo-200 p-4 rounded-xl text-center">
                <h2 class="text-xl font-bold text-indigo-900">実験前チェック</h2>
                <p class="text-xs text-indigo-700 mt-1">以下の質問にお答えください</p>
            </div>

            <form id="checklist-form" class="space-y-4 bg-white p-5 rounded-2xl shadow-sm border border-slate-200" onsubmit="handleChecklistSubmit(event)">
                <!-- 1. 睡眠時間 -->
                <div class="space-y-1">
                    <label class="block text-sm font-semibold text-slate-700">1. 前日の睡眠時間 <span class="text-red-500">*</span></label>
                    <div class="flex items-center gap-2">
                        <input type="number" id="check-sleep" step="0.5" min="0" max="24" required placeholder="例: 7" class="w-full p-3 border border-slate-300 rounded-xl focus:ring-2 focus:ring-indigo-500 focus:outline-none text-base">
                        <span class="text-sm font-bold text-slate-600">時間</span>
                    </div>
                </div>

                <!-- 2. 食事時刻 -->
                <div class="space-y-1">
                    <label class="block text-sm font-semibold text-slate-700">2. 最後に食事した時刻 <span class="text-red-500">*</span></label>
                    <div class="flex items-center gap-2">
                        <input type="number" id="check-meal" min="0" max="23" required placeholder="例: 12" class="w-full p-3 border border-slate-300 rounded-xl focus:ring-2 focus:ring-indigo-500 focus:outline-none text-base">
                        <span class="text-sm font-bold text-slate-600">時（分数なし）</span>
                    </div>
                </div>

                <!-- 3. 今日の運動 -->
                <div class="space-y-1">
                    <label class="block text-sm font-semibold text-slate-700">3. 今日の運動 <span class="text-red-500">*</span></label>
                    <div class="grid grid-cols-2 gap-3">
                        <label class="border rounded-xl p-3 flex items-center justify-center gap-2 cursor-pointer hover:bg-indigo-50 border-slate-300 has-[:checked]:border-indigo-600 has-[:checked]:bg-indigo-50">
                            <input type="radio" name="check-exercise" value="はい" required class="w-4 h-4 text-indigo-600">
                            <span class="font-medium text-sm">はい</span>
                        </label>
                        <label class="border rounded-xl p-3 flex items-center justify-center gap-2 cursor-pointer hover:bg-indigo-50 border-slate-300 has-[:checked]:border-indigo-600 has-[:checked]:bg-indigo-50">
                            <input type="radio" name="check-exercise" value="いいえ" required class="w-4 h-4 text-indigo-600">
                            <span class="font-medium text-sm">いいえ</span>
                        </label>
                    </div>
                </div>

                <!-- 4. カフェイン摂取 -->
                <div class="space-y-1">
                    <label class="block text-sm font-semibold text-slate-700">4. 今日のカフェイン摂取 <span class="text-red-500">*</span></label>
                    <div class="grid grid-cols-2 gap-3">
                        <label class="border rounded-xl p-3 flex items-center justify-center gap-2 cursor-pointer hover:bg-indigo-50 border-slate-300 has-[:checked]:border-indigo-600 has-[:checked]:bg-indigo-50">
                            <input type="radio" name="check-caffeine" value="はい" required class="w-4 h-4 text-indigo-600">
                            <span class="font-medium text-sm">はい</span>
                        </label>
                        <label class="border rounded-xl p-3 flex items-center justify-center gap-2 cursor-pointer hover:bg-indigo-50 border-slate-300 has-[:checked]:border-indigo-600 has-[:checked]:bg-indigo-50">
                            <input type="radio" name="check-caffeine" value="いいえ" required class="w-4 h-4 text-indigo-600">
                            <span class="font-medium text-sm">いいえ</span>
                        </label>
                    </div>
                </div>

                <!-- 5. 体調 -->
                <div class="space-y-1">
                    <label class="block text-sm font-semibold text-slate-700">5. 現在の体調 (1:悪い ~ 5:良い) <span class="text-red-500">*</span></label>
                    <div class="grid grid-cols-5 gap-1">
                        <template id="health-buttons">
                            <!-- JS Generated -->
                        </template>
                        <div id="health-options" class="contents"></div>
                    </div>
                </div>

                <!-- 6. その他自由記述 -->
                <div class="space-y-1">
                    <label class="block text-sm font-semibold text-slate-700">6. その他（任意）</label>
                    <textarea id="check-other" rows="2" placeholder="気になる点があればご記入ください（空欄可）" class="w-full p-3 border border-slate-300 rounded-xl focus:ring-2 focus:ring-indigo-500 focus:outline-none text-sm"></textarea>
                </div>

                <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 active:scale-[0.98] text-white font-bold py-3.5 rounded-xl shadow transition duration-150 text-base mt-2">
                    実験を開始する
                </button>
            </form>
        </div>

        <!-- VIEW 3: PRE-INFO INSTRUCTION (with-info only) -->
        <div id="view-pre-info" class="hidden space-y-6 text-center">
            <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200 space-y-6 my-auto">
                <div class="inline-block p-3 bg-amber-100 text-amber-600 rounded-full">
                    <i data-lucide="info" class="w-8 h-8"></i>
                </div>
                <p class="text-base font-bold text-slate-800 leading-relaxed">
                    これから多くのものが写った街中の画像を30秒間出します。
                </p>
                <button onclick="startImageDisplay()" class="w-full bg-indigo-600 hover:bg-indigo-700 active:scale-[0.98] text-white font-bold py-3.5 rounded-xl shadow text-base">
                    次へ
                </button>
            </div>
        </div>

        <!-- VIEW 4: IMAGE DISPLAY (30s) -->
        <div id="view-image-display" class="hidden flex flex-col items-center justify-center min-h-[60vh] space-y-4">
            <div class="relative w-full max-w-sm rounded-2xl overflow-hidden shadow-lg border border-slate-200 bg-black flex items-center justify-center">
                <!-- Stimulus Image Element -->
                <img id="stimulus-image" src="stimulus.jpg" alt="実験用画像" class="w-full h-auto object-contain max-h-[60vh]" onerror="handleImageError(this)">
            </div>
            <p class="text-xs text-slate-400">画像を集中してご覧ください</p>
        </div>

        <!-- VIEW 5: MATH DISTRACTOR TASK (30s) -->
        <div id="view-math-task" class="hidden space-y-4">
            <div class="bg-amber-50 border border-amber-200 p-3 rounded-xl text-center">
                <h3 class="font-bold text-amber-900 text-sm">計算課題（暗算してください）</h3>
                <p class="text-xs text-amber-700">回答入力は不要です。画面の計算を頭の中で行ってください。</p>
            </div>

            <div id="math-questions-grid" class="bg-white p-4 rounded-2xl shadow-sm border border-slate-200 grid grid-cols-2 gap-2 text-center font-mono font-bold text-base text-slate-800 no-select">
                <!-- 20 math problems generated dynamically -->
            </div>
        </div>

        <!-- VIEW 6: MEMORY TEST (11 Questions) -->
        <div id="view-memory-test" class="hidden space-y-5">
            <div class="bg-indigo-50 border border-indigo-200 p-3 rounded-xl text-center">
                <h2 class="text-lg font-bold text-indigo-900">記憶テスト</h2>
                <p class="text-xs text-indigo-700">全11問に回答し、自信度を選択してください</p>
            </div>

            <form id="memory-test-form" class="space-y-4" onsubmit="handleTestSubmit(event)">
                <div id="questions-container" class="space-y-4">
                    <!-- 11 questions dynamically generated -->
                </div>

                <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-200 space-y-2">
                    <button type="submit" id="submit-btn" class="w-full bg-emerald-600 hover:bg-emerald-700 active:scale-[0.98] text-white font-bold py-3.5 rounded-xl shadow transition duration-150 text-base">
                        回答を送信する
                    </button>
                    <p id="validation-msg" class="text-xs text-red-500 font-bold text-center hidden">未回答の質問または自信度があります</p>
                </div>
            </form>
        </div>

        <!-- VIEW 7: COMPLETE -->
        <div id="view-complete" class="hidden text-center space-y-5">
            <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200 space-y-4">
                <div class="inline-block p-4 bg-emerald-100 text-emerald-600 rounded-full">
                    <i data-lucide="check-circle-2" class="w-12 h-12"></i>
                </div>
                <h2 class="text-2xl font-bold text-slate-800">実験終了</h2>
                <p class="text-sm text-slate-600 leading-relaxed">
                    ご協力ありがとうございました。<br>回答データが記録されました。
                </p>
                <div id="gas-status" class="text-xs p-3 rounded-lg bg-slate-100 text-slate-600 font-mono">
                    データ記録ステータスを確認中...
                </div>
            </div>

            <!-- AI Memory Analysis Card on Completion -->
            <div class="bg-white p-5 rounded-2xl shadow-sm border border-indigo-200 space-y-4 text-left">
                <div class="flex items-center justify-between border-b pb-2">
                    <h3 class="font-bold text-indigo-900 text-sm flex items-center gap-2">
                        <i data-lucide="sparkles" class="w-4 h-4 text-indigo-600"></i> Gemini AI 記憶・確信度分析
                    </h3>
                    <span class="text-[10px] bg-indigo-100 text-indigo-700 px-2 py-0.5 rounded-full font-bold">メタ認知解析</span>
                </div>
                <p class="text-xs text-slate-600 leading-relaxed">
                    あなたの回答データ（正解率と自信度のズレ、過信傾向など）をGemini AIが心理学の観点から分析し、自由研究の「考察」に使える解説を生成します。
                </p>
                <button id="btn-run-ai-analysis" onclick="runAiResultAnalysis()" class="w-full bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 active:scale-[0.98] text-white font-bold py-3 px-4 rounded-xl shadow text-sm flex items-center justify-center gap-2 transition">
                    <i data-lucide="sparkles" class="w-4 h-4 text-amber-300"></i> AI分析レポートを生成する
                </button>

                <!-- AI Analysis Output Box -->
                <div id="ai-analysis-output" class="hidden bg-slate-50 border border-slate-200 p-4 rounded-xl space-y-3 text-xs text-slate-700 leading-relaxed max-h-80 overflow-y-auto">
                    <!-- Populated dynamically by JS -->
                </div>
            </div>
        </div>

        <!-- MODAL: Gemini AI Tools Modal -->
        <div id="ai-modal" class="hidden fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 p-4 overflow-y-auto flex items-center justify-center">
            <div class="bg-white rounded-2xl shadow-xl max-w-xl w-full p-5 space-y-4 my-8">
                <div class="flex justify-between items-center border-b pb-3">
                    <h3 class="font-bold text-slate-800 flex items-center gap-2 text-base">
                        <i data-lucide="sparkles" class="text-indigo-600"></i> Gemini AI 自由研究ツール
                    </h3>
                    <button onclick="closeAiModal()" class="text-slate-400 hover:text-slate-600">
                        <i data-lucide="x" class="w-6 h-6"></i>
                    </button>
                </div>

                <!-- AI Modal Tabs -->
                <div class="flex gap-2 border-b pb-2">
                    <button onclick="switchAiTab('image')" id="ai-tab-image" class="px-3 py-1.5 text-xs rounded-lg font-bold bg-indigo-600 text-white flex items-center gap-1">
                        <i data-lucide="image-plus" class="w-3.5 h-3.5"></i> 実験画像生成
                    </button>
                    <button onclick="switchAiTab('tutor')" id="ai-tab-tutor" class="px-3 py-1.5 text-xs rounded-lg font-bold bg-slate-100 text-slate-700 flex items-center gap-1">
                        <i data-lucide="messages-square" class="w-3.5 h-3.5"></i> 心理学AIチャット
                    </button>
                </div>

                <!-- AI Tab Content: Image Generator -->
                <div id="ai-panel-image" class="space-y-4">
                    <p class="text-xs text-slate-600 leading-relaxed">
                        Gemini 3.1 Flash Image AIを使って、記憶実験用の新しい刺激画像を生成します。
                    </p>
                    <div class="space-y-2">
                        <label class="block text-xs font-bold text-slate-700">プロンプト（画像の説明）</label>
                        <textarea id="ai-image-prompt" rows="3" class="w-full p-3 border border-slate-300 rounded-xl text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none" placeholder="例: 人通りが多く、自転車、標識、カフェ、看板、犬などの小物がたくさん写った賑やかな街のイラスト"></textarea>
                    </div>

                    <div class="flex gap-2">
                        <button onclick="setPromptPreset('street')" class="text-[11px] bg-slate-100 hover:bg-slate-200 text-slate-700 py-1 px-2.5 rounded-lg border">🏙️ 賑やかな街並み</button>
                        <button onclick="setPromptPreset('room')" class="text-[11px] bg-slate-100 hover:bg-slate-200 text-slate-700 py-1 px-2.5 rounded-lg border">🏠 散らかった部屋</button>
                        <button onclick="setPromptPreset('store')" class="text-[11px] bg-slate-100 hover:bg-slate-200 text-slate-700 py-1 px-2.5 rounded-lg border">🛒 スーパー陳列棚</button>
                    </div>

                    <button onclick="generateAiStimulusImage()" id="btn-generate-image" class="w-full bg-indigo-600 hover:bg-indigo-700 active:scale-95 text-white font-bold py-2.5 rounded-xl text-xs flex items-center justify-center gap-2 shadow">
                        <i data-lucide="sparkles" class="w-4 h-4 text-amber-300"></i> AIで画像を生成する (Gemini 3.1)
                    </button>

                    <div id="ai-image-preview-container" class="hidden space-y-2 border-t pt-3">
                        <span class="text-xs font-bold text-slate-700">生成された実験画像:</span>
                        <div class="relative rounded-xl overflow-hidden border border-slate-300 bg-black flex items-center justify-center">
                            <img id="ai-generated-img" src="" alt="AI generated stimulus" class="w-full h-auto max-h-52 object-contain">
                        </div>
                        <button onclick="applyGeneratedImageAsStimulus()" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-bold py-2 rounded-xl text-xs shadow flex items-center justify-center gap-1">
                            <i data-lucide="check" class="w-4 h-4"></i> この画像を本実験に適用する
                        </button>
                    </div>
                </div>

                <!-- AI Tab Content: Psychology Tutor -->
                <div id="ai-panel-tutor" class="hidden space-y-3">
                    <p class="text-xs text-slate-600">
                        記憶の仕組みや事前情報（プライミング効果・枠組み効果）について、Gemini AIに質問できます。
                    </p>
                    <div id="ai-chat-history" class="bg-slate-50 border border-slate-200 p-3 rounded-xl h-48 overflow-y-auto space-y-2 text-xs">
                        <div class="bg-indigo-100 text-indigo-900 p-2.5 rounded-xl max-w-[85%]">
                            こんにちは！記憶実験や心理学について気になる疑問（例：「なぜ見誤るの？」「事前に言うとどう変わる？」）を気軽に質問してください！
                        </div>
                    </div>
                    <div class="flex gap-2">
                        <input type="text" id="ai-chat-input" placeholder="質問を入力... (例: 偽記憶とは何ですか？)" class="flex-grow p-2.5 border border-slate-300 rounded-xl text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none" onkeydown="if(event.key==='Enter') sendAiTutorQuestion()">
                        <button onclick="sendAiTutorQuestion()" id="btn-send-chat" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 rounded-xl text-xs font-bold flex items-center justify-center">
                            送信
                        </button>
                    </div>
                </div>

                <div class="pt-2 text-right">
                    <button onclick="closeAiModal()" class="bg-slate-200 hover:bg-slate-300 text-slate-700 text-xs px-4 py-2 rounded-xl font-bold">
                        閉じる
                    </button>
                </div>
            </div>
        </div>

        <!-- MODAL: GitHub Pages Files Generator Modal -->
        <div id="file-exporter-modal" class="hidden fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 p-4 overflow-y-auto flex items-center justify-center">
            <div class="bg-white rounded-2xl shadow-xl max-w-xl w-full p-5 space-y-4 my-8">
                <div class="flex justify-between items-center border-b pb-3">
                    <h3 class="font-bold text-slate-800 flex items-center gap-2 text-base">
                        <i data-lucide="files" class="text-indigo-600"></i> GitHub Pages ファイル構成一覧
                    </h3>
                    <button onclick="toggleFileExporter()" class="text-slate-400 hover:text-slate-600">
                        <i data-lucide="x" class="w-6 h-6"></i>
                    </button>
                </div>

                <p class="text-xs text-slate-600">
                    GitHub Pagesのリポジトリルート階層に以下のファイル名（小文字・半角）で作成・配置してください。
                </p>

                <!-- File Directory Structure Preview -->
                <div class="bg-slate-900 text-slate-200 p-3 rounded-xl font-mono text-xs overflow-x-auto">
                    <div class="text-emerald-400 font-bold mb-1">memory-experiment/</div>
                    <div class="pl-4">├── index.html</div>
                    <div class="pl-4">├── with-info.html</div>
                    <div class="pl-4">├── without-info.html</div>
                    <div class="pl-4">├── stimulus.jpg</div>
                    <div class="pl-4">├── config.js</div>
                    <div class="pl-4">└── Google_Apps_Script.gs</div>
                </div>

                <!-- File Tabs & Code Exporter -->
                <div class="space-y-2">
                    <div class="flex flex-wrap gap-1 border-b pb-2" id="file-tabs">
                        <button onclick="switchTab('config')" class="tab-btn px-2.5 py-1 text-xs rounded-lg font-mono bg-indigo-600 text-white" id="tab-config">config.js</button>
                        <button onclick="switchTab('gas')" class="tab-btn px-2.5 py-1 text-xs rounded-lg font-mono bg-slate-100 text-slate-700" id="tab-gas">Google_Apps_Script.gs</button>
                        <button onclick="switchTab('with')" class="tab-btn px-2.5 py-1 text-xs rounded-lg font-mono bg-slate-100 text-slate-700" id="tab-with">with-info.html</button>
                        <button onclick="switchTab('without')" class="tab-btn px-2.5 py-1 text-xs rounded-lg font-mono bg-slate-100 text-slate-700" id="tab-without">without-info.html</button>
                        <button onclick="switchTab('stimulus')" class="tab-btn px-2.5 py-1 text-xs rounded-lg font-mono bg-slate-100 text-slate-700" id="tab-stimulus">stimulus.jpg生成</button>
                    </div>

                    <div class="relative">
                        <pre id="code-preview" class="bg-slate-800 text-slate-100 p-3 rounded-xl text-xs font-mono max-h-60 overflow-y-auto whitespace-pre-wrap break-all"></pre>
                        <button onclick="copyCode()" class="absolute top-2 right-2 bg-indigo-600 hover:bg-indigo-700 text-white text-xs px-2.5 py-1 rounded shadow flex items-center gap-1">
                            <i data-lucide="copy" class="w-3 h-3"></i> コピー
                        </button>
                    </div>
                </div>

                <div class="pt-2 text-right">
                    <button onclick="toggleFileExporter()" class="bg-slate-200 hover:bg-slate-300 text-slate-700 text-xs px-4 py-2 rounded-xl font-bold">
                        閉じる
                    </button>
                </div>
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="p-3 text-center text-xs text-slate-400 border-t border-slate-200 bg-white">
        記憶の正確さと確信度に関する心理学実験 &copy; 2026 自由研究
    </footer>

    <script>
        // State variables
        let experimentCondition = "with-info"; // 'with-info' or 'without-info'
        let sessionId = "";
        let experimentTimestamps = {
            checklistStart: "",
            mathTaskStart: "",
            mathTaskEnd: ""
        };
        let checklistData = {};
        let completedAnswersPayload = null; // Store for Gemini AI Analysis

        // Utility helper for API exponential backoff fetch
        async function fetchWithRetry(url, options, maxRetries = 3) {
            let delay = 1000;
            for (let i = 0; i < maxRetries; i++) {
                try {
                    const response = await fetch(url, options);
                    if (response.status === 429) {
                        // Rate limited - backoff
                        await new Promise(r => setTimeout(r, delay));
                        delay *= 2;
                        continue;
                    }
                    return response;
                } catch (err) {
                    if (i === maxRetries - 1) throw err;
                    await new Promise(r => setTimeout(r, delay));
                    delay *= 2;
                }
            }
        }

        function openAiModal(defaultTab = 'image') {
            document.getElementById("ai-modal").classList.remove("hidden");
            switchAiTab(defaultTab);
        }

        function closeAiModal() {
            document.getElementById("ai-modal").classList.add("hidden");
        }

        function switchAiTab(tabKey) {
            const btnImg = document.getElementById("ai-tab-image");
            const btnTutor = document.getElementById("ai-tab-tutor");
            const panelImg = document.getElementById("ai-panel-image");
            const panelTutor = document.getElementById("ai-panel-tutor");

            if (tabKey === 'image') {
                btnImg.className = "px-3 py-1.5 text-xs rounded-lg font-bold bg-indigo-600 text-white flex items-center gap-1";
                btnTutor.className = "px-3 py-1.5 text-xs rounded-lg font-bold bg-slate-100 text-slate-700 flex items-center gap-1";
                panelImg.classList.remove("hidden");
                panelTutor.classList.add("hidden");
            } else {
                btnTutor.className = "px-3 py-1.5 text-xs rounded-lg font-bold bg-indigo-600 text-white flex items-center gap-1";
                btnImg.className = "px-3 py-1.5 text-xs rounded-lg font-bold bg-slate-100 text-slate-700 flex items-center gap-1";
                panelTutor.classList.remove("hidden");
                panelImg.classList.add("hidden");
            }
        }

        function setPromptPreset(type) {
            const promptInput = document.getElementById("ai-image-prompt");
            if (type === 'street') {
                promptInput.value = "水色の自転車、緑色の建物、黄色の標識、ゴミ袋4つ、寝ている猫、赤い虫がはっきり描かれている、細部が賑やかな街並みの鮮明なイラスト。明るい日中。";
            } else if (type === 'room') {
                promptInput.value = "本や文房具、時計、ぬいぐるみ、マグカップ、クッションなどが机や床にたくさん置かれた子供部屋のイラスト。細部まで観察できる構図。";
            } else if (type === 'store') {
                promptInput.value = "カラフルなお菓子や飲み物、値札、缶詰、果物が綺麗に並べられたスーパーマーケットの商品の棚のイラスト。観察テスト用。";
            }
        }

        async function generateAiStimulusImage() {
            const prompt = document.getElementById("ai-image-prompt").value.trim();
            if (!prompt) {
                alert("プロンプト（画像の説明）を入力してください。");
                return;
            }

            const btn = document.getElementById("btn-generate-image");
            const originalBtnText = btn.innerHTML;
            btn.disabled = true;
            btn.innerHTML = `<i data-lucide="loader-2" class="w-4 h-4 animate-spin"></i> 生成中... (約5〜10秒)`;
            lucide.createIcons();

            try {
                const apiKey = ""; // Runtime automatically injected by environment
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3.1-flash-image:generateContent?key=${apiKey}`;

                const payload = {
                    contents: [{
                        parts: [{ text: `High quality detailed stimulus image for psychological memory experiment: ${prompt}` }]
                    }],
                    generationConfig: {
                        responseModalities: ['IMAGE'],
                        imageConfig: { aspectRatio: "4:3" }
                    }
                };

                const response = await fetchWithRetry(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();
                const part = result?.candidates?.[0]?.content?.parts?.find(p => p.inlineData);

                if (part && part.inlineData?.data) {
                    const imageUrl = `data:${part.inlineData.mimeType};base64,${part.inlineData.data}`;
                    const imgEl = document.getElementById("ai-generated-img");
                    imgEl.src = imageUrl;
                    document.getElementById("ai-image-preview-container").classList.remove("hidden");
                } else {
                    alert("画像の生成に失敗しました。プロンプトを変えて再度お試しください。");
                }
            } catch (err) {
                console.error("AI Image Generation Error:", err);
                alert("エラーが発生しました: " + err.message);
            } finally {
                btn.disabled = false;
                btn.innerHTML = originalBtnText;
                lucide.createIcons();
            }
        }

        function applyGeneratedImageAsStimulus() {
            const generatedImgSrc = document.getElementById("ai-generated-img").src;
            if (generatedImgSrc) {
                const mainStimulusImg = document.getElementById("stimulus-image");
                mainStimulusImg.src = generatedImgSrc;
                closeAiModal();
                alert("生成した画像を実験用刺激画像として設定しました！");
            }
        }

        async function runAiResultAnalysis() {
            if (!completedAnswersPayload) {
                alert("回答データが見つかりません。");
                return;
            }

            const btn = document.getElementById("btn-run-ai-analysis");
            const outputBox = document.getElementById("ai-analysis-output");
            
            btn.disabled = true;
            btn.innerHTML = `<i data-lucide="loader-2" class="w-4 h-4 animate-spin"></i> Gemini AI が分析中...`;
            outputBox.classList.remove("hidden");
            outputBox.innerHTML = "<p class='text-slate-500 italic'>Gemini AIで記憶データ（正答率・確信度・過信の指標）を解析中...</p>";
            lucide.createIcons();

            const prompt = `
あなたは心理学の専門家であり、中学3年生の自由研究をアドバイスする優れたメンターです。
以下の心理学記憶実験の参加者データに基づいて、メタ認知（記憶の確信度と実際の正確さのズレ）や過信傾向、および自由研究のレポートに載せる「考察ドラフト」を分かりやすく日本語で作成してください。

【実験条件】: ${completedAnswersPayload.condition}
【事前チェックリスト】:
- 睡眠時間: ${completedAnswersPayload.sleepHours}時間
- 今日の運動: ${completedAnswersPayload.exercise}
- カフェイン摂取: ${completedAnswersPayload.caffeine}
- 体調 (1-5): ${completedAnswersPayload.health}

【テスト結果】:
- 合計正答数: ${completedAnswersPayload.score} / 11問
- 各問の詳細（問題番号, 回答, 正誤, 確信度0-5）:
${completedAnswersPayload.details}

【回答に含める項目】:
1. 📊 **記憶の正確さと自信度の分析**:
   - 自信度（5や4）が高かったのに間違えた「過信（偽記憶）」傾向があったか？
   - 自信度は低かったが正解した項目はあったか？
2. 🧠 **条件・生活習慣からの考察**:
   - 睡眠時間や事前情報の有無が今回の結果にどのように影響を与えたか心理学的にコメント。
3. 📝 **自由研究の「考察」まとめ（論文風ドラフト）**:
   - そのまま自由研究のノートに書けるような簡潔で丁寧な文章（300文字程度）。
`;

            try {
                const apiKey = "";
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;

                const payload = {
                    contents: [{ parts: [{ text: prompt }] }],
                    systemInstruction: {
                        parts: [{ text: "あなたは中学生の心理学自由研究をサポートする親切で正確なAI研究パートナーです。Markdown形式で読みやすく構成してください。" }]
                    }
                };

                const response = await fetchWithRetry(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();
                const text = result?.candidates?.[0]?.content?.parts?.[0]?.text;

                if (text) {
                    // Render formatted response
                    outputBox.innerHTML = text.replace(/\n/g, '<br>').replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
                } else {
                    outputBox.innerHTML = "<p class='text-red-500'>分析結果の取得に失敗しました。</p>";
                }
            } catch (err) {
                console.error("AI Analysis Error:", err);
                outputBox.innerHTML = `<p class='text-red-500'>エラーが発生しました: ${err.message}</p>`;
            } finally {
                btn.disabled = false;
                btn.innerHTML = `<i data-lucide="sparkles" class="w-4 h-4 text-amber-300"></i> 再度AI分析を実行する`;
                lucide.createIcons();
            }
        }

        async function sendAiTutorQuestion() {
            const inputEl = document.getElementById("ai-chat-input");
            const query = inputEl.value.trim();
            if (!query) return;

            const chatHistory = document.getElementById("ai-chat-history");
            
            // Append User Question
            const userMsg = document.createElement("div");
            userMsg.className = "bg-slate-200 text-slate-800 p-2.5 rounded-xl max-w-[85%] ml-auto text-right font-medium";
            userMsg.textContent = query;
            chatHistory.appendChild(userMsg);
            inputEl.value = "";
            chatHistory.scrollTop = chatHistory.scrollHeight;

            // Loading state
            const loadingMsg = document.createElement("div");
            loadingMsg.className = "bg-indigo-100 text-indigo-900 p-2.5 rounded-xl max-w-[85%] text-left italic";
            loadingMsg.textContent = "Gemini AI 考え中...";
            chatHistory.appendChild(loadingMsg);
            chatHistory.scrollTop = chatHistory.scrollHeight;

            try {
                const apiKey = "";
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;

                const payload = {
                    contents: [{ parts: [{ text: query }] }],
                    systemInstruction: {
                        parts: [{ text: "あなたは心理学と記憶の仕組みに詳しい親切なAIチューターです。中学生にもわかりやすく丁寧かつ簡潔（200文字以内）に答えてください。" }]
                    }
                };

                const response = await fetchWithRetry(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();
                const replyText = result?.candidates?.[0]?.content?.parts?.[0]?.text || "すみません、回答を作成できませんでした。";

                loadingMsg.className = "bg-indigo-100 text-indigo-900 p-2.5 rounded-xl max-w-[85%] text-left";
                loadingMsg.textContent = replyText;
            } catch (err) {
                loadingMsg.className = "bg-red-100 text-red-800 p-2.5 rounded-xl max-w-[85%] text-left";
                loadingMsg.textContent = "エラーが発生しました: " + err.message;
            } finally {
                chatHistory.scrollTop = chatHistory.scrollHeight;
            }
        }

        function handleTestSubmit(e) {
            e.preventDefault();
            const valMsg = document.getElementById("validation-msg");
            valMsg.classList.add("hidden");

            // Validate all 11 questions have both Answer and Confidence selected
            let allAnswered = true;
            let totalCorrect = 0;
            const answersData = {};
            let detailsLog = "";

            QUESTIONS.forEach(q => {
                const ans = document.querySelector(`input[name="ans-${q.id}"]:checked`)?.value;
                const conf = document.querySelector(`input[name="conf-${q.id}"]:checked`)?.value;

                if (!ans || conf === undefined) {
                    allAnswered = false;
                } else {
                    const isCorrect = (ans === q.answer) ? "正解" : "不正解";
                    if (isCorrect === "正解") totalCorrect++;

                    answersData[`${q.id}_ans`] = ans;
                    answersData[`${q.id}_isCorrect`] = isCorrect;
                    answersData[`${q.id}_conf`] = conf;

                    detailsLog += `- ${q.id} (${q.text}): 回答=${ans}, 判定=${isCorrect}, 自信度=${conf}\n`;
                }
            });

            if (!allAnswered) {
                valMsg.classList.remove("hidden");
                return;
            }

            // Save payload for AI Analysis
            completedAnswersPayload = {
                condition: experimentCondition === 'with-info' ? '事前情報あり' : '事前情報なし',
                sleepHours: checklistData.sleepHours,
                exercise: checklistData.exercise,
                caffeine: checklistData.caffeine,
                health: checklistData.health,
                score: totalCorrect,
                details: detailsLog
            };

            // Construct Final Payload for Google Sheets
            const payloadRow = [
                new Date().toLocaleString('ja-JP'),
                sessionId,
                experimentCondition === 'with-info' ? '事前情報あり' : '事前情報なし',
                checklistData.sleepHours,
                checklistData.lastMealHour,
                checklistData.startTime,
                checklistData.exercise,
                checklistData.caffeine,
                checklistData.health,
                checklistData.other,
                "30秒",
                experimentTimestamps.mathTaskStart,
                experimentTimestamps.mathTaskEnd
            ];

            QUESTIONS.forEach(q => {
                payloadRow.push(answersData[`${q.id}_ans`]);
                payloadRow.push(answersData[`${q.id}_isCorrect`]);
                payloadRow.push(answersData[`${q.id}_conf`]);
            });

            payloadRow.push(totalCorrect);

            showView('view-complete');
            sendDataToGoogleSheets(payloadRow);
        }

        function sendDataToGoogleSheets(rowArray) {
            const statusEl = document.getElementById("gas-status");
            const scriptUrl = window.CONFIG?.APPS_SCRIPT_URL;

            if (!scriptUrl || scriptUrl.trim() === "") {
                statusEl.className = "text-xs p-3 rounded-lg bg-amber-100 text-amber-800 font-mono text-left space-y-1";
                statusEl.innerHTML = `
                    <div class="font-bold">⚠️ Google Apps Script URL未設定</div>
                    <div>config.js に APPS_SCRIPT_URL が指定されていないため、ローカル表示のみ行いました。</div>
                    <div class="text-[10px] mt-1 text-amber-700">合計正答数: ${rowArray[rowArray.length - 1]} / 11 問</div>
                `;
                return;
            }

            statusEl.textContent = "Googleスプレッドシートへデータ送信中...";

            fetch(scriptUrl, {
                method: "POST",
                mode: "no-cors", // Standard for Google Apps Script Web App
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ row: rowArray })
            })
            .then(() => {
                statusEl.className = "text-xs p-3 rounded-lg bg-emerald-100 text-emerald-800 font-mono";
                statusEl.textContent = "✓ Googleスプレッドシートへの保存完了";
            })
            .catch(err => {
                console.error("Transmission Error:", err);
                statusEl.className = "text-xs p-3 rounded-lg bg-red-100 text-red-800 font-mono";
                statusEl.textContent = "✕ 送信に失敗しました（設定を確認してください）";
            });
        }

        const FILE_CONTENTS = {
            config: `// config.js - Webアプリ設定ファイル
// Google Apps ScriptのWebアプリデプロイURLをここに貼り付けてください
window.CONFIG = {
    APPS_SCRIPT_URL: "https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec"
};`,

            gas: `// Google_Apps_Script.gs
// このコードをGoogle Apps Scriptのエディタに貼り付けて「Webアプリ」としてデプロイしてください。
// アクセスできるユーザー: 「全員 (Anyone)」に設定してください。

function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var data = JSON.parse(e.postData.contents);
    
    // ヘッダー（項目名）が未作成の場合は自動挿入
    if (sheet.getLastRow() === 0) {
      sheet.appendRow([
        "日時", "匿名セッションID", "実験条件", 
        "睡眠時間", "最終食事時刻", "実験開始時刻", "運動", "カフェイン", "体調", "その他",
        "画像提示時間", "計算開始時刻", "計算終了時刻",
        "Q1回答", "Q1正誤", "Q1自信度",
        "Q2回答", "Q2正誤", "Q2自信度",
        "Q3回答", "Q3正誤", "Q3自信度",
        "Q4回答", "Q4正誤", "Q4自信度",
        "Q5回答", "Q5正誤", "Q5自信度",
        "Q6回答", "Q6正誤", "Q6自信度",
        "Q7回答", "Q7正誤", "Q7自信度",
        "Q8回答", "Q8正誤", "Q8自信度",
        "Q9回答", "Q9正誤", "Q9自信度",
        "Q10回答", "Q10正誤", "Q10自信度",
        "Q11回答", "Q11正誤", "Q11自信度",
        "合計正答数"
      ]);
    }
    
    sheet.appendRow(data.row);
    return ContentService.createTextOutput(JSON.stringify({result: "success"})).setMimeType(ContentService.MimeType.JSON);
  } catch(err) {
    return ContentService.createTextOutput(JSON.stringify({result: "error", error: err.toString()})).setMimeType(ContentService.MimeType.JSON);
  }
}`,

            with: `<!-- with-info.html -->
<!-- GitHub Pagesルートに置くことで直接リンク可能 -->
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="refresh" content="0; url=index.html?mode=with-info">
    <title>事前情報あり実験</title>
</head>
<body>
    <p>リダイレクト中... <a href="index.html?mode=with-info">こちらをクリック</a></p>
</body>
</html>`,

            without: `<!-- without-info.html -->
<!-- GitHub Pagesルートに置くことで直接リンク可能 -->
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="refresh" content="0; url=index.html?mode=without-info">
    <title>事前情報なし実験</title>
</head>
<body>
    <p>リダイレクト中... <a href="index.html?mode=without-info">こちらをクリック</a></p>
</body>
</html>`,

            stimulus: `/* stimulus.jpg の作成方法 */
- 画像ファイルを「stimulus.jpg」という名前でGitHub Pagesのルートディレクトリに配置してください。
- このWebアプリは同じフォルダにある stimulus.jpg を自動読み込みします。
- 差し替えることで別の画像での実験も可能です。`
        };

        function toggleFileExporter() {
            const modal = document.getElementById("file-exporter-modal");
            modal.classList.toggle("hidden");
            if (!modal.classList.contains("hidden")) {
                switchTab('config');
            }
        }

        function switchTab(key) {
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.className = "tab-btn px-2.5 py-1 text-xs rounded-lg font-mono bg-slate-100 text-slate-700";
            });
            const activeTab = document.getElementById(`tab-${key}`);
            if (activeTab) {
                activeTab.className = "tab-btn px-2.5 py-1 text-xs rounded-lg font-mono bg-indigo-600 text-white";
            }
            document.getElementById("code-preview").textContent = FILE_CONTENTS[key];
        }

        function copyCode() {
            const text = document.getElementById("code-preview").textContent;
            navigator.clipboard.writeText(text).then(() => {
                alert("コードをクリップボードにコピーしました！");
            });
        }
    </script>
</body>
</html>
