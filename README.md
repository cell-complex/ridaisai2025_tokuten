<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>N○M休</title>
  <style>
    html, body {
  height: 100vh;
  margin: 0;
  font-family: "Yu Gothic", sans-serif;
  background: #f6f6f6;
  text-align: center;
  overflow: hidden; /* ← スクロールを防止 */
}

#title {
  font-size: 1.8vw;
  margin-top: 0.5vw;
}

#controls {
  margin: 0.5vw 0;
}

#board {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-template-rows: repeat(2, 1fr);
  gap: 0.8vw;
  justify-items: center;
  align-items: center;
  width: 95%;
  height: 75vh; /* ← ここで高さを制御 */
  margin: 0 auto;
}

.player {
  width: 13vw;
  height: 35vh; /* ← 縦方向をvh基準に変更 */
  background: white;
  border-radius: 0.8vw;
  box-shadow: 0 0 0.4vw rgba(0, 0, 0, 0.3);
  padding: 1vw;
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
  font-size: 1.8vw;
  color: white;
}

.score {
  font-size: 3vw;
  font-weight: bold;
}

.status {
  font-size: 0.9vw;
}

.休 {
  color: black;
  font-size: 1.5vw;
}

.btns {
  display: flex;
  gap: 0.6vw;
  justify-content: center;
  width: 90%;
}

.btns button {
  flex: 1;
  aspect-ratio: 1;
  border: none;
  border-radius: 0.8vw;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5vw;
  transition: 0.2s;
}

.btns .reset {
  flex: none;
  aspect-ratio: 2;
  width: 85%;
  font-size: 1vw;
  background: gray;
  color: white;
  border-radius: 0.6vw;
}

.btns button:hover {
  opacity: 0.8;
}

.plus {
  background: red;
  color: white;
}

.miss {
  background: blue;
  color: white;
}

#nextBtn {
  background: #4CAF50;
  color: white;
  font-weight: bold;
  border: none;
  border-radius: 0.8vw;
  padding: 0.4vw 1.5vw;
  cursor: pointer;
  font-size: 1.3vw;
  transition: 0.3s;
}

#nextBtn:hover {
  background: #45a049;
}

#controls input[type="number"] {
  width: 3.5vw;
  padding: 0.2vw 0.4vw;
  border: 0.1vw solid #ccc;
  border-radius: 0.5vw;
  text-align: center;
  font-size: 1vw;
  margin-right: 0.8vw;
}

#controls label {
  font-weight: bold;
  margin-right: 0.3vw;
  font-size: 1vw;
}

  </style>
  <!-- <style>
    html, body {
      height: 100vh;
      margin: 0;
      font-family: "Yu Gothic", sans-serif;
      background: #f6f6f6;
      text-align: center;
    }

    #title {
      font-size: 2.2vw; /* ビューポート幅基準 */
    }

    h1 {
      margin: 0.3vw;
    }

    #controls {
      margin: 1vw 0;
    }

    #board {
      display: grid;
      grid-template-columns: repeat(6, 1fr);
      grid-template-rows: repeat(2, 1fr);
      gap: 1vw;
      justify-items: center;
      margin: 2vw auto;
      width: 90%;
      font-weight: bold;
      font-size: 1.8vw;
    }

    .player {
      width: 13vw;
      height: 21vw;
      background: white;
      border-radius: 1vw;
      box-shadow: 0 0 0.5vw rgba(0, 0, 0, 0.2);
      padding: 1vw;
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
      font-size: 2vw;
      font-weight: bold;
      color: white;
    }

    .score {
      font-size: 5vw;
      font-weight: bold;
      padding: 0;
    }

    .status {
      font-size: 1vw;
    }

    .休 {
      color: black;
      font-size: 2.5vw;
    }

    .btns {
      display: flex;
      gap: 1vw;
      justify-content: center;
      width: 80%;
      margin: 0 auto;
    }

    .btns button {
      flex: 1;
      aspect-ratio: 1;
      border: none;
      border-radius: 1vw;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2vw;
      transition: 0.2s;
    }

    .btns .reset {
      flex: none;
      aspect-ratio: 2;
      width: 90%;
      font-size: 1.2vw;
      background: gray;
      color: white;
      border-radius: 1vw;
    }

    .btns button:hover {
      opacity: 0.8;
    }

    .plus {
      background: red;
      color: white;
    }

    .miss {
      background: blue;
      color: white;
    }

    .reset {
      background: gray;
      color: white;
    }

    #nextBtn {
      background: #4CAF50;
      color: white;
      font-weight: bold;
      border: none;
      border-radius: 1vw;
      padding: 0.6vw 2vw;
      cursor: pointer;
      font-size: 1.5vw;
      transition: 0.3s;
    }

    #nextBtn:hover {
      background: #45a049;
    }

    #controls input[type="number"] {
      width: 4vw;
      padding: 0.3vw 0.5vw;
      border: 0.1vw solid #ccc;
      border-radius: 0.6vw;
      text-align: center;
      font-size: 1.2vw;
      margin-right: 1vw;
    }

    #controls label {
      font-weight: bold;
      margin-right: 0.4vw;
      font-size: 1.2vw;
    }
  </style> -->
</head>

<body>

  <h1 id="title">N○M休</h1>

  <div id="controls">
    <label>N○：</label><input type="number" id="winCount" value="3" min="1">
    <label>M休：</label><input type="number" id="restCount" value="1" min="1">
    <button id="nextBtn">スルー</button>
  </div>

  <div id="board"></div>

  <script>
    const board = document.getElementById("board");
    const N = 12;
    let winNeeded = parseInt(document.getElementById("winCount").value);
    let restTurns = parseInt(document.getElementById("restCount").value);

    let players = Array.from({ length: N }, (_, i) => ({
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
          score.innerHTML = `<span class="winner-text">抜け！</span>`;
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
          plusBtn.onclick = () => {
            p.score++;
            if (p.score >= winNeeded) {
              p.winner = true;
              p.active = false;
            }
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
          missBtn.onclick = () => {
            p.rest = restTurns;
            p.active = false;
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
            Object.assign(p, { score: 0, rest: 0, active: true, winner: false });
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
