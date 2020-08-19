<template>
  <header>
    <h1>Demo</h1>
    <img src="https://static.tumblr.com/vr9xgox/oiLnf8zpv/rss.gif" />
  </header>
</template>

<script>
export default {};
</script>

<style scoped>
header {
  display: grid;
  grid: auto / 1fr auto;
  border-bottom: 1px solid grey;
}

img {
  justify-self: end;
  align-self: flex-end;
}
h1 {
  justify-self: center;
  align-self: center;
  color: #444;
  font-size: 3.4375rem;
  font-weight: bold;
}
</style>