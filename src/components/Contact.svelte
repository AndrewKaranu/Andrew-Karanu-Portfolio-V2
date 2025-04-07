<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  
  let isVisible = false;
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      if (entries[0].isIntersecting) {
        isVisible = true;
      }
    }, { threshold: 0.1 });
    
    const section = document.getElementById('contact');
    if (section) observer.observe(section);
    
    return () => {
      if (section) observer.unobserve(section);
    };
  });
</script>

<section id="contact" class="contact-section">
  <div class="bg-accent accent-1"></div>
  <div class="bg-accent accent-2"></div>
  
  <div class="section-header" class:visible={isVisible}>
    <h2>Get In Touch</h2>
    <div class="section-line"></div>
  </div>
  
  <div class="contact-container" class:visible={isVisible}>
    <div class="contact-card">
      <p class="contact-intro">
        I'm always open to new opportunities and collaborations. Feel free to reach out through any of the following channels:
      </p>
      
      <div class="contact-info">
        <div class="contact-item" in:fly={{ y: 20, delay: 100, duration: 400 }}>
          <div class="contact-icon">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path><polyline points="22,6 12,13 2,6"></polyline></svg>
          </div>
          <div class="contact-text">
            <h3>Email</h3>
            <p><a href="mailto:andrewkaranu03@gmail.com">andrewkaranu03@gmail.com</a></p>
          </div>
        </div>
        
        <div class="contact-item" in:fly={{ y: 20, delay: 200, duration: 400 }}>
          <div class="contact-icon">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path><circle cx="12" cy="10" r="3"></circle></svg>
          </div>
          <div class="contact-text">
            <h3>Location</h3>
            <p>Montreal, Quebec, Canada</p>
          </div>
        </div>
      </div>
      
      <div class="social-section">
        <h3>Connect With Me</h3>
        <div class="social-links">
          <a href="https://github.com/AndrewKaranu" target="_blank" rel="noopener" aria-label="GitHub" in:fly={{ y: 20, delay: 300, duration: 400 }}>
            <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
            <span>GitHub</span>
          </a>
          
          <a href="https://www.linkedin.com/in/andrew-karanu-998910237" target="_blank" rel="noopener" aria-label="LinkedIn" in:fly={{ y: 20, delay: 400, duration: 400 }}>
            <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path><rect x="2" y="9" width="4" height="12"></rect><circle cx="4" cy="4" r="2"></circle></svg>
            <span>LinkedIn</span>
          </a>
        </div>
      </div>
      
      <div class="resume-section" in:fly={{ y: 20, delay: 600, duration: 400 }}>
        <a href="\Andrew_Kamami_Resume.pdf" class="resume-btn" download>
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path><polyline points="7 10 12 15 17 10"></polyline><line x1="12" y1="15" x2="12" y2="3"></line></svg>
          Download Resume
        </a>
      </div>
    </div>
  </div>
</section>

