<template>
    <div ref="dom"></div>
</template>

<script>
import echarts from 'echarts'
import { on, off } from '@/libs/tools'
export default {
  name: 'serviceRequests',
  data () {
    return {
      dom: null
    }
  },
  methods: {
    resize () {
      this.dom.resize()
    }
  },
  mounted () {
    const option = {
      tooltip: {
        trigger: 'axis',
        axisPointer: {
          type: 'cross',
          label: {
            backgroundColor: '#6a7985'
          }
        }
      },
      grid: {
        top: '3%',
        left: '1.2%',
        right: '1%',
        bottom: '3%',
        containLabel: true
      },
      xAxis: [
        {
          type: 'category',
          boundaryGap: false,
          data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
        }
      ],
      yAxis: [
        {
          type: 'value'
        }
      ],
      series: [
        {
          name: '心率',
          type: 'line',
          stack: '总量',
          areaStyle: { normal: {
            color: '#2d8cf0'
          } },
          data: [120, 111, 101, 99, 110, 120, 99]
        },
        {
          name: '血压',
          type: 'line',
          stack: '总量',
          areaStyle: { normal: {
            color: '#10A6FF'
          } },
          data: [115, 116, 120, 116, 113, 111, 112]
        },
        {
          name: '温度',
          type: 'line',
          stack: '总量',
          areaStyle: { normal: {
            color: '#0C17A6'
          } },
          data: [37, 26, 35, 29, 31, 30, 35]
        },
        {
          name: '湿度',
          type: 'line',
          stack: '总量',
          areaStyle: { normal: {
            color: '#4608A6'
          } },
          data: [60, 70, 55, 77, 66, 66, 77]
        }
        // {
        //   name: '快递/电商',
        //   type: 'line',
        //   stack: '总量',
        //   label: {
        //     normal: {
        //       show: true,
        //       position: 'top'
        //     }
        //   },
        //   areaStyle: { normal: {
        //     color: '#398DBF'
        //   } },
        //   data: [820, 645, 546, 745, 872, 624, 258]
        // }
      ]
    }
    this.$nextTick(() => {
      this.dom = echarts.init(this.$refs.dom)
      this.dom.setOption(option)
      on(window, 'resize', this.resize)
    })
  },
  beforeDestroy () {
    off(window, 'resize', this.resize)
  }
}
</script>
