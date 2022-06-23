<script>
  import { push, location } from 'svelte-spa-router';

  function handleRouteChange(to) {
    console.log(to);
    push(to);
  }

  export let name;
  export let path;
  $: type = name.slice(name.lastIndexOf('.') + 1);
</script>

<span>
    <span on:click="{() => handleRouteChange(`${path}/${name}`)}"
        class="{name === $location.slice(1) ? '-active' : ''}">
        {name}
    </span>
        <a href="{`${path}/${name}/index.html`}" target="_blank">↗</a>
</span>

<style>
  span {
    padding: 0 0 0 1.5em;
    background: 0 0.1em no-repeat;
    background-size: 1em 1em;
  }
</style>
