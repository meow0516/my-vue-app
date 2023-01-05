<template>
  <div class="outer">
    <vue-highcharts
        type="stockChart"
        :options="chartOptions"
        :redrawOnUpdate="true"
        :oneToOneUpdate="false"
        :animateOnUpdate="true"/>
    <div class="">
      <p @mousedown="changeType(0,$event)">一般</p>
      <p @mousedown="changeType(1,$event)">百分比</p>
    </div>
  </div>
</template>

<style scoped>
.outer{
  width:1000px;
}

</style>

<script setup>
import { ref,computed } from 'vue';
import VueHighcharts from 'vue3-highcharts';
import HighCharts from 'highcharts';
import StockCharts from 'highcharts/modules/stock';
import moment from 'moment'
import _ from 'lodash'
import mockNavApi from './mockNavApi'

StockCharts(HighCharts);

const chartType = ref(0)
const changeType = (id,$event)=>{
  $event.preventDefault();
  chartType.value = id
}
const chartOptions = computed(()=>{return {
  rangeSelector: {
    verticalAlign: 'top',
    x: 0,
    y: 0,
    inputDateFormat: '%b %e, %Y %H:%M'
},

  title: {
    text: 'Stock Prices',
  },
  plotOptions: {
            series: {
                compare: chartType.value == 0 ? '':'percent'
            }
        },
  series: [
    {
      name: 'MyStock',
      data: mockNav.value/* [
        [1537795800000, 55.2],
        [1537882200000, 55.55],
        [1537968600000, 55.1],
        [1538055000000, 56.24],
        [1538141400000, 56.44],
        [1538400600000, 56.81],
        [1538487000000, 57.32],
        [1538573400000, 58.02],
        [1538659800000, 57]], */
        
    },
  ],
}})



// const mockNavApi = ref();
const mockNav1 = _.orderBy(mockNavApi.Data.NAV,'NAV_DATE')
const mockNav = ref(mockNav1.map(x=>[parseInt(moment(x.NAV_DATE).format('x')), x.NAV_B]))
// const mockNav = mockNavApi.value.Data.NAV.
</script>