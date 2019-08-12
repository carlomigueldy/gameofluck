<template>
  <div class="container">
    <div class="card card-body mb-3">
      <div class="row text-center">
        <div class="col">
          <h1>You</h1>
          <div class="progress" style="height: 50%;">
            <div class="progress-bar bg-success" role="progressbar" 
            style="width: 100%" :style="{width: playerHp + '%'}"
            :aria-valuenow="playerHp" aria-valuemin="0" aria-valuemax="100"><h3>{{ playerHp + '%' }}</h3></div>
          </div>
        </div>
        <div class="col">
          <h1>Monster</h1>
          <div class="progress" style="height: 50%;">
            <div class="progress-bar" role="progressbar" 
              style="width: 100%;" :style="{width: monsterHp + '%'}"
              :aria-valuenow="monsterHp" aria-valuemin="0" aria-valuemax="100"><h3>{{ monsterHp + '%' }}</h3></div>
            </div>
          </div>
      </div>
      <div class="row">
        <div class="col text-center card-body pt-5" v-if="remarks">
          <div class="badge badge-danger"><h1>{{ remarks }}</h1></div>
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
        <div class="col">
          <div class="text-center">
            <div class="bg-primary text-white" v-for="pStatus in playerStatus" :key="pStatus">{{ status }}</div>
            <div class="bg-danger text-white" v-for="mStatus in monsterStatus" :key="mStatus">{{ mStatus }}</div>
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
      playerStatus: [''],
      monsterStatus: [''],
      remarks: ''
    }
  },
  methods: {
    gameStart() {
      this.gameStarted = true
      this.playerHp = 100
      this.monsterHp = 100
    },
    attack() {
      var min=5, max=15
      var damage = Math.random() * (+max - +min) + +min
      this.playerHp -= Math.round(damage)
      this.playerStatus.push(`Player taken damge of ${Math.round(damage)}`)

      if(this.playerHp <= 0) {
        this.remarks = 'You have been defeated!'
        this.gameStarted = false
      }

      min = 1, max = 7
      damage = Math.random() * (+max - +min) + +min
      this.monsterHp -= Math.round(damage)
      this.monsterStatus.push(`Monster taken damge of ${Math.round(damage)}`)

      if(this.monsterHp <= 0) {
        this.remarks = 'The monster has been slain'
        this.gameStarted = false
      }
    },
    specialAttack() {

    },
    heal() {

    },
    giveUp() {
      this.gameStarted = !this.gameStarted
      this.playerStatus = ['']
      this.monterStatus = ['']
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
