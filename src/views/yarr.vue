<template>
  <div class="cyd" :id="`main2${value}${index}`"></div>
</template>

<script>
import { getCurrentInstance, watch, onMounted, reactive } from 'vue'

export default {
  props: {
    value: {
      type: Number
    },
    color: {
      type: String
    },
    index: {
      type: Number
    }
  },
  setup(props) {
    let echarts = ''
    let myChart = ''

    watch(
      props,
      (count) => {
        echinit2()
      }
    )
    onMounted(() => {
      echinit()
    })

    function echinit2 () {
      let a = 100 - props.value

      myChart.setOption({
        title: {
          text: props.value
        },
        series: [{
          data: [
            { value: a },
            { value: props.value }]
        }]
      })
    }
    function echinit () {
        echarts = getCurrentInstance().appContext.config.globalProperties.$echarts
        myChart = echarts.init(document.getElementById(`main2${props.value}${props.index}`));

        let a = 100 - props.value
        const opt = {
        legend: {
          top: '5%',
          left: 'center'
        },
        title: { //图中间文字样式
          text: props.value,  //图形标题，配置在中间对应效果图的80%
          left: "center",
          top: "40%",
          textStyle: {
            color:  props.color,
            fontSize: 16,
            align: "center"
          }
        },
        series: [{
          name: 'Access From',
          type: 'pie',
          radius: ['40%', '70%'],
          avoidLabelOverlap: false,
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
            { value: props.value },
          ],
          itemStyle: {
            normal: {
              color:function(params) {
                //自定义颜色
                var colorList = ['#f1f1f1', props.color];
                return colorList[params.dataIndex]
              }
            }
          },
          // 设置圆环图宽度
          radius: ["70%", "80%"] 
        }]
      }

      // 基于准备好的dom，初始化echarts实例
      
      myChart.setOption(opt, true) 
    }

    return {
      echinit
    }
  },
}
</script>

<style>
  .cyd {
    width: 70px;
    height: 100px;
  }
</style>