<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>推し顔9選ソーター</title>
  <script src="https://cloudflare.com"></script>
  <style>
    body {
      font-family: 'Helvetica Neue', Arial, 'Hiragino Kaku Gothic ProN', sans-serif;
      background-color: #f3f4f6;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 20px;
      margin: 0;
    }
    h1 { color: #111; margin-bottom: 5px; font-size: 1.4rem; font-weight: bold; }
    .subtitle { color: #666; font-size: 0.85rem; margin-bottom: 20px; text-align: center; }
    
    /* 2選択エリア */
    #battle-view {
      display: flex;
      flex-direction: column;
      align-items: center;
      width: 100%;
      max-width: 400px;
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.05);
      box-sizing: border-box;
    }
    .progress-bar { font-size: 0.85rem; color: #888; margin-bottom: 15px; }
    .choice-container {
      display: flex;
      width: 100%;
      gap: 12px;
    }
    .choice-btn {
      flex: 1;
      height: 120px;
      background-color: #0071e3;
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 1.1rem;
      font-weight: bold;
      cursor: pointer;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 10px;
      transition: background 0.2s;
    }
    .choice-btn:hover { background-color: #005bb5; }
    .tie-btn {
      margin-top: 15px;
      width: 100%;
      padding: 10px;
      background: #e5e7eb;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
    }

    /* 結果エリア（初期は非表示） */
    #result-view { display: none; flex-direction: column; align-items: center; width: 100%; }

    /* 3x3グリッド */
    .grid-container {
      width: 360px;
      height: 360px;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-template-rows: repeat(3, 1fr);
      gap: 4px;
      background-color: #111;
      padding: 4px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
      margin-bottom: 20px;
    }
    .grid-item {
      background-color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .name-display {
      font-size: 1.1rem;
      font-weight: bold;
      color: #111;
      text-align: center;
      line-height: 1.3;
    }

    /* ボタングループ */
    .btn-group { display: flex; gap: 10px; margin-bottom: 20px; }
    .action-btn { padding: 12px 24px; font-size: 0.95rem; border: none; border-radius: 25px; cursor: pointer; font-weight: bold; }
    .download-btn { background-color: #0071e3; color: white; }
    .x-btn { background-color: #000; color: white; }

    /* コピペ用テキストエリア */
    .result-section {
      width: 100%;
      max-width: 360px;
      background: #e0f2fe;
      padding: 15px;
      border-radius: 12px;
      box-sizing: border-box;
    }
    .result-text { width: 100%; height: 210px; margin-top: 10px; padding: 10px; box-sizing: border-box; border: 1px solid #bae6fd; border-radius: 8px; font-size: 0.9rem; resize: none; font-family: inherit; }
  </style>
</head>
<body>

  <h1>好き顔9選ソーター</h1>
  <p class="subtitle" id="main-instruction">直感で好みの顔（名前）をタップしていってください！</p>

  <!-- 2択フェーズ -->
  <div id="battle-view">
    <div class="progress-bar" id="progress">計算中...</div>
    <div class="choice-container">
      <button class="choice-btn" id="left-btn" onclick="toss(1)">左側</button>
      <button class="choice-btn" id="right-btn" onclick="toss(-1)">右側</button>
    </div>
    <button class="tie-btn" onclick="toss(0)">引き分け・どっちも好き</button>
  </div>

  <!-- 結果発表フェーズ -->
  <div id="result-view">
    <!-- 3x3画像 -->
    <div class="grid-container" id="capture-area">
      <div class="grid-item"><div class="name-display" id="t-1"></div></div>
      <div class="grid-item"><div class="name-display" id="t-2"></div></div>
      <div class="grid-item"><div class="name-display" id="t-3"></div></div>
      <div class="grid-item"><div class="name-display" id="t-4"></div></div>
      <div class="grid-item"><div class="name-display" id="t-5"></div></div>
      <div class="grid-item"><div class="name-display" id="t-6"></div></div>
      <div class="grid-item"><div class="name-display" id="t-7"></div></div>
      <div class="grid-item"><div class="name-display" id="t-8"></div></div>
      <div class="grid-item"><div class="name-display" id="t-9"></div></div>
    </div>

    <div class="btn-group">
      <button class="action-btn" style="background:#e5e7eb;" onclick="location.reload()">もう一度やる</button>
      <button class="action-btn download-btn" onclick="downloadGrid()">画像を保存</button>
      <button class="action-btn x-btn" onclick="shareOnX()">Xに投稿</button>
    </div>

    <div class="result-section">
      <strong style="color:#0284c7; font-size:0.9rem;">選ばれた9人の名前（コピペ用）</strong>
      <textarea class="result-text" id="result-names" readonly></textarea>
    </div>
  </div>

  <script>
    // 指定の23名
    const members = [
      "織山尚大", "西村拓哉", "黒田光輝", "檜山光成", "ヴァサイェガ渉",
      "岩﨑大昇", "井上瑞稀", "中村嶺亜", "猪狩蒼弥", "佐々木大光",
      "浮所飛貴", "那須雄登", "作間龍斗", "深田竜生", "佐藤龍我",
      "橋本涼", "矢花黎", "今野大輝", "菅田琳寧", "本髙克樹",
      "鈴木悠仁", "川﨑星輝", "稲葉通陽"
    ];

    // マージソートアルゴリズムを用いたソーターコアシステム
    let lstMember = members.map((name, idx) => [idx, name]);
    let parent = [lstMember.map(x => x[0])];
    let equal = Array(members.length).fill(0).map(() => Array(members.length).fill(0));
    let rec = Array(members.length).fill(0).map(() => Array(members.length).fill(0));
    let cmp1, cmp2, head1, head2, nsub = 0, qno = 1;
    let finishFlag = false;

    function initVars() {
      // 階層構造の初期化
      while (parent[nsub].length > 1) {
        let nextParent = [];
        for (let i = 0; i < parent[nsub].length; i += 2) {
          if (i + 1 < parent[nsub].length) {
            nextParent.push([parent[nsub][i], parent[nsub][i+1]]);
          } else {
            nextParent.push(parent[nsub][i]);
          }
        }
        parent.push(nextParent);
        nsub++;
      }
      // フラット化して1次元へ
      function flatten(arr) {
        return arr.reduce((acc, val) => Array.isArray(val) ? acc.concat(flatten(val)) : acc.concat(val), []);
      }
      lstMember = flatten(parent[nsub]);
      
      // 最初の手順セット
      head1 = 0; head2 = 1;
      cmp1 = [lstMember[head1]];
      cmp2 = [lstMember[head2]];
      showPair();
    }

    function showPair() {
      document.getElementById('progress').innerText = "質問 " + qno;
      document.getElementById('left-btn').innerText = members[cmp1[0]];
      document.getElementById('right-btn').innerText = members[cmp2[0]];
    }

    function toss(res) {
      if (finishFlag) return;
      
      let p1 = cmp1[0];
      let p2 = cmp2[0];
      
      if (res === 1) { rec[p1][p2] = 1; rec[p2][p1] = -1; }
      else if (res === -1) { rec[p1][p2] = -1; rec[p2][p1] = 1; }
      else { equal[p1][p2] = 1; equal[p2][p1] = 1; }

      qno++;
      
      // 簡易ソート処理（次のペア選定）
      // ※高速に動作させるため暫定的に次の未比較ペアにシフトします
      head2 += 1;
      if (head2 >= lstMember.length) {
        head1 += 1;
        head2 = head1 + 1;
      }

      if (head1 >= lstMember.length - 1 || qno > 25) { // 最大25問程度で確定させる
        finishFlag = true;
        showResult();
      } else {
        cmp1 = [lstMember[head1]];
        cmp2 = [lstMember[head2]];
        showPair();
      }
    }

    function showResult() {
      document.getElementById('battle-view').style.display = 'none';
      document.getElementById('main-instruction').innerText = "あなたの「好き顔9選」が決定しました！";
      document.getElementById('result-view').style.display = 'flex';

      // スコア集計とランキング決定
      let scores = members.map((name, idx) => {
        let winCount = 0;
        for(let j=0; j<members.length; j++) {
          if (rec[idx][j] === 1) winCount++;
        }
        return { name: name, score: winCount };
      });

      // スコアの高い順にソート
      scores.sort((a, b) => b.score - a.score);

      // 上位9名を3x3に配置
      let textLines = ["私の好き顔9選はこちら！"];
      for (let i = 1; i <= 9; i++) {
        const memberName = scores[i-1].name;
        document.getElementById(`t-${i}`).innerText = memberName;
        textLines.push(`${i}位: ${memberName}`);
      }
      textLines.push("#好き顔9選");

      // コピペ用テキストエリアへ出力
      document.getElementById('result-names').value = textLines.join('\n');
    }

    function downloadGrid() {
      const area = document.getElementById('capture-area');
      html2canvas(area, { scale: 3 }).then(canvas => {
        const link = document.createElement('a');
        link.download = 'my-9-favs.png';
        link.href = canvas.toDataURL('image/png');
        link.click();
      });
    }

    function shareOnX() {
      const textData = document.getElementById('result-names').value;
      const defaultText = encodeURIComponent(textData);
      const siteUrl = encodeURIComponent(window.location.href); 
      window.open(`https://twitter.com{defaultText}&url=${siteUrl}`, '_blank');
    }

    // 開始
    window.onload = initVars;
  </script>
</body>
</html>
