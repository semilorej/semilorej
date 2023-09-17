<script>
  export let count;
  export let average;
</script>

<div class="feedback-stats">
  <h1>{count} Reviews</h1>
  <h1>Average Rating: {average}</h1>
</div>

<style>
  .feedback-stats {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>
