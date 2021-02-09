<template>
  <v-app> 
    <v-main>
      <v-toolbar dark fixed width="100%">
        <v-toolbar-title>
          <span class="display-1 font-weight-medium" style="color: red">Subway <span class="font-weight-light white--text">Rankings</span></span>
        </v-toolbar-title>
        <v-toolbar-items><v-btn target="_blank" href="https://jbrill.com/subway-guide" absolute right fab icon><v-icon>mdi-book-open-blank-variant</v-icon></v-btn></v-toolbar-items>
      </v-toolbar>
      <v-container dark fill-height align="center" justify="center" flex>
        <!-- <p class="white--text">{{ selectedGroup }}</p> -->
        <!-- <v-avatar
          v-for="(chart, chartIdx) in getChartGroup(selectedGroup)"
          :key="'CHART' - chartIdx"
          left
          :color="'#' + chart.color"
          size="48"
          style="{ font-family: 'Helvetica' !important}"
          class="white--text headline font-weight-bold chart-title"
        >
          {{ chart.className }}
        </v-avatar> -->
        <v-row flex align="center" justify="space-between">
          <v-col>
            <p class="white--text header-1">Straphangers Visualization</p>
            <p class="grey--text caption">These radar chart visualizations are based off of Straphanger's 'State of the Subways' Report Card Campaign.</p>
            <p class="grey--text caption">This "State of the Subways" Report Card tells riders how their lines do on these key aspects of service.</p>
            <p class="grey--text caption">Each category is ranked from 0 to 22, where 22 is the highest score possible, and 0 is the lowest.</p>
            <p class="grey--text caption">You can read more about the campaign <a href="https://www.straphangers.org/reports/2016/StateoftheSubways2016.pdf" target="_blank">here</a>.</p>
          </v-col>
          <v-col cols="12" sm="4" id="radar-guide"></v-col>
        </v-row>
        <v-row align="center" justify="center" v-for="rowIdx in Math.floor(getOrganizedCharts().length / 4)" :key="'row-' + rowIdx" no-gutters>
          <v-col class="d-flex justify-center" v-for="(chart, chartIdx) in getOrganizedCharts().slice((rowIdx - 1) * 4, (rowIdx - 1) * 4 + 4)" :key="'row-' + (rowIdx * 4 + chartIdx)">
            <v-avatar
              left
              :color="'#' + chart.color"
              size="34"
              style="{ font-family: 'Helvetica' !important}"
              class="white--text headline font-weight-bold chart-title"
            >
              {{ chart.className }}
            </v-avatar>
            <div
              :id="'chart-' + ((rowIdx - 1) * 4 + chartIdx)">
            </div>
          </v-col>
        </v-row>
      </v-container>
      <!-- <v-container>
        <v-card
          outlined
          shaped
          ripple
          raised
          dark
          true
          v-for="(n, idx) in 8"
          :key="n"
          class="lighten-5 mb-6"
        >
          <v-card-title>
            <v-avatar
              v-for="(chart, chartIdx) in getChartGroup(idx)"
              :key="'CHART' - chartIdx"
              left
              :color="'#' + chart.color"
              size="48"
              style="{ font-family: 'Helvetica' !important}"
              class="white--text headline font-weight-bold chart-title"
            >
              {{ chart.className }}
            </v-avatar>
          </v-card-title>
          <v-card-text>
            <v-row no-gutters justify="space-around">
              <v-col width="30%" align="left">
                <v-card flat class="pa-2" :id="'chart-' + idx"></v-card>
              </v-col>
              <v-row no-gutters justify="space-around" align="center">
                <v-col v-for="(subChart, subChartIdx) in getChartGroup(idx)"
                    :key="'subChart-' + subChartIdx" class="d-flex justify-center">
                  <v-avatar
                    left
                    :color="'#' + subChart.color"
                    size="34"
                    style="{ font-family: 'Helvetica' !important}"
                    class="white--text headline font-weight-bold chart-title"
                  >
                    {{ subChart.className }}
                  </v-avatar>
                  <div
                    :id="'chart-' + idx + '-' + subChartIdx">
                  </div>
                </v-col>
              </v-row>
            </v-row>
          </v-card-text>
        </v-card>
      </v-container> -->
      <v-footer dark fixed elevation="10">
        <v-layout justify-space-between flex>
          <span class="caption">Data from <a target="_blank" class="white--text" href="https://www.straphangers.org/reports/2016/StateoftheSubways2016.pdf"><strong>Straphangers</strong></a>. Charting with <a href="https://d3js.org/" target="_blank" class="white--text">D3js</a>.</span>
          <span class="caption"><a style="color: steelblue" href="https://github.com/jbrill/data-viz-project-1a" target="_blank">Code</a> by <a target="_blank" href="https://jbrill.com" class="white--text"><strong>Jason Brill</strong></a></span>
        </v-layout>
      </v-footer>
    </v-main>
  </v-app>
