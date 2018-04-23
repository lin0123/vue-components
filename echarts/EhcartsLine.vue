<template>
  <div class="tmpl-ehcarts-line">
    <div ref="echartsLine" class="echarts-line">      
    </div>
  </div>
</template>

<script>
  let echarts = require('echarts');
  export default {
    name: 'ehcarts-line',
    props: {
    },
    components: {
    },
    created () {
    },
    mounted () {
      this.renderEchartsLine(this.data);
    },
    data () {
      return {
        myChart: null,
        data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子'],
        toolTip: '这是备注内容',
      };
    },
    methods: {
      showPopup () {
        this.isPopMove = true;
      },
      callback (params) {
        // console.log(params);
        return `点击编辑</br>${params.name}${params.data}</br>备注</br>${this.toolTip}`;
      },
      renderEchartsLine (data) {
        // 基于准备好的dom，初始化echarts实例
        let vm = this;
        this.myChart = echarts.init(this.$refs.echartsLine);
        window.onresize = this.myChart.resize;
        // 绘制图表
        this.myChart.setOption({
          title: {
            text: 'ECharts',
          },
          tooltip: {
            type: 'line',
            axisPointer: {
              snap: true,
              // type: 'cross',
              // axis: 'auto',
            },
            enterable: true,
            // position: [20, 40],
            label: {
              show: false,
            },
            // trigger: 'axis',
            formatter: vm.callback,
          },
          legend: {
            data: ['销量'],
          },
          xAxis: {
            data: data,
            // nameLocation: 'middle',
          },
          yAxis: {},
          series: [
            {
              name: '销量',
              type: 'line',
              data: [5, 20, 36, 10, 10, 20],
            },
            {
              name: '量化',
              type: 'line',
              data: [90, 100, 136, 110, 190, 220],
            },
          ],
          // 高亮样式。
          emphasis: {
            itemStyle: {
              // 高亮时点的颜色。
              color: 'blue',
            },
            // label: {
            //   show: true,
            //   // 高亮时标签的文字。
            //   formatter: '显示高亮的tip',
            // },
          },
        });
        this.myChart.dispatchAction(
          {
            type: 'highlight',
            // 可选，系列 index，可以是一个数组指定多个系列
            seriesIndex: 2,
            // 可选，系列名称，可以是一个数组指定多个系列
            seriesName: '测试',
            // 可选，数据的 index
            dataIndex: 3,
            // 可选，数据的 名称
            name: '是',
          },
        );
        this.myChart.on('click', (params) => {
          console.log('dianji');
        });
      },
    },
    beforeDestroy () {
      this.myChart.dispose;
    },
  };
</script>

<style lang="stylus" scoped>
  font-size(n)
    n = unit(n, 'px')
    font-size: n
    [data-dpr="2"] &
      font-size: n * 2
    [data-dpr="3"] &
      font-size: n * 3

  rem(pixel, context = 75)
    (pixel / context) * 1rem
  .tmpl-ehcarts-line
    font-size(16)
    .echarts-line
      width 100%
      height rem(400)
  
</style>
