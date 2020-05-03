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
                <td
                  v-for="(block, j) in line"
                  :key="j"
                  class="block"
                  :class="line | blockClass"
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
  ZERO: [
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  I: [
    [0, 0, 1, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  O: [
    [0, 0, 0, 0, 0],
    [0, 0, 1, 1, 0],
    [0, 0, 1, 1, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  T: [
    [0, 0, 0, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 1, 1, 1, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  J: [
    [0, 0, 0, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 1, 1, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  L: [
    [0, 0, 0, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 1, 1, 0],
    [0, 0, 0, 0, 0]
  ],
  S: [
    [0, 0, 0, 0, 0],
    [0, 0, 1, 1, 0],
    [0, 1, 1, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ],
  Z: [
    [0, 0, 0, 0, 0],
    [0, 1, 1, 0, 0],
    [0, 0, 1, 1, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0]
  ]
};
export default {
  data: function() {
    return {
      field: {
        data: [],
        x: 10,
        y: 20
      },
      block: {
        // ブロックタイプ
        type: '',
        data: [],
        // x軸座標
        x: 0,
        // y軸座標
        y: 0
      }
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
    console.error('field.data', this.field.data);
  },
  // メソッド
  methods: {
    /**
     * 初期化
     */
    clear() {
      this.field.data = [...Array(this.field.y)].map(() => Array(this.field.x).fill(0));
    },
    setBlock() {

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
  min-height: 100vh;
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
