<script>
    import { onMount } from 'svelte';
    import Typed from 'typed.js';
  
    export let strings = [];
  
    let element;
  
    onMount(() => {
      new Typed(element, {
        strings: strings,
        typeSpeed: 100,
        backSpeed: 80,
        loop: true,
        backDelay: 1500
      });
    });
  </script>
  
  <span bind:this={element}></span>