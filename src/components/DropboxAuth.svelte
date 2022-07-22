<script type="ts">

$: if(window.location.hash) {
  if(window.location.hash.includes('#access_token=')) {
    const hash = window.location.hash.replace('#','');
    const parts = hash.split('&');
    console.log(parts);
    for(const i in parts) {
      let pair = parts[i];
      const row = pair.split('=');
      localStorage[row[0]] = row[1];
    }
    
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