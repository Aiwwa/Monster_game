<template>
  <div class="game">
    <CharacterCard :player="player" :class="{ winner: player.winner }" />
    <div class="field">
      <div class="gold">Gold: {{ player.gold }}</div>
      <div class="weapons">
        <Weapon
          :weapon="sword"
          :player="player"
          :monster="monster"
          @playerUsedSword="swordAttack"
        />
        <Weapon :weapon="axe" :player="player" @playerUsedAxe="axeAttack" />
        <Weapon
          :weapon="bow"
          :player="player"
          :monster="monster"
          @playerUsedBow="bowAttack"
        />
      </div>
    </div>
    <CharacterCard :player="monster" :class="{ winner: monster.winner }" />
  </div>
  <div class="btn">
    <button @click="handleAttack" v-if="attack">Attack</button>
    <div></div>
    <div></div>
  </div>
  <div class="play-again" @click="playAgain" v-if="isPlayign">
    PLAY AGAIN
  </div>
</template>

<script>
import CharacterCard from './components/CharacterCard.vue'
import Weapon from './components/Weapon.vue'

export default {
  name: 'App',
  components: { CharacterCard, Weapon },
  data() {
    return {
      player: {
        name: 'Silver Fighter',
        gold: 0,
        health: 100,
        url:
          'https://i.pinimg.com/originals/4b/9b/d9/4b9bd9a32b7026df440d094eb8bf0b72.jpg',
        winer: false,
        attack: null,
      },
      monster: {
        name: 'Midnight Dragon',
        health: 100,
        url:
          'https://townsquare.media/site/442/files/2014/09/the-hobbit-2-tag-page.jpg?w=980&q=75',
        winner: false,
        attack: null,
      },
      isPlayign: false,
      attack: true,
      sword: {
        name: 'SWORD',
        bio: 'Gives player 25% chance to doge enemy attack',
        url:
          'https://www.medievalcollectibles.com/wp-content/uploads/2020/06/MG01.jpg',
        price: 100,
      },
      axe: {
        name: 'AXE',
        bio: 'Heals player on every enemy hit from 0 to 5 hit points',
        url: 'https://m.media-amazon.com/images/I/61bBk0tgh0L._AC_SL1500_.jpg',
        price: 200,
      },
      bow: {
        name: 'BOW',
        bio: 'Has 50% chance to hit enemy two times in a row',
        url:
          'https://www.vippng.com/png/detail/513-5139207_this-png-file-is-about-game-ancient-fight.png',
        price: 300,
      },
    }
  },
  methods: {
    handleAttack() {
      this.playerAttack()
    },
    playerAttack() {
      let randomNum = Math.floor(Math.random() * 10) + 1
      let randomNum2 = Math.floor(Math.random() * 15) + 1

      this.player.gold += Math.floor(Math.random() * 50) + 1

      this.monster.attack = randomNum
      this.player.attack = randomNum2

      if (
        this.monster.health - randomNum >= 0 &&
        this.player.health - randomNum2 >= 0
      ) {
        this.monster.health -= randomNum
        this.player.health -= randomNum2
      } else {
        if (this.monster.health > this.player.health) {
          this.monster.winner = true
          this.isPlayign = true
          this.attack = false
        } else {
          this.player.winner = true
          this.isPlayign = true
          this.attack = false
        }
      }
    },
    playAgain() {
      this.monster.health = 100
      this.player.health = 100
      this.player.winner = false
      this.monster.winner = false
      this.isPlayign = false
      this.attack = true
      this.player.gold = 0
    },
    swordAttack(healt, price) {
      this.player.health += healt
      this.player.gold -= price
    },
    axeAttack(healNum, price) {
      this.player.health += healNum
      this.player.gold -= price
    },
    bowAttack(doubleAttack, price) {
      this.monster.health -= doubleAttack
      this.player.gold -= price
    },
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: rgb(53, 52, 52);
  color: white;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 1200px;
  display: flex;
  flex-direction: column;
}

.game {
  display: flex;
  justify-content: space-evenly;
  margin: 50px 40px 0 40px;
}

.btn {
  margin-top: 20px;
  display: flex;
  justify-content: center;
}

button {
  margin-top: 60px;
  padding: 10px 20px;
  outline: none;
  border: none;
  background: rgb(216, 67, 22);
  font-weight: 900;
  -webkit-box-shadow: 0px 3px 27px -1px #000000;
  box-shadow: 0px 3px 27px -1px #000000;
}

button:hover {
  transform: scale(1.2);
  background: rgb(255, 60, 0);
}

.winner {
  border: 4px solid rgb(210, 210, 50);
  transform: scale(1.1);
  border-radius: 20px;
  padding: 20px;
  animation-name: stretch;
  animation-duration: 0.8s;
  animation-timing-function: ease-in-out;
  animation-delay: 0;
  animation-direction: alternate;
  animation-iteration-count: infinite;
  animation-play-state: running;
}

@keyframes stretch {
  0% {
    transform: scale(1);
    border: 4px solid rgb(245, 245, 211);
  }
  100% {
    transform: scale(1.2);
    border: 4px solid rgb(255, 255, 0);
  }
}

.play-again {
  background: rgb(230, 21, 21);
  margin: 0 auto;
  margin-top: 150px;
  padding: 10px 20px;
  font-weight: 900;
}

.play-again:hover {
  background: red;
  transform: scale(1.2);
}

.field {
  margin: 0 30px;
}

.weapons {
  display: flex;
  justify-content: space-evenly;
}

.weapons img {
  width: 100px;
  height: 100px;
  margin: 10px 20px;
  border-radius: 10px;
}

.gold {
  margin: 40px 0;
  color: yellow;
  font-weight: 900;
  text-transform: uppercase;
}
</style>
