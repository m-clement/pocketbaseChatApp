<script lang="ts">
  import { currentUser, pb } from './pocketbase'
</script>

{#if $currentUser} 
  <p>Signed in as {$currentUser.username}</p>
{/if}
