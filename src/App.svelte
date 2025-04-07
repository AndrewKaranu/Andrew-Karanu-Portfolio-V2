<script>
	import Header from './components/Header.svelte';
	import Home from './components/Home.svelte';
	import About from './components/About.svelte';
	import Projects from './components/Projects.svelte';
	import Contact from './components/Contact.svelte';
  </script>
  
  <Header />
  <main>
	<Home />
	<About />
	<Projects />
	<Contact />
  </main>
  <footer>
	<div class="copyright">
	  <p>&copy; 2023 Your Name. All rights reserved.</p>
	</div>
  </footer>
  
  <style>
	/* Add any global styles here */
	:global(body) {
	  font-family: 'Poppins', sans-serif;
	  line-height: 1.6;
	  color: #ffffff;
	  background: linear-gradient(-45deg, #4d4d4d, #000000, #ac621d, #3d4140);
	  background-size: 400% 400%;
	  animation: gradient 15s ease infinite;
	}
  
	@keyframes gradient {
	  0% { background-position: 0% 50%; }
	  50% { background-position: 100% 50%; }
	  100% { background-position: 0% 50%; }
	}
  
	main {
	  max-width: 1200px;
	  margin: 0 auto;
	  padding: 0 20px;
	}
  
	footer {
	  text-align: center;
	  padding: 20px 0;
	  background-color: #505554;
	}
  </style>