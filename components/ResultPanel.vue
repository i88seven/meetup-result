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
      </label>
    </div>
  </el-card>
</template>

<script>
export default {
  props: {
    teamName: String,
    point: Number,
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
</style>
