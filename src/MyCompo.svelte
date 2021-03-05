<script>
  import {
    useQuery,
    useMutation,
    useQueryClient,
  } from "@sveltestack/svelte-query";

  // Access the client
  const queryClient = useQueryClient();

  const wait = (n) => new Promise((r) => setTimeout(r, n));

  // Queries
  const queryResult = useQuery("todos", async () => {
    console.log("fetching");
    await wait(1000);
    return [
      {
        title: "do something",
      },
      {
        title: "do something else",
      },
    ];
  });
</script>

{#if $queryResult.status === 'loading'}
  <span>Loading...</span>
{:else if $queryResult.status === 'error'}
  <span>Error: {$queryResult.error.message}</span>
{:else}
  <ul>
    {#each $queryResult.data as todo}
      <li>{todo.title}</li>
    {/each}
  </ul>
  <button on:click={$queryResult.refetch} disabled={$queryResult.isFetching}>refresh</button>
{/if}
