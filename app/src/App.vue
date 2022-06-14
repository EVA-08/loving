<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
  </div>
</template>
<script>
import StyleEditor from './components/StyleEditor'
import ResumeEditor from './components/ResumeEditor'
import './assets/reset.css'


let isPc = (function() {
  var userAgentInfo = navigator.userAgent;
  var Agents = ["Android", "iPhone",
    "SymbianOS", "Windows Phone",
    "iPad", "iPod"
  ];
  var flag = true;
  for (var v = 0; v < Agents.length; v++) {
    if (userAgentInfo.indexOf(Agents[v]) > 0) {
      flag = false;
      break;
    }
  }
  return flag;
}());
let getDateDiff = function(startDate, endDate) {
  var startTime = new Date(Date.parse(startDate.replace(/-/g, "/"))).getTime();
  var endTime = new Date(Date.parse(endDate.replace(/-/g, "/"))).getTime();
  var dates = Math.abs((startTime - endTime)) / (1000 * 60 * 60 * 24);
  return dates;
}
document.title += getDateDiff((new Date()).getFullYear() + '-' + ((new Date()).getMonth() + 1) + '-' + (new Date()).getDate(), '2016-09-15') + 1 + '天';
export default {
  name: 'app',
  components: {
    StyleEditor,
    ResumeEditor
  },
  data() {
    return {
      interval: 50,
      currentStyle: '',
      enableHtml: false,
      fullStyle: [
        `/*
* Hi。亲爱的！
* 现学了点前端的东西，给你玩一玩
* 先区分下手机和电脑
* 你的设备是...${isPc ? '电脑' : '手机'}
*/

/* 首先给所有元素加上过渡效果 */
* {
  -webkit-transition: all 1s;
  transition: all 1s;
}
/* 来点蓝黑背景 */
html {
  color: rgb(248,248,242);
  background: rgb(0,42,54);
}
/* 增大一下文字间距 */
.styleEditor {
  padding: .15em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  ${ isPc ? 'width: 48%;height: 96%;' : 'width: 96%;height: 50%;' };
  font-size: 18px;
  line-height:2;
}
/* 换成我常用的主题 */
.token.selector{ color: rgb(139,233,253) }
.token.property{ color: rgb(255,184,108) }
.token.punctuation{ color: rgb(248,248,242) }
.token.function{ color: rgb(80,250,123) }
.token.comment{ color: rgb(98,114,164) }

/* 调整一下 */
.styleEditor {
  transform-style: preserve-3d;
  -webkit-perspective: 500px;
          perspective: 500px;
  transform-origin: 250px 250px;
  ${ isPc ? 'left: 0;' : 'left:0;right:0;margin:auto;'}
  top: 0;
  ${ isPc ? '-webkit-transform: rotateY(10deg) translateZ(-100px) ;transform: rotateY(10deg) translateZ(-100px) ;' : '-webkit-transform: rotateX(-10deg) translateZ(-100px) ;transform: rotateX(-10deg) translateZ(-100px) ;' }
  ${ isPc ? '' : '-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;' }
}

/* 再来一张信纸 */
.resumeEditor{
  position: fixed;
  ${ isPc ? 'right: 0;' : 'left:0;right:0;margin:auto;'}
  ${ isPc ? 'top: 0;' : 'bottom:2%;'}
  padding: .5em;
  ${ isPc ? 'margin: .5em;' : ''}
  ${ isPc ? 'width: 48%;height: 96%;' : 'width: 96%;height: 50%;' }
  border: 1px solid;
  color: #222;
  overflow: auto;
  font-size: 18px;
  line-height: 2;
  ${ isPc ? '-webkit-transform: rotateY(-10deg) translateZ(-100px) ;transform: rotateY(-10deg) translateZ(-100px) ;' : '-webkit-transform: rotateX(10deg) translateZ(-100px) ;transform: rotateX(10deg) translateZ(-100px) ;' }
    ${ isPc ? '' : '-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;' }
  }
/* 现在给你写首诗 */

`,
        `
/* 是不是看着很简陋粗糙？
 * 因为这是 Markdown 格式的
 * 一种程序员用来写文档日志的简易语言
 * 翻译成 网页 就行了
 */
`,
        `
/* 再加点样式 */
.resumeEditor{
  padding: 2em;
  line-height:1.8;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
  font-size:18px;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor hr {
  margin-top: 1em;
  margin-bottom: 1em;
}

/*  */

`
      ],
      currentMarkdown: '',
      fullMarkdown: `

* 慵懒的早晨，温暖的床
* 看一眼纷繁的世界
* 再看看熟睡的你
* 呼吸均匀，小梦正香

----

* 忍不住将你抱起
* 忍不住逗你醒来
* 软软的脸蛋，红红的嘴唇
* 捏一捏心喜，亲一亲花开

----

* 你的可爱，我无法抵挡
* 你的美艳，我只有陶醉
* 春风扶腰细柳
* 苍穹皓齿明眸

----

* 你的智慧让我自叹
* 你的温柔让我心安
* 风火雷电予我启示
* 要做你的另一半

----

* 你是我最喜欢的人，是我的至爱
* 多么幸运能遇到你，多么难以置信的奇迹
* 和你永远在一起
* 是我的本命

----

* 从虚空中走来，又向虚空归去
* 曾经的我，没有初始化人生意义
* 你的到来赋予了我新的生活
* 也带给我生命的启迪

----

* You pull me from the matrix
* pull me from the mirror
* You guide me to actual world
* guide me to form my real

----

* 你也不完美，但犯错也可以带来欢乐
* 你也会脆弱，但哭泣会产生更大勇气
* 我们两个人，一起喜怒哀乐
* 一起走向命运的彼岸

----

* May us to retrive confidence
* May us to rebuild hometown
* May us to hold each other
* May us to be in love for long

----

* 枝枝相覆盖
* 叶叶相交通
* 鱼水俱赴海
* 云雨共向南

----

* At the end of our life
* I'll be next to your side
* Standing on the beach
* Waiting for the sunrise
`
    }
  },

  mounted() {
    this.makeResume()
  },

  methods: {
    makeResume: async function() {
      await this.progressivelyShowStyle(0)

      await this.progressivelyShowResume()
      await this.progressivelyShowStyle(1)
      await this.showHtml()
      await this.progressivelyShowStyle(2)
    },
    showHtml: function() {
      return new Promise((resolve, reject) => {
        this.enableHtml = true
        resolve()
      })
    },

    progressivelyShowStyle(n) {
      return new Promise((resolve, reject) => {
        let interval = 30
        let showStyle = (async function() {
          let style = this.fullStyle[n]
          if (!style) {
            return
          }
          // 计算前 n 个 style 的字符总数
          let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
          let prefixLength = length - style.length
          if (this.currentStyle.length < length) {
            let l = this.currentStyle.length - prefixLength
            let char = style.substring(l, l + 1) || ' '
            this.currentStyle += char
            if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
              this.$nextTick(() => {
                this.$refs.styleEditor.goBottom()
              })
            }
            setTimeout(showStyle, interval)
          } else {
            resolve()
          }
        }).bind(this)
        showStyle()
      })
    },
    progressivelyShowResume() {
      return new Promise((resolve, reject) => {
        let length = this.fullMarkdown.length
        let interval = 70
        let showResume = () => {
          if (this.currentMarkdown.length < length) {
            this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
            let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
            let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
            if (prevChar === '\n' && this.$refs.resumeEditor) {
              this.$nextTick(() => this.$refs.resumeEditor.goBottom())
            }
            setTimeout(showResume, interval)
          } else {
            resolve()
          }
        }
        showResume()
      })
    }
  }
}
</script>
<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

html {
  min-height: 100%;
}
.styleEditor {
  -webkit-backface-visibility: hidden;
}
</style>