</template>

<script>
const { RadarChart } = require('radar-chart-d3');
const d3 = require ('d3')

export default {
  name: 'App',

  components: {
  },
  mounted () {
    // var chart = RadarChart.chart();
    // var cfg = chart.config(); // retrieve default config
    // var svg = d3.select('body').append('svg')
    //   .attr('width', cfg.w + cfg.w + 50)
    //   .attr('height', cfg.h + cfg.h / 4);
    // svg.append('g').classed('single', 1).datum(randomDataset()).call(chart);

    // // many radars
    // chart.config({w: cfg.w / 4, h: cfg.h / 4, axisText: false, levels: 0, circles: false});
    // cfg = chart.config();
    // function render() {
    //   var game = svg.selectAll('g.game').data(
    //     [
    //       this.randomDataset(),
    //       this.randomDataset(),
    //       this.randomDataset(),
    //       this.randomDataset()
    //     ]
    //   );
    //   game.enter().append('g').classed('game', 1);
    //   game
    //     .attr('transform', function(d, i) { return 'translate('+((cfg.w * 4) + 50 + (i * cfg.w))+','+ (cfg.h * 1.3) +')'; })
    //     .call(chart);

    //   setTimeout(render, 1000);
    // }
    // render();
    // RadarChart.draw(
    //   '#radar-guide', [this.randomDataset()]
    // )
    RadarChart.defaultConfig.radius = 4;
    RadarChart.defaultConfig.w = 400;
    RadarChart.defaultConfig.h = 400;
    RadarChart.defaultConfig.minValue = 0;
    RadarChart.defaultConfig.maxValue = 22;
    RadarChart.defaultConfig.axisText = true;
    RadarChart.defaultConfig.axisLine = true;
    RadarChart.defaultConfig.circles = true;
    RadarChart.defaultConfig.levels = 4;
    RadarChart.defaultConfig.radians = 2 * Math.PI;
    RadarChart.defaultConfig.factor = 0;
    RadarChart.defaultConfig.factorLegend = 2;

    let chart = RadarChart.chart();
    let cfg = chart.config();
    let instance = this;
    let svg = d3.select('#radar-guide').append('svg')
      .attr('width', cfg.w + cfg.w + 50)
      .attr('height', cfg.h + cfg.h / 4);

    let randomDataset = this.getChartGroup(this.selectedGroup)
    svg.append('g').classed('single', 1).datum([randomDataset]).call(chart);
    function render () {
      RadarChart.defaultConfig.radius = 4;
      RadarChart.defaultConfig.w = 400;
      RadarChart.defaultConfig.h = 400;
      RadarChart.defaultConfig.minValue = 0;
      RadarChart.defaultConfig.maxValue = 22;
      RadarChart.defaultConfig.axisText = true;
      RadarChart.defaultConfig.axisLine = true;
      RadarChart.defaultConfig.circles = true;
      RadarChart.defaultConfig.levels = 4;
      RadarChart.defaultConfig.radians = 2 * Math.PI;
      RadarChart.defaultConfig.factor = 0.95;
      RadarChart.defaultConfig.factorLegend = 1;
      // var cfg = chart.config(); // retrieve default config
      // d3.selectAll('g.single').remove();
      let selectedGroup = instance.getSelectedGroup();
      svg.selectAll('g.single').datum(
        instance.getChartGroup(selectedGroup)
      ).call(chart);
      // myChart.enter().append('g').classed('game', 1)
      
      setTimeout(render, 2000);
    }
    render();
    for (let chartIdx = 0; chartIdx < this.getOrganizedCharts().length; chartIdx++) {
      RadarChart.defaultConfig.radius = 2;
      RadarChart.defaultConfig.w = 100;
      RadarChart.defaultConfig.h = 100;
      RadarChart.defaultConfig.axisText = false;
      RadarChart.defaultConfig.circles = true;
      RadarChart.defaultConfig.levels = 4;
      // RadarChart.defaultConfig.color = function() { return chartGroup[0].color };
      // for (let subIdx = 0; subIdx < chartGroup.length; subIdx++) {
      RadarChart.draw(
        `#chart-${chartIdx}`, [this.getOrganizedCharts()[chartIdx]]
      );
      // }
    }
    // for (let idx = 0; idx < 8; idx++) {
    //   RadarChart.defaultConfig.radius = 3;
    //   RadarChart.defaultConfig.w = 400;
    //   RadarChart.defaultConfig.h = 400;
    //   RadarChart.defaultConfig.axisText = true;
    //   RadarChart.defaultConfig.levels = 5;
    //   RadarChart.defaultConfig.circles = true;
    //   let chartGroup = this.getChartGroup(idx);
    //   RadarChart.draw(
    //     `#chart-${idx}`, this.getChartGroup(idx)
    //   );

    //   RadarChart.defaultConfig.radius = 2;
    //   RadarChart.defaultConfig.w = 100;
    //   RadarChart.defaultConfig.h = 100;
    //   RadarChart.defaultConfig.axisText = false;
    //   RadarChart.defaultConfig.circles = true;
    //   RadarChart.defaultConfig.levels = 4;
    //   // RadarChart.defaultConfig.color = function() { return chartGroup[0].color };
    //   for (let subIdx = 0; subIdx < chartGroup.length; subIdx++) {
    //     RadarChart.draw(
    //       `#chart-${idx}-${subIdx}`, [chartGroup[subIdx]]
    //     );
    //   }
    // }
  },
  data: () => ({
    chart: null,
    selectedGroup: 0,
    chartData: [
      {
        className: '1',
        color: 'E60D2E',
        group: 0,
        axes: [
          {axis: "Frequency of Trains", value: 20},
          {axis: "Reliability of Service", value: 20},
          {axis: "Breakdown Rate", value: 8},
          {axis: "Seat Availability", value: 12},
          {axis: "Interior Cleanliness", value: 21},
          {axis: "Clarity of Announcements", value: 16}
        ]
      },
      {
        className: '2',
        color: 'E60D2E',
        group: 0,
        axes: [
          {axis: "Frequency of Trains", value: 13},
          {axis: "Reliability of Service", value: 3},
          {axis: "Breakdown Rate", value: 13},
          {axis: "Seat Availability", value: 5},
          {axis: "Interior Cleanliness", value: 8},
          {axis: "Clarity of Announcements", value: 21}
        ]
      },
      {
        className: '3',
        color: 'E60D2E',
        group: 0,
        axes: [
          {axis: "Frequency of Trains", value: 13},
          {axis: "Reliability of Service", value: 12},
          {axis: "Breakdown Rate", value: 11},
          {axis: "Seat Availability", value: 9},
          {axis: "Interior Cleanliness", value: 20},
          {axis: "Clarity of Announcements", value: 14}
        ]
      },
      {
        className: '4',
        color: '00933C',
        group: 1,
        axes: [
          {axis: "Frequency of Trains", value: 19},
          {axis: "Reliability of Service", value: 2},
          {axis: "Breakdown Rate", value: 17},
          {axis: "Seat Availability", value: 8},
          {axis: "Interior Cleanliness", value: 19},
          {axis: "Clarity of Announcements", value: 19}
        ]
      },
      {
        className: '5',
        color: '00933C',
        group: 1,
        axes: [
          {axis: "Frequency of Trains", value: 15},
          {axis: "Reliability of Service", value: 1},
          {axis: "Breakdown Rate", value: 20},
          {axis: "Seat Availability", value: 7},
          {axis: "Interior Cleanliness", value: 18},
          {axis: "Clarity of Announcements", value: 22}
        ]
      },
      {
        className: '6',
        color: '00933C',
        group: 1,
        axes: [
          {axis: "Frequency of Trains", value: 22},
          {axis: "Reliability of Service", value: 5},
          {axis: "Breakdown Rate", value: 16},
          {axis: "Seat Availability", value: 4},
          {axis: "Interior Cleanliness", value: 17},
          {axis: "Clarity of Announcements", value: 21}
        ]
      },
      {
        className: '7',
        color: 'B933AD',
        group: 2,
        axes: [
          {axis: "Frequency of Trains", value: 22},
          {axis: "Reliability of Service", value: 18},
          {axis: "Breakdown Rate", value: 9},
          {axis: "Seat Availability", value: 16},
          {axis: "Interior Cleanliness", value: 2},
          {axis: "Clarity of Announcements", value: 9}
        ]
      },
      {
        className: 'L',
        color: 'A7A9AC',
        group: 3,
        axes: [
          {axis: "Frequency of Trains", value: 16},
          {axis: "Reliability of Service", value: 20},
          {axis: "Breakdown Rate", value: 19},
          {axis: "Seat Availability", value: 2},
          {axis: "Interior Cleanliness", value: 12},
          {axis: "Clarity of Announcements", value: 19}
        ]
      },
      {
        className: 'F',
        color: 'FF6319',
        group: '5',
        axes: [
          {axis: "Frequency of Trains", value: 18},
          {axis: "Reliability of Service", value: 7},
          {axis: "Breakdown Rate", value: 14},
          {axis: "Seat Availability", value: 18},
          {axis: "Interior Cleanliness", value: 1},
          {axis: "Clarity of Announcements", value: 6}
        ]
      },
      {
        className: 'J',
        color: '996633',
        group: 6,
        axes: [
          {axis: "Frequency of Trains", value: 11},
          {axis: "Reliability of Service", value: 18},
          {axis: "Breakdown Rate", value: 10},
          {axis: "Seat Availability", value: 11},
          {axis: "Interior Cleanliness", value: 3},
          {axis: "Clarity of Announcements", value: 12}
        ]
      },
      {
        className: 'Z',
        color: '996633',
        group: 6,
        axes: [
          {axis: "Frequency of Trains", value: 11},
          {axis: "Reliability of Service", value: 18},
          {axis: "Breakdown Rate", value: 10},
          {axis: "Seat Availability", value: 11},
          {axis: "Interior Cleanliness", value: 3},
          {axis: "Clarity of Announcements", value: 12}
        ]
      },
      {
        className: 'M',
        color: 'FF6319',
        group: '5',
        axes: [
          {axis: "Frequency of Trains", value: 2},
          {axis: "Reliability of Service", value: 21},
          {axis: "Breakdown Rate", value: 5},
          {axis: "Seat Availability", value: 14},
          {axis: "Interior Cleanliness", value: 12},
          {axis: "Clarity of Announcements", value: 15}
        ]
      },
      {
        className: 'N',
        color: 'FCCC0A',
        group: 7,
        axes: [
          {axis: "Frequency of Trains", value: 5},
          {axis: "Reliability of Service", value: 15},
          {axis: "Breakdown Rate", value: 21},
          {axis: "Seat Availability", value: 15},
          {axis: "Interior Cleanliness", value: 9},
          {axis: "Clarity of Announcements", value: 11}
        ]
      },
      {
        className: 'Q',
        color: 'FCCC0A',
        group: 7,
        axes: [
          {axis: "Frequency of Trains", value: 10},
          {axis: "Reliability of Service", value: 11},
          {axis: "Breakdown Rate", value: 22},
          {axis: "Seat Availability", value: 21},
          {axis: "Interior Cleanliness", value: 4},
          {axis: "Clarity of Announcements", value: 2}
        ]
      },
      {
        className: 'R',
        color: 'FCCC0A',
        group: 7,
        axes: [
          {axis: "Frequency of Trains", value: 10},
          {axis: "Reliability of Service", value: 4},
          {axis: "Breakdown Rate", value: 6},
          {axis: "Seat Availability", value: 20},
          {axis: "Interior Cleanliness", value: 16},
          {axis: "Clarity of Announcements", value: 11}
        ]
      },
      {
        className: 'B',
        color: 'FF6319',
        group: 5,
        axes: [
          {axis: "Frequency of Trains", value: 4},
          {axis: "Reliability of Service", value: 9},
          {axis: "Breakdown Rate", value: 15},
          {axis: "Seat Availability", value: 10},
          {axis: "Interior Cleanliness", value: 22},
          {axis: "Clarity of Announcements", value: 9}
        ]
      },
      {
        className: 'D',
        color: 'FF6319',
        group: 5,
        axes: [
          {axis: "Frequency of Trains", value: 7},
          {axis: "Reliability of Service", value: 11},
          {axis: "Breakdown Rate", value: 18},
          {axis: "Seat Availability", value: 17},
          {axis: "Interior Cleanliness", value: 6},
          {axis: "Clarity of Announcements", value: 2}
        ]
      },
      {
        className: 'A',
        color: '0039A6',
        group: 4,
        axes: [
          {axis: "Frequency of Trains", value: 14},
          {axis: "Reliability of Service", value: 13},
          {axis: "Breakdown Rate", value: 2},
          {axis: "Seat Availability", value: 13},
          {axis: "Interior Cleanliness", value: 16},
          {axis: "Clarity of Announcements", value: 6}
        ]
      },
      {
        className: 'C',
        color: '0039A6',
        group: 4,
        axes: [
          {axis: "Frequency of Trains", value: 3},
          {axis: "Reliability of Service", value: 13},
          {axis: "Breakdown Rate", value: 2},
          {axis: "Seat Availability", value: 6},
          {axis: "Interior Cleanliness", value: 16},
          {axis: "Clarity of Announcements", value: 6}
        ]
      },
      {
        className: 'E',
        color: '0039A6',
        group: 4,
        axes: [
          {axis: "Frequency of Trains", value: 18},
          {axis: "Reliability of Service", value: 14},
          {axis: "Breakdown Rate", value: 7},
          {axis: "Seat Availability", value: 3},
          {axis: "Interior Cleanliness", value: 12},
          {axis: "Clarity of Announcements", value: 17}
        ]
      },
    ]
  }),
  methods: {
    getChartGroup (idx) {
      return this.chartData.filter( obj => {
        return obj.group.toString() === idx.toString();
      });
    },
    getSelectedGroup() {
      let selectedGroup = Math.floor(Math.random() * 7);
      this.selectedGroup = selectedGroup;
      return selectedGroup;
    },
    getOrganizedCharts () {
      return this.chartData.sort(function(a, b) {
        // Compare the 2 dates
        if (a.group < b.group) return -1;
        if (a.group > b.group) return 1;
        return 0;
      });
    },
    randomDataset() {
      return this.chartData[Math.floor(Math.random() * this.chartData.length)]
    }
  }
};
</script>

