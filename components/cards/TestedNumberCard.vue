<template>
  <v-col cols="12" md="6" class="DataCard">
    <time-stacked-bar-chart
      :title="$t('検査実施数')"
      :title-id="'number-of-tested'"
      :chart-id="'time-stacked-bar-chart-inspections'"
      :chart-data="inspectionsGraph"
      :date="Data.inspections_summary.date"
      :items="inspectionsItems"
      :labels="inspectionsLabels"
      :unit="$t('件.tested')"
      :url="'https://www.pref.nagano.lg.jp/joho/kensei/tokei/johoka/opendata/'"
    />
    <!-- 件.tested = 検査数 -->
  </v-col>
</template>

<script>
import dayjs from 'dayjs'

import Data from '@/data/data.json'
import testCount from '@/data/test_count.json'
import TimeStackedBarChart from '@/components/TimeStackedBarChart.vue'

export default {
  components: {
    TimeStackedBarChart
  },
  data() {
    // 検査実施日別状況
    const inspectionsGraph = [
      testCount.map(data => data.positiveNum),
      testCount.map(data => data.negativeNum)
    ]
    const inspectionsItems = [this.$t('陽性'), this.$t('陰性')]
    const inspectionsLabels = testCount.map(data => {
      return dayjs(data.YMD).format('MM/DD')
    })

    const data = {
      Data,
      inspectionsGraph,
      inspectionsItems,
      inspectionsLabels
    }
    return data
  }
}
</script>
