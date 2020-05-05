<template>
  <div id="app">
    <div class="display">
      <div class="field">
        <div class="left">
          <div class="queue holdQueue">
            hold
          </div>
          <div class="gameInformation">
            <ul>
              <div class="box scoreBox">
                <li class="scoreTitle">
                  SCORE
                </li>
                <li class="count scoreCount">
                  1234567890
                </li>
              </div>
              <div class="box timeBox">
                <li class="timeTitle">
                  TIME
                </li>
                <li class="count timeCount">
                  00:00:00
                </li>
              </div>
              <div class="box lineBox">
                <li class="lineTitle">
                  LINE:
                </li>
                <li class="count linesCount">
                  10
                </li>
              </div>
              <div class="box levelBox">
                <li class="levelTitle">
                  LEVEL:
                </li>
                <li class="count levelCount">
                  00
                </li>
              </div>
              <div class="box goalBox">
                <li class="goalTitle">
                  GOAL:
                </li>
                <li class="count goalCount">
                  00
                </li>
              </div>
              <div class="box tetliseBox">
                <li class="tetriseTitle">
                  TETRISES:
                </li>
                <li class="count tetrisesCount">
                  00
                </li>
              </div>
            </ul>
          </div>
        </div>
        <div class="center">
          <div class="matrix">
            <table>
              <tr
                v-for="(line, i) in display"
                :key="i"
              >
                <!-- mustaches展開 -->
                <td
                  v-for="(cell, j) in line"
                  :key="j"
                  class="block"
                  :class="cell | blockClass"
                />
              </tr>
            </table>
          </div>
        </div>
        <div class="right">
          <div class="queue nextQueue">
            next
          </div>
          <div class="queue afterQueue">
            afterQueue
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// テトリミノ
const tetrimino = {
  0: [
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  // I Tetrimino
  1: [
    [0, 0, 1, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  // O Tetrimino
  2: [
    [0, 0, 0, 0, 0],
    [0, 0, 2, 2, 0],
    [0, 0, 2, 2, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  // T Tetrimino
  3: [
    [0, 0, 0, 0, 0],
    [0, 0, 3, 0, 0],
    [0, 3, 3, 3, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  // J Tetrimino
  4: [
    [0, 0, 0, 0, 0],
    [0, 0, 4, 0, 0],
    [0, 0, 4, 0, 0],
    [0, 4, 4, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  // L Tetrimino
  5: [
    [0, 0, 0, 0, 0],
    [0, 0, 5, 0, 0],
    [0, 0, 5, 0, 0],
    [0, 0, 5, 5, 0],
    [0, 0, 0, 0, 0]
  ],
  // S Tetrimino
  6: [
    [0, 0, 0, 0, 0],
    [0, 0, 6, 6, 0],
    [0, 6, 6, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  // Z Tetrimino
  7: [
    [0, 0, 0, 0, 0],
    [0, 7, 7, 0, 0],
    [0, 0, 7, 7, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ]
};
export default {
  filters: {
    blockClass(val) {
      switch (val) {
        case 1:
          return 'tetrimino-i';
        case 2:
          return 'tetrimino-o';
        case 3:
          return 'tetrimino-t';
        case 4:
          return 'tetrimino-j';
        case 5:
          return 'tetrimino-l';
        case 6:
          return 'tetrimino-s';
        case 7:
          return 'tetrimino-z';
        default:
          return '';
      }
    }
  },
  data: function() {
    return {
      field: {
        data: [],
        x: 10,
        y: 20
      },
      block: {
        // ブロックタイプ
        type: 1,
        data: [],
        // x軸座標
        x: 0,
        // y軸座標
        y: 0
      },
      isInterval: true
    };
  },
  computed: {
    /**
     * フィールド画面の表示
     */
    display() {
      // ボードのコピー
      const field = JSON.parse(JSON.stringify(this.field.data));
      if (this.block.data.length === 0) {
        return field;
      }
      // ブロックの描画switch
      for (let h = 0; h < this.block.data.length; h++) {
        for (let v = 0; v < this.block.data[h].length; v++) {
          const y = this.block.y + h;
          const x = this.block.x + v;
          if (y < 0 || x < 0 || y > this.field.y - 1 || x > this.field.x - 1) {
            continue;
          }
          if (this.block.data[h][v] === 0) {
            continue;
          }
          field[h + this.block.y][v + this.block.x] = this.block.data[h][v];
        }
      }
      return field;
    }
  },
  // ライフサイクル
  created() {
    this.clear();
    this.setBlock();
  },
  mounted() {
    window.addEventListener('keydown', this.handleKeydown);
    this.dropDown();
  },
  beforeDestroy() {
    window.removeEventListener('keydown', this.handleKeydown);
  },
  // メソッド
  methods: {
    /**
     * 初期化
     */
    clear() {
      this.field.data = [...Array(this.field.y)].map(() => Array(this.field.x).fill(0));
    },
    /**
     * テトリミノの表示
     */
    setBlock() {
      this.block.x = 1;
      this.block.y = this.block.type === 1 ? 1 : -1;
      this.block.data = JSON.parse(JSON.stringify(tetrimino[this.block.type]));
      // while (this.isOverlap()) {
      //   this.block.y -= 1;
      // }
    },
    /**
     * 移動可否判定
     * @param  Array block アクティブテトリミノ
     * @param  int   x     アクティブテトリミノのx座標
     * @param  int   y     アクティブテトリミノのy座標
     * @return false       移動不可
     */
    canMove(block, x, y) {
      for (let h = 0; h < block.length; h++) {
        for (let v = 0; v < block[h].length; v++) {
          //左端判定
          if (x + v < 0 && block[h][v] > 0) {
            return false;
          }
          //右端判定
          if (x + v > this.field.x - 1 && block[h][v] > 0) {
            return false;
          }
          //下端判定
          if (y + h > this.field.y - 1 && block[h][v] > 0) {
            return false;
          }
          //上端判定
          if (y + h < 0 && block[h][v] > 0) {
            return false;
          }
          //ボード外の座標は無視
          if (x + v < 0 || x + v > this.field.x - 1 || y + h > this.field.y - 1 || y + h < 0) {
            continue;
          }
          //ブロック判定
          if (this.field.data[y + h][x + v] > 0 && block[h][v] > 0) {
            return false;
          }
        }
      }
      return true;
    },
    /**
     * 右移動
     */
    right() {
      if (!this.canMove(this.block.data, this.block.x + 1, this.block.y)) {
        return;
      }
      this.block.x += 1;
    },
    /**
     * 左移動
     */
    left() {
      if (!this.canMove(this.block.data, this.block.x - 1, this.block.y)) {
        return;
      }
      this.block.x -= 1;
    },
    /**
     * 下移動（ソフトドロップ）
     */
    softDrop() {
      if (!this.canMove(this.block.data, this.block.x, this.block.y + 1)) {
        return;
      }
      this.block.y += 1;
    },
    /**
     * 最下移動（ハードドロップ）
     */
    hardDrop() {
      while (this.canMove(this.block.data, this.block.x, this.block.y + 1)) {
        this.softDrop();
      }
    },
    /**
     * 回転
     * @return {[type]} [description]
     */
    rotate() {
      // O型は回転しない
      if (this.block.type === 2) {
        return;
      }

      // 回転後のブロック生成
      const rotatedTetrimino = JSON.parse(JSON.stringify(this.block.data));
      for (let h = 0; h < rotatedTetrimino.length; h++) {
        for (let v = 0; v < rotatedTetrimino[h].length; v++) {
          rotatedTetrimino[rotatedTetrimino.length - v - 1][h] = this.block.data[h][v];
        }
      }

      // 回転可否判定
      if (!this.canMove(rotatedTetrimino, this.block.x, this.block.y)) {
        return;
      }

      this.block.data = rotatedTetrimino;
    },
    /**
     * キー設定
     * @param event イベント
     */
    handleKeydown(event) {
      // 最下移動（space）
      if (event.keyCode === 32) {
        this.hardDrop();
      }
      // 左移動（←）
      else if (event.keyCode === 37) {
        this.left();
      }
      // 回転移動（↑）
      else if (event.keyCode === 38) {
        this.rotate();
      }
      // 右移動（→）
      else if (event.keyCode === 39) {
        this.right();
      }
      // 下移動（↓）
      else if (event.keyCode === 40) {
        this.softDrop();
      }
    },
    /**
     * 自動落下
     * 一定間隔ごとにメソッドを実行
     */
    dropDown() {
      this.isInterval = setInterval(this.softDrop, 1000);
    },
    stopDropDown() {
      clearInterval(this.isInterval);
    }
  }
};
</script>

<style>
:root {
  --field-block: calc(100vh * 0.045);
}

li {
  list-style: none;
}

table {
  border: 5px #626261 solid;
  border-collapse: collapse;
}

tr,
td {
  border: 1px #626261 solid;
  height: var(--field-block);
  min-width: var(--field-block);
}

.display {
  height: 100vh;
  width: 100vw;
  background-color: #B2B3B2;
}

.field {
  display: flex;
  justify-content: center;
  width: 80%;
  margin: auto;
  padding-top: 20px;
}

.left {
  margin-right: 10px;
}

.block {
  width: var(--field-block);
  height: var(--field-block);
  background-color: white;
}

.tetrimino-i {
  background: #3498db;
}

.tertimino-o {
  background: #f1c40f;
}

.tertimino-t {
  background: #9b59b6;
}

.tertimino-j {
  background: #1e3799;
}

.tertimino-l {
  background: #e67e22;
}

.tertimino-s {
  background: #2ecc71;
}

.tetrimino-z {
  background: #e74c3c;
}

.queue {
  width: 100px;
  height: 100px;
  background-color: white;
}

.holdQueue {
  margin-left: auto;
}

.gameInformation {
  margin-top: 20px;
}

.box {
  margin-bottom: 8px;
}

.count {
  font-weight: bold;
}

.right {
  margin-left: 10px;
}

.afterQueue {
  margin-top: 20px;
}
</style>
