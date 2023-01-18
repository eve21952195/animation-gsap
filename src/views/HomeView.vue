<template>
<div class="container">
    <!-- 十字跑馬 -->
    <squareMarquee></squareMarquee>
    <!-- 頭部展示 -->
    <aboutItem></aboutItem>
    <!-- logo跑馬 -->
    <logoMarquee>
      <!-- slot -->
      <img
        class="text"
        src="https://northman-hokkaido.com/assets/parts/type-northmanhokkaido.svg"
        alt=""
      />
      <img
        class="flower"
        src="https://northman-hokkaido.com/assets/parts/icon-sevenstar-outline.svg"
        alt=""
      />
    </logoMarquee>
    <!-- 卡片群組 -->
    <slideCards></slideCards>
</div>
</template>

<script>
// 引入元件
import squareMarquee from '../components/squareMarquee.vue'
import logoMarquee from '../components/logoMarquee.vue'
import slideCards from '../components/slideCards.vue'
import aboutItem from '../components/aboutItem.vue'

export default {
  name: 'HomeView',
  components: {
    squareMarquee,
    logoMarquee,
    slideCards,
    aboutItem
  }
}
</script>

<style scoped>
.container {
  height: 700vh;
}
</style>
