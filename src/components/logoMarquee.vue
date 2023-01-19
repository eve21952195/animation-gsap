<template>
  <div class="scroll logoOuter">
    <ul class="logoList">
      <li ref="logoArray" v-for="item in items(logomarWidth)" :key="item">
        <slot></slot>
      </li>
    </ul>
  </div>
</template>

<script>
import gsap from 'gsap'

export default {
  name: 'logoMarquee',
  data () {
    return {
      // 插入圖片寬度
      logomarWidth: 207,
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
    items (imageWidth) {
      return Math.ceil(this.width / imageWidth) * 2
    }
  },
  mounted () {
    // 動畫
    gsap.to('.logoList', {
      x: '-50%',
      duration: 18,
      ease: 'none',
      repeat: -1
    })
    gsap.to('.flower', {
      rotation: 360,
      duration: 6,
      ease: 'none',
      repeat: -1
    })
    // 利用 ResizeObserver 观察slot元素的长宽变化。為了在一開始就抓到 slot img 的寬度
    this.myObserver = new ResizeObserver((entries) => {
      entries.forEach((entry) => {
        this.logomarWidth = this.$slots.default[0].elm.clientWidth
      })
    })
    this.myObserver.observe(this.$slots.default[0].elm)
    // 對 window 監聽 resize 事件
    window.addEventListener('resize', this.resizeHandler)
  },
  beforeDestroy () {
    // 移除監聽
    window.removeEventListener('resize', this.resizeHandler)
    this.myObserver.unobserve(this.$slots.default[0].elm)
  }
}
</script>

<style scoped>
.scroll {
  width: 100%;
  overflow: hidden;
}
.logoOuter {
  height: 50px;
  border: 1px solid #d8d8d8;
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
.logoList li {
  display: flex;
}
.scroll .text {
  height: 50%;
}
.scroll .flower {
  padding: 0 6px;
}
</style>
