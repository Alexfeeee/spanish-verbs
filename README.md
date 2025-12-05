<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>西语动词大师 (Versión Definitiva)</title>
    <style>
        :root {
            --primary: #b71c1c; /* 经典红 */
            --primary-light: #ff8a80;
            --secondary: #f9a825; /* 经典黄 */
            --text: #263238;
            --text-light: #546e7a;
            --bg: #f5f5f5;
            --white: #ffffff;
            --hover-row: #fff3e0;
            --border: #e0e0e0;
            --accent-irreg: #1565c0; /* 不规则部分蓝色 */
            --accent-ending: #d32f2f; /* 词尾红色 */
        }

        body {
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            margin: 0;
            display: flex;
            flex-direction: column;
            height: 100vh;
        }

        /* --- 导航栏 --- */
        nav {
            background: var(--primary);
            color: white;
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
            z-index: 100;
        }
        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            height: 60px;
        }
        .nav-title { font-size: 1.3rem; font-weight: bold; display: flex; align-items: center; gap: 10px; }
        .nav-tabs { display: flex; gap: 5px; height: 100%; }
        .nav-item {
            padding: 0 20px;
            height: 100%;
            display: flex;
            align-items: center;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.2s;
            border-bottom: 4px solid transparent;
            opacity: 0.9;
        }
        .nav-item:hover { background: rgba(255,255,255,0.1); opacity: 1; }
        .nav-item.active { border-bottom-color: var(--secondary); opacity: 1; background: rgba(255,255,255,0.15); }

        /* --- 主布局 --- */
        main {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
            width: 100%;
            box-sizing: border-box;
        }

        .section { display: none; animation: fadeIn 0.3s ease; }
        .section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }

        /* --- 卡片与排版 --- */
        .card {
            background: var(--white);
            border-radius: 8px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
            padding: 25px;
            margin-bottom: 25px;
        }
        h2 { margin-top: 0; color: var(--primary); border-left: 5px solid var(--secondary); padding-left: 15px; }
        h3 { 
            color: var(--text); 
            margin: 30px 0 20px 0; 
            font-size: 1.3rem; 
            border-bottom: 2px solid var(--primary); 
            padding-bottom: 8px; 
            display: inline-block;
        }
        h4 { color: var(--text-light); margin: 20px 0 10px 0; font-size: 1rem; font-weight: 700; letter-spacing: 0.5px; }
        
        /* --- 变位选择器 --- */
        .verb-selector {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-bottom: 20px;
            padding: 15px;
            background: #fff;
            border-radius: 8px;
            border: 1px solid var(--border);
        }
        .verb-btn {
            background: #f5f5f5;
            border: 1px solid #ddd;
            padding: 8px 16px;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.2s;
            font-size: 0.9rem;
        }
        .verb-btn:hover { border-color: var(--primary); color: var(--primary); }
        .verb-btn.active { background: var(--primary); color: white; border-color: var(--primary); }

        /* --- 变位表格系统 --- */
        .tense-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }
        .tense-card {
            background: var(--white);
            border: 1px solid var(--border);
            border-radius: 6px;
            overflow: hidden;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        .tense-header {
            background: #fafafa;
            padding: 12px 15px;
            font-weight: bold;
            color: var(--primary);
            border-bottom: 1px solid var(--border);
            font-size: 1rem;
            text-align: center;
        }
        
        .cj-table { width: 100%; border-collapse: collapse; font-size: 0.95rem; }
        .cj-table td { padding: 10px 15px; border-bottom: 1px solid #f0f0f0; }
        .cj-table tr:last-child td { border-bottom: none; }
        .cj-table tr:hover { background-color: var(--hover-row); }
        
        .pronoun-col { color: #999; width: 30%; font-size: 0.85rem; background-color: #fcfcfc; border-right: 1px solid #f0f0f0; }
        .verb-col { color: var(--text); font-family: 'Georgia', serif; font-weight: 500; }

        /* 颜色教学系统 */
        .root { color: #000; }
        .ending { color: var(--accent-ending); font-weight: bold; }
        .irreg { color: var(--accent-irreg); font-weight: bold; }
        .aux { color: #666; font-size: 0.95em; } 
        .participle { color: var(--text); font-weight: bold; }

        /* 非人称形式特别展示 */
        .np-container {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
        }
        .np-card {
            flex: 1;
            background: #e3f2fd;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
            border: 1px solid #bbdefb;
        }
        .np-label { display: block; color: #1565c0; font-size: 0.9rem; margin-bottom: 8px; text-transform: uppercase; letter-spacing: 1px; font-weight: bold;}
        .np-val { font-size: 1.5rem; color: #333; font-family: 'Georgia', serif;}

        /* --- 练习与记录 --- */
        .quiz-container { text-align: center; max-width: 600px; margin: 40px auto; }
        .quiz-input { 
            font-size: 1.4rem; padding: 10px; width: 100%; text-align: center; 
            border: 2px solid #ddd; border-radius: 8px; margin: 15px 0;
        }
        .quiz-input:focus { border-color: var(--primary); outline: none; }
        .btn-action {
            background: var(--primary); color: white; border: none; padding: 12px 30px;
            border-radius: 6px; font-size: 1rem; cursor: pointer;
        }
        .char-bar button { background: #fff; border: 1px solid #ccc; padding: 8px 12px; margin: 2px; border-radius: 4px; cursor: pointer; }
        
        .record-item {
            border-left: 4px solid var(--primary);
            background: #fff;
            padding: 15px;
            margin-bottom: 10px;
            box-shadow: 0 1px 2px rgba(0,0,0,0.05);
        }

    </style>
</head>
<body>

<nav>
    <div class="nav-container">
        <div class="nav-title">🇪🇸 变位大师 Pro</div>
        <ul class="nav-tabs">
            <li class="nav-item active" onclick="switchTab('learn', this)">系统学习 (Estudio)</li>
            <li class="nav-item" onclick="switchTab('quiz', this)">强化测试 (Prueba)</li>
            <li class="nav-item" onclick="switchTab('records', this)">错题本 (Errores)</li>
        </ul>
    </div>
</nav>

<main>

    <!-- 1. 系统学习模块 -->
    <div id="learn" class="section active">
        <div class="card">
            <h2 style="margin-bottom: 20px;">选择动词 (Seleccionar Verbo)</h2>
            
            <div class="verb-selector">
                <span style="width:100%; color:#666; font-size:0.9em; margin-bottom:5px;">规则动词 (Regulares)</span>
                <button class="verb-btn active" onclick="loadVerb('hablar')">Hablar (-AR)</button>
                <button class="verb-btn" onclick="loadVerb('comer')">Comer (-ER)</button>
                <button class="verb-btn" onclick="loadVerb('vivir')">Vivir (-IR)</button>
            </div>
            
            <div class="verb-selector">
                <span style="width:100%; color:#666; font-size:0.9em; margin-bottom:5px;">不规则动词 (Irregulares)</span>
                <button class="verb-btn" onclick="loadVerb('pensar')">Pensar (e-ie)</button>
                <button class="verb-btn" onclick="loadVerb('poder')">Poder (o-ue)</button>
                <button class="verb-btn" onclick="loadVerb('hacer')">Hacer (Yo-Go)</button>
                <button class="verb-btn" onclick="loadVerb('ser')">Ser (Total)</button>
                <button class="verb-btn" onclick="loadVerb('ir')">Ir (Total)</button>
                <button class="verb-btn" onclick="loadVerb('estar')">Estar (Total)</button>
                <button class="verb-btn" onclick="loadVerb('tener')">Tener (Total)</button>
            </div>
        </div>

        <div id="conjugation-view">
            <!-- 动态生成的内容将填充于此 -->
        </div>
    </div>

    <!-- 2. 测试模块 -->
    <div id="quiz" class="section">
        <div class="card quiz-container">
            <h2>全时态变位挑战</h2>
            <div style="color:#666; margin-bottom:20px;" id="q-meta">加载中...</div>
            <div style="font-size:3rem; color:var(--primary); font-weight:bold; margin:10px 0;" id="q-verb">...</div>
            
            <div class="char-bar">
                <button onclick="addChar('á')">á</button>
                <button onclick="addChar('é')">é</button>
                <button onclick="addChar('í')">í</button>
                <button onclick="addChar('ó')">ó</button>
                <button onclick="addChar('ú')">ú</button>
                <button onclick="addChar('ñ')">ñ</button>
            </div>

            <input type="text" id="q-input" class="quiz-input" placeholder="输入变位..." autocomplete="off">
            <div id="q-feedback" style="height:30px; font-weight:bold; margin-bottom:10px;"></div>
            
            <button class="btn-action" onclick="checkAnswer()">提交 (Enter)</button>
            <button style="background:none; border:none; color:#999; cursor:pointer; margin-left:10px;" onclick="nextQuestion()">跳过</button>
        </div>
    </div>

    <!-- 3. 错题本 -->
    <div id="records" class="section">
        <div class="card">
            <div style="display:flex; justify-content:space-between; align-items:center;">
                <h2>错题记录本</h2>
                <button class="verb-btn" onclick="clearRecords()">清空所有</button>
            </div>
            <p style="color:#666; margin-bottom:20px;">这里记录了你在测试中出错的词汇。</p>
            <div id="records-list"></div>
        </div>
    </div>

</main>

<script>
/**
 * --- 1. 核心数据 (Data Definition) ---
 */

const pronouns = ['Yo', 'Tú', 'Él/Ella/Usted', 'Nosotros/as', 'Vosotros/as', 'Ellos/as/Ustedes'];

// 规则词尾 (Regular Endings) - 涵盖所有16种时态情况
const regularEndings = {
    ar: {
        pres: ['o','as','a','amos','áis','an'],
        imp: ['aba','abas','aba','ábamos','abais','aban'],
        pret: ['é','aste','ó','amos','asteis','aron'],
        fut: ['aré','arás','ará','aremos','aréis','arán'],
        cond: ['aría','arías','aría','aríamos','aríais','arían'],
        sub_pres: ['e','es','e','emos','éis','en'],
        sub_imp1: ['ara','aras','ara','áramos','arais','aran'],
        sub_fut: ['are','ares','are','áremos','areis','aren'],
        part: 'ado', ger: 'ando'
    },
    er: {
        pres: ['o','es','e','emos','éis','en'],
        imp: ['ía','ías','ía','íamos','íais','ían'],
        pret: ['í','iste','ió','imos','isteis','ieron'],
        fut: ['eré','erás','erá','eremos','eréis','erán'],
        cond: ['ería','erías','ería','eríamos','eríais','erían'],
        sub_pres: ['a','as','a','amos','áis','an'],
        sub_imp1: ['iera','ieras','iera','iéramos','ierais','ieran'],
        sub_fut: ['iere','ieres','iere','iéremos','iereis','ieren'],
        part: 'ido', ger: 'iendo'
    },
    ir: {
        pres: ['o','es','e','imos','ís','en'],
        imp: ['ía','ías','ía','íamos','íais','ían'],
        pret: ['í','iste','ió','imos','isteis','ieron'],
        fut: ['iré','irás','irá','iremos','iréis','irán'],
        cond: ['iría','irías','iría','iríamos','iríais','irían'],
        sub_pres: ['a','as','a','amos','áis','an'],
        sub_imp1: ['iera','ieras','iera','iéramos','ierais','ieran'],
        sub_fut: ['iere','ieres','iere','iéremos','iereis','ieren'],
        part: 'ido', ger: 'iendo'
    }
};

// 助动词 Haber Forms (用于复合时态)
const haberForms = {
    pres: ['he','has','ha','hemos','habéis','han'],
    imp: ['había','habías','había','habíamos','habíais','habían'],
    pret: ['hube','hubiste','hubo','hubimos','hubisteis','hubieron'], // 用于先过去时
    fut: ['habré','habrás','habrá','habremos','habréis','habrán'],
    cond: ['habría','habrías','habría','habríamos','habríais','habrían'],
    sub_pres: ['haya','hayas','haya','hayamos','hayáis','hayan'],
    sub_imp: ['hubiera','hubieras','hubiera','hubiéramos','hubierais','hubieran'],
    sub_fut: ['hubiere','hubieres','hubiere','hubiéremos','hubiereis','hubieren']
};

// 动词库
const verbsDB = {
    hablar: { trans: '说', type: 'reg', end: 'ar' },
    comer: { trans: '吃', type: 'reg', end: 'er' },
    vivir: { trans: '生活', type: 'reg', end: 'ir' },
    pensar: { trans: '想', type: 'stem', end: 'ar', rule: 'e-ie' },
    
    // PODER FIX: 定义为完全不规则，覆盖所有时态
    poder: {
        trans: '能够', type: 'total', end: 'er',
        // 完整且准确的主要时态（手工列出以避免引擎回退错误）
        forms: {
            pres: ['puedo','puedes','puede','podemos','podéis','pueden'],
            imp: ['podía','podías','podía','podíamos','podíais','podían'],
            pret: ['pude','pudiste','pudo','pudimos','pudisteis','pudieron'],
            fut: ['podré','podrás','podrá','podremos','podréis','podrán'],
            cond: ['podría','podrías','podría','podríamos','podríais','podrían'],
            sub_pres: ['pueda','puedas','pueda','podamos','podáis','puedan'],
            sub_imp1: ['pudiera','pudieras','pudiera','pudiéramos','pudierais','pudieran'],
            sub_fut: ['pudiere','pudieres','pudiere','pudiéremos','pudiereis','pudieren'],
            // 肯定命令式（对应 pronouns 索引; index 0 (Yo) 被跳过）
            imp_af: ['-','puede','pueda','podamos','poded','puedan'],
            // 提供否定命令式（部分浏览器/地区习惯更明确）
            imp_neg: ['no pueda','no puedas','no pueda','no podamos','no podáis','no puedan']
        },
        ger: 'pudiendo', // 副动词
        part: 'podido'   // 过去分词
    },
    
    jugar: { trans: '玩', type: 'stem', end: 'ar', rule: 'u-ue' },
    pedir: { trans: '请求', type: 'stem', end: 'ir', rule: 'e-i' },
    hacer: { trans: '做', type: 'yoga', end: 'er', yo: 'hago', part: 'hecho' },
    conocer: { trans: '认识', type: 'yoga', end: 'er', yo: 'conozco' },
    dar: { trans: '给', type: 'yoga', end: 'ar', yo: 'doy', sub_pres: ['dé','des','dé','demos','deis','den'] },

    ser: { trans: '是', type: 'total', end: 'er', forms: {
        pres: ['soy','eres','es','somos','sois','son'],
        imp: ['era','eras','era','éramos','erais','eran'],
        pret: ['fui','fuiste','fue','fuimos','fuisteis','fueron'],
        sub_pres: ['sea','seas','sea','seamos','seáis','sean'],
        imp_af: ['-','sé','sea','seamos','sed','sean']
    }},
    estar: { trans: '在', type: 'total', end: 'ar', forms: {
        pres: ['estoy','estás','está','estamos','estáis','están'],
        pret: ['estuve','estuviste','estuvo','estuvimos','estuvisteis','estuvieron'],
        sub_pres: ['esté','estés','esté','estemos','estéis','estén']
    }},
    ir: { trans: '去', type: 'total', end: 'ir', forms: {
        pres: ['voy','vas','va','vamos','vais','van'],
        imp: ['iba','ibas','iba','íbamos','ibais','iban'],
        pret: ['fui','fuiste','fue','fuimos','fuisteis','fueron'],
        sub_pres: ['vaya','vayas','vaya','vayamos','vayáis','vayan'],
        imp_af: ['-','ve','vaya','vayamos','id','vayan']
    }},
    tener: { trans: '拥有', type: 'total', end: 'er', forms: {
        pres: ['tengo','tienes','tiene','tenemos','tenéis','tienen'],
        pret: ['tuve','tuviste','tuvo','tuvimos','tuvisteis','tuvieron'],
        fut: ['tendré','tendrás','tendrá','tendremos','tendréis','tendrán'],
        cond: ['tendría','tendrías','tendría','tendríamos','tendríais','tendrían'],
        sub_pres: ['tenga','tengas','tenga','tengamos','tengáis','tengan'],
        imp_af: ['-','ten','tenga','tengamos','tened','tengan']
    }},
    haber: { trans: '有(辅助)', type: 'total', end: 'er', forms: {
        pres: ['he','has','ha','hemos','habéis','han'],
        pret: ['hube','hubiste','hubo','hubimos','hubisteis','hubieron'],
        fut: ['habré','habrás','habrá','habremos','habréis','habrán'],
        cond: ['habría','habrías','habría','habríamos','habríais','habrían'],
        sub_pres: ['haya','hayas','haya','hayamos','hayáis','hayan']
    }}
};

// 结构化时态分类 (按用户要求严格分组)
const structure = [
    {
        header: '陈述式 (Modo Indicativo)',
        sections: [
            {
                title: '时态列表',
                tenses: ['pres', 'comp_pres', 'imp', 'comp_imp', 'pret', 'comp_pret', 'fut', 'comp_fut']
            }
        ]
    },
    {
        header: '条件式 (Modo Condicional)',
        sections: [
            {
                title: '时态列表',
                tenses: ['cond', 'comp_cond']
            }
        ]
    },
    {
        header: '虚拟式 (Modo Subjuntivo)',
        sections: [
            {
                title: '时态列表',
                tenses: ['sub_pres', 'sub_comp_pres', 'sub_imp1', 'sub_comp_imp', 'sub_fut', 'sub_comp_fut']
            }
        ]
    },
    {
        header: '命令式 (Modo Imperativo)',
        sections: [
            {
                title: '形式',
                tenses: ['imp_af', 'imp_neg']
            }
        ]
    },
    {
        header: '非人称形式 (Formas no personales)',
        special: true
    }
];

// 时态名称映射 (严格对应用户需求)
const tenseLabels = {
    pres: '现在时 (Presente)',
    comp_pres: '现在完成时 (Perfecto)',
    imp: '过去未完成时 (Imperfecto)',
    comp_imp: '过去完成时 (Pluscuamperfecto)',
    pret: '简单过去时 (Indefinido)',
    comp_pret: '近逾/先过去时 (Anterior)', 
    fut: '将来未完成时 (Futuro)',
    comp_fut: '将来完成时 (Futuro Perfecto)',
    cond: '简单条件式 (Condicional Simple)',
    comp_cond: '复合条件式 (Condicional Compuesto)',
    sub_pres: '现在时 (Subj. Presente)',
    sub_comp_pres: '现在完成时 (Subj. Perfecto)',
    sub_imp1: '过去未完成时 (Imperfecto -ra)',
    sub_comp_imp: '过去完成时 (Subj. Pluscuamperfecto)',
    sub_fut: '将来未完成时 (Subj. Futuro)',
    sub_comp_fut: '将来完成时 (Subj. Futuro Perfecto)',
    imp_af: '肯定形式 (Afirmativo)',
    imp_neg: '否定形式 (Negativo)'
};

/**
 * --- 2. 变位逻辑引擎 (Logic Engine) ---
 */

function getParticiple(verb) {
    const vData = verbsDB[verb];
    if(!vData) return 'Error';
    if(vData.part) return vData.part;
    // Common Irregulars
    if(verb==='hacer') return 'hecho';
    if(verb==='ver') return 'visto';
    if(verb==='decir') return 'dicho';
    if(verb==='volver') return 'vuelto';
    if(verb==='escribir') return 'escrito';
    if(verb==='poner') return 'puesto';
    if(verb==='morir') return 'muerto';
    if(verb==='abrir') return 'abierto';
    if(verb==='romper') return 'roto';
    
    return verb.slice(0,-2) + regularEndings[vData.end].part;
}

function getGerund(verb) {
    const vData = verbsDB[verb];
    if(!vData) return 'Error';
    
    if(vData.ger) return vData.ger; // Explicit override (e.g. poder -> pudiendo)

    const stem = verb.slice(0,-2);
    // Simple stem changing rules for gerund
    if(vData.end === 'ir' && (vData.rule === 'e-ie' || vData.rule === 'e-i')) return stem.replace(/e(?!.*e)/, 'i') + 'iendo';
    if(verb === 'dormir') return stem.replace(/o(?!.*o)/, 'u') + 'iendo';
    if(verb === 'ir') return 'yendo';
    if(verb === 'leer') return 'leyendo';
    return stem + regularEndings[vData.end].ger;
}

function conjugate(verb, tense, pIdx) {
    const vData = verbsDB[verb];
    if(!vData) return 'Error';

    // 1. 处理复合时态 (Compound)
    if(tense.includes('comp_')) {
        const pp = getParticiple(verb);
        let auxKey = tense.replace('comp_', '');
        // Mapping adjustments for special keys
        if(tense === 'sub_comp_pres') auxKey = 'sub_pres';
        if(tense === 'sub_comp_imp') auxKey = 'sub_imp';
        if(tense === 'sub_comp_fut') auxKey = 'sub_fut';
        if(tense === 'comp_cond') auxKey = 'cond';
        if(tense === 'comp_pret') auxKey = 'pret'; // Anterior uses Pret of Haber
        
        const aux = haberForms[auxKey] ? haberForms[auxKey][pIdx] : '???';
        return `<span class="aux">${aux}</span> <span class="participle">${pp}</span>`;
    }

    // 2. 完全不规则 (Total Irregular)
    if (vData.type === 'total' && vData.forms && vData.forms[tense]) {
        const form = vData.forms[tense][pIdx];
        if(form) return `<span class="irreg">${form}</span>`;
        // Fallthrough if specific tense form is missing in total irreg def (should be caught by data)
    }

    // 3. 规则回退 (Regular Fallback)
    const endingType = vData.end;
    const stem = verb.slice(0, -2);
    let suffix = regularEndings[endingType][tense] ? regularEndings[endingType][tense][pIdx] : '';
    let currStem = stem;
    let isIrreg = false;

    // 命令式特殊处理
    if (tense === 'imp_af') {
        if (pIdx === 1) { // Tú
            const shorts = {decir:'di', hacer:'haz', ir:'ve', poner:'pon', salir:'sal', ser:'sé', tener:'ten', venir:'ven'};
            if (shorts[verb]) return `<span class="irreg">${shorts[verb]}</span>`;
            let regSuffix = endingType === 'ar' ? 'a' : 'e';
            return `<span class="root">${stem}</span><span class="ending">${regSuffix}</span>`;
        }
        if (pIdx === 4) return `<span class="root">${stem}</span><span class="ending">d</span>`; // Vosotros
        // Others borrow from Subj Present
        return conjugate(verb, 'sub_pres', pIdx);
    }
    if (tense === 'imp_neg') {
        let subForm = conjugate(verb, 'sub_pres', pIdx);
        let clean = subForm.replace(/<[^>]*>/g, '');
        return `<span class="aux">no</span> <span class="root">${clean}</span>`;
    }

    // Stem Changing Logic
    if (vData.type === 'stem') {
        if ((tense === 'pres' || tense === 'sub_pres') && ![3,4].includes(pIdx)) {
            if (vData.rule === 'e-ie') currStem = stem.replace(/e(?!.*e)/, 'ie');
            if (vData.rule === 'o-ue') currStem = stem.replace(/o(?!.*o)/, 'ue');
            if (vData.rule === 'u-ue') currStem = stem.replace(/u(?!.*u)/, 'ue');
            if (vData.rule === 'e-i')  currStem = stem.replace(/e(?!.*e)/, 'i');
            if (currStem !== stem) isIrreg = true;
        }
    }

    // Yo-Go Logic
    if (vData.type === 'yoga' || vData.type === 'yo-zc') {
        if (tense === 'pres' && pIdx === 0) return `<span class="irreg">${vData.yo}</span>`;
        if (tense === 'sub_pres') {
            let yoBase = vData.yo.slice(0, -1);
            if (vData.yo === 'doy') yoBase = 'd';
            return `<span class="irreg">${yoBase}</span><span class="ending">${suffix}</span>`;
        }
    }

    if (isIrreg) return `<span class="irreg">${currStem}</span><span class="ending">${suffix}</span>`;
    return `<span class="root">${currStem}</span><span class="ending">${suffix}</span>`;
}

/* --- 渲染 --- */

function renderView(verb) {
    const container = document.getElementById('conjugation-view');
    const vData = verbsDB[verb];
    let html = `<div class="card"><h2>${verb.toUpperCase()} (${vData.trans})</h2></div>`;

    structure.forEach(block => {
        if (block.special) {
            // 非人称
            html += `<h3>${block.header}</h3><div class="np-container">
                <div class="np-card"><span class="np-label">过去分词 (Participio)</span><span class="np-val">${getParticiple(verb)}</span></div>
                <div class="np-card"><span class="np-label">副动词 (Gerundio)</span><span class="np-val">${getGerund(verb)}</span></div>
                <div class="np-card"><span class="np-label">原形动词 (Infinitivo)</span><span class="np-val">${verb}</span></div>
            </div>`;
        } else {
            html += `<h3>${block.header}</h3>`;
            block.sections.forEach(sec => {
                html += `<h4>${sec.title}</h4><div class="tense-grid">`;
                sec.tenses.forEach(t => {
                    html += `<div class="tense-card">
                        <div class="tense-header">${tenseLabels[t]}</div>
                        <table class="cj-table"><tbody>`;
                    
                    pronouns.forEach((p, idx) => {
                        if ((t === 'imp_af' || t === 'imp_neg') && idx === 0) return;
                        let res = conjugate(verb, t, idx);
                        html += `<tr><td class="pronoun-col">${p}</td><td class="verb-col">${res}</td></tr>`;
                    });
                    html += `</tbody></table></div>`;
                });
                html += `</div>`;
            });
        }
    });
    container.innerHTML = html;
    
    // Update buttons
    document.querySelectorAll('.verb-btn').forEach(b => b.classList.remove('active'));
    const btn = document.querySelector(`button[onclick="loadVerb('${verb}')"]`);
    if(btn) btn.classList.add('active');
}

function loadVerb(verb) { renderView(verb); }
function switchTab(id, el) {
    document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
    el.classList.add('active');
    if(id==='quiz') loadQuiz();
    if(id==='records') showRecords();
}

/* --- 测试系统 --- */
let qData = null;
let records = JSON.parse(localStorage.getItem('sp_pro_rec') || '[]');

function loadQuiz() {
    const keys = Object.keys(verbsDB);
    const verb = keys[Math.floor(Math.random()*keys.length)];
    // Flat list of testable tenses
    const tenses = ['pres','pret','imp','fut','cond','sub_pres','sub_imp1'];
    const tense = tenses[Math.floor(Math.random()*tenses.length)];
    let pIdx = Math.floor(Math.random()*6);
    qData = { verb, tense, pIdx };
    
    document.getElementById('q-verb').innerText = verb.toUpperCase();
    document.getElementById('q-meta').innerText = `${tenseLabels[tense]} - ${pronouns[pIdx]}`;
    document.getElementById('q-input').value = '';
    document.getElementById('q-feedback').innerText = '';
    document.getElementById('q-input').focus();
}

function checkAnswer() {
    if(!qData) return;
    const user = document.getElementById('q-input').value.trim().toLowerCase();
    const correctHtml = conjugate(qData.verb, qData.tense, qData.pIdx);
    const correct = correctHtml.replace(/<[^>]*>/g, '').toLowerCase().trim();
    
    const fb = document.getElementById('q-feedback');
    if(user === correct) {
        fb.innerHTML = '<span class="correct">¡Correcto!</span>';
        setTimeout(loadQuiz, 1000);
    } else {
        fb.innerHTML = `<span class="incorrect">Error. Respuesta: ${correct}</span>`;
        saveRecord(qData, correct);
    }
}

function saveRecord(q, ans) {
    const ctx = `${pronouns[q.pIdx]} <strong>${ans}</strong> (${q.verb})`;
    records.unshift({...q, ans, ctx, time: new Date().toLocaleDateString()});
    if(records.length > 50) records.pop();
    localStorage.setItem('sp_pro_rec', JSON.stringify(records));
}

function showRecords() {
    const div = document.getElementById('records-list');
    if(records.length === 0) {
        div.innerHTML = '<div style="text-align:center;color:#999;padding:20px;">暂无记录</div>';
        return;
    }
    let html = '';
    records.forEach(r => {
        html += `<div class="record-item">
            <div style="font-weight:bold;">${r.verb.toUpperCase()} - ${tenseLabels[r.tense]}</div>
            <div style="margin:5px 0; color:#d32f2f;">正确: ${r.ans}</div>
            <div style="background:#f5f5f5; padding:5px;">${r.ctx}</div>
        </div>`;
    });
    div.innerHTML = html;
}
function clearRecords() {
    if(confirm('Clear?')) {
        records = [];
        localStorage.setItem('sp_pro_rec', '[]');
        showRecords();
    }
}
function addChar(c) { 
    const i = document.getElementById('q-input');
    i.value += c; i.focus();
}
function nextQuestion() { loadQuiz(); }
document.getElementById('q-input').addEventListener('keypress', e => { if(e.key==='Enter') checkAnswer(); });

// Init
renderView('hablar');
</script>
</body>
</html>
