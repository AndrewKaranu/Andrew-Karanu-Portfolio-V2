<script>
  import TypingEffect from './TypingEffect.svelte';
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  
  let loaded = false;
  
  onMount(() => {
    setTimeout(() => {
      loaded = true;
    }, 100);
  });
</script>

<section id="home" class="hero-section" class:loaded={loaded}>
  <div class="hero-bg">
    <!-- Overlay is commented out in your original code -->
    <!-- <div class="overlay"></div> -->
  </div>
  
  <div class="hero-content">
    <div class="content-container" in:fade={{duration: 1000, delay: 300}}>
      <div class="profile-wrapper" in:fly={{y: -20, duration: 800, delay: 400}}>
        <div class="profile-circle">
          <div class="outer-ring"></div>
          <div class="inner-circle">
            <img src="Images/Photo.png" alt="Andrew Kamami" />
          </div>
        </div>
      </div>
      
      <div class="greeting">Hello, I'm</div>
      <h1 class="name">Andrew Kamami</h1>
      <div class="role-container">
        <div class="role-prefix">I'm a </div>
        <div class="role-text">
          <TypingEffect strings={["ML & AI Enthusiast","Web Developer", "Python Developer", "Java Developer", "Full Stack Engineer"]} />
        </div>
      </div>
      
      <p class="bio">
        Passionate developer with expertise in building modern web applications,
        data-driven solutions, and innovative software systems.
      </p>
      
      <div class="resume-button" in:fade={{duration: 800, delay: 600}}>
        <a href="\Andrew_Kamami_Resume.pdf" class="custom-button" download>
          <div class="button-content">
            <div class="button-icon">
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path><polyline points="7 10 12 15 17 10"></polyline><line x1="12" y1="15" x2="12" y2="3"></line></svg>
            </div>
            <span class="button-text">Download Resume</span>
          </div>
        </a>
      </div>

      <div class="social-links">
        <a href="https://github.com/AndrewKaranu" target="_blank" rel="noopener" aria-label="GitHub">
          <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
        </a>
        <a href="https://www.linkedin.com/in/andrew-karanu-998910237" target="_blank" rel="noopener" aria-label="LinkedIn">
          <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path><rect x="2" y="9" width="4" height="12"></rect><circle cx="4" cy="4" r="2"></circle></svg>
        </a>
      </div>
    </div>
  </div>
  
  <div class="scroll-indicator">
    <div class="mouse">
      <div class="wheel"></div>
    </div>
    <div class="arrow"></div>
  </div>
</section>

