<template>
  <div>
    <Row :gutter="20">
      <i-col :xs="12" :md="8" :lg="4" v-for="(infor, i) in inforCardData" :key="`infor-${i}`" style="height: 120px;padding-bottom: 10px;">
        <infor-card shadow :color="infor.color" :icon="infor.icon" :icon-size="36">
          <count-to :end="infor.count" count-class="count-style"/>
          <p>{{ infor.title }}</p>
        </infor-card>
      </i-col>
    </Row>
    <Row :gutter="20" style="margin-top: 10px;">
      <i-col :md="24" :lg="8" style="margin-bottom: 20px;">
        <Card shadow>
          <chart-pie style="height: 300px;" :value="pieData" text="用户访问来源"></chart-pie>
        </Card>
      </i-col>
      <i-col :md="24" :lg="16" style="margin-bottom: 20px;">
        <Card shadow>
          <chart-bar style="height: 300px;" :value="barData" text="每周用户活跃量"/>
        </Card>
      </i-col>
    </Row>
    <Row>
      <Card shadow>
        <example style="height: 310px;"/>
      </Card>
    </Row>
  </div>
</template>

<script>
import InforCard from '_c/info-card'
import CountTo from '_c/count-to'
import { ChartPie, ChartBar } from '_c/charts'
import Example from './example.vue'
export default {
  name: 'myData',
  components: {
    InforCard,
    CountTo,
    Example
  },
  data () {
    return {
      inforCardData: [
        { title: '心率', icon: 'md-person-add', count: 60, color: '#2d8cf0' },
        { title: '血压', icon: 'md-locate', count: 115, color: '#19be6b' },
        // { title: '血氧', icon: 'md-help-circle', count: 142, color: '#ff9900' },
        { title: '温度', icon: 'md-share', count: 37, color: '#ed3f14' },
        { title: '湿度', icon: 'md-chatbubbles', count: 78, color: '#E46CBB' }
        // { title: '新增页面', icon: 'md-map', count: 14, color: '#9A66E4' }
      ]

    }
  },
  mounted () {
    //
  }
}
</script>

<style lang="less">
.count-style{
  font-size: 50px;
}
</style>
