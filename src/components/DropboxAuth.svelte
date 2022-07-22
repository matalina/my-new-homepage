<script type="ts">

$: if(window.location.hash) {
  if(window.location.hash.includes('#access_token=')) {
    const access_token = window.location.hash.replace('#access_token=','');
    localStorage.access_token = access_token;
    window.location.replace('/');
  }
}

$: loggedIn = localStorage.access_token;

import { DropboxAuth } from 'dropbox';
async function dropboxAuth() {
  const auth = new DropboxAuth({
    clientId: import.meta.env.VITE_DROPBOX_API,
    clientSecret: import.meta.env.VITE_DROPBOX_SECRET,
  });
  const url = await auth.getAuthenticationUrl(window.location.href);
  console.log(url);
  window.location = url as any;
}
</script>

{#if !loggedIn}
<button on:click={dropboxAuth}>Connect to Dropbox</button>
{/if}