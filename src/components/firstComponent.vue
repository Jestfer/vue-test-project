<template>
  <div class="firstComponent">
    <h1>First component info</h1>

    <p>{{ message }}</p>

    <v-card outlined max-width="344">
      <v-card-title>This is an example joke</v-card-title>
      <v-card-subtitle>We hope you like it :)</v-card-subtitle>
      <p>REPLACE FOR JOKE</p>
    </v-card>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class FirstComponent extends Vue {
  message = ''
}
</script>

<style></style>
