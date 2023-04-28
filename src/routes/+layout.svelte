<script lang="ts">
  import { applyAction, enhance } from '$app/forms'
  import { currentUser, pb } from '$lib/pocketbase'
  import '../app.postcss'
</script>

<div class="bg-neutral text-neutral-content">
  <div class="mx-auto navbar">
    <div class="navbar-start">
      <a href="/" class="btn- btn-ghost text-xl">Floyd County Water Department</a>
    </div>
    <div class="navbar-end">
      <ul class="menu menu-horizontal">
        {#if $currentUser}
        <li><a href="/posts">Posts</a>
          <a href="/">{$currentUser.email}</a>
            <form
              method="POST"
              action="/logout"
              use:enhance={() => {
                return async ({ result }) => {
                  pb.authStore.clear()
                  await applyAction(result)
                }
              }}
            >
              <button>Log out</button>
            </form>
          </li>
        {:else}
          <li><a href="/login">Log in</a></li>
          <li><a href="/register">Register</a></li>
        {/if}
      </ul>
    </div>
  </div>
</div>

<div class="mx-16 px-4 flex justify-center">
  <slot />
</div>

<footer class="footer fixed bottom-0 footer-center p-4 bg-base-300 text-base-content">
  <div>
    <p>Floyd County Water Department</p>
  </div>
</footer>