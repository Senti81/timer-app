<template>
	<v-container fluid>
    <v-layout>
      <v-flex xs12 pa-3>
        <div class="label">
          <div class="score">
            <h1>{{scoreHome}}</h1>
          </div>
          <div class="score">
            <h1>:</h1>
          </div>
          <div class="score">
            <h1>{{scoreAway}}</h1>
          </div>
        </div>
        <v-card>
          <v-card-title class="secondary white--text font-weight-light display-2 text-uppercase justify-center">
            {{ timer }}
          </v-card-title>
          <v-card-text>
            <v-list>
              <v-btn
                block
                class="success mb-3"
                @click="$emit('start')"
                :disabled="state == 'running'"
              >
                Start
              </v-btn>             
              <v-btn
                block
                class="warning mb-3"
                @click="$emit('pause')"
                :disabled="state == 'stopped' || state == 'paused'"
              >
                Pause
              </v-btn>
              <v-btn
                block
                class="error"
                @click="$emit('stop')"
                :disabled="state == 'stopped'"
              >
                Stop
              </v-btn>
              <div class="flex-container">
                <div class="left">
                  <v-btn 
                    fab
                    class="success"
                    @click="increaseHome(9)"
                    >+</v-btn>
                  <v-btn
                    fab
                    class="error"
                    @click="decreaseHome(0)"
                    >-</v-btn>
                </div>
                <div class="right">
                  <v-btn
                    fab
                    class="success"
                    @click="increaseAway(9)"
                    >+</v-btn>
                  <v-btn
                    fab
                    class="error"
                    @click="decreaseAway(0)">-</v-btn>
                </div>
              </div>     
            </v-list>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      scoreHome: 0,
      scoreAway: 0,
    }
  },
  methods: {
    increaseHome(limit) {
      if(this.scoreHome < limit) this.scoreHome++;
    },
    decreaseHome(limit) {
      if (this.scoreHome > limit) this.scoreHome--;
    },
    increaseAway(limit) {
      if(this.scoreAway < limit) this.scoreAway++;
    },
    decreaseAway(limit) {
      if (this.scoreAway > limit) this.scoreAway--;
    }
  },
  name: 'Timer',
  props: ['timer', 'state']
}
</script>

<style scoped>
  .label {
    text-align: center;    
  }

  .score {
    display: inline-block;
    width: 15%;
    height: 150px;
    margin: 20px;
  }

  h1 {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 72px;
  }

  .flex-container {
    display: flex;
  }

  .left{
    display: flex;
    flex-direction: row;
    width: 50%;
  }

  .right{
    display: flex;
    flex-direction: row-reverse;
    width: 50%;
  }

</style>