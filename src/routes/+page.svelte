<script>
  import { supabase } from '$lib/supabase';

  let isSignedIn = false;
  let message = '';
  let isLoading = false;
  const signIn = async () => {
    isLoading = true;
    const { data, error } = await supabase.auth.signInWithOAuth({
      provider: 'google',
      options: {
        queryParams: {
          access_type: 'offline',
          prompt: 'consent',
        },
      },
    });
    if (error) {
      isSignedIn = false;
      message = 'an error ocurred';
      isLoading = false;
      return;
    }
    if (data) {
      isSignedIn = true;
      message = 'signedIn';
      isLoading = false;
    }
  };
</script>

<section>
  <button on:click={signIn}> sign In </button>

  {#if isSignedIn || !isSignedIn}
    <p>{message}</p>
  {/if}
</section>

<style>
</style>
