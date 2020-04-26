<template>
  <div id="app">
    <div class="display">
      <div class="field">
        <div class="left">
          <div class="queue holdQueue">hold</div>
          <div class="gameInformation">
            <ul>
              <div class="box scoreBox">
                <li class="scoreTitle">SCORE</li>
                <li class="count scoreCount">1234567890</li>
              </div>
              <div class="box timeBox">
                <li class="timeTitle">TIME</li>
                <li class="count timeCount">00:00:00</li>
              </div>
              <div class="box lineBox">
                <li class="lineTitle">LINE:</li>
                <li class="count linesCount">10</li>
              </div>
              <div class="box levelBox">
                <li class="levelTitle">LEVEL:</li>
                <li class="count levelCount">00</li>
              </div>
              <div class="box goalBox">
                <li class="goalTitle">GOAL:</li>
                <li class="count goalCount">00</li>
              </div>
              <div class="box tetliseBox">
                <li class="tetriseTitle">TETRISES:</li>
                <li class="count tetrisesCount">00</li>
              </div>
            </ul>
          </div>
        </div>
        <div class="center">
          <div class="matrix">
            <table>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
              </tr>
              <tr>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
                <td>あ</td>
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

</script>

<style>

li {
  list-style: none;
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
