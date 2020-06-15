<template>
  <div class="firstComponent">
    <h1>First component info</h1>

    <p>{{ message }}</p>

    <v-card outlined max-width="344" class="centered">
      <v-card-title>This is an example joke</v-card-title>
      <v-card-subtitle>We hope you like it :)</v-card-subtitle>
      <p>{{ joke }}</p>
    </v-card>

    <br /><br />
    <div>{{ count }}</div>
    <br /><br />
    <button v-stream:click="plus$">+ SUMA</button>
    <br /><br />
    <button v-stream:click="minus$">- RESTA</button>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import { merge, Subject } from 'rxjs'
import { map, startWith, scan, first } from 'rxjs/operators'
import Axios from 'axios-observable'

@Component
export default class FirstComponent extends Vue {
  message = ''
  joke = ''
  count = null as unknown
  plus$ = new Subject()
  minus$ = new Subject()

  mounted() {
    // subscriptions() gives issues in Component-class based: https://github.com/vuejs/vue-rx/issues/71#issuecomment-372154250
    this.$subscribeTo(
      merge(
        this.plus$.pipe(map(() => 1)),
        this.minus$.pipe(map(() => -1))
      ).pipe(
        startWith(0),
        scan((total, change) => (this.count = total + change))
      ),
      clicksCount => {
        this.count = clicksCount
      }
    )

    // TODO: this belongs in a service, added here for quick POC
    Axios.get('https://icanhazdadjoke.com/', {
      headers: {
        Accept: 'application/json'
      }
    })
      .pipe(first())
      .subscribe(res => {
        this.joke = res.data.joke
      })
  }
}
</script>

<style>
.centered {
  margin: 0 auto;
}
</style>
