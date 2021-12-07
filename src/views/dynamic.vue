<template>
  <!-- 旁边动态框组件 -->
  <div class="ddd">
    <div class="box">
      <div v-for="(i, index) in clicolor.value" class="mcy">
        <div class="cyd1">
          {{cmyk2[index]}}
        </div>
        <yarr :value="i" :color="color[index]" :index="index" />
      </div>
      <div v-for="(i, index) in ['r','g','b']" id="box2" :class="`d${i}`">
        <div class="ii">{{i.toUpperCase()}}</div>
        <div v-show="pro2[index] > 100 || flag" :class="`box${i}1`">
          <div class="a1">0</div>
          <div class="a1">1</div>
          <div class="a1">2</div>
          <div class="a1">3</div>
          <div class="a1">4</div>
          <div class="a1">5</div>
          <div class="a1">6</div>
          <div class="a1">7</div>	
          <div class="a1">8</div>	
          <div class="a1">9</div>
        </div>
        <div v-show="pro2[index] < 100 && !flag" style="width: 17px; height: 70px; margin-left: 12px"></div>
        <div :class="`box${i}2`">
          <div class="a2">0</div>
          <div class="a2">1</div>
          <div class="a2">2</div>
          <div class="a2">3</div>
          <div class="a2">4</div>
          <div class="a2">5</div>
          <div class="a2">6</div>
          <div class="a2">7</div>	
          <div class="a2">8</div>	
          <div class="a2">9</div>
        </div>
        <div :class="`box${i}3`">
          <div class="a2">0</div>
          <div class="a2">1</div>
          <div class="a2">2</div>
          <div class="a2">3</div>
          <div class="a2">4</div>
          <div class="a2">5</div>
          <div class="a2">6</div>
          <div class="a2">7</div>	
          <div class="a2">8</div>	
          <div class="a2">9</div>
        </div>
      </div>
    </div>
    <div class="font">
      <div class="font-1">
        {{clicolor.c}}
      </div>
      <div class="font-2">
        {{clicolor.c2.toUpperCase()}}
      </div>
    </div>
    <h2>
       
    </h2>
  </div>

</template>

<script>
import { ref, reactive, watch, onMounted } from 'vue'
import yarr from './yarr.vue'

export default {
  data() {
    return {
      cmyk2: ['C', 'M', 'Y', 'K'],
      color: ['#1599D3', '#CD1A78', '#FEF011', '#474747']
    }
  },
  components: {
    yarr
  },
  props: {
    clicolor: {
      type: Object,
      default: {
        value: [0, 0, 0, 0],
        val: [255, 255, 255],
      }
    }
  },
  setup(props, context) {
    watch(
      props,
      (count) => {
        pro = props.clicolor.val
        flag.value = true
        cli()
      }
    )

    onMounted(() => {
      cli()
    })
    let pro = props.clicolor.val
    let pro2 = reactive({})
    let flag = ref(true)

    function cli () {
      let a = 0
      let n
      numflag()
      
      for(let i of ['r', 'g', 'b']) {
        let bpx = document.getElementsByClassName(`box${i}1`)
        bpx[0].style.transform = `translateY(-${pro[a].toString()[0] * 70}px)`
        let bpx2 = document.getElementsByClassName(`box${i}2`)
        bpx2[0].style.transform = `translateY(-${pro[a].toString()[1] * 70}px)`
        let bpx3 = document.getElementsByClassName(`box${i}3`)
        bpx3[0].style.transform = `translateY(-${pro[a].toString()[2] * 70}px)`
        ++a
      }

      setTimeout(() => {
        flag.value = false
        Object.assign(pro2, pro)
      }, 1000)
      
    }

    function numflag () {
      let arr = []
      console.log(pro);
      for(let n of pro) {
        if(n < 100 && n > 10) {
           arr.push('0'+ n)
        } else if(n < 10) {
          arr.push('00' + n)
        } else {
          arr.push(n)
        }
      }
      pro = arr
      
    }

    return {
      numflag, cli, pro2, flag
    }
  },
  methods: {

  }
}
</script>

<style scoped lang="less">
  .ddd {
    position: fixed;
    display: flex;
    margin-left: 100px;
  }
  .box {
    position: relative;
    width: 70px;
    height: 540px;
  }
  #box2 {
    position: relative;
    display: flex;
    height: 53px;
    width: 70px;
    overflow: hidden;
    border-bottom: 1px solid #fff;
    color: #fff;
    .ii {
      position: absolute;
      font-size: 15px;
      
    }
    > div {
      position: relative;
      transition: all 1s ease;
      > div {
        width: 17px;
        height: 70px;
        text-align: right;
        line-height: 65px;
        font-size: 28px;
        font-weight: 300;
      }
      .a1 {
        margin-left: 12px;
      }
    }
  }
  .mcy {
    position: relative;
    .cyd1 {
      position: absolute;
      left: 3px;
      top: 3px;
      color: #fff;
    }
  }
  .font {
    text-align: center;
    margin-left: 70px;
  }
  .font-1 {
    font-family: 'lixukexingshu1b969ad7dc1c3e5';
    font-size: 100px;
    color: #fff;
    writing-mode: tb-rl;
    letter-spacing: .5em;
  }
  .font-2 {
    font-family: Georgia;
    color: #fff;
    font-size: 16px;
    font-weight: 700;
  }
  h2 {
    height: 520px;
    width: 60px;
    background-image: url('../img/logo.png');
    background-repeat: no-repeat;
    margin-left: 70px;
  }
</style>