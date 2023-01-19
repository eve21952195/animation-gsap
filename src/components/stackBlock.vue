<template>
    <div class="cards">
      <div class="cardItem" v-for="(card, index) in cardsContent" :key="`card_${index}`">
        <div class="left">
          <div class="number">
            <div class="count">
              <span
                :style="{
                  backgroundImage: `url(https://northman-hokkaido.com/assets/parts/number0${
                    index + 1
                  }.svg)`,
                }"
              ></span>
            </div>
            <div class="star">
              <div class="icon"></div>
            </div>
            <div class="smallTitle">{{ card.smallTitle }}</div>
          </div>
          <div class="content">
            <h3>
              <span>{{ card.largeTitle01 }}</span>
              <span>{{ card.largeTitle02 }}</span>
            </h3>
            <div class="detail">
              <p>{{ card.text01 }}</p>
              <p>{{ card.text02 }}</p>
            </div>
          </div>
        </div>
        <div class="right">
          <div class="largeOuter">
            <img
              class="large"
              :src="`https://northman-hokkaido.com/assets/img/feature-${
                index + 1
              }l@1x.jpg`"
              alt=""
            />
          </div>
          <div
            class="rotateCard"
            :style="{
              backgroundImage: `url(https://northman-hokkaido.com/assets/img/feature-${
                index + 1
              }s@1x.jpg)`,
            }"
          ></div>
        </div>
      </div>
    </div>
</template>

<script>
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
// 註冊外掛
gsap.registerPlugin(ScrollTrigger)

export default {
  name: 'stackBlock',
  data () {
    return {
      cardsContent: [
        {
          smallTitle: 'PIE',
          largeTitle01: '半世紀続く伝統の',
          largeTitle02: 'パイ生地をアップデート',
          text01:
            '開発時からパイには多くのこだわりが詰まっています。噛んだ時の食感を楽しんでもらうために、バターを練り込んだ生地を500層に折り込み、さらに0度に温度管理した状態で一晩寝かせてから焼き上げ、時間を置いてしっとりさせることで薄い生地ながらも、しっかりと食感のあるパイ生地に仕上がっています。',
          text02:
            '今回は北海道産小麦粉を生地に配合し、より北海道を感じられる生地にしました。パイらしい食感を感じつつも中身のあんこと生クリームを邪魔せず全体が自然と馴染む味わいになっています。'
        },
        {
          smallTitle: 'CREAM',
          largeTitle01: '北海道産生クリームを',
          largeTitle02: 'たっぷり使用',
          text01:
            '北海道産生クリームをたっぷりと使用し、あんこの食感に合うようにふわふわに仕立てました。あんこ派にも生クリーム派にも喜んでもらえるバランスを目指し、通常のノースマンよりも少しあんこの量を少なくし、生クリームがたくさん入るように調整しています。',
          text02:
            '甘みを抑えて渋味の少ないあんこに、生クリームのみずみずしさと食感が組み合わさることでお口が喜ぶ食べ応えです。'
        },
        {
          smallTitle: 'RED BEAN PASTE',
          largeTitle01: '今も昔も変わらない',
          largeTitle02: '一手間かけた皮むき餡',
          text01:
            'ノースマンの開発時に皮を剥かない小豆をあんこを使うと渋みが出てパイとの相性が悪いことがわかりました。そこで一手間かけて皮をむき渋みを消した、皮むき餡が使われています。',
          text02:
            '今回の生ノースマンでも様々なあんこを試しましたが、やはりこれまでのあんこが一番でした。変わらないあんこでも生クリームとの出会いで新しい姿を見せてくれます。'
        }
      ]
    }
  },
  mounted () {
    ScrollTrigger.defaults({
      start: 'top 80%',
      scrub: true,
      markers: false,
      toggleActions: 'restart pause reverse pause'
    })
    // 外部大卡
    gsap.utils.toArray('.cardItem').forEach((item, index, arr) => {
      // 如果是最後一張
      if (index === arr.length - 1) {
        gsap.to(item, {
          scrollTrigger: {
            trigger: item,
            end: '+=2000'
          },
          ease: 'power2.inOut',
          y: -50 + 15 * index
        })
      } else {
        gsap.to(item, {
          scrollTrigger: {
            trigger: arr[index + 1],
            end: '+=1500'
          },
          ease: 'power2.inOut',
          y: -50 + 10 * index,
          scale: 0.94 - 0.02 * (arr.length - 1 - index),
          transformOrigin: '50% 0%'
        })
      }
    })
    // 內部小卡旋轉
    gsap.utils.toArray('.rotateCard').forEach((item) => {
      gsap.to(item, {
        scrollTrigger: {
          trigger: item,
          start: 'center bottom',
          end: '+=700'
        },
        rotation: 35,
        y: 40
      })
    })
    // 右側圖片變小
    gsap.utils.toArray('.large').forEach((item, index) => {
      gsap.to(item, {
        scrollTrigger: {
          trigger: item,
          start: 'top bottom',
          scrub: false
        },
        scale: 1,
        duration: 1.5,
        ease: 'power1.inOut'
      })
    })
    gsap.to('.star', {
      rotation: 360,
      repeat: -1,
      duration: 4,
      ease: 'none'
    })
  }
}
</script>

<style scoped>
.cards {
  padding: 50px 3.5vh 0;
  height: 600vh;
}
.rotateCard {
  background-color: rgb(225, 225, 225);
  width: 18vw;
  height: 23vw;
  border-radius: 20px;
  transform: rotate(2deg);
  transform-origin: 100% 100%;
  position: absolute;
  right: 8vw;
  bottom: 9vh;
  background-image: url("https://northman-hokkaido.com/assets/img/feature-1s@1x.jpg");
  background-size: cover;
}
.cardItem {
  border: 2px solid #d8d8d8;
  height: 70vh;
  margin-bottom: 14vh;
  position: sticky;
  border-radius: 50px;
  background-color: #fff;
  top: 60px;
  padding: 3.5714285714vw;
  display: flex;
}
.left {
  /* background-color: lightblue; */
  width: 50%;
}
.right {
  /* background-color: pink; */
  height: 100%;
  width: 50%;
}
.number {
  display: flex;
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
.count {
  width: 22px;
  height: 18px;
}
.count span {
  /* border: 1px solid blue; */
  display: block;
  height: 100%;
  background-repeat: no-repeat;
  background-position: center;
}
.number .star {
  width: 80px;
}
.number .star .icon {
  height: 100%;
  background-image: url("../assets/icon-sevenstar-orange.svg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
}
.smallTitle {
  display: flex;
  align-items: center;
}
/* 內文 */
.content {
  width: 32vw;
  /* border: 1px solid red; */
  position: absolute;
  top: 18%;
  left: 10%;
}
.detail p {
  font-size: 16px;
}
/* 左大圖 */
.largeOuter {
  border-radius: 30px;
  width: 39.2857142857vw;
  height: 100%;
  background-color: pink;
  overflow: hidden;
}
.large {
  width: 100%;
  height: 100%;
  transform: scale(1.2);
}
</style>
