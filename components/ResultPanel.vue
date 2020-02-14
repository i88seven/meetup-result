<template>
  <el-card
    class="result-panel"
  >
    <h2>
      {{ teamName }}
    </h2>
    <div class="point-container">
      <label class="point">
        {{ point }}
        <span
          class="diff-text"
          v-if="diff !== null && diff !== undefined"
        >
          (+<span class="diff-number">{{ diff }}</span>)
        </span>
      </label>
    </div>
  </el-card>
</template>

<script>
export default {
  props: {
    teamName: String,
    point: Number,
    diff: Number | null
  },
};
</script>

<style>
.result-panel {
  width: 18vw;
  text-align: center;
}
.point-container {
  margin-top: 20px;
}
.point {
  font-size: 40px;
  font-weight: bold;
}
.diff-text {
  font-size: 20px;
  font-weight: normal;
}
.diff-text .diff-number {
  font-size: 24px;
  font-weight: bold;
}
</style>
