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
    }
  },
  created() {
    for (let index = 0; index < 9; index++) {
      this.teamResults.push({
        teamName: String.fromCharCode(65 + index),
        point: 0,
      });
    }
  },
  methods: {
    start() {
      if (this.interval) {
        return;
      }
      this.interval = setInterval(() => {
        const randVal = Math.ceil(Math.random() * 90) + 10
        this.teamResults.forEach((teamResult) => {
          teamResult.point = randVal;
        })
      }, 20);
    },
    stop() {
      clearInterval(this.interval);
      this.interval = 0;
      this.teamResults = [
        {
          teamName: 'A',
          point: 1,
        },
        {
          teamName: 'B',
          point: 0,
        },
        {
          teamName: 'C',
          point: 1,
        },
        {
          teamName: 'D',
          point: 0,
        },
        {
          teamName: 'E',
          point: 0,
        },
        {
          teamName: 'F',
          point: 0,
        },
        {
          teamName: 'G',
          point: 0,
        },
        {
          teamName: 'H',
          point: 0,
        },
        {
          teamName: 'I',
          point: 0,
        },
      ];
    }
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
