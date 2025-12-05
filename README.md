# spanish-verbs
Spanish-verbs
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>西班牙语动词大师 (Maestro de Verbos)</title>
    <style>
        :root {
            --primary: #b71c1c; /* Deep Spanish Red */
            --primary-light: #f05545;
            --secondary: #fbc02d; /* Spanish Yellow */
            --dark: #263238;
            --light: #eceff1;
            --white: #ffffff;
            --gray: #78909c;
            --success: #43a047;
            --error: #e53935;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f5f5f5;
            color: var(--dark);
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            height: 100vh;
        }

        /* Navigation */
        nav {
            background-color: var(--primary);
            color: white;
            padding: 0 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        nav h1 { margin: 15px 0; font-size: 1.5em; }

        .nav-tabs {
            display: flex;
            list-style: none;
            margin: 0;
            padding: 0;
        }

        .nav-item {
            padding: 20px 25px;
            cursor: pointer;
            transition: background 0.3s;
            font-weight: bold;
            opacity: 0.8;
        }

        .nav-item:hover { opacity: 1; background-color: rgba(255,255,255,0.1); }
        .nav-item.active {
            background-color: var(--white);
            color: var(--primary);
            opacity: 1;
            border-bottom: 4px solid var(--secondary);
        }

        /* Content Area */
        .main-content {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
            max-width: 1200px;
            margin: 0 auto;
            width: 100%;
            box-sizing: border-box;
        }

        .section { display: none; animation: fadeIn 0.3s; }
        .section.active { display: block; }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Cards & Layout */
        .card {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            padding: 25px;
            margin-bottom: 20px;
        }

        h2 { color: var(--primary); border-bottom: 2px solid var(--light); padding-bottom: 10px; margin-top: 0;}
        h3 { color: var(--dark); margin-top: 20px; }

        /* Verb Tables */
        .verb-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
        }

        .conjugation-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.9em;
            margin-top: 10px;
        }

        .conjugation-table th {
            background-color: var(--light);
            padding: 8px;
            text-align: left;
            color: var(--gray);
        }

        .conjugation-table td {
            padding: 8px;
            border-bottom: 1px solid #eee;
        }

        .highlight-root { color: var(--dark); }
        .highlight-ending { color: var(--primary); font-weight: bold; }

        /* Buttons */
        .btn {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1em;
            transition: all 0.2s;
        }
        .btn:hover { background-color: var(--primary-light); transform: translateY(-1px); }
        .btn-secondary { background-color: var(--gray); }
        .btn-outline { background: transparent; border: 1px solid var(--primary); color: var(--primary); }
        .btn-outline:hover { background: var(--primary); color: white; }

        /* Quiz Section */
        .quiz-container {
            text-align: center;
            max-width: 600px;
            margin: 0 auto;
        }
        
        .quiz-card {
            background: var(--white);
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .quiz-verb { font-size: 3em; color: var(--dark); margin: 10px 0; font-weight: bold; }
        .quiz-info { font-size: 1.2em; color: var(--gray); margin-bottom: 20px; }
        .quiz-input {
            width: 80%;
            padding: 15px;
            font-size: 1.5em;
            text-align: center;
            border: 2px solid var(--light);
            border-radius: 8px;
            margin-bottom: 20px;
        }
        .quiz-input:focus { border-color: var(--primary); outline: none; }
        
        .feedback-msg { margin-top: 15px; font-weight: bold; font-size: 1.1em; min-height: 24px;}
        .correct-text { color: var(--success); }
        .wrong-text { color: var(--error); }

        /* Char buttons */
        .char-keys { margin-bottom: 15px; }
        .char-key {
            background: var(--light);
            border: none;
            padding: 8px 12px;
            margin: 0 2px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1.1em;
        }
        .char-key:hover { background: #cfd8dc; }

        /* Records Section */
        .error-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            background: #fff0f0;
            border-left: 4px solid var(--error);
            margin-bottom: 10px;
            border-radius: 4px;
        }
        .error-details { flex: 1; }
        .error-verb { font-weight: bold; font-size: 1.1em; }
        .error-context { color: var(--gray); font-size: 0.9em; margin-top: 5px; }
        .error-correction { color: var(--success); font-weight: bold; margin-top: 2px; }

        /* Irregular Tags */
        .tag {
            display: inline-block;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 0.75em;
            margin-left: 5px;
            color: white;
        }
        .tag-e-ie { background-color: #FF9800; }
        .tag-o-ue { background-color: #9C27B0; }
        .tag-e-i { background-color: #2196F3; }
        .tag-total { background-color: #f44336; }

    </style>
</head>
<body>

    <nav>
        <h1>🇪🇸 Maestro de Verbos</h1>
        <ul class="nav-tabs">
            <li class="nav-item active" onclick="switchTab('regular')">规则动词</li>
            <li class="nav-item" onclick="switchTab('irregular')">不规则动词</li>
            <li class="nav-item" onclick="switchTab('quiz')">测试 (Prueba)</li>
            <li class="nav-item" onclick="switchTab('records')">错题记录</li>
        </ul>
    </nav>

    <div class="main-content">
        
        <!-- 1. 规则动词模块 -->
        <div id="regular" class="section active">
            <div class="card">
                <h2>规则动词变位逻辑 (Verbos Regulares)</h2>
                <p>西班牙语规则动词分为三类：<strong>-AR</strong>, <strong>-ER</strong>, <strong>-IR</strong>。虽然时态众多，但只要记住词尾变化规律，就能掌握成千上万个动词。</p>
                <div style="margin-top: 20px;">
                    <button class="btn" onclick="showRegularTable('ar')">查看 -AR 变位表</button>
                    <button class="btn" onclick="showRegularTable('er')">查看 -ER 变位表</button>
                    <button class="btn" onclick="showRegularTable('ir')">查看 -IR 变位表</button>
                </div>
            </div>

            <div id="regular-display-area">
                <!-- Dynamic Content Loaded Here -->
                <div class="card">
                    <h3>示例：Hablar (说) -AR结尾规则动词</h3>
                    <p class="text-muted">点击上方按钮切换不同类型的动词示例。</p>
                    <div id="reg-table-container"></div>
                </div>
            </div>
        </div>

        <!-- 2. 不规则动词模块 -->
        <div id="irregular" class="section">
            <div class="card">
                <h2>不规则动词分类 (Verbos Irregulares)</h2>
                <p>不规则动词通常分为“有规律的不规则”（如元音变化）和“完全不规则”（无规律可循）。</p>
            </div>

            <div class="verb-grid">
                <div class="card">
                    <h3>1. 词根元音变化 (Cambio Vocálico)</h3>
                    <p>重音落在词根上时发生变化 (Nosotros/Vosotros 除外)。</p>
                    <ul>
                        <li><strong>e → ie</strong>: Pensar, Querer, Sentir, Empezar, Perder <span class="tag tag-e-ie">e-ie</span></li>
                        <li><strong>o → ue</strong>: Poder, Contar, Dormir, Volver, Encontrar <span class="tag tag-o-ue">o-ue</span></li>
                        <li><strong>e → i</strong>: Pedir, Servir, Repetir, Vestir <span class="tag tag-e-i">e-i</span></li>
                    </ul>
                    <button class="btn-outline" onclick="showIrregDetails('stem')">查看变位示例</button>
                </div>

                <div class="card">
                    <h3>2. 仅第一人称单数不规则 (Yo-Go等)</h3>
                    <p>仅在陈述式现在时 "Yo" 发生变化，通常影响虚拟式。</p>
                    <ul>
                        <li><strong>-go</strong>: Hacer (hago), Poner (pongo), Salir (salgo), Traer (traigo)</li>
                        <li><strong>-zco</strong> (元音+cer/cir): Conocer (conozco), Traducir (traduzco)</li>
                        <li><strong>Otros</strong>: Saber (sé), Ver (veo), Dar (doy)</li>
                    </ul>
                    <button class="btn-outline" onclick="showIrregDetails('yo')">查看变位示例</button>
                </div>

                <div class="card">
                    <h3>3. 完全不规则 (Totalmente Irregulares)</h3>
                    <p>必须死记硬背，没有通用规律，但在不同时态间有内部联系。</p>
                    <ul>
                        <li><strong>Ser</strong> (是), <strong>Estar</strong> (在), <strong>Ir</strong> (去)</li>
                        <li><strong>Haber</strong> (有/辅助), <strong>Tener</strong> (拥有)</li>
                        <li><strong>Decir</strong> (说), <strong>Venir</strong> (来)</li>
                    </ul>
                    <button class="btn-outline" onclick="showIrregDetails('total')">查看所有完全不规则</button>
                </div>
            </div>
            
            <div id="irreg-detail-area" style="margin-top:20px;"></div>
        </div>

        <!-- 3. 测试模块 -->
        <div id="quiz" class="section">
            <div class="quiz-container">
                <div class="quiz-card">
                    <div class="quiz-info">
                        <span id="q-tense" class="tag" style="background:#333; font-size:1em; padding:5px 10px;">Presente</span>
                        <br><br>
                        <span id="q-pronoun" style="color:var(--primary); font-weight:bold;">Yo</span>
                    </div>
                    <div id="q-verb" class="quiz-verb">Hablar</div>
                    
                    <div class="char-keys">
                        <button class="char-key" onclick="addChar('á')">á</button>
                        <button class="char-key" onclick="addChar('é')">é</button>
                        <button class="char-key" onclick="addChar('í')">í</button>
                        <button class="char-key" onclick="addChar('ó')">ó</button>
                        <button class="char-key" onclick="addChar('ú')">ú</button>
                        <button class="char-key" onclick="addChar('ñ')">ñ</button>
                    </div>

                    <input type="text" id="q-input" class="quiz-input" placeholder="输入变位..." autocomplete="off">
                    
                    <div>
                        <button id="btn-check" class="btn" onclick="checkAnswer()">检查答案</button>
                        <button id="btn-next" class="btn btn-secondary" onclick="nextQuestion()" style="display:none;">下一题</button>
                    </div>

                    <div id="q-feedback" class="feedback-msg"></div>
                </div>
            </div>
        </div>

        <!-- 4. 错题记录模块 -->
        <div id="records" class="section">
            <div class="card">
                <div style="display:flex; justify-content:space-between; align-items:center;">
                    <h2>错题本 (Registro de Errores)</h2>
                    <button class="btn-outline" onclick="clearRecords()" style="font-size:0.8em;">清空记录</button>
                </div>
                <p>这里记录了你在测试中出错的动词。系统会自动生成例句帮助你记忆。</p>
                <div id="error-list">
                    <!-- Errors injected here -->
                </div>
            </div>
        </div>

    </div>

<script>
    // --- DATA ENGINE ---
    
    // 动词库：包含原形、翻译、类型、变位数据（如果是不规则）
    const verbsDB = {
        // Regular Models
        'hablar': { trans: '说', type: 'reg-ar' },
        'comer': { trans: '吃', type: 'reg-er' },
        'vivir': { trans: '生活', type: 'reg-ir' },
        'estudiar': { trans: '学习', type: 'reg-ar' },
        'beber': { trans: '喝', type: 'reg-er' },
        'escribir': { trans: '写', type: 'reg-ir' },

        // Irregular Patterns
        'pensar': { trans: '想', type: 'ie', stem: 'pens' },
        'poder': { trans: '能够', type: 'ue', stem: 'pod' },
        'pedir': { trans: '请求', type: 'i', stem: 'ped' },
        'hacer': { trans: '做', type: 'g-yo' },
        'conocer': { trans: '认识', type: 'zc-yo' },

        // Total Irregular (Hardcoded for simplicity in this demo version)
        'ser': { 
            trans: '是', type: 'total',
            forms: {
                'Presente': ['soy','eres','es','somos','sois','son'],
                'Indefinido': ['fui','fuiste','fue','fuimos','fuisteis','fueron'],
                'Imperfecto': ['era','eras','era','éramos','erais','eran'],
                'Futuro': ['seré','serás','será','seremos','seréis','serán']
            }
        },
        'ir': {
            trans: '去', type: 'total',
            forms: {
                'Presente': ['voy','vas','va','vamos','vais','van'],
                'Indefinido': ['fui','fuiste','fue','fuimos','fuisteis','fueron'],
                'Imperfecto': ['iba','ibas','iba','íbamos','ibais','iban'],
                'Futuro': ['iré','irás','irá','iremos','iréis','irán']
            }
        },
        'estar': {
            trans: '在', type: 'total',
            forms: {
                'Presente': ['estoy','estás','está','estamos','estáis','están'],
                'Indefinido': ['estuve','estuviste','estuvo','estuvimos','estuvisteis','estuvieron']
            }
        },
        'tener': {
            trans: '拥有', type: 'total',
            forms: {
                'Presente': ['tengo','tienes','tiene','tenemos','tenéis','tienen'],
                'Indefinido': ['tuve','tuviste','tuvo','tuvimos','tuvisteis','tuvieron'],
                'Futuro': ['tendré','tendrás','tendrá','tendremos','tendréis','tendrán']
            }
        }
    };

    // Regular Endings Map
    const regularEndings = {
        'ar': {
            'Presente': ['o', 'as', 'a', 'amos', 'áis', 'an'],
            'Indefinido': ['é', 'aste', 'ó', 'amos', 'asteis', 'aron'],
            'Imperfecto': ['aba', 'abas', 'aba', 'ábamos', 'abais', 'aban'],
            'Futuro': ['aré', 'arás', 'ará', 'aremos', 'aréis', 'arán'],
            'Condicional': ['aría', 'arías', 'aría', 'aríamos', 'aríais', 'arían'],
            'Subjuntivo Presente': ['e', 'es', 'e', 'emos', 'éis', 'en']
        },
        'er': {
            'Presente': ['o', 'es', 'e', 'emos', 'éis', 'en'],
            'Indefinido': ['í', 'iste', 'ió', 'imos', 'isteis', 'ieron'],
            'Imperfecto': ['ía', 'ías', 'ía', 'íamos', 'íais', 'ían'],
            'Futuro': ['eré', 'erás', 'erá', 'eremos', 'eréis', 'erán'],
            'Condicional': ['ería', 'erías', 'ería', 'eríamos', 'eríais', 'erían'],
            'Subjuntivo Presente': ['a', 'as', 'a', 'amos', 'áis', 'an']
        },
        'ir': {
            'Presente': ['o', 'es', 'e', 'imos', 'ís', 'en'],
            'Indefinido': ['í', 'iste', 'ió', 'imos', 'isteis', 'ieron'],
            'Imperfecto': ['ía', 'ías', 'ía', 'íamos', 'íais', 'ían'],
            'Futuro': ['iré', 'irás', 'irá', 'iremos', 'iréis', 'irán'],
            'Condicional': ['iría', 'irías', 'iría', 'iríamos', 'iríais', 'irían'],
            'Subjuntivo Presente': ['a', 'as', 'a', 'amos', 'áis', 'an']
        }
    };

    const pronouns = ['Yo', 'Tú', 'Él/Ella/Usted', 'Nosotros', 'Vosotros', 'Ellos/Ustedes'];

    // --- LOGIC ENGINE ---

    function conjugate(verb, tense, personIndex) {
        const vData = verbsDB[verb];
        
        // 1. Handle Totally Irregular
        if (vData.type === 'total') {
            if (vData.forms[tense]) return vData.forms[tense][personIndex];
            // Fallback to regular generation if tense not explicitly listed as irreg
        }

        const ending = verb.slice(-2);
        const stem = verb.slice(0, -2);
        const suffix = regularEndings[ending][tense][personIndex];

        // 2. Handle Stem Changing (e-ie, o-ue, e-i) in Presente
        if (tense === 'Presente' && (personIndex !== 3 && personIndex !== 4)) { // Not nosotros/vosotros
            if (vData.type === 'ie') return stem.replace(/e(?!.*e)/, 'ie') + suffix;
            if (vData.type === 'ue') return stem.replace(/o(?!.*o)/, 'ue') + suffix;
            if (vData.type === 'i') return stem.replace(/e(?!.*e)/, 'i') + suffix;
        }

        // 3. Handle Yo-Go / ZC in Presente Yo
        if (tense === 'Presente' && personIndex === 0) {
            if (vData.type === 'g-yo') return stem + 'go';
            if (vData.type === 'zc-yo') return stem.slice(0,-1) + 'zco';
        }

        // 4. Regular Fallback
        return stem + suffix;
    }

    function generateTableHTML(verb, title) {
        const tenses = ['Presente', 'Indefinido', 'Imperfecto', 'Futuro', 'Subjuntivo Presente'];
        let html = `<h3>${title} (${verbsDB[verb].trans})</h3><div class="verb-grid">`;
        
        tenses.forEach(tense => {
            html += `<div class="card" style="padding:15px;"><h4>${tense}</h4><table class="conjugation-table">`;
            pronouns.forEach((p, i) => {
                const form = conjugate(verb, tense, i);
                // Simple highlighting logic: stem + ending
                // For totally irregulars, we just show the word. For regulars, we try to bold ending.
                let displayForm = form;
                if(verbsDB[verb].type.startsWith('reg')) {
                    const stem = verb.slice(0,-2);
                    if(form.startsWith(stem)) {
                        const ending = form.slice(stem.length);
                        displayForm = `<span class="highlight-root">${stem}</span><span class="highlight-ending">${ending}</span>`;
                    }
                } else {
                     displayForm = `<span class="highlight-ending">${form}</span>`;
                }

                html += `<tr><td>${p}</td><td>${displayForm}</td></tr>`;
            });
            html += `</table></div>`;
        });
        html += `</div>`;
        return html;
    }

    // --- UI FUNCTIONS ---

    function switchTab(tabId) {
        document.querySelectorAll('.section').forEach(el => el.classList.remove('active'));
        document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
        
        document.getElementById(tabId).classList.add('active');
        document.querySelector(`.nav-item[onclick="switchTab('${tabId}')"]`).classList.add('active');

        if(tabId === 'quiz') loadNewQuestion();
        if(tabId === 'records') renderRecords();
    }

    function showRegularTable(type) {
        const verbs = {
            'ar': 'hablar',
            'er': 'comer',
            'ir': 'vivir'
        };
        const container = document.getElementById('reg-table-container');
        container.innerHTML = generateTableHTML(verbs[type], verbs[type].charAt(0).toUpperCase() + verbs[type].slice(1));
    }

    function showIrregDetails(category) {
        const container = document.getElementById('irreg-detail-area');
        let verbsToShow = [];
        
        if (category === 'stem') verbsToShow = ['pensar', 'poder', 'pedir'];
        else if (category === 'yo') verbsToShow = ['hacer', 'conocer'];
        else if (category === 'total') verbsToShow = ['ser', 'ir', 'tener', 'estar'];

        let html = '';
        verbsToShow.forEach(v => {
            html += generateTableHTML(v, v.toUpperCase());
        });
        container.innerHTML = html;
        // Scroll to details
        container.scrollIntoView({behavior: "smooth"});
    }

    // --- QUIZ & RECORDS LOGIC ---

    let currentQ = {};
    let records = JSON.parse(localStorage.getItem('verbTrainerRecords')) || [];

    function loadNewQuestion() {
        const verbKeys = Object.keys(verbsDB);
        const verb = verbKeys[Math.floor(Math.random() * verbKeys.length)];
        const tenses = ['Presente', 'Indefinido', 'Imperfecto', 'Futuro']; // Keep simple for now
        
        // Check if verb has total irregular forms defined for this tense, otherwise skip if total irregular
        // Simplification: Just retry if total irregular doesn't have that tense defined in my mini DB
        let tense = tenses[Math.floor(Math.random() * tenses.length)];
        const personIdx = Math.floor(Math.random() * 6);

        // Edge case: if total irreg doesn't have tense in DB, swap to Presente
        if(verbsDB[verb].type === 'total' && !verbsDB[verb].forms[tense]) {
            tense = 'Presente';
        }

        currentQ = { verb, tense, personIdx };

        document.getElementById('q-verb').innerText = verb + ` (${verbsDB[verb].trans})`;
        document.getElementById('q-tense').innerText = tense;
        document.getElementById('q-pronoun').innerText = pronouns[personIdx];
        
        const input = document.getElementById('q-input');
        input.value = '';
        input.disabled = false;
        input.focus();
        
        document.getElementById('q-feedback').innerHTML = '';
        document.getElementById('btn-check').style.display = 'inline-block';
        document.getElementById('btn-next').style.display = 'none';
    }

    function checkAnswer() {
        const userVal = document.getElementById('q-input').value.trim().toLowerCase();
        const correctVal = conjugate(currentQ.verb, currentQ.tense, currentQ.personIdx);

        const feedback = document.getElementById('q-feedback');
        const input = document.getElementById('q-input');

        if (userVal === correctVal) {
            feedback.innerHTML = '<span class="correct-text">¡Correcto! (正确)</span>';
            input.disabled = true;
            document.getElementById('btn-check').style.display = 'none';
            document.getElementById('btn-next').style.display = 'inline-block';
            document.getElementById('btn-next').focus();
        } else {
            feedback.innerHTML = `<span class="wrong-text">错误。正确答案是: ${correctVal}</span>`;
            saveError(currentQ.verb, currentQ.tense, currentQ.personIdx, correctVal);
            
            input.disabled = true;
            document.getElementById('btn-check').style.display = 'none';
            document.getElementById('btn-next').style.display = 'inline-block';
        }
    }

    function nextQuestion() {
        loadNewQuestion();
    }

    function addChar(char) {
        const input = document.getElementById('q-input');
        input.value += char;
        input.focus();
    }

    // Enable Enter key
    document.getElementById('q-input').addEventListener('keypress', function (e) {
        if (e.key === 'Enter') checkAnswer();
    });
    document.addEventListener('keypress', function(e) {
        if (e.key === 'Enter' && document.getElementById('btn-next').style.display !== 'none') {
            nextQuestion();
        }
    });

    // --- RECORD MANAGEMENT ---

    function saveError(verb, tense, pIdx, correct) {
        const record = {
            verb: verb,
            tense: tense,
            person: pronouns[pIdx],
            correct: correct,
            timestamp: new Date().getTime()
        };
        records.unshift(record); // Add to top
        if(records.length > 50) records.pop(); // Keep max 50
        localStorage.setItem('verbTrainerRecords', JSON.stringify(records));
    }

    function generateExampleSentence(verb, person, correct) {
        // Super simple sentence generator for context
        const contextMap = {
            'Yo': '___ (我) mucho.',
            'Tú': '¿Por qué no ___ (你)?',
            'Él/Ella/Usted': '___ (他/她) hoy.',
            'Nosotros': '___ (我们) en casa.',
            'Vosotros': '___ (你们) bien.',
            'Ellos/Ustedes': 'No ___ (他们) nunca.'
        };
        let template = contextMap[person] || '___ ...';
        return template.replace('___', `<span style="color:var(--primary); font-weight:bold;">${correct}</span>`);
    }

    function renderRecords() {
        const list = document.getElementById('error-list');
        if (records.length === 0) {
            list.innerHTML = '<p style="color:#888; text-align:center;">暂无错题记录。去测试区练习吧！</p>';
            return;
        }

        let html = '';
        records.forEach(rec => {
            const sentence = generateExampleSentence(rec.verb, rec.person, rec.correct);
            html += `
                <div class="error-item">
                    <div class="error-details">
                        <div class="error-verb">${rec.verb} (${verbsDB[rec.verb].trans}) - <small>${rec.tense} | ${rec.person}</small></div>
                        <div class="error-correction">正确变位: ${rec.correct}</div>
                        <div class="error-context">例句: ${sentence}</div>
                    </div>
                </div>
            `;
        });
        list.innerHTML = html;
    }

    function clearRecords() {
        if(confirm('确定要清空所有错题记录吗？')) {
            records = [];
            localStorage.setItem('verbTrainerRecords', JSON.stringify([]));
            renderRecords();
        }
    }

    // Initialize View
    showRegularTable('ar'); // Preload a table
</script>

</body>
</html>
