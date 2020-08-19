<template>
  <div class="date-container">
    <span class="day">WED</span>
    <span class="date">
      <div>NOV</div>
      <div>8TH</div>
    </span>
  </div>
</template>

<script>
export default {};
</script>

<style>
.date-container {
  display: grid;
  grid-auto-flow: column;
  column-gap: 10px;
  align-items: start;
}
.date {
  background: var(--main-blue);
  color: white;
  font-weight: bold;
  padding: 5px;
}

.day {
  color: var(--main-grey);
  font-size: 2.125rem;
}
</style>