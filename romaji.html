<!doctype html>
<html lang="zh-CN">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>日语自动分句 + 罗马音 & Ruby 注音（含词典）</title>
<style>
  :root { --gap: 14px; --mono: ui-monospace,SFMono-Regular,Menlo,Consolas,"Liberation Mono",monospace; }
  body { font: 16px/1.6 system-ui,-apple-system,Segoe UI,Roboto,"Noto Sans CJK SC","Helvetica Neue",Arial; margin: 0; padding: 24px; background:#fafafa; color:#111; }
  h1 { font-size: 20px; margin: 0 0 var(--gap); }
  textarea { width: 100%; min-height: 180px; padding: 12px; box-sizing: border-box; font: 15px/1.6 var(--mono); }
  .row { display: grid; grid-template-columns: 1fr; gap: var(--gap); }
  .panel { background:#fff; border:1px solid #e5e7eb; border-radius: 10px; padding: 14px; }
  .panel h2 { font-size: 16px; margin: 0 0 8px; display:flex; align-items:center; justify-content:space-between; }
  .btns { display:flex; gap:8px; flex-wrap:wrap; }
  button,.btn { cursor:pointer; border:1px solid #d1d5db; border-radius:8px; background:#fff; padding:8px 12px; font: 14px/1 system-ui; }
  button:hover,.btn:hover { background:#f3f4f6; }
  .opt { display:flex; gap:14px; align-items:center; flex-wrap:wrap; color:#374151; }
  code.k { background:#f3f4f6; padding:2px 6px; border-radius:6px; font-family:var(--mono); }
  .out { font-family: var(--mono); white-space: pre-wrap; word-wrap: break-word; }
  .sent { margin-bottom: 8px; }
  ruby { ruby-position: over; }
  rt { font-size: .65em; color:#2563eb; }
  .muted { color:#6b7280; }
  .bar { display:flex; gap:8px; align-items:center; justify-content:space-between; margin: 8px 0 0; }
  .small { font-size:12px; }
  .badge { display:inline-block; padding:2px 6px; border-radius:999px; background:#eef2ff; color:#3730a3; font-size:12px; }
</style>
</head>
<body>
  <h1>日语 → 罗马音（自动读音）& Ruby 注音</h1>

  <div class="panel">
    <div class="badge" id="status">正在加载词典…（首次约 2–3 MB）</div>
    <h2>输入</h2>
    <textarea id="inp" placeholder="粘贴日语原文即可。可选：仍然支持君[きみ]这种手工读音覆盖。"></textarea>
    <div class="bar">
      <div class="opt">
        <label><input type="checkbox" id="splitComma" /> 逗点（、）也换行</label>
        <label><input type="checkbox" id="apostropheN" checked /> ‘ん’ 碰到元音/y 加撇 (n')</label>
        <label><input type="checkbox" id="woAsWo" /> 把 <code class="k">を</code> 转成 <code class="k">wo</code>（默认 <code class="k">o</code>）</label>
        <label>Ruby 注音：
          <label><input type="radio" name="rubyMode" value="romaji" checked /> 罗马音</label>
          <label><input type="radio" name="rubyMode" value="kana" /> 假名</label>
        </label>
      </div>
      <div class="btns">
        <button id="demo">填入示例</button>
        <button id="run">转换</button>
        <button id="clr">清空</button>
      </div>
    </div>
  </div>

  <div class="row">
    <div class="panel">
      <h2>罗马音（按句分行） <button class="btn" id="copyRoma">复制</button></h2>
      <div class="out" id="roma"></div>
      <div class="small muted">注：使用 kuromoji 词典自动推断汉字读音；若有专名/特殊读音，可用 <code class="k">漢字[かな]</code> 或 <code class="k">漢字（かな）</code> 覆盖。</div>
    </div>
    <div class="panel">
      <h2>原文 + Ruby 注音（可拷到文档里） <button class="btn" id="copyRuby">复制 HTML</button></h2>
      <div id="rubyOut"></div>
    </div>
  </div>

<!-- kuromoji.js（含词典） -->
<script src="https://cdn.jsdelivr.net/npm/kuromoji@0.1.2/dist/kuromoji.js"></script>

<script>
/* ====================== 基础工具 ====================== */
const isKana = s => /[\p{sc=Hiragana}\p{sc=Katakana}ー]/u.test(s);
const hasKanaOnly = s => /^[\p{sc=Hiragana}\p{sc=Katakana}ー]+$/u.test(s);
const isPunc = s => /^[。、，・：；「」『』（）\(\)\[\]〈〉《》…—？！?!.,;:\-]+$/u.test(s);
const toKatakana = s => s.replace(/[\u3041-\u3096]/g, ch => String.fromCharCode(ch.charCodeAt(0) + 0x60));
const toHiragana = s => s.replace(/[\u30A1-\u30FA]/g, ch => String.fromCharCode(ch.charCodeAt(0) - 0x60));
const lastVowel = s => (s.match(/[aeiou](?!.*[aeiou])/))?.[0] || '';

/* ====================== 假名→罗马音映射（Hepburn 近似） ====================== */
const baseMapHira = {
  'あ':'a','い':'i','う':'u','え':'e','お':'o',
  'か':'ka','き':'ki','く':'ku','け':'ke','こ':'ko',
  'さ':'sa','し':'shi','す':'su','せ':'se','そ':'so',
  'た':'ta','ち':'chi','つ':'tsu','て':'te','と':'to',
  'な':'na','に':'ni','ぬ':'nu','ね':'ne','の':'no',
  'は':'ha','ひ':'hi','ふ':'fu','へ':'he','ほ':'ho',
  'ま':'ma','み':'mi','む':'mu','め':'me','も':'mo',
  'や':'ya','ゆ':'yu','よ':'yo',
  'ら':'ra','り':'ri','る':'ru','れ':'re','ろ':'ro',
  'わ':'wa','ゐ':'wi','ゑ':'we','を':'o',
  'ん':'n',
  'が':'ga','ぎ':'gi','ぐ':'gu','げ':'ge','ご':'go',
  'ざ':'za','じ':'ji','ず':'zu','ぜ':'ze','ぞ':'zo',
  'だ':'da','ぢ':'ji','づ':'zu','で':'de','ど':'do',
  'ば':'ba','び':'bi','ぶ':'bu','べ':'be','ぼ':'bo',
  'ぱ':'pa','ぴ':'pi','ぷ':'pu','ぺ':'pe','ぽ':'po',
  'ぁ':'a','ぃ':'i','ぅ':'u','ぇ':'e','ぉ':'o',
  'ゃ':'ya','ゅ':'yu','ょ':'yo','ゎ':'wa',
  'ゔ':'vu'
};
const yoonPairsHira = {
  'きゃ':'kya','きゅ':'kyu','きょ':'kyo',
  'ぎゃ':'gya','ぎゅ':'gyu','ぎょ':'gyo',
  'しゃ':'sha','しゅ':'shu','しょ':'sho',
  'じゃ':'ja','じゅ':'ju','じょ':'jo',
  'ちゃ':'cha','ちゅ':'chu','ちょ':'cho',
  'にゃ':'nya','にゅ':'nyu','にょ':'nyo',
  'ひゃ':'hya','ひゅ':'hyu','ひょ':'hyo',
  'びゃ':'bya','びゅ':'byu','びょ':'byo',
  'ぴゃ':'pya','ぴゅ':'pyu','ぴょ':'pyo',
  'みゃ':'mya','みゅ':'myu','みょ':'myo',
  'りゃ':'rya','りゅ':'ryu','りょ':'ryo',
  'ゔぁ':'va','ゔぃ':'vi','ゔぇ':'ve','ゔぉ':'vo','ゔゅ':'vyu'
};
const kataForeignPairs = {
  'シェ':'she','ジェ':'je','チェ':'che',
  'ティ':'ti','ディ':'di','トゥ':'tu','ドゥ':'du',
  'ファ':'fa','フィ':'fi','フェ':'fe','フォ':'fo','フュ':'fyu',
  'ウィ':'wi','ウェ':'we','ウォ':'wo',
  'イェ':'ye',
  'テュ':'tyu','デュ':'dyu',
  'クァ':'kwa','クィ':'kwi','クェ':'kwe','クォ':'kwo',
  'グァ':'gwa','グィ':'gwi','グェ':'gwe','グォ':'gwo'
};
const baseMap = { ...baseMapHira };
for (const [k,v] of Object.entries(baseMapHira)) baseMap[toKatakana(k)] = v;
const pairMap = { ...yoonPairsHira };
for (const [k,v] of Object.entries(yoonPairsHira)) pairMap[toKatakana(k)] = v;
Object.assign(pairMap, kataForeignPairs);

/* ====================== 假名→罗马音 主函数 ====================== */
function kanaToRomaji(input, opts={apostropheN:true, woAsWo:false}) {
  let s = input.normalize('NFKC');
  let out = '', i = 0, sokuon = false;

  const nextRomaHead = (idx) => {
    const tri = s.slice(idx, idx+3);
    const bi  = s.slice(idx, idx+2);
    if (pairMap[tri]) return pairMap[tri][0];
    if (pairMap[bi]) return pairMap[bi][0];
    const ch = s[idx];
    if (baseMap[ch]) return baseMap[ch][0];
    return null;
  };

  while (i < s.length) {
    const tri = s.slice(i, i+3);
    if (pairMap[tri]) {
      let roma = pairMap[tri];
      if (sokuon) { roma = (roma.startsWith('ch') ? 't' : roma[0]) + roma; sokuon = false; }
      out += roma; i += 3; continue;
    }
    const bi = s.slice(i, i+2);
    if (pairMap[bi]) {
      let roma = pairMap[bi];
      if (sokuon) { roma = (roma.startsWith('ch') ? 't' : roma[0]) + roma; sokuon = false; }
      out += roma; i += 2; continue;
    }
    const ch = s[i];

    if (ch === 'っ' || ch === 'ッ') { sokuon = true; i++; continue; }
    if (ch === 'ー') { const v = lastVowel(out); out += v || ''; i++; continue; }
    if (ch === 'ん' || ch === 'ン') {
      const head = nextRomaHead(i+1);
      if (opts.apostropheN && head && ('aeiouy'.includes(head))) out += "n'";
      else out += 'n';
      i++; continue;
    }
    if (baseMap[ch]) {
      let roma = baseMap[ch];
      if (!opts.woAsWo && (ch === 'を' || ch === 'ヲ')) roma = 'o';
      if (sokuon) { roma = (roma.startsWith('ch') ? 't' : roma[0]) + roma; sokuon = false; }
      out += roma;
      i++; continue;
    }

    out += ch; i++;
  }
  return out;
}

/* ====================== 分句 & 智能拼接 ====================== */
function splitSentences(text, splitComma=false) {
  const sep = splitComma ? /(?<=[。！？?!…、]+)\s*/u : /(?<=[。！？?!…]+)\s*/u;
  return text.split(/\n+/).flatMap((line, idx, arr) => {
    const sents = line.split(sep);
    if (idx < arr.length - 1) sents.push('\n');
    return sents.filter(Boolean);
  });
}
function smartJoin(parts) {
  const res = [];
  for (let i=0;i<parts.length;i++){
    const cur = parts[i];
    if (cur === '\n') { res.push('\n'); continue; }
    if (i===0) { res.push((cur||'').trimStart()); continue; }
    const prev = res[res.length-1];
    const needSpace = !(prev?.endsWith(' ') || prev === '\n' || isPunc(cur)) && !(typeof prev === 'string' && /[ \n]$/.test(prev));
    res.push((needSpace ? ' ' : '') + cur);
  }
  return res.join('').replace(/[ ]+([。！？?!…、，,.;:])/g, '$1');
}

/* ====================== 解析手工覆盖（可选） ====================== */
/* 支持：漢字[かな] / 漢字（かな） */
function parseAnnotatedSegments(sentence) {
  const re = /([一-龯々〆ヵヶ]+)[\[\(（]([ぁ-ゖァ-ヺー]+)[\]\)）]/gu;
  let idx = 0, segs = [];
  let m;
  while ((m = re.exec(sentence)) !== null) {
    if (m.index > idx) segs.push({ type:'plain', text: sentence.slice(idx, m.index) });
    segs.push({ type:'annot', base: m[1], reading: m[2] });
    idx = re.lastIndex;
  }
  if (idx < sentence.length) segs.push({ type:'plain', text: sentence.slice(idx) });
  return segs;
}

/* ====================== Ruby 构建 ====================== */
function rubyWrap(base, rtText) {
  const ruby = document.createElement('ruby');
  const rb = document.createElement('rb'); rb.textContent = base;
  const rt = document.createElement('rt'); rt.textContent = rtText;
  ruby.appendChild(rb); ruby.appendChild(rt);
  return ruby;
}

/* ====================== kuromoji 加载 ====================== */
const statusEl = document.getElementById('status');
let tokenizer = null;
let building = false;

function buildTokenizer() {
  if (tokenizer || building) return;
  building = true;
  statusEl.textContent = '正在加载词典…';
  // CDN 词典路径（可替换为本地 ./dict/）
  const dicPath = "https://cdn.jsdelivr.net/npm/kuromoji@0.1.2/dict/";
  kuromoji.builder({ dicPath }).build(function(err, tkz) {
    building = false;
    if (err) {
      statusEl.textContent = '加载失败：' + (err.message || err);
      statusEl.style.background = '#fee2e2'; statusEl.style.color = '#991b1b';
      console.error(err);
      return;
    }
    tokenizer = tkz;
    statusEl.textContent = '词典已就绪 ✅';
    statusEl.style.background = '#dcfce7'; statusEl.style.color = '#166534';
  });
}
buildTokenizer();

/* ====================== 主流程：自动读音 + 分句 ====================== */
const $ = s => document.querySelector(s);
const inp = $('#inp'), romaOut = $('#roma'), rubyOut = $('#rubyOut');

function runConvert() {
  if (!tokenizer) { statusEl.textContent = '词典尚未就绪，请稍后再试…'; return; }

  const text = inp.value || '';
  const splitComma = $('#splitComma').checked;
  const opts = { apostropheN: $('#apostropheN').checked, woAsWo: $('#woAsWo').checked };
  const rubyMode = document.querySelector('input[name="rubyMode"]:checked').value; // 'romaji' | 'kana'

  const sentences = splitSentences(text, splitComma);
  romaOut.textContent = '';
  rubyOut.innerHTML = '';

  const romaLines = [];

  for (const sent of sentences) {
    if (sent === '\n') { rubyOut.appendChild(document.createElement('br')); romaLines.push('\n'); continue; }

    const segs = parseAnnotatedSegments(sent);
    const rubyNodes = [];
    const romajiPieces = [];

    const pushRubyAndRoma = (base, readingKana) => {
      const kanaNorm = readingKana.normalize('NFKC');
      const rtText = rubyMode === 'kana' ? toHiragana(kanaNorm) : kanaToRomaji(kanaNorm, opts);
      rubyNodes.push(rubyWrap(base, rtText));
      romajiPieces.push(kanaToRomaji(kanaNorm, opts));
    };

    for (const seg of segs) {
      if (seg.type === 'annot') { // 手工覆盖优先
        pushRubyAndRoma(seg.base, seg.reading);
        continue;
      }
      // 交给 kuromoji 分词
      const tokens = tokenizer.tokenize(seg.text);
      for (const tk of tokens) {
        const surf = tk.surface_form || '';
        const readingKata = tk.reading; // 可能为 undefined
        const isSymbol = tk.pos === '記号' || isPunc(surf) || /^\s+$/.test(surf);
        const isAscii = /^[A-Za-z0-9]+$/.test(surf);

        if (readingKata) {
          // 有词典读音
          pushRubyAndRoma(surf, readingKata);
        } else if (hasKanaOnly(surf)) {
          // 纯假名词
          pushRubyAndRoma(surf, surf);
        } else if (isSymbol || isAscii) {
          // 标点/空白/ASCII 直接原样
          rubyNodes.push(document.createTextNode(surf));
          romajiPieces.push(surf);
        } else {
          // 实在无读音（极少）：原样显示，罗马音也原样保留
          rubyNodes.push(document.createTextNode(surf));
          romajiPieces.push(surf);
        }
      }
    }

    const wrap = document.createElement('div');
    wrap.className = 'sent';
    rubyNodes.forEach(n => wrap.appendChild(n));
    rubyOut.appendChild(wrap);
    romaLines.push(smartJoin(romajiPieces).trim());
  }

  romaOut.textContent = romaLines.join('\n').replace(/\n{3,}/g, '\n\n');
}

/* ====================== UI 绑定 ====================== */
$('#run').addEventListener('click', runConvert);
$('#clr').addEventListener('click', () => { inp.value=''; romaOut.textContent=''; rubyOut.innerHTML=''; });
$('#demo').addEventListener('click', () => {
  inp.value = '君がそこにいるだけで、心が軽くなる。雨の日でも、笑顔を思い出せば前を向ける。';
  runConvert();
});
$('#copyRoma').addEventListener('click', async () => {
  await navigator.clipboard.writeText(romaOut.textContent.trim());
});
$('#copyRuby').addEventListener('click', async () => {
  await navigator.clipboard.writeText(rubyOut.innerHTML.trim());
});

</script>
</body>
</html>
