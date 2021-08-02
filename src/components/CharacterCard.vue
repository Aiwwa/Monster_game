<template>
  <div>
    <h2 v-if="player.winner" class="win">WINNER</h2>
    <div>{{ player.name }}</div>
    <img :src="player.url" alt="" />
    <div>Health {{ player.health }}</div>
    <div class="health-wrap">
      <div class="health" :style="{ width: player.health + '%' }"></div>
    </div>
    <div></div>
  </div>
</template>

<script>
export default {
  props: ['player'],
}
</script>

<style scoped>
img {
  width: 350px;
  height: 500px;
  object-fit: cover;
}

.health-wrap {
  background: black;
  border-radius: 30px;
}
.health {
  margin: 10px 0;
  height: 20px;
  background: rgb(99, 164, 38);
  border-radius: 30px;
  -webkit-box-shadow: 3px 3px 19px 3px #000000;
  box-shadow: 3px 3px 19px 3px #000000;
}

.win {
  color: red;
  font-weight: 900;
  margin: 10px 0;
}

img {
  margin: 20px 0;
  border-radius: 30px;
  -webkit-box-shadow: 5px 5px 15px 5px #000000;
  box-shadow: 5px 5px 15px 5px #000000;
}
</style>
