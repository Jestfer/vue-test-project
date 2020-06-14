<template>
  <div class="firstComponent">
    <h1>First component template</h1>

    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: 'This is my first component in View'
    }
  }
}
</script>

<style></style>
