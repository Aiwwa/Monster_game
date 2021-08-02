<template>
  <div class="weapon">
    <h3>{{ weapon.name }}</h3>
    <img :src="weapon.url" alt="" />
    <div>{{ weapon.bio }}</div>
    <p>Price {{ weapon.price }}</p>
    <button @click="handleWeapon">BUY</button>
  </div>
</template>

<script>
export default {
  props: ['weapon', 'player', 'monster'],
  methods: {
    handleWeapon() {
      let num = Math.floor(Math.random() * 4) + 1
      let healNum = Math.floor(Math.random() * 5) + 1
      let bowNum = Math.floor(Math.random() * 2) + 1

      switch (this.weapon.name) {
        case 'SWORD':
          if (num > 2 && this.weapon.price < this.player.gold) {
            this.$emit(
              'playerUsedSword',
              this.monster.attack,
              this.weapon.price,
            )
          }
          break
        case 'AXE':
          if (this.weapon.price < this.player.gold) {
            this.$emit('playerUsedAxe', healNum, this.weapon.price)
          }
          break
        case 'BOW':
          if (bowNum > 1 && this.weapon.price < this.player.gold) {
            let doubleAttack = this.player.attack * 2
            this.$emit('playerUsedBow', doubleAttack, this.weapon.price)
          }
          break
        default:
          break
      }
    },
  },
}
</script>

<style scoped>
.weapon {
  margin: 0 10px;
}

.weapon div {
  margin: 20px 0 10px 0;
  height: 100px;
  text-align: inherit;
}
.weapon button {
  background: rgb(255, 217, 0);
  color: black;
  margin: 10px 0;
  padding: 4px 10px;
}

button:hover {
  background: rgb(237, 211, 13);
}
</style>
