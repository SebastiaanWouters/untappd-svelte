<script>
  import { createQuery } from "@tanstack/svelte-query";

  const data = createQuery({
    queryKey: ["untappd_data"],
    queryFn: fetchUserData,
  });

  async function fetchUserData() {
    const data = await fetch("https://untappd.sebdev.be/api/stats");
    const json = await data.json();
    return json;
  }

  // Reactive statement to sort the stats based on beers count
  $: sortedStats = $data.data
    ? [...$data.data.stats].sort((a, b) => b.beers - a.beers)
    : [];
</script>

<h3>Untappd Leaderboard</h3>
<table>
  <tr>
    <th>#</th>
    <th>Name</th>
    <th>Beers</th>
    <th>Badges</th>
    <th>Checkins</th>
  </tr>
  {#if $data.isSuccess}
    {#each sortedStats as user, i}
      <tr>
        <td>{i + 1}</td>
        <td>{user.firstname}</td>
        <td>{user.beers}</td>
        <td>{user.badges}</td>
        <td>{user.checkins}</td>
      </tr>
    {/each}
  {:else}
    <tr>
      <td>Failed</td>
      <td>to</td>
      <td>get</td>
      <td>data</td>
      <td>rip</td>
    </tr>
  {/if}
</table>

<style>
  h3 {
    font-size: calc(var(--size-fluid-4) * 0.99);
  }
</style>
