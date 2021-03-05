<script>
  import { QueryClient, QueryClientProvider } from "@sveltestack/svelte-query";
  import MyCompo from "./MyCompo.svelte";
  const queryClient = new QueryClient();
</script>

<main>
  <QueryClientProvider client={queryClient}>
    <MyCompo/>
  </QueryClientProvider>
</main>
