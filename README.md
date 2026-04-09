<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nada Translate - المترجم الذكي</title>
    <style>
        :root {
            /* نظام ألوان احترافي ومريح */
            --bg: #f9fafb;
            --card: rgba(255, 255, 255, 0.7);
            --text-primary: #111827;
            --text-secondary: #6b7280;
            --accent: #4f46e5; /* أزرق نيلي احترافي */
            --accent-hover: #4338ca;
            --border: rgba(229, 231, 235, 0.5);
            --textarea-bg: rgba(255, 255, 255, 0.9);
            --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }

        [data-theme="dark"] {
            --bg: #111827;
            --card: rgba(31, 41, 55, 0.7);
            --text-primary: #f9fafb;
            --text-secondary: #d1d5db;
            --accent: #818cf8; /* أزرق نيلي أفتح للوضع الليلي */
            --accent-hover: #a5b4fc;
            --border: rgba(75, 85, 99, 0.5);
            --textarea-bg: rgba(17, 24, 39, 0.8);
            --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.3), 0 2px 4px -1px rgba(0, 0, 0, 0.18);
            --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.3), 0 4px 6px -2px rgba(0, 0, 0, 0.15);
        }

        body {
            font-family: 'Inter', system-ui, -apple-system, sans-serif; /* خط عصري واحترافي */
            background-color: var(--bg);
            color: var(--text-primary);
            transition: background-color 0.3s ease, color 0.3s ease;
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        /* رأس الصفحة - احترافي وبسيط */
        .header {
            width: 100%;
            max-width: 1100px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
            margin-bottom: 30px;
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .logo-icon {
            font-size: 28px;
            color: var(--accent);
        }

        .header h1 {
            margin: 0;
            font-size: 28px;
            font-weight: 800; /* خط عريض */
            letter-spacing: -0.5px;
        }

        .header h1 span {
            font-weight: 400; /* وزن أخف لكلمة Translate */
            color: var(--text-secondary);
        }

        .sub-header {
            font-size: 16px;
            color: var(--text-secondary);
            max-width: 600px;
            margin: -10px auto 30px auto;
            text-align: center;
        }

        .theme-toggle {
            cursor: pointer;
            background: var(--card);
            border: 1px solid var(--border);
            padding: 10px 18px;
            border-radius: 50px; /* تصميم دائري */
            color: var(--text-primary);
            font-size: 14px;
            font-weight: 500;
            backdrop-filter: blur(8px);
            transition: all 0.2s;
            box-shadow: var(--shadow-md);
        }

        .theme-toggle:hover {
            transform: translateY(-1px);
            box-shadow: var(--shadow-lg);
        }

        /* الحاوية الرئيسية - تصميم زجاجي مُحسّن */
        .main-container {
            width: 100%;
            max-width: 1100px;
            background: var(--card);
            border-radius: 20px;
            box-shadow: var(--shadow-lg);
            padding: 30px;
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            border: 1px solid var(--border);
        }

        /* عناصر التحكم */
        .controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            gap: 15px;
            flex-wrap: wrap;
        }

        .controls-group {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        select, .file-btn {
            background: var(--textarea-bg);
            color: var(--text-primary);
            border: 1px solid var(--border);
            padding: 12px 18px;
            border-radius: 10px;
            outline: none;
            cursor: pointer;
            font-weight: 500;
            font-size: 15px;
            transition: 0.2s;
        }
        
        select:focus, .file-btn:hover {
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
        }

        .file-btn {
            background-color: var(--accent);
            color: white;
            border: none;
        }
        
        .file-btn:hover {
            background-color: var(--accent-hover);
        }

        /* شبكة الترجمة */
        .translation-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
        }

        .box-wrapper { position: relative; }

        textarea, .output-box {
            width: 100%;
            height: 320px;
            border: 1px solid var(--border);
            padding: 25px;
            font-size: 18px;
            border-radius: 16px;
            background: var(--textarea-bg);
            color: var(--text-primary);
            resize: none;
            outline: none;
            box-sizing: border-box;
            line-height: 1.7;
            transition: border-color 0.2s;
        }
        
        textarea:focus {
            border-color: var(--accent);
        }

        .output-box {
            border-color: var(--border);
            overflow-y: auto; /* للسماح بالتمرير */
        }

        /* زر النطق الصوتي - أكثر وضوحًا */
        .voice-btn {
            position: absolute;
            bottom: 20px;
            left: 20px;
            background: white;
            color: #333;
            border: 1px solid rgba(0,0,0,0.1);
            width: 48px;
            height: 48px;
            border-radius: 50%;
            cursor: pointer;
            box-shadow: var(--shadow-md);
            transition: 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
        }
        
        [data-theme="dark"] .voice-btn {
            background: #2d3748;
            color: #f9fafb;
            border-color: rgba(255,255,255,0.1);
        }

        .voice-btn:hover { transform: scale(1.05); box-shadow: var(--shadow-lg); }

        /* أدوات التذييل */
        .footer-tools {
            margin-top: 30px;
            display: flex;
            gap: 20px;
            justify-content: center;
            align-items: center;
        }

        .btn-main {
            background: var(--accent);
            color: white;
            padding: 14px 40px;
            border: none;
            border-radius: 12px;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 4px 6px -1px rgba(79, 70, 229, 0.2);
        }
        
        .btn-main:hover { background-color: var(--accent-hover); transform: translateY(-1px); box-shadow: 0 10px 15px -3px rgba(79, 70, 229, 0.3); }

        .btn-secondary {
            background: none;
            border: none;
            color: var(--text-secondary);
            cursor: pointer;
            font-weight: 500;
            padding: 10px;
            border-radius: 8px;
            transition: 0.2s;
        }
        
        .btn-secondary:hover { color: var(--text-primary); background-color: rgba(0,0,0,0.05); }
        [data-theme="dark"] .btn-secondary:hover { background-color: rgba(255,255,255,0.05); }

        /* الشارة السفلية */
        .copy-badge {
            margin-top: 40px;
            font-size: 14px;
            color: var(--text-secondary);
            opacity: 0.7;
        }

        @media (max-width: 850px) {
            .translation-grid { grid-template-columns: 1fr; }
            .header { flex-direction: column; text-align: center; gap: 15px; }
            .controls { justify-content: center; }
        }
    </style>
</head>
<body>

    <div class="header">
        <div class="brand">
            <span class="logo-icon">🌐</span>
            <h1>Nada <span>Translate</span></h1>
        </div>
        <button class="theme-toggle" onclick="toggleTheme()">🌓 تبديل الوضع</button>
    </div>
    
    <p class="sub-header">مترجم ذكي واحترافي يدعم لغات متعددة بتصميم عصري</p>

    <div class="main-container">
        <div class="controls">
            <div class="controls-group">
                <select id="sourceLang">
                    <option value="en">الإنجليزية</option>
                    <option value="ar">العربية</option>
                    <option value="fr">الفرنسية</option>
                    <option value="de">الألمانية</option>
                </select>
                <label class="file-btn" for="fileInput">📁 رفع ملف</label>
                <input type="file" id="fileInput" hidden accept=".txt">
            </div>
            
            <select id="targetLang">
                <option value="ar" selected>العربية</option>
                <option value="en">الإنجليزية</option>
                <option value="fr">الفرنسية</option>
                <option value="de">الألمانية</option>
            </select>
        </div>

        <div class="translation-grid">
            <div class="box-wrapper">
                <textarea id="inputText" placeholder="اكتب أو الصق النص هنا..."></textarea>
                <button class="voice-btn" onclick="speak('inputText', 'sourceLang')" title="نطق النص">🔊</button>
            </div>
            
            <div class="box-wrapper">
                <div id="outputText" class="output-box">الترجمة ستظهر هنا...</div>
                <button class="voice-btn" onclick="speak('outputText', 'targetLang')" title="نطق الترجمة">🔊</button>
            </div>
        </div>

        <div class="footer-tools">
            <button class="btn-main" onclick="copyText()">نسخ الترجمة</button>
            <button class="btn-secondary" onclick="clearAll()">مسح الكل</button>
        </div>
    </div>

    <div class="copy-badge">© 2023 Nada Translate. جميع الحقوق محفوظة.</div>

    <script>
        // إعدادات الوضع الداكن
        function toggleTheme() {
            const body = document.body;
            const currentTheme = body.getAttribute('data-theme');
            const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
            body.setAttribute('data-theme', newTheme);
            localStorage.setItem('theme', newTheme); // حفظ الاختيار
        }

        // تحميل الوضع المحفوظ
        const savedTheme = localStorage.getItem('theme');
        if (savedTheme) {
            document.body.setAttribute('data-theme', savedTheme);
        }

        // معالجة رفع الملفات
        document.getElementById('fileInput').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = (e) => {
                document.getElementById('inputText').value = e.target.result;
                translate(); // بدء الترجمة فوراً
            };
            reader.readAsText(file);
        });

        // دالة الترجمة (باستخدام API)
        async function translate() {
            const text = document.getElementById('inputText').value;
            const outputDiv = document.getElementById('outputText');
            
            if(!text.trim()) {
                outputDiv.innerText = "الترجمة ستظهر هنا...";
                return;
            }
            
            const s = document.getElementById('sourceLang').value;
            const t = document.getElementById('targetLang').value;
            
            outputDiv.innerText = "جاري الترجمة..."; // مؤشر تحميل

            try {
                // استخدام API مجاني للترجمة (MyMemory)
                const r = await fetch(`https://api.mymemory.translated.net/get?q=${encodeURIComponent(text)}&langpair=${s}|${t}`);
                const d = await r.json();
                outputDiv.innerText = d.responseData.translatedText;
            } catch(e) { 
                outputDiv.innerText = "عذراً، حدث خطأ في الاتصال. يرجى المحاولة لاحقاً.";
            }
        }

        // دالة النطق الصوتي
        function speak(id, langId) {
            const el = document.getElementById(id);
            const text = el.value || el.innerText;
            if(!text || text.includes("...")) return;
            
            window.speechSynthesis.cancel();
            const msg = new SpeechSynthesisUtterance(text);
            msg.lang = document.getElementById(langId).value;
            window.speechSynthesis.speak(msg);
        }

        // استخدام Debounce لتقليل طلبات API أثناء الكتابة
        let timer;
        document.getElementById('inputText').addEventListener('input', () => {
            clearTimeout(timer);
            timer = setTimeout(translate, 800); // ترجمة بعد توقف الكتابة بـ 800ms
        });

        // دالة نسخ النص
        function copyText() {
            const text = document.getElementById('outputText').innerText;
            if(text.includes("...")) return;
            navigator.clipboard.writeText(text).then(() => {
                alert("تم نسخ الترجمة بنجاح!");
            });
        }

        // دالة مسح الكل
        function clearAll() {
            document.getElementById('inputText').value = "";
            document.getElementById('outputText').innerText = "الترجمة ستظهر هنا...";
            window.speechSynthesis.cancel();
        }
    </script>
</body>
</html>
