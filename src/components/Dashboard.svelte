<script type="ts">
import { Dropbox } from "dropbox";
import { onMount } from "svelte";


$: loggedIn = localStorage.access_token;
$: currentUser = localStorage.user ? JSON.parse(localStorage.user) : {};

let dropbox = new Dropbox({
  accessToken: localStorage.access_token,
  accessTokenExpiresAt: localStorage.expires_in,
});

async function getUser() {
  const response = await dropbox.usersGetCurrentAccount();
  localStorage.user = JSON.stringify(response.result);
}

onMount(() => {
  getUser();
})

</script>

{#if loggedIn}
<p>Logged in as: <strong>{currentUser.name.display_name}</strong>
{/if}