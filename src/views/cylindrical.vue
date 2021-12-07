<template>
  <!-- 单个颜色组件 -->
  <a class="box">
    <div class="chunk" :style="{ backgroundColor: arrs.v }"></div>
    <div class="midclo">
      <div class="mcy">
        <div v-for="(i, index) in arrs.value" :id="`main${i}${arrs.c2}${index}`"></div>
      </div>
      <div :style="{ color: arrs.v }">
        {{arrs.c}}
      </div>
    </div>
    <div class="butbox">
      <div style="margin-bottom: -16px; color: #E8E8E8; font-size: 15px;">{{arrs.c2.toUpperCase()}}</div>
      <div style="margin-bottom: 15px;">
        <div class="pro" v-for="j in arrs.val">
          <progress id="pg" max="255" :value="j"></progress>
        </div>
      </div>
      <div style="color: #E8E8E8; font-size: 13px;">{{arrs.v}}</div>
    </div>
  </a>
</template>

<script>
import { getCurrentInstance } from 'vue'
export default {
  data() {
    return {
    }
  },
  props: {
    arrs: {
      type: Object
    }
  },
  mounted() {
    // 绘制图表
    let echarts = getCurrentInstance().appContext.config.globalProperties.$echarts
    for(let i in this.arrs.value) {
      let a = 100 - this.arrs.value[i]
      const opt = {
      legend: {
        top: '5%',
        left: 'center'
      },
      series: [{
          name: 'Access From',
          type: 'pie',
          radius: ['40%', '70%'],
          avoidLabelOverlap: false,
          label: {
            normal: {
              
            }
          },
          emphasis: {
            label: {
              show: true,
              fontSize: '40',
              fontWeight: 'bold'
            }
          },
          labelLine: {
            show: false
          },
          data: [
            { value: a },
            { value: this.arrs.value[i] },
          ],
          itemStyle: {
            normal: {
              color:function(params) {
                //自定义颜色
                var colorList = ['#f1f1f1', '#E1E1E1'];
                return colorList[params.dataIndex]
              }
            }
          },
          // 设置圆环图宽度
          radius: ["40%", "80%"] 
        }]
      }
      // 基于准备好的dom，初始化echarts实例
      var myChart = echarts.init(document.getElementById(`main${this.arrs.value[i]}${this.arrs.c2}${i}`));
      myChart.setOption(opt) 
    }
  }
}
</script>

<style scoped lang="less">
  .box {
    width: 50px;
    cursor: pointer;
    margin-bottom: 130px;
    margin-left: 10px;
    .chunk {
      width: 100%;
      height: 8px;
      background-color: #ddd;
      margin-bottom: 10px;
    }
    .midclo {
      display: flex;
      justify-content: space-around;
      .mcy {
        > div {
          width: 30px;
          height: 30px;
        }
      }
    }
  }
  #main {
    width: 150px;
    height: 220px;
  }
  .butbox {
    transform:rotate(90deg);
    .pro {
      height: 5px;
    }
    progress{
      width: 168px;
      height: 3px;
      color:#f00;
      background:#EDEDED;
    }
    /* 表示总长度背景色 */
    progress::-webkit-progress-bar{     
      background-color:#ddd;
    }
    /* 表示已完成进度背景色 */
    progress::-webkit-progress-value{
        background-color:#EDEDED;
    }
  }

</style>