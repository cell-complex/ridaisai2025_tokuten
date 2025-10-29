<!DOCTYPE html> 
<html lang="ja">
<head>
<meta charset="UTF-8">
<title>N○M休 スコアボード</title>
<style>
  body {
    font-family: "Yu Gothic", sans-serif;
    background: #f6f6f6;
    text-align: center;
  }
  #title {
    font-size: 20px;
  }
  h1 {
    margin: 2px;
  }
  #controls {
    margin: 10px;
  }
  #board {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-template-rows: repeat(2, 1fr);
    gap: 10px;
    justify-items: center;
    margin: 20px;
    font-weight: bold;
    font-size: 20px; 
  }
  .player {
    width: 130px;
    height: 210px;
    background: white;
    border-radius: 12px;
    box-shadow: 0 0 5px rgba(0,0,0,0.2);
    padding: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    transition: 0.3s;
  }
  .inactive {
    background: #ddd;
    color: #888;
  }
  .winner {
    background: red;
    color: #000;
    font-weight: bold;
  }
  .winner-text {
    font-size: 24px; 
    font-weight: bold;
    color: white;
  }
  .score {
    font-size: 50px;
    font-weight: bold;
  }
  .status {
    font-size: 10px;
  }
  .休 {
    color: black;
    font-size: 30px;
  }
  .btns button {
    margin: 3px;
    padding: 5px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  .btns button:hover {
    opacity: 0.8;
  }
  .plus { font-size: 30px; background: blue; color: white; }
  .miss { font-size: 30px; background: red; color: white; }
  .reset { font-size: 20px; background: gray; color: white; }

  #nextBtn {
    background: #4CAF50;
    color: white;
    font-weight: bold;
    border: none;
    border-radius: 8px;
    padding: 10px 30px;
    cursor: pointer;
    transition: 0.3s;
  }
  #nextBtn:hover {
    background: #45a049;
  }

  #controls input[type="number"] {
    width: 60px;
    padding: 4px 6px;
    border: 1px solid #ccc;
    border-radius: 6px;
    text-align: center;
    font-size: 16px;
    margin-right: 10px;
  }
  #controls label {
    font-weight: bold;
    margin-right: 4px;
  }
</style>
</head>
<body>

<h1 id="title">N○M休</h1>

<div id="controls">
  <label>N○：</label><input type="number" id="winCount" value="3" min="1" style="width:50px;">
  <label>M休：</label><input type="number" id="restCount" value="2" min="1" style="width:50px;">
  <button id="nextBtn">スルー</button>
</div>

<div id="board"></div>

<script>
const board = document.getElementById("board");
const N = 12;
let winNeeded = parseInt(document.getElementById("winCount").value);
let restTurns = parseInt(document.getElementById("restCount").value);

let players = Array.from({length: N}, (_, i) => ({
  id: i + 1,
  score: 0,
  rest: 0,
  active: true,
  winner: false
}));

function render() {
  board.innerHTML = "";
  winNeeded = parseInt(document.getElementById("winCount").value);
  restTurns = parseInt(document.getElementById("restCount").value);

  players.forEach(p => {
    const div = document.createElement("div");
    div.className = "player";
    if (!p.active && !p.winner) div.classList.add("inactive");
    if (p.winner) div.classList.add("winner");

    const header = document.createElement("div");
    header.textContent = `No.${p.id}`;

    const score = document.createElement("div");
    score.className = "score";
    if (p.winner) {
      score.innerHTML = `<span class="winner-text">勝ち抜け！</span>`;
    } else {
      score.textContent = p.score;
    }

    const status = document.createElement("div");
    status.className = "status";
    if (p.rest > 0 && !p.winner) {
      status.innerHTML = `<span class="休">${p.rest}休</span>`;
    } else {
      status.innerHTML = "";
    }

    const btns = document.createElement("div");
    btns.className = "btns";

    if (!p.winner) {
      const plusBtn = document.createElement("button");
      plusBtn.textContent = "○";
      plusBtn.className = "plus";
      plusBtn.disabled = !p.active;
      // 正解ボタン
      plusBtn.onclick = () => {
        p.score++;
        if (p.score >= winNeeded) {
          p.winner = true;
          p.active = false;
        }
        // 他プレイヤーの休みを1減らす
        players.forEach(other => {
          if (other.id !== p.id && other.rest > 0) {
            other.rest--;
            if (other.rest === 0 && !other.winner) other.active = true;
          }
        });
        render();
      };

      const missBtn = document.createElement("button");
      missBtn.textContent = "×";
      missBtn.className = "miss";
      missBtn.disabled = !p.active;
      // 誤答ボタン
      missBtn.onclick = () => {
        p.rest = restTurns;
        p.active = false;
        // 他プレイヤーの休みを1減らす
        players.forEach(other => {
          if (other.id !== p.id && other.rest > 0) {
            other.rest--;
            if (other.rest === 0 && !other.winner) other.active = true;
          }
        });
        render();
      };

      btns.append(plusBtn, missBtn);
    } else {
      const resetBtn = document.createElement("button");
      resetBtn.textContent = "リセット";
      resetBtn.className = "reset";
      resetBtn.onclick = () => {
        Object.assign(p, {score: 0, rest: 0, active: true, winner: false});
        render();
      };
      btns.append(resetBtn);
    }

    div.append(header, score, status, btns);
    board.appendChild(div);
  });
}

document.getElementById("nextBtn").onclick = () => {
  players.forEach(p => {
    if (p.rest > 0) {
      p.rest--;
      if (p.rest === 0 && !p.winner) p.active = true;
    }
  });
  render();
};

render();
</script>

</body>
</html>

