<template>
  <div class="home">
    TITLE
    <div id="Map" style="width:1000px;height:1000px;background-color:red;margin:0 auto;"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts'
import 'echarts-gl'

export default {
  name: 'Home',
  components: {
  },
  data() {
    return {
      areaCode: 110000,
    }
  },
  mounted() {
    this.initMap()
  },
  methods: {
    initMap() {
      // 获取地图数据
      let geoJson = require('./ChinaMap/' + this.areaCode + '.json')
      console.log({geoJson})
      echarts.registerMap('china', geoJson, {});
      let chartDom = document.getElementById('Map');
      console.log({chartDom})
      let myChart = echarts.init(chartDom);
      let option = this.getMapData();
      console.log({option})
      myChart.setOption(option)
    },
    getMapData() {
      return {
        geo3D: {
          map: 'china',
          boxWidth: 100,
          boxHeight: 100,
          boxDepth: 80,
          // roam: true,
          itemStyle: {
            color: '#072041',
            opacity: 1,
            borderWidth: 2,
            borderColor: '#0C6DAA'
          },
          label: { // 标签的相关设置
            show: true, // (地图上的城市名称)是否显示标签 [ default: false ]
            // distance: 50, // 标签距离图形的距离，在三维的散点图中这个距离是屏幕空间的像素值，其它图中这个距离是相对的三维距离
            // formatter:, // 标签内容格式器
            textStyle: { // 标签的字体样式
              color: '#fff', // 地图初始化区域字体颜色
              fontSize: 12, // 字体大小
              opacity: 1, // 字体透明度
              backgroundColor: 'transparent' // 字体背景色
            },
          },
          // viewControl: {
          //   distance: 100,// 地图视角 控制初始大小
          //   rotateSensitivity: 100,// 旋转
          //   zoomSensitivity: 200,// 缩放
          // },
          // label: {
          //   show: true,
          //   distance: 0,
          //   textStyle: { // 标签的字体样式
          //     color: '#fff', // 地图初始化区域字体颜色
          //     fontSize: 30, // 字体大小
          //     opacity: 1, // 字体透明度
          //     backgroundColor: 'transparent' // 字体背景色
          //   },
          // },
          //
          emphasis: { //当鼠标放上去  地区区域是否显示名称
            label: {
              show: true,
              textStyle: {
                color: '#fff',
                fontSize: 30,
                backgroundColor: 'rgba(0,23,11,0)'
              }
            },
            itemStyle: {
              color: '#FFF'
            }
          },
          light: { //光照阴影
            main: {
              color: '#fff', //光照颜色
              intensity: 1, //光照强度
              shadow: false, //是否显示阴影
              alpha: 55,
              beta: 10
            },
            ambient: {
              intensity: 1
            }
          }
        },
      }
    }
  }
}
</script>
