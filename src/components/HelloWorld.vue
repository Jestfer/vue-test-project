<template>
  <v-container>
    {{ details }}
    <p>{{ msg }}</p>
  </v-container>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string

  details = 'Sandbox for Vue app'
}
</script>
