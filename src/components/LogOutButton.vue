<template>
  <!-- Your login form template -->
  <button @click="lougOut">Log me Out</button>
</template>

<script>
export default {
  methods: {
    lougOut() {
      // Perform login logic here
        alert('NEIn')
      this.$emit('logOutSuccess') // Emit the loginSuccess event
    }
  }
}
</script>
