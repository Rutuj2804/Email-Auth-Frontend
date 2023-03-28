<script>
export default {
  created() {
    if(!localStorage.getItem("email-token")) this.$router.push("/login")
  }
}
</script>

<template>
  <main>
    Home
  </main>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@400;600;700&display=swap');

@import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@400;600&display=swap');

*{
  margin: 0%;
  padding: 0%;
  box-sizing: border-box;
  font-family: 'Source Sans Pro', sans-serif;
}

</style>