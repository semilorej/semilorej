<script>
  import { v4 as uuidv4 } from "uuid";
  import Button from "./Button.svelte";
  import { createEventDispatcher } from "svelte";
  import Card from "./Card.svelte";
  import RatingSelect from "./RatingSelect.svelte";

  const dispatch = createEventDispatcher();

  let text;
  let btnDisabled = true;
  let rating = 10;
  let min = 10;
  let message;

  const handleSubmit = () => {
    if (text.trim().length >= min) {
      const newFeedback = {
        id: uuidv4(),
        text,
        rating: +rating,
      };
      dispatch("add-feedback", newFeedback);

      text = "";
    }
  };

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

  <form on:submit|preventDefault={handleSubmit}>
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
