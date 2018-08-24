<template>
<div class="CatcherGame">
  <div id="gameBox">
    <div id="catcher" class="catcher"
  >{{ CatcherContent }}</div>
  </div>

</div>
</template>

<script>
import TweenMax from 'gsap/TweenMax';
// import TimelineMax from 'gsap/TimelineMax';
// import EasePack from 'gsap';
// import Draggable from "gsap/Draggable";


/** mounted hook function */
function mountedCallback() {
  /** 設定 catcher 起始位置 */
  this.setCatcherToReady();
  /** 設定鍵盤移動事件 */
  this.addkeyDownEvent();
  /** 設定水平儀移動事件 */
  this.setDeviceOrientationEvent();
}

function onChangeOrientation(event) {
  const moveData = {
    alpha: Math.round(event.alpha),
    beta: Math.round(event.beta),
    gamma: Math.round(event.gamma),
  };
  console.log(moveData);
  return JSON.stringify(moveData);
}

export default {
  name: 'CatcherGame',
  data() {
    return {
      CatcherContent: '← -- →',
    };
  },
  components: {},
  methods: {
    /** 設定 catcher 起始位置 */
    setCatcherToReady() {
      console.log('設定畫面中的 catcher 位置');
      const gameBox = document.querySelector('#gameBox');
      const catcher = document.querySelector('#catcher');
      TweenMax.set(catcher, {
        x: (gameBox.clientWidth / 2) - (catcher.clientWidth / 2),
        y: gameBox.clientHeight - catcher.clientHeight - 40,
      });
    },
    /** 設定鍵盤移動事件 */
    addkeyDownEvent() {
      /** 先移除避免重複註冊 */
      this.removekeyDownEvent();
      document.addEventListener('keydown', this.keyDownEvent);
    },
    /** 解除移動事件 */
    removekeyDownEvent() {
      document.removeEventListener('keydown', this.keyDownEvent);
    },
    /** 鍵盤移動事件 */
    keyDownEvent(event) {
      const gameBox = document.querySelector('#gameBox');
      const catcher = document.querySelector('#catcher');

      const maxRange = gameBox.clientWidth - catcher.clientWidth; // 最大移動寬距
      const minRange = 0; // 最小移動寬距
      let moveX = 0;
      const moveXWidth = 80;
      const time = 0.3;

      if (event.keyCode && event.which === 39) {
        // ->
        moveX = (catcher._gsTransform.x + moveXWidth) > maxRange
          ? maxRange : catcher._gsTransform.x + moveXWidth;
      }

      if (event.keyCode && event.which === 37) {
        // <-
        moveX = (catcher._gsTransform.x - moveXWidth) < minRange
          ? minRange : catcher._gsTransform.x - moveXWidth;
      }

      TweenMax.to(catcher, time, { x: moveX });
    },
    /** 設定水平儀移動事件 */
    setDeviceOrientationEvent() {
      /** 先移除避免重複註冊 */
      this.removeDeviceOrientationEvent();
      if (window.DeviceOrientationEvent) {
        console.log('add Device Orientation Event');
        window.addEventListener('deviceorientation', onChangeOrientation, false);
      } else {
        // return false;
        console.log('not support orientation');
      }
    },
    removeDeviceOrientationEvent() {
      if (window.DeviceOrientationEvent) {
        console.log('remove Device Orientation Event');
        window.removeEventListener('deviceorientation', onChangeOrientation, false);
      }
    },
  },
  mounted: mountedCallback,
  /** 離開此 component 後需要移除事件 */
  beforeDestroy() {
    this.removekeyDownEvent();
    this.removeDeviceOrientationEvent();
  },
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

#catcher {
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
