<template>
  <v-app> 
    <v-main>
      <v-container> 
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
            <v-col
              tile
            >
              <v-container class="pa-2 chart-contain" :id="'chart-' + idx"></v-container>
            </v-col>
          </v-row>
          </v-card-text>
        </v-card>
        
        <!-- <v-row>
          <v-col v-for="(chart, chartIdx) in chartData" :key="'chart-' + chartIdx">
            <v-card>
              <v-card-title><v-avatar
                left
                :color="'#' + chart.color"
                size="48"
                style="font-family: 'Helvetica' !important"
                class="white--text headline font-weight-bold"
              >{{ chart.className }}</v-avatar></v-card-title>
              <v-card-text class="chart-contain" :id="'chart-' + chartIdx"></v-card-text>
            </v-card>
          </v-col>
        </v-row> -->
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
const { RadarChart } = require('radar-chart-d3');

export default {
  name: 'App',

  components: {
  },
  mounted () {
    RadarChart.defaultConfig.radius = 3;
    RadarChart.defaultConfig.w = 400;
    RadarChart.defaultConfig.h = 400;
    for (let idx = 0; idx < 8; idx++) {
      RadarChart.draw(
        `#chart-${idx}`, this.getChartGroup(idx)
      );
    }
  },
  data: () => ({
    chart: null,
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
        className: 'J&Z',
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
    ]
  }),
  methods: {
    getChartGroup (idx) {
      console.log(
        this.chartData.filter( obj => {
          console.log(obj.group.toString())
          console.log(idx.toString())
          obj.group.toString() === idx.toString();
        })
      )
      return this.chartData.filter( obj => {
        return obj.group.toString() === idx.toString();
      });
    },
  }
};
</script>

<style>
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
  font-family: 'Helvetica' !important;
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
.axis text,line {
  fill: white;
}
.radar-chart {
  overflow: inherit !important;
}
</style>