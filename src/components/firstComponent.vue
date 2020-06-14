<template>
  <div class="firstComponent">
    <h1>First component info</h1>

    <p>{{ message }}</p>

    <v-card outlined max-width="344">
      <v-card-title>This is an example joke</v-card-title>
      <v-card-subtitle>We hope you like it :)</v-card-subtitle>
      <p>REPLACE FOR JOKE</p>
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
import { map, startWith, scan } from 'rxjs/operators'

@Component
export default class FirstComponent extends Vue {
  message = ''
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
  }
}
</script>

<style></style>
