<template>
    <div class="scroll logoOuter">
      <ul class="logoList">
        <li ref="logoArray" v-for="item in items(logomarWidth)" :key="item">
          <slot>
          </slot>
          <img
            class="flower"
            src="https://northman-hokkaido.com/assets/parts/icon-sevenstar-outline.svg"
            alt=""
          />
        </li>
      </ul>
    </div>
</template>

<script>
// 引入 gsap
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
    items (e) {
      return Math.ceil(this.width / (e + 32)) * 2
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
    // 利用 ResizeObserver 观察原素的长宽变化
    const myObserver = new ResizeObserver((entries) => {
      console.log(entries)
      entries.forEach((entry) => {
        console.log('entry宽度', entry.contentRect.width)
        // 取得 插槽的節點寬度
        console.log('slot', this.$slots.default[0].elm.clientWidth)
        console.log(this.$slots)
        this.logomarWidth = this.$slots.default[0].elm.clientWidth
      })
    })
    if (myObserver) {
      myObserver.observe(this.$slots.default[0].elm)
    }
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
.logoOuter {
  height: 50px;
  border: 1px solid #d8d8d8;
}
.scroll > ul {
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
