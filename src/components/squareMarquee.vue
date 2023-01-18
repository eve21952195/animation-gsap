<template>
  <div class="scroll squareOuter">
    <ul class="squareList">
      <li v-for="item in items(crossmar)" :key="item">
        <img class="square_bc" src="../assets/square_bc.svg" alt="" />
        <img
          class="cross cross01"
          src="../assets/square_cross_blue.svg"
          alt=""
        />
        <img
          class="cross cross02"
          src="../assets/square_cross_red.svg"
          alt=""
        />
        <img
          class="cross cross03"
          src="../assets/square_cross_blue.svg"
          alt=""
        />
        <img
          class="cross cross04"
          src="../assets/square_cross_red.svg"
          alt=""
        />
      </li>
    </ul>
  </div>
</template>

<script>
import gsap from 'gsap'

export default {
  name: 'squareMarquee',
  data () {
    return {
      marqueeAnimate: {},
      crossmar: 178,
      // 取得視窗寬度
      width: document.documentElement.clientWidth
    }
  },
  methods: {
    // 取得視窗寬度的方法
    resizeHandler () {
      this.width = document.documentElement.clientWidth
    },
    // 隨著視窗寬度變化，計算需要幾組li(*2是因為要前後兩組)
    items (target) {
      return Math.ceil(this.width / target) * 2
    }
  },
  mounted () {
    this.marqueeAnimate = gsap.timeline()
    this.marqueeAnimate
      .to('.cross', {
        rotation: 360,
        duration: 4,
        repeat: -1,
        ease: 'power4.out',
        stagger: 0.05
      })
      .to('.squareList', {
        x: '-50%',
        duration: 20,
        repeat: -1,
        yoyo: true,
        ease: 'steps(20)'
      }, '<1')
    // 對 window 監聽 resize 事件
    window.addEventListener('resize', this.resizeHandler)
  },
  beforeDestroy () {
    // 移除監聽
    window.removeEventListener('resize', this.resizeHandler)
  }
}
</script>

<style scoped>
.scroll {
  width: 100%;
  overflow: hidden;
}
.scroll > ul {
  margin: 0;
  padding: 0;
  list-style: none;
  display: flex;
  height: 100%;
  width: max-content;
}
.scroll > ul > li {
  /* 不要被壓縮 */
  flex-shrink: 0;
  /* outline: 1px solid orange; */
  justify-content: center;
  align-items: center;
}
/* svg方塊跑馬 */
.squareList > li {
  height: 77px;
  width: 178px;
  position: relative;
}
.square_bc {
  width: 100%;
  height: 100%;
}
.square_bc ~ img {
  position: absolute;
}
.cross01 {
  left: -2px;
}
.cross02 {
  left: 88px;
}
.cross03 {
  left: 42px;
  top: 52px;
}
.cross04 {
  left: 133px;
  top: 52px;
}

</style>
