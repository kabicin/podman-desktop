<script lang="ts">
import { createEventDispatcher, onMount } from 'svelte';
import { Input } from '@podman-desktop/ui-svelte';
import Fa from 'svelte-fa';
import { faEye, faEyeSlash } from '@fortawesome/free-regular-svg-icons';

export let id: string;
export let password: string | undefined = undefined;
export let passwordHidden: boolean = true;
export let readonly: boolean = false;

let element: HTMLInputElement;

const dispatch = createEventDispatcher();

onMount(() => {
  element.type = 'password';
});

// show/hide if the parent doesn't override
async function onShowHide() {
  if (dispatch('toggleShowHide', { cancelable: true })) {
    passwordHidden = !passwordHidden;
    element.type = passwordHidden ? 'password' : 'text';
  }
}
</script>

<Input
  class="{$$props.class || ''}"
  id="password-{id}"
  name="password-{id}"
  placeholder="Password"
  bind:value="{password}"
  aria-label="password {id}"
  bind:readonly="{readonly}"
  on:input
  bind:element="{element}">
  <svelte:fragment slot="right">
    <button
      class="px-1 cursor-pointer text-gray-700 group-hover:text-gray-900 group-focus-within:text-gray-900"
      class:hidden="{!password || readonly}"
      aria-label="show/hide"
      on:click="{onShowHide}"
      >{#if passwordHidden}
        <Fa icon="{faEye}" />
      {:else}
        <Fa icon="{faEyeSlash}" />
      {/if}
    </button>
  </svelte:fragment>
</Input>
