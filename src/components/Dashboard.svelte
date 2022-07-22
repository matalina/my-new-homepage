<script type="ts">
  $: loggedIn = localStorage.access_token;
</script>

{#if loggedIn}
<h1>Dashboard</h1>
{/if}