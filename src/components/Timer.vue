<template>
	<v-container fluid>
    <v-layout>
      <v-flex xs12 pa-3>
        <v-card>
          <v-card-title class="secondary white--text font-weight-light display-2 text-uppercase justify-center">
            {{ timer }}
          </v-card-title>
          <v-card-text>
            <v-btn
              block
              class="success mb-3"
              @click="$emit('start')"
              :disabled="state == 'running'"
              color="success"
            >
              Start
            </v-btn>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: 'Timer',
  props: ['timer', 'state']
}
</script>