<style>
  .contact-section {
    padding: 7rem 0;
    position: relative;
    overflow: hidden;
  }
  
  /* Decorative background accents */
  .bg-accent {
    position: absolute;
    border-radius: 50%;
    opacity: 0.15;
    filter: blur(60px);
    z-index: -1;
  }
  
  .accent-1 {
    width: 500px;
    height: 500px;
    background: radial-gradient(circle, rgba(184, 115, 51, 0.4) 0%, rgba(184, 115, 51, 0.1) 70%, transparent 100%);
    top: -150px;
    right: -150px;
    animation: float 20s infinite alternate ease-in-out;
  }
  
  .accent-2 {
    width: 400px;
    height: 400px;
    background: radial-gradient(circle, rgba(184, 115, 51, 0.3) 0%, rgba(184, 115, 51, 0.1) 60%, transparent 100%);
    bottom: -100px;
    left: -100px;
    animation: float 15s infinite alternate-reverse ease-in-out;
  }
  
  @keyframes float {
    0% { transform: translate(0, 0); }
    50% { transform: translate(30px, 30px); }
    100% { transform: translate(0, 0); }
  }
  
  .section-header {
    text-align: center;
    margin-bottom: 3.5rem;
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  
  .section-header.visible {
    opacity: 1;
    transform: translateY(0);
  }
  
  .section-header h2 {
    font-size: 2.8rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
    color: #ffffff;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    position: relative;
    display: inline-block;
  }
  
  .section-header h2::before,
  .section-header h2::after {
    content: '';
    position: absolute;
    height: 3px;
    width: 40px;
    background: #B87333;
    top: 50%;
  }
  
  .section-header h2::before {
    right: 100%;
    margin-right: 20px;
  }
  
  .section-header h2::after {
    left: 100%;
    margin-left: 20px;
  }
  
  .section-line {
    height: 4px;
    width: 60px;
    background: #B87333;
    margin: 0 auto;
    border-radius: 2px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  }
  
  .contact-container {
    width: 90%;
    max-width: 800px;
    margin: 0 auto;
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 1s ease, transform 1s ease;
    transition-delay: 0.2s;
  }
  
  .contact-container.visible {
    opacity: 1;
    transform: translateY(0);
  }
  
  .contact-card {
    background: rgba(25, 25, 25, 0.8);
    border-radius: 16px;
    overflow: hidden;
    box-shadow: 0 15px 35px rgba(0, 0, 0, 0.35);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(60, 60, 60, 0.5);
    position: relative;
    padding: 3.5rem;
    color: #e0e0e0;
  }
  
  .contact-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 3px;
    background: linear-gradient(to right, transparent, #B87333, transparent);
  }
  
  .contact-intro {
    font-size: 1.2rem;
    line-height: 1.7;
    margin-bottom: 3rem;
    text-align: center;
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
  }
  
  .contact-info {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2.5rem;
    margin-bottom: 3rem;
  }
  
  .contact-item {
    display: flex;
    align-items: flex-start;
    gap: 1.2rem;
    transition: transform 0.3s ease;
  }
  
  .contact-item:hover {
    transform: translateY(-5px);
  }
  
  .contact-icon {
    background: rgba(40, 40, 40, 0.7);
    width: 50px;
    height: 50px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #B87333;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    border: 1px solid rgba(70, 70, 70, 0.6);
    flex-shrink: 0;
    transition: all 0.3s ease;
  }
  
  .contact-item:hover .contact-icon {
    background: rgba(184, 115, 51, 0.2);
    border-color: rgba(184, 115, 51, 0.4);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.25);
    transform: scale(1.05);
  }
  
  .contact-text h3 {
    color: #B87333;
    font-size: 1.2rem;
    margin-bottom: 0.5rem;
    font-weight: 600;
  }
  
  .contact-text p {
    font-size: 1.05rem;
    line-height: 1.5;
  }
  
  .contact-text a {
    color: #e0e0e0;
    text-decoration: none;
    transition: color 0.3s ease;
    position: relative;
  }
  
  .contact-text a:hover {
    color: #B87333;
  }
  
  .contact-text a::after {
    content: '';
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 100%;
    height: 1px;
    background: rgba(184, 115, 51, 0.5);
    transform: scaleX(0);
    transform-origin: right;
    transition: transform 0.3s ease;
  }
  
  .contact-text a:hover::after {
    transform: scaleX(1);
    transform-origin: left;
  }
  
  .social-section {
    margin-bottom: 3rem;
    text-align: center;
  }
  
  .social-section h3 {
    color: #ffffff;
    font-size: 1.4rem;
    margin-bottom: 1.5rem;
    position: relative;
    display: inline-block;
    padding-bottom: 0.8rem;
  }
  
  .social-section h3::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 80px;
    height: 2px;
    background: rgba(184, 115, 51, 0.6);
    border-radius: 1px;
  }
  
  .social-links {
    display: flex;
    justify-content: center;
    gap: 2rem;
    flex-wrap: wrap;
  }
  
  .social-links a {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.7rem;
    color: #e0e0e0;
    text-decoration: none;
    transition: all 0.3s ease;
    padding: 1rem;
    border-radius: 12px;
    background: rgba(40, 40, 40, 0.5);
    border: 1px solid rgba(70, 70, 70, 0.5);
    min-width: 110px;
  }
  
  .social-links a:hover {
    background: rgba(184, 115, 51, 0.1);
    border-color: rgba(184, 115, 51, 0.3);
    transform: translateY(-5px);
    color: #B87333;
  }
  
  .social-links a svg {
    transition: transform 0.3s ease;
  }
  
  .social-links a:hover svg {
    transform: scale(1.2);
  }
  
  .social-links a span {
    font-size: 0.95rem;
    font-weight: 500;
  }
  
  .resume-section {
    text-align: center;
    margin-top: 2rem;
  }
  
  .resume-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 0.8rem;
    padding: 0.9rem 2rem;
    border-radius: 30px;
    font-size: 1.1rem;
    font-weight: 500;
    text-decoration: none;
    text-align: center;
    transition: all 0.3s ease;
    border: 2px solid transparent;
    background: #B87333;
    color: #fff;
    box-shadow: 0 4px 15px rgba(184, 115, 51, 0.3);
  }
  
  .resume-btn:hover {
    background: #cf8d4b;
    transform: translateY(-3px);
    box-shadow: 0 6px 20px rgba(184, 115, 51, 0.4);
  }
  
  @media (max-width: 992px) {
    .contact-section {
      padding: 5rem 2rem;
    }
    
    .contact-card {
      padding: 2.5rem;
    }
    
    .section-header h2::before,
    .section-header h2::after {
      width: 30px;
    }
    
    .section-header h2::before {
      margin-right: 15px;
    }
    
    .section-header h2::after {
      margin-left: 15px;
    }
  }
  
  @media (max-width: 768px) {
    .contact-section {
      padding: 5rem 1rem;
    }
    
    .section-header h2 {
      font-size: 2.2rem;
    }
    
    .section-header h2::before,
    .section-header h2::after {
      display: none;
    }
    
    .contact-card {
      padding: 2rem;
    }
    
    .contact-intro {
      font-size: 1.1rem;
      margin-bottom: 2rem;
    }
    
    .contact-info {
      grid-template-columns: 1fr;
      gap: 2rem;
    }
    
    .social-links {
      gap: 1rem;
    }
    
    .social-links a {
      padding: 0.8rem;
      min-width: 100px;
    }
  }
</style>