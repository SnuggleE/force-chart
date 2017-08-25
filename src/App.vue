<template>
  <div id="app">
    <div ref="chart" class="chart"></div>
  </div>
</template>

<script>
  import echarts from 'echarts'
export default {
  name: 'app',
  data(){
      return{
          relationData:{
              links:[
                {
                    id:null,
                  source:0,
                  target:1,
                  lineStyle:{
                        normal:{
                            color:'#000',
                          width:2
                        },
                    emphasis:{
                            color:'red',
                      width:'4'
                    }
                  }
                },
                {
                    id:2,
                  source:0,
                  target:2,
                  lineStyle:{
                        normal:{
                            color:'#e4393c',
                          width:'8'
                        }
                  }
                },
                {
                    id:2,
                  source:0,
                  target:3
                },
                {
                    id:2,
                  source:3,
                  target:1
                },
                {
                    id:2,
                  source:1,
                  target:2
                },
                {
                    id:2,
                  source:3,
                  target:2
                },
              ],
            nodes:[
              {
                  id:1,
                name:'学校1',
                category:0,
                itemId:12,
                count:20
              },
              {
                  id:2,
                name:'学校2',
                category:0,
                itemId:13,
                count:20
              },
              {
                  id:3,
                name:'商家1',
                category:1,
                itemId:23,
                count:8
              },
              {
                  id:4,
                name:'商家2',
                category:1,
                count:30,

              }
            ]
          }

      }
  },
  mounted(){
      let context=this;
      let chartDiv=context.$refs.chart;
      let forceChart=echarts.init(chartDiv);
      let categories=[
        {
            name:'学校'
        },
        {
            name:'商家'
        }
      ];
    context.relationData.nodes.forEach(function (node) {
      node.itemStyle = null;
      node.symbolSize = node.count;
      node.value = node.symbolSize;

      // Use random x, y
      node.x = node.y = null;
      node.draggable = true;
    });
    let option = {
      title: {
        text: 'Les Miserables',
        subtext: 'Default layout',
        top: 'bottom',
        left: 'right'
      },
      tooltip: {},
      legend: [{
        // selectedMode: 'single',
        data: categories.map(function (a) {
          return a.name;
        })
      }],
      animation: false,
      series : [
        {
          name: 'Les Miserables',
          type: 'graph',
          layout: 'force',
          data: context.relationData.nodes,
          links: context.relationData.links,
          categories: categories,
          roam: true,
          label: {
            normal: {
              position: 'right'
            }
          },
          force: {
            repulsion: 100
          }
        }
      ]
    };
    forceChart.setOption(option);
    forceChart.on('click',function (params) {
      console.log(params)
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
  div.chart{
    width: 100%;
    height: 600px;
  }
</style>
