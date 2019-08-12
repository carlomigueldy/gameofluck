<template>
  <div class="container pt-3">
    <div class="card card-body mb-3">
      <div class="row text-center">
        <div class="col">
          <div class="card-body">
            <img class="img-thumbnail border-0" src="https://blizzardwatch.com/wp-content/uploads/2017/11/Anduin_wrynn_battle_cinematic.jpg" alt="">
            <h1>You</h1>
            <div class="progress" style="height: 50%;">
              <div class="progress-bar bg-success" role="progressbar" 
              style="width: 100%" :style="{width: playerHp + '%'}"
              :aria-valuenow="playerHp" aria-valuemin="0" aria-valuemax="100"><h3>{{ playerHp + '%' }}</h3></div>
            </div>
          </div>
        </div>
        <div class="col">
          <div class="card-body">
            <img class="img-thumbnail border-0" src="https://www.wallpaperup.com/uploads/wallpapers/2015/11/07/830798/aaaadace7ece91a93fc72e87890404f9-700.jpg" alt="">
          <h1>Monster</h1>
          <div class="progress" style="height: 50%;">
            <div class="progress-bar bg-danger" role="progressbar" 
              style="width: 100%;" :style="{width: monsterHp + '%'}"
              :aria-valuenow="monsterHp" aria-valuemin="0" aria-valuemax="100"><h3>{{ monsterHp + '%' }}</h3></div>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col text-center card-body pt-5" v-if="remarks">
          <div class="badge badge-danger"><h1>{{ remarks }}</h1></div>
        </div>
        <div class="col" v-else>

        </div>
      </div>
    </div>
    <div class="card card-body mb-3">
      <div class="row">
        <div class="col">
          <div class="text-center" v-if="gameStarted">
            <button @click="attack()" class="btn btn-primary m-1">Attack</button>
            <button @click="specialAttack()" class="btn btn-danger m-1">Special Attack</button>
            <button @click="heal()" class="btn btn-success m-1">Heal</button>
            <button @click="giveUp()" class="btn btn-secondary m-1">Give Up</button>
          </div>
          <div class="text-center" v-else>
            <button @click="gameStart()" class="btn btn-success">Start Game</button>
          </div>
        </div>
      </div>
    </div>
    <div class="card card-body mb-3">
      <div class="row">
        <div class="col text-center">
          <div v-for="player in playerStatus" :key="player">
            <div class="bg-primary text-white">{{ player }}</div>
          </div>
        </div>
        <div class="col text-center">
          <div v-for="monster in monsterStatus" :key="monster">
            <div class="bg-danger text-white">{{ monster }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      gameStarted: false,
      playerHp: 100,
      monsterHp: 100,
      playerStatus: [],
      monsterStatus: [],
      remarks: '',
    }
  },
  methods: {
    gameStart() {
      this.gameStarted = true
      this.playerHp = 100
      this.monsterHp = 100
      this.remarks = ''
      this.playerStatus = []
      this.monsterStatus = []
    },
    attack() {
      this.monsterAttacks()
      this.playerAttacks()
      this.checkWin()
    },
    monsterAttacks() {
      var damage = this.calculateDamage(5, 15)
      this.playerHp -= damage
      this.playerStatus.push(`Player takes ${damage} damage from monster`)
    },
    playerAttacks() {
      var damage = this.calculateDamage(5, 15)
      this.monsterHp -= damage
      this.monsterStatus.push(`Monster takes ${damage} damage from player`)
    },
    specialAttack() {
      var damage = this.calculateDamage(10, 20)
      this.monsterHp -= damage
      this.monsterStatus.push(`Monster takes ${damage} damage from player's special attack`)
      this.monsterAttacks()
      this.checkWin()
    },
    heal() {
      if (this.playerHp < 100) {
        var heal = this.calculateDamage(1, 20)
        this.playerHp += heal
        this.playerStatus.push(`Player heals for ${heal}`)
        this.monsterAttacks()
        this.checkWin()
      } else {
        return
      }
    },
    giveUp() {
      this.gameStarted = false
      this.playerStatus = this.monsterStatus = []
    },
    calculateDamage(min, max) {
      return Math.round(Math.random() * (+max - +min) + +min)
    },
    checkWin() {
      if(this.playerHp <= 0) {
        if (confirm('You have been defeated! Do you want to play again?')) {
          this.gameStart()
        } else {
          this.remarks = `Don't be a pussy, play another game`
        }
      } else if (this.monsterHp <= 0) {
        if (confirm('You have won! Do you want to play again?')) {
          this.gameStart()
        } else {
          this.remarks = `Thank you for playing my game of luck, best wishes!`
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
img {
  max-width: 30%;
  max-height: 200px;
  border-radius: 50%;
}
</style>
