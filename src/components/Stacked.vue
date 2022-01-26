<template>
    <v-container>

      <highcharts class="hc" :options="chartOptions" ref="chart"></highcharts>

    </v-container>
</template>

<script>
//chart js



  export default {
    name: 'Stacked',
    props:[
      'indicator'
    ],
    data: () => ({
        chartOptions: {
chart: {
    type: 'column'
  },
  title: {
    text: 'Indicators by Trend'
  },
  xAxis: {
    categories: ["Education & Workforce", "Prosperity", "Justice & Safety", "Infrastructure", "Natural Resources", "Government Performance","Health"]
  },
  yAxis: {
    min: 0,
    title: {
      text: 'Percent Trend'
    },
    stackLabels: {
      enabled: false,
      style: {
        fontWeight: 'bold',
        color: 'gray'
      }
    }
  },
  legend: {
    align: 'right',
    x: -30,
    verticalAlign: 'top',
    y: 25,
    floating: true,
    backgroundColor: 'white',
    borderColor: '#CCC',
    borderWidth: 1,
    shadow: false
  },
  tooltip: {
    headerFormat: '<b>{point.x}</b><br/>',
    pointFormat: '{series.name}: {point.y}<br/>Total: {point.stackTotal}'
  },
  plotOptions: {
    column: {
      stacking: 'normal',
      dataLabels: {
        enabled: false
      }
    }
  },
  series: [{
    name: 'Up',
    color:'green',
    //data: [5, 3, 4, 7, 2,5, 3]
    data:[12.5,0,0,44.44,40,18.18,20]
  }, {
    name: 'Down',
    color:'red',
    //data: [2, 2, 3, 2, 1,5, 3]
    data:[37.5,50,33.33,0,0,0,33.33]
  }, {
    name: 'Flat',
    color:'blue',
    //data: [3, 4, 4, 2, 5,5, 3]
    data:[0,0,50,44.44,40,27.27,33.33]
  }, 
  {
    name: 'NA',
    color:'grey',
    //data: [3, 4, 4, 2, 5,5, 3]
    data:[50,50,16.67,11.11,20,55,13.33]
  }
  ]
      }

    }),
  }
</script>
