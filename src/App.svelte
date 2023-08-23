<script lang="ts">
  import {
    QueryClient,
    QueryClientProvider,
    createQuery,
  } from "@tanstack/svelte-query";
  import Leaderboard from "./lib/components/Leaderboard.svelte";

  const queryClient = new QueryClient();
</script>

<QueryClientProvider client={queryClient}>
  <div class="container">
    <Leaderboard />
  </div>
</QueryClientProvider>

<style>
  .container {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: var(--size-4);
    gap: var(--size-5);
  }
</style>
