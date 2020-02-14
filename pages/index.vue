<template>
  <div class="container">
    <h1 class="title">
      結果発表！！！
    </h1>
    <div class="result-row">
      <result-panel
        v-for="teamResult in teamResults.filter((item, i) => i <= 4)"
        :key="teamResult.teamName"
        :team-name="teamResult.teamName"
        :point="teamResult.point"
      />
    </div>
    <div class="result-row">
      <result-panel
        v-for="teamResult in teamResults.filter((item, i) => i > 4)"
        :key="teamResult.teamName"
        :team-name="teamResult.teamName"
        :point="teamResult.point"
      />
    </div>
    <div class="footer">
      <el-button
        @click="start"
      >
        start
      </el-button>
      <el-button
        @click="stop"
        :disabled="!stopButtonActive"
      >
        stop
      </el-button>
    </div>
  </div>
</template>

<script>
import ResultPanel from '~/components/ResultPanel.vue'

export default {
  components: {
    ResultPanel,
  },
  data() {
    return {
      teamResults: [],
      interval: 0,
      stopButtonActive: false,
      fetchedData: [],
    }
  },
  created() {
    for (let index = 0; index < 9; index++) {
      this.teamResults.push({
        teamName: String.fromCharCode(65 + index),
        point: 0,
      });
    }
    this.teamResults.push({
      teamName: 'Hangout',
      point: 0,
    });
  },
  methods: {
    start() {
      if (this.interval) {
        return;
      }
      this.stopButtonActive = false;
      this.fetchResults().then(() => {
        this.stopButtonActive = true;
      }).catch(() => {
        this.stopInterval();
        this.$notify.error({
          title: 'エラー',
          message: '点数の読み込みに失敗しました...'
        });
        this.teamResults = this.teamResults.map(teamResult => {
          return {
            teamName: teamResult.teamName,
            point: 0,
          }
        });
      });
      this.interval = setInterval(() => {
        const randVal = Math.ceil(Math.random() * 90) + 10
        this.teamResults.forEach((teamResult) => {
          teamResult.point = randVal;
        })
      }, 20);
    },
    stop() {
      this.stopInterval();
      this.teamResults = this.teamResults.map((teamResult, i) => {
        return {
          teamName: teamResult.teamName,
          point: this.fetchedData[i],
        }
      });
    },
    stopInterval() {
      clearInterval(this.interval);
      this.interval = 0;
    },
    async fetchResults() {
      const gasApi = process.env.GAS_API;
      this.fetchedData = await this.$axios.$get(`https://script.google.com/macros/s/${gasApi}/exec`);
    },
  }
};
</script>

<style>

.title {
  margin-bottom: 20px;
}

.container {
  min-height: 100vh;
  margin: 20px;
}

.result-row {
  width: 100%;
  display: flex;
}
.footer {
  margin-top: 20px;
}
</style>
