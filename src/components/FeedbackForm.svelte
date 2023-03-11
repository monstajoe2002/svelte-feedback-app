<script>
  import { v4 as uuidV4 } from "uuid";
  import { FeedbackStore } from "../stores";
  import Button from "./Button.svelte";
  import Card from "./Card.svelte";
  import RatingSelect from "./RatingSelect.svelte";
  let text = "";
  let message;
  let btnDisabled = true;
  let rating = 10;
  const handleSelect = (e) => (rating = e.detail);
  const handleInput = () => {
    if (text.trim().length <= 10) {
      message = "Text must be at least 10 characters long";
      btnDisabled = true;
    } else {
      message = null;
      btnDisabled = false;
    }
  };
  const handleSubmit = () => {
    if (text.trim().length > 10) {
      const newFeedback = {
        id: uuidV4(),
        text,
        rating: +rating,
      };
      FeedbackStore.update((currFeedback) => {
        return [newFeedback, ...currFeedback];
      });
      text = "";
    }
  };
</script>

<Card>
  <header>
    <h2>How would you rate your service with us?</h2>
  </header>
  <form on:submit|preventDefault={handleSubmit}>
    <RatingSelect on:rating-select={handleSelect} />
    <div class="input-group">
      <input
        type="text"
        on:input={handleInput}
        bind:value={text}
        placeholder="Tell us something that keeps you coming back"
      />
      <Button type="submit" disabled={btnDisabled}>Send</Button>
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
  }
  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }
  .input-group {
    display: flex;
    flex-direction: row;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }
  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }
  input:focus {
    outline: none;
  }
  .message {
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>
