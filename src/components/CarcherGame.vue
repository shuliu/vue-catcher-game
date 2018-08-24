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

/** mounted hook function */
function mountedCallback() {
  /** 設定 carcher 起始位置 */
  this.setCarcherToReady();
  /** 設定畫面 */
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
    setCarcherToReady: () => {
      console.log('設定畫面中的 carcher 位置');
      const gameBox = document.querySelector('#gameBox');
      const carcher = document.querySelector('#carcher');
      TweenMax.set(carcher, {
        x: (gameBox.clientWidth / 2) - (carcher.clientWidth / 2),
        y: (gameBox.clientHeight - carcher.clientHeight) - 40,
      });
    },
    keyMove: (event) => {
      console.log(event);
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
  background: #E6E;
  border-radius: 15px;
  border: 1px solid #D3D;
  position: absolute;
}

.hide {
  display: none;
}

button {
  border: 1px solid #DDD;
  border-radius: 15px;
  padding: 2px 12px;
}
button:disabled {
  color: #CCC;
  background: #666;
}
</style>
