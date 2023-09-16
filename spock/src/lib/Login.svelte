<script lang="ts">
  import { currentUser, pb } from './pocketbase'

  let username: string;
  let password: string;

  async function login() {
    await pb.collection('users').authWithPassword(username, password);
  }

  async function signup() {
    
    try {
      const data = {
        username,
        password,
        passwordConfirm: password,
        name: 'hi mom!'
      };
      const createdUser = await pb.collection('users').create(data);
      await login();
    } catch (err) {
      console.error(err);
    }
  }

  function signOut() {
    pb.authStore.clear();
  }

</script>

{#if $currentUser} 
  <p>Signed in as {$currentUser.username}</p>
{:else}
  <form>
    <input
      placeholder="Username"
      type="text"
      bind:value={username}
    />

    <input
      placeholder="Password"
      type="password"
      bind:value={password}
    />

    <button>Sign up</button>
    <button>Login</button>
  </form>
{/if}
