<template>
	<v-container fluid>
    <v-layout>
      <v-flex xs12 pa-3>      
        <div class="flex-container">
          <div class="home">
            <div>
              <v-btn 
                fab
                large
                class="success"
                @click="increaseHome(9)"
              >+</v-btn>
            </div>
            <div>
              <v-btn                                 
                fab
                large              
                class="error"
                @click="decreaseHome(0)"
              >-</v-btn>
            </div>
          </div>
          <div class="score">
            <h1>{{scoreHome}} : {{scoreAway}}</h1>
          </div>
          <div class="away">
            <div>
              <v-btn 
                fab
                large
            class="success"
                @click="increaseAway(9)"
              >+</v-btn>
            </div>
            <div>
              <v-btn 
                fab
                large
                class="error"
                @click="decreaseAway(0)"
              >-</v-btn>
            </div>
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
  .score {  
    text-align: center;
  }

  h1 {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 144px;
  }

  .btn-container {
    display: flex;
  }

  .btn-home{
    flex: 1;
    text-align: start;
  }

  .btn-away{
    flex: 1;
    text-align: end;
  }

  .flex-container {
    display: flex;
  }

  .home {
    display: flex;
    flex: 1;
    flex-direction: column;
    text-align: start;
    margin: auto;
  }

  .away {
    display: flex;
    flex: 1;
    flex-direction: column;
    text-align: end;
    margin: auto;
  }

</style>