<style>
html, body {
  font-family: 'Roboto', sans-serif;
}
.radar-chart .area {
  fill-opacity: 0.7;
}
.radar-chart.focus .area {
  fill-opacity: 0.3;
}
.radar-chart.focus .area.focused {
  fill-opacity: 0.9;
}
.area.chart-0, .chart-0 .circle {
  fill: #FFD700;
  stroke: none;
}
.area.chart-1, .chart-1 .circle {
  fill: #ADD8E6;
  stroke: none;
}
#app {
  background: black;
}
.chart-contain {
  display: flex;
  align-content: center;
  justify-content: center;
}
.radar-chart .area {
  fill-opacity: 0.7;
}
.radar-chart.focus .area {
  fill-opacity: 0.3;
}
.radar-chart.focus .area.focused {
  fill-opacity: 0.9;
}
.area {
  fill: #FFD700;
  stroke: none;
}
.radar-chart .circle {
  fill: #ADD8E6;
  stroke: none;
}
.chart-title {
  margin-right: 5px;
}
.axis line, circle {
  stroke: rgba(190, 190, 190, 0.267) !important;
}
.level-group line {
  stroke: rgba(190, 190, 190, 0.26);
}
.axis text {
  fill: white !important;
}
.radar-chart {
  overflow: inherit !important;
}
html {
  background: black;
}
.chart-title {
  font-family: 'Helvetica' !important;
}
</style>