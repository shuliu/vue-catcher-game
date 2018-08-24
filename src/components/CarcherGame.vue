<template>
<div class="CarcherGame">
  <div id="gameBox">
    <div id="carcher" class="carcher"
  >{{ carcherContent }}</div>
  </div>

</div>
</template>

<script>
import TweenMax from 'gsap/TweenMax';
// import TimelineMax from 'gsap/TimelineMax';
// import EasePack from 'gsap';
// import Draggable from "gsap/Draggable";

/** Elements */


/** mounted hook function */
function mountedCallback() {
  /** 設定 carcher 起始位置 */
  this.setCarcherToReady();
  /** 設定鍵盤移動事件 */
  this.addkeyDownEvent();
}

export default {
  name: 'CarcherGame',
  data() {
    return {
      carcherContent: '← -- →',
    };
  },
  components: {},
  methods: {
    /** 設定 carcher 起始位置 */
    setCarcherToReady() {
      console.log('設定畫面中的 carcher 位置');
      const gameBox = document.querySelector('#gameBox');
      const carcher = document.querySelector('#carcher');
      TweenMax.set(carcher, {
        x: (gameBox.clientWidth / 2) - (carcher.clientWidth / 2),
        y: gameBox.clientHeight - carcher.clientHeight - 40,
      });
    },
    /** 設定移動事件 */
    addkeyDownEvent() {
      document.addEventListener('keydown', this.keyDownEvent);
    },
    /** 解除移動事件 */
    removekeyDownEvent() {
      document.removeEventListener('keydown', this.keyDownEvent);
    },
    /** 鍵盤移動事件 */
    keyDownEvent(event) {
      const gameBox = document.querySelector('#gameBox');
      const carcher = document.querySelector('#carcher');

      const maxRange = gameBox.clientWidth - carcher.clientWidth; // 最大移動寬距
      const minRange = 0; // 最小移動寬距
      let moveX = 0;
      const moveXWidth = 80;
      const time = 0.3;

      if (event.keyCode && event.which === 39) {
        // ->
        moveX = (carcher._gsTransform.x + moveXWidth) > maxRange
          ? maxRange : carcher._gsTransform.x + moveXWidth;
      }

      if (event.keyCode && event.which === 37) {
        // <-
        moveX = (carcher._gsTransform.x - moveXWidth) < minRange
          ? minRange : carcher._gsTransform.x - moveXWidth;
      }

      TweenMax.to(carcher, time, { x: moveX });
    },
  },
  mounted: mountedCallback,
};
</script>

<style>
#gameBox {
  min-width: 300px;
  width: 100%;
  height: 500px;
  margin: auto;
  background: #666;
  overflow: hidden;
  position: relative;
  text-align: left;
}

#carcher {
  width: 16%;
  height: 20px;
  display: inline-block;
  background: lightblue;
  padding: 2px;
  text-align: center;
}

.gift {
  width: 20px;
  height: 20px;
  background: #e6e;
  border-radius: 15px;
  border: 1px solid #d3d;
  position: absolute;
}

.hide {
  display: none;
}

button {
  border: 1px solid #ddd;
  border-radius: 15px;
  padding: 2px 12px;
}
button:disabled {
  color: #ccc;
  background: #666;
}
</style>
