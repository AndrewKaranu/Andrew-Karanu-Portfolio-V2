<script>
  import { scrollTo } from 'svelte-scrollto';
</script>

<header class="header-area">
  <div class="container">
    <div class="header">
      <div class="logo">
        <a href="#home"><img src="./Images/Logo.png" alt="Logo" width="50" height="50"></a>
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
  .header-area {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 1000;
    background: rgba(0, 0, 0, 0.8);
    backdrop-filter: blur(5px);
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  }
  
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
  }
  
  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 6px 0;
    min-height: 60px;
  }
  
  .logo {
    display: flex;
    align-items: center;
  }
  
  .logo img {
    display: block;
    transition: transform 0.3s ease;
    max-height: 50px;
    width: auto;
  }
  
  .logo img:hover {
    transform: scale(1.05);
  }
  
  .menu ul {
    display: flex;
    gap: 2rem;
    list-style: none;
    margin: 0;
    padding: 0;
  }
  
  .menu a {
    color: #e0e0e0;
    text-decoration: none;
    font-size: 1rem;
    font-weight: 500;
    letter-spacing: 0.5px;
    transition: all 0.3s ease;
    padding: 6px 0;
    position: relative;
  }
  
  .menu a:hover {
    color: #B87333;
  }
  
  .menu a::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 0;
    height: 2px;
    background-color: #B87333;
    transition: width 0.3s ease;
  }
  
  .menu a:hover::after {
    width: 100%;
  }
  
  @media (max-width: 768px) {
    .header {
      flex-direction: row;
      padding: 8px 0;
      flex-wrap: wrap;
      justify-content: center;
    }
    
    .logo {
      margin-right: 1.5rem;
    }
    
    .logo img {
      max-height: 40px;
    }
    
    .menu ul {
      gap: 1rem;
    }
    
    .menu a {
      font-size: 0.95rem;
      padding: 4px 0;
    }
  }
  
  @media (max-width: 576px) {
    .header {
      flex-direction: column;
      padding: 10px 0;
    }
    
    .logo {
      margin-right: 0;
      margin-bottom: 8px;
    }
    
    .menu ul {
      gap: 0.75rem;
    }
  }
</style>