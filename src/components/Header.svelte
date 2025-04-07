<script>
    import { scrollTo } from 'svelte-scrollto';
  </script>
  
  <header class="header-area">
    <div class="container">
      <div class="header">
        <div class="logo">
          <a href="#home"><img src="Images/Logo.png" alt="Logo" width="80" height="80"></a>
        </div>
        <nav class="menu">
          <ul>
            {#each ['Home', 'About', 'Projects', 'Contact'] as item}
              <li><a href="#{item.toLowerCase()}" on:click|preventDefault={() => scrollTo({element: `#${item.toLowerCase()}`})}>{item}</a></li>
            {/each}
          </ul>
        </nav>
      </div>
    </div>
  </header>
  
  <style>
    /* Add your existing CSS here */
    .header-area {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      z-index: 1000;
      background: rgba(0, 0, 0, 0.8);
      backdrop-filter: blur(5px);
    }
    /* Add more styles as needed */
  </style>