<style>
  .hero-section {
    position: relative;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    opacity: 0;
    transition: opacity 1s ease;
  }
  
  .hero-section.loaded {
    opacity: 1;
  }

  .hero-bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
  }
  
  .hero-content {
    width: 100%;
    max-width: 900px;
    margin: 0 auto;
    padding: 60px 20px 0;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    z-index: 1;
  }
  
  .content-container {
    max-width: 800px;
    width: 100%;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  /* Enhanced Profile Circle Styles */
  .profile-wrapper {
    margin-bottom: 2rem;
    display: flex;
    justify-content: center;
  }
  
  .profile-circle {
    position: relative;
    width: 160px;
    height: 160px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .outer-ring {
    position: absolute;
    width: 160px;
    height: 160px;
    border-radius: 50%;
    border: 2px solid #B87333;
    box-shadow: 0 0 20px rgba(184, 115, 51, 0.3);
    animation: pulse-ring 2s infinite ease-in-out;
  }
  
  .inner-circle {
    position: relative;
    width: 150px;
    height: 150px;
    border-radius: 50%;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
    border: 3px solid rgba(255, 255, 255, 0.2);
    transition: all 0.3s ease;
    z-index: 1;
    background: #1a1a1a; /* Dark background in case image has transparency */
  }
  
  .inner-circle:hover {
    transform: scale(1.05);
    border-color: rgba(184, 115, 51, 0.4);
  }
  
  .profile-circle img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
    transition: all 0.5s ease;
    transform: scale(1.02); /* Slightly oversized to avoid white edges */
    -webkit-backface-visibility: hidden; /* Helps with sharpness on some browsers */
    backface-visibility: hidden;
    image-rendering: -webkit-optimize-contrast; /* Helps with image clarity */
  }
  
  @keyframes pulse-ring {
    0% { transform: scale(1); opacity: 0.6; }
    50% { transform: scale(1.05); opacity: 1; }
    100% { transform: scale(1); opacity: 0.6; }
  }
  
  .greeting {
    font-size: 1.3rem;
    font-weight: 900;
    color: #cacaca;
    margin-bottom: 0.5rem;
    letter-spacing: 1px;
  }
  
  .name {
    font-size: 4.5rem;
    font-weight: 800;
    margin: 0.5rem 0;
    line-height: 1.1;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    background: linear-gradient(90deg, #ffffff, #B87333);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    text-fill-color: transparent;
  }
  
  .role-container {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    margin: 1rem 0 1.5rem;
    font-size: 1.6rem;
    color: #e0e0e0;
  }

  
  
  .role-text {
    color: #B87333;
    font-weight: 600;
  }
  
  .bio {
    font-size: 1.2rem;
    line-height: 1.6;
    color: #e0e0e0;
    margin: 0 auto 2rem;
    max-width: 700px;
  }
  
  .resume-button {
    margin-bottom: 2.5rem;
    display: flex;
    justify-content: center;
    width: 100%;
  }
  
  .custom-button {
    display: block;
    background: #B87333;
    color: #ffffff;
    text-decoration: none;
    font-weight: 500;
    font-size: 1.1rem;
    position: relative;
    border-radius: 30px;
    overflow: hidden;
    box-shadow: 0 4px 15px rgba(184, 115, 51, 0.3);
    transition: all 0.3s ease;
    width: 220px;
  }
  
  .button-content {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0.9rem 1.5rem;
    position: relative;
    z-index: 2;
  }
  
  .button-icon {
    margin-right: 0.8rem;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: transform 0.3s ease;
  }
  
  .custom-button::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(to right, #B87333, #d99d4f);
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  
  .custom-button:hover {
    transform: translateY(-3px);
    box-shadow: 0 6px 20px rgba(184, 115, 51, 0.4);
  }
  
  .custom-button:hover::after {
    opacity: 1;
  }
  
  .custom-button:hover .button-icon {
    transform: translateY(3px);
  }
  
  @media (max-width: 768px) {
    .custom-button {
      width: 100%;
      max-width: 280px;
    }
    
    .button-content {
      padding: 0.8rem 1.5rem;
    }
  }
  .social-links {
    display: flex;
    gap: 1.5rem;
    justify-content: center;
  }
  
  .social-links a {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background: rgba(30, 30, 30, 0.4);
    color: #e0e0e0;
    transition: all 0.3s ease;
    border: 1px solid rgba(60, 60, 60, 0.8);
  }
  
  .social-links a:hover {
    background: rgba(184, 115, 51, 0.8);
    color: #fff;
    transform: translateY(-3px) scale(1.1);
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  }
  
  .scroll-indicator {
    position: absolute;
    bottom: 30px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    opacity: 0.7;
    transition: opacity 0.3s ease;
  }
  
  .scroll-indicator:hover {
    opacity: 1;
  }
  
  .mouse {
    width: 28px;
    height: 45px;
    border: 2px solid #B87333;
    border-radius: 25px;
    position: relative;
  }
  
  .wheel {
    width: 3px;
    height: 8px;
    background: #B87333;
    position: absolute;
    top: 8px;
    left: 50%;
    transform: translateX(-50%);
    border-radius: 3px;
    animation: scroll 2s infinite;
  }
  
  .arrow {
    width: 12px;
    height: 12px;
    border-right: 2px solid #B87333;
    border-bottom: 2px solid #B87333;
    transform: rotate(45deg);
    animation: arrow 2s infinite;
  }
  
  @keyframes scroll {
    0% { top: 8px; opacity: 1; }
    100% { top: 25px; opacity: 0; }
  }
  
  @keyframes arrow {
    0% { opacity: 0; }
    50% { opacity: 1; }
    100% { opacity: 0; }
  }
  
  @media (max-width: 992px) {
    .hero-content {
      padding-top: 100px;
    }
    
    .name {
      font-size: 3.5rem;
    }
    
    .role-container {
      font-size: 1.4rem;
    }
    
    .bio {
      font-size: 1.1rem;
    }
  }
  
  @media (max-width: 768px) {
    .hero-section {
      padding: 0 1rem;
    }
    
    .profile-circle {
      width: 140px;
      height: 140px;
    }
    
    .outer-ring {
      width: 140px;
      height: 140px;
    }
    
    .inner-circle {
      width: 130px;
      height: 130px;
    }
    
    .name {
      font-size: 2.5rem;
    }
    
    .greeting {
      font-size: 1.1rem;
    }
    
    .role-container {
      font-size: 1.2rem;
    }
    
    .bio {
      font-size: 1rem;
    }
    
    
  }
</style>