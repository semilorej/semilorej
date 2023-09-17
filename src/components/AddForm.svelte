<script>
  import Button from "./Button.svelte";
  import Card from "./Card.svelte";
  import RatingSelect from "./RatingSelect.svelte";

  let text;
  let btnDisabled = true;
  let rating = 10;
  let min = 10;
  let message;

  const handleInput = () => {
    if (text.trim().length <= min) {
      message = `Text must be ${min} characters`;
      btnDisabled = true;
    } else {
      message = null;
      btnDisabled = false;
    }
  };

  const handleSelect = (e) => (rating = e.detail);
</script>

<Card
  ><header>
    <h2>How would you rate your service with us?</h2>
  </header>

  <form>
    <RatingSelect on:rating-select={handleSelect} />
    <div class="input-group">
      <input
        type="text"
        bind:value={text}
        on:input={handleInput}
        placeholder="Tell us something that makes you come back"
      />
      <Button disabled={btnDisabled} type="submit">Send</Button>
    </div>
    {#if message}
      <div class="message">
        {message}
      </div>
    {/if}
  </form>
</Card>

<style>
  header {
    max-width: 400px;
    margin: auto;
    text-align: center;
  }

  input {
    width: 550px;
    margin: 0;
    height: 30px;
  }
</style>
