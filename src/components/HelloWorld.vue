<template lang='pug'>
#hello
  .loading
    .square 無畏無懼
    .square2 11/06
    .square3 見證搖滾盛典
    .star-wrap
      .triangle
      .triangle-r
  .q(v-for="(problem, pId) in problems",:class="{qhide: pId != currentStep}", :id="'q-'+pId", :key="problem.id" v-if="start")
    .sec-left(:id="'left-'+pId")
      .question-frame
        h1 {{problem.id}}
        .question {{problem.title}}
        .remark {{problem.subTitle}}
        .options(v-for="option in problem.answer")
          .option(@click="answer(pId,option.point)") {{option.option}}
  #done-wrap
    h1 感謝您的參與!
    h3 獲獎者將於10/31前由CheerLife專人通知
    p  《波希米亞狂想曲》電影首映會
     |
     br
     | 開演時間 : 11/06(二) 19:30
     |
     br
     | 地點 : 哈拉影城(台北市內湖區康寧路三段72號) 影廳4樓5廳
    .option
      a(v-bind:href="hala") 如何前往
    .option
      a(v-bind:href="link") 電影預告
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
// import qs from 'qs'

Vue.prototype.$axios = axios
Vue.prototype.$ajax = axios
Vue.use(VueAxios, axios)

export default {
  name: 'HelloWorld',
  data () {
    return {
      problems: [
        {
          id: 'Q',
          title: '最喜愛的CheerLife功能是?',
          subTitle: '回答就有機會得到六福村雙人票呦',
          answer: [{
            option: '特約優惠識別證',
            point: 1
          }, {
            option: '美食車送餐',
            point: 2
          }, {
            option: '票券優惠',
            point: 3
          }, {
            option: '地圖查找',
            point: 4
          }]
        }
      ],
      currentStep: 0,
      totalPoint: 0,
      filltime: '',
      name: '',
      userID: '',
      start: false,
      isRouterAlive: true,
      link: 'https://www.youtube.com/watch?v=2w3WtmVdsU0&feature=youtu.be',
      hala: 'https://goo.gl/maps/PWhncXhxcMB2'
    }
  },
  methods: {
    reload () {
      this.$router.go(0)
    },
    answer (questionId, point) {
      console.log(questionId + ' ' + point)
      // this.totalPoint += process.initgroups()
      this.loadingTransform(questionId, point)
    },
    loadingTransform (questionId, point) {
      if (questionId === 0) {
        let leftTag = document.getElementById('left-' + questionId)
        leftTag.classList.add('qhide')
        let nextTag = document.getElementById('done-wrap')
        nextTag.style.display = 'inline-block'
        let userID = location.search.substring(1)
        let filltime = String(new Date())
        this.submitForm(point, filltime, userID)
      }
    },
    submitForm (point, filltime, userID) {
      axios.get('https://script.google.com/macros/s/AKfycbxAtwkPB43ME-0zndShEgdsfMjYxHmOcw_wbOxSH9xCOjRJLFmZ/exec',
        {
          params: {
            name: userID,
            answer: point,
            time: filltime
          }
        })
        .then(function (response) {
          console.log(response)
        })
        .catch(function (error) {
          console.log(error)
        })
    }
  },
  mounted () {
    console.log('mounted')
    setTimeout(() => {
      this.start = true
      // let app = document.getElementById('app')
      // app.classList.add('bg2')
    }, 4000)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
$vue-color: #fad033;
h1 {
  color: $vue-color;
}
h3{
  color:#fff;
}
</style>
