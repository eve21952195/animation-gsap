<template>
    <section class="about">
      <div class="about-title">
        <div class="label-title">
          <span>BRAND NEW NORTHMAN</span>
          <div class="star">
            <img src="../assets/icon-sevenstar-black.svg" alt="" />
          </div>
        </div>
        <h2 class="name-logo">
          <svg width="95" height="70" viewBox="0 0 95 70">
            <defs>
              <mask id="mask">
                <!-- 遮罩的顏色 + 遮罩的形狀 -->
                <path
                  fill="#fff"
                  d="M82.13,42.24l4.25-9.9h-19.53l4.84-11.27h19.45l4.5-10.49h-19.45L80.69,.1h-22.55l-4.5,10.48h-10.94L47.24,0H30.21c-1.49,3.68-2.92,7.12-4.21,10.02-2.67,6.03-12.94,11.46-17.81,11.46l-3.95,9.2c3.98,0,10.41-.6,13.19-1.2,3.95-.86,11.15-4.08,14.57-6.12,1-.6,2.09-1.39,3.16-2.3h13.97l-4.84,11.27H24.35l-4.25,9.9h19.94l-7.97,18.56H4.37L.42,70H75.52l3.95-9.2h-24.85l7.97-18.56h19.54Z"
                ></path>
              </mask>
            </defs>
            <rect
              id="logo1"
              x="0"
              y="0"
              width="100%"
              height="100%"
              fill="#f04933"
              mask="url(#mask)"
            />
            <rect
              id="logo2"
              x="0"
              y="0"
              width="100%"
              height="100%"
              fill="#232742"
              mask="url(#mask)"
            />
          </svg>
          <img src="../assets/logo-northman.svg" alt="" />
        </h2>
      </div>
      <div class="about-layout">
        <div class="about-img">
          <div class="pic1">
            <img
              src="https://northman-hokkaido.com/assets/img/aboutnama-1@1x.jpg"
              alt=""
            />
          </div>
          <div class="pic2">
            <img
              src="https://northman-hokkaido.com/assets/img/aboutnama-2@1x.jpg"
              alt=""
            />
          </div>
        </div>
        <div class="about-body">
          <h3 class="about-headline">
            <span>ノースマンらしさを残しながら</span>
            <span>進化した、生ノースマン</span>
          </h3>
          <div class="about-content">
            <p>和菓子と洋菓子の融合した第3のお菓子として生まれたノースマン。</p>
            <p>
              あんこを主役にするために薄めでしっとりしたパイで包んでいます。さらに今回は生クリームをたっぷり入れ、お馴染みの味をリッチに進化させました。
            </p>
            <p>
              あんこ、パイ、生クリームが合わさる食感と風味のハーモニーをお楽しみください。
            </p>
          </div>
        </div>
      </div>
    </section>
</template>

<script>
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
// 註冊外掛
gsap.registerPlugin(ScrollTrigger)

export default {
  name: 'aboutSection',
  data () {
    return {
      titleAnimate: {}
    }
  },
  mounted () {
    ScrollTrigger.defaults({
      start: 'top 80%',
      scrub: true,
      markers: false,
      toggleActions: 'restart pause reverse pause'
    })
    // 左小圖縮放
    gsap.to('.pic1 img', {
      scrollTrigger: {
        trigger: '.pic1 img',
        start: 'center bottom',
        scrub: false
      },
      scale: 1,
      duration: 1,
      ease: 'power1.out'
    })
    // 標題往上長動畫
    this.titleAnimate = gsap.timeline()
    this.titleAnimate
      .to('#logo1', {
      // 往內縮0%，相當於完整露出
        clipPath: 'inset(0% 0% 0% 0%)',
        duration: 2,
        repeat: -1,
        repeatDelay: 7,
        ease: 'power1.out'
      })
      .to('#logo2', {
        clipPath: 'inset(0% 0% 0% 0%)',
        duration: 2,
        repeat: -1,
        repeatDelay: 7,
        ease: 'power1.out'
      }, '<0.5')
  }
}
</script>

<style scoped>
.about {
  height: 120vh;
  padding: 14.2857142857vw 7.1428571429vw;
}
.about-title {
  display: flex;
  margin: 7.1428571429vw 3.5714285714vw 7.1428571429vw 0;
  justify-content: flex-end;
  align-items: flex-start;
}
.label-title {
  display: flex;
  justify-content: center;
  align-items: center;
}
.label-title span {
  white-space: nowrap;
  font-size: 21px;
}
.label-title .star {
  margin-left: 12px;
  width: 20px;
  height: 20px;
}
.label-title .star img {
  width: 100%;
  height: 100%;
}
.name-logo {
  height: 153px;
  display: flex;
}
.name-logo svg {
  height: 100%;
  width: 230px;
}
.name-logo img {
  height: 100%;
  margin-left: -30px;
}
/* --logo遮罩動畫-- */
#logo1 {
  /* 上方往內壓縮100%，相當於消失隱藏。選擇上方是為了出現的方向性  */
  clip-path: inset(100% 0 0 0);
}
#logo2 {
  clip-path: inset(100% 0 0 0);
}
.about-layout {
  display: flex;
}
.about-img {
  width: 35vw;
  position: relative;
}
.about-img .pic1 {
  height: 27.55102vw;
  width: 21.4285714286vw;
  border-radius: 30px;
  overflow: hidden;
  position: absolute;
  top: 0;
  left: 0;
}
.about-img .pic1 img {
  width: 100%;
  height: 100%;
  transform: scale(1.2);
}
.about-img .pic2 {
  height: 32.1428571429vw;
  width: 25vw;
  border-radius: 30px;
  overflow: hidden;
  position: absolute;
  top: 11.5vw;
  left: 11.5vw;
}
.about-img .pic2 img {
  width: 100%;
  height: 100%;
}
.about-body {
  width: 50vw;
  position: relative;
  /* background-color: blue; */
}
.about-headline {
  font-size: 3.3333333333vw;
  margin-top: 50px;
}
.about-content {
  background-color: #fff;
  margin: 5.3571428571vw 3.5714285714vw 3.5714285714vw 14.2857142857vw;
  font-size: 24px;
}
h3 {
  font-weight: 500;
  line-height: 1.6;
  font-size: 36px;
  padding-bottom: 45px;
}
span{
  display: block;
}
p {
  text-align: left;
  line-height: 1.6;
  padding: 10px 0;
  font-weight: 100;
}

</style>
