<script>
  import AddForm from "./components/AddForm.svelte";
  import FeedbackList from "./components/FeedbackList.svelte";
  import FeedbackStats from "./components/FeedbackStats.svelte";

  $: count = feedback.length;
  $: average =
    feedback.reduce((a, { rating }) => a + rating, 0) / feedback.length;
  let feedback = [
    {
      id: 1,
      rating: 10,
      text: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Inventore laborum molestiae at repudiandae dolorum exercitationem veniam omnis a, voluptatum mollitia adipisci eveniet fugit rem totam. Consequatur culpa incidunt ipsa accusantium!",
    },
    {
      id: 2,
      rating: 8,
      text: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Inventore laborum molestiae at repudiandae dolorum exercitationem veniam omnis a, voluptatum mollitia adipisci eveniet fugit rem totam. Consequatur culpa incidunt ipsa accusantium!",
    },
    {
      id: 3,
      rating: 9,
      text: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Inventore laborum molestiae at repudiandae dolorum exercitationem veniam omnis a, voluptatum mollitia adipisci eveniet fugit rem totam. Consequatur culpa incidunt ipsa accusantium!",
    },
  ];

  const addFeedback = (e) => {
    const newFeedback = e.detail;
    feedback = [newFeedback, ...feedback];
  };

  const handleDeleteTask = (e) => {
    const id = e.detail;
    feedback = feedback.filter((item) => item.id != id);
  };
</script>

<main class="container">
  <AddForm on:add-feedback={addFeedback} />
  <FeedbackStats {count} {average} />
  <FeedbackList {feedback} on:delete-feedback={handleDeleteTask} />
</main>

<style>
</style>
