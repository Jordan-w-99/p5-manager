<script>
  import { onMount } from 'svelte';
  import Collection from "./Collection.svelte";

  let isActive = false;
  let loaded = false;
  let projectTree;

  const fetchData = async () => {
    const response = await fetch('/api/p5rc');
    return await response.json();
  };

  function handleToggle() {
    isActive = !isActive;
  }

  onMount(async () => {
    try {
      projectTree = await fetchData();
      console.log(projectTree);
      loaded = true;
    } catch (error) {
      console.error(error);
    }
  });
</script>

<div class="sidebar {isActive ? '-active' : ''}">
  <button class="toggle" on:click="{handleToggle}">
    <img src="/assets/star.png" alt="star.png" />
  </button>

  {#if loaded}
    <Collection name="collections" projects={projectTree} expanded path=''/>
  {/if}

  <div class="footer">
    <a href="https://github.com/chiunhau/p5-manager" class="version">
      p5-manager v1.4.0
    </a>
    <br />
    by
    <a href="https://twitter.com/chiunhauyou" class="author highlight"
      >@chiunhauyou</a>
  </div>
</div>

<style>
  .sidebar {
    position: absolute;
    top: 0;
    left: -220px;
    width: 220px;
    height: 100%;
    padding-left: 20px;
    background-color: #f5f5f5;
    text-align: left;
    transition: all 0.5s;
    -webkit-transition: all 0.5s;
    z-index: 10;
    box-sizing: border-box;
  }

  .sidebar.-active {
    left: 0;
  }

  .toggle {
    position: absolute;
    top: 10px;
    right: -40px;
    background-color: transparent;
    border: none;
    transition: all 1s;
    -webkit-transition: all 1s;
    z-index: 11;
    cursor: pointer;
  }

  .toggle > img {
    width: 24px;
  }

  .sidebar.-active .toggle {
    -ms-transform: rotate(144deg);
    -webkit-transform: rotate(144deg);
    transform: rotate(144deg);
  }

  .sidebar ul li a {
    color: #333;
  }

  .sidebar .footer {
    position: absolute;
    bottom: 20px;
    font-size: 13px;
    color: #333;
  }

  .highlight {
    color: #f07;
  }
</style>
