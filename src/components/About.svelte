<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  
  let activeTab = 'skills';
  let isVisible = false;

  function openTab(tabName) {
    activeTab = tabName;
  }

  const skills = [
    { title: "Full-Stack Development", description: "Building scalable web and desktop applications using modern tech stacks." },
    { title: "Data Integration & Analysis", description: "Transforming and analyzing data to build smart, efficient ML systems." },
    { title: "AI & Machine Learning", description: "Developing models and systems with OpenAI, AutoML, NLP, and embeddings." }
  ];

  // Updated techStack array with SimpleIcons CDN URLs
  const techStack = [
    { 
      name: "Python", 
      icon: "https://cdn.simpleicons.org/python/3776AB" 
    },
    { 
      name: "JavaScript", 
      icon: "https://cdn.simpleicons.org/javascript/F7DF1E" 
    },
    { 
      name: "React", 
      icon: "https://cdn.simpleicons.org/react/61DAFB" 
    },
    { 
      name: "Node.js", 
      icon: "https://cdn.simpleicons.org/nodedotjs/339933" 
    },
    { 
      name: "MongoDB", 
      icon: "https://cdn.simpleicons.org/mongodb/47A248" 
    },
    { 
      name: "Flask", 
      icon: "https://cdn.simpleicons.org/flask/000000" 
    },
    { 
      name: "Java", 
      icon: "https://cdn.simpleicons.org/java/007396" 
    },
    { 
      name: "MySQL", 
      icon: "https://cdn.simpleicons.org/mysql/4479A1" 
    },
    { 
      name: "OpenCV", 
      icon: "https://cdn.simpleicons.org/opencv/5C3EE8" 
    },
    { 
      name: "Adobe Photoshop", 
      icon: "https://cdn.simpleicons.org/adobephotoshop/31A8FF" 
    },
    { 
      name: "Adobe Illustrator", 
      icon: "https://cdn.simpleicons.org/adobeillustrator/FF9A00" 
    },
    { 
      name: "TypeScript", 
      icon: "https://cdn.simpleicons.org/typescript/3178C6" 
    },
    { 
      name: "Svelte", 
      icon: "https://cdn.simpleicons.org/svelte/FF3E00" 
    },
    { 
      name: "Git", 
      icon: "https://cdn.simpleicons.org/git/F05032" 
    }
  ];

  const education = [
    {
      school: "Concordia University, Montreal",
      degree: "Bachelor of Computer Science – Co-op Program (Expected May 2027)"
    },
    {
      school: "Relevant Courses",
      course: "Data Structures & Algorithms, Data Analytics, Operating Systems, Advanced Program Design with C++"
    },
    {
      school: "Institute for Co-operative Education",
      course: "Member of Concordia's Co-op Program"
    }
  ];
  
  // Optional: Handle icon loading errors
  function handleIconError(event) {
    // Provide a fallback icon if loading fails
    event.target.src = "https://cdn.simpleicons.org/dev-dot-to/0A0A0A";
  }
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      if (entries[0].isIntersecting) {
        isVisible = true;
      }
    }, { threshold: 0.1 });
    
    const section = document.getElementById('about');
    if (section) observer.observe(section);
    
    return () => {
      if (section) observer.unobserve(section);
    };
  });
</script>

<section id="about" class="about-section">
  <!-- Decorative background elements -->
  <div class="bg-accent accent-1"></div>
  <div class="bg-accent accent-2"></div>
  
  <div class="section-header" class:visible={isVisible}>
    <h2>About Me</h2>
    <div class="section-line"></div>
  </div>

  <div class="about-container" class:visible={isVisible}>
    <div class="about-card">
      <div class="about-content">
        <p class="intro-text">
          I'm <span class="highlight">Andrew Kamami</span>, a Computer Science student at Concordia University and a passionate full-stack developer. I love building projects that blend powerful backends with engaging, accessible user interfaces. From hackathon-winning platforms to machine learning-driven automation tools, I thrive at the intersection of software development and real-world impact.
        </p>
        
        <div class="tabs-container">
          <div class="tab-nav">
            {#each ['skills', 'tech-stack', 'education'] as tab}
              <button 
                class="tab-btn" 
                class:active={activeTab === tab} 
                on:click={() => openTab(tab)}
                on:keydown={e => e.key === 'Enter' && openTab(tab)}
              >
                {tab.charAt(0).toUpperCase() + tab.slice(1).replace('-', ' ')}
              </button>
            {/each}
          </div>
          
          <div class="tab-content">
            {#if activeTab === 'skills'}
              <div class="tab-panel" transition:fade={{ duration: 300 }}>
                <div class="skills-grid">
                  {#each skills as skill, i}
                    <div class="skill-card" in:fly={{ y: 20, delay: i * 100, duration: 400 }}>
                      <h3>{skill.title}</h3>
                      <p>{skill.description}</p>
                    </div>
                  {/each}
                </div>
              </div>
            {:else if activeTab === 'tech-stack'}
              <div class="tab-panel" transition:fade={{ duration: 300 }}>
                <div class="tech-grid">
                  {#each techStack as tech, i}
                    <div class="tech-item" in:fly={{ y: 15, delay: i * 50, duration: 300 }}>
                      <div class="tech-icon">
                        <img 
                          src={tech.icon} 
                          alt={tech.name} 
                          on:error={handleIconError}
                        />
                      </div>
                      <span>{tech.name}</span>
                    </div>
                  {/each}
                </div>
              </div>
            {:else if activeTab === 'education'}
              <div class="tab-panel" transition:fade={{ duration: 300 }}>
                <div class="education-timeline">
                  {#each education as edu, i}
                    <div class="education-item" in:fly={{ x: -20, delay: i * 150, duration: 400 }}>
                      <div class="timeline-dot"></div>
                      <div class="education-content">
                        <h3>{edu.school}</h3>
                        <p>{edu.degree || edu.course}</p>
                      </div>
                    </div>
                  {/each}
                </div>
              </div>
            {/if}
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<style>

.tech-icon {
    width: 60px;
    height: 60px;
    background: rgba(40, 40, 40, 0.8);
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0.8rem;
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
    border: 1px solid rgba(70, 70, 70, 0.6);
    transition: all 0.3s ease;
  }

  .tech-icon img {
    width: 100%;
    height: 100%;
    object-fit: contain;
    filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.2));
  }

  .about-section {
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
  
  .about-container {
    width: 90%;
    max-width: 1000px;
    margin: 0 auto;
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 1s ease, transform 1s ease;
    transition-delay: 0.2s;
  }
  
  .about-container.visible {
    opacity: 1;
    transform: translateY(0);
  }
  
  .about-card {
    background: rgba(25, 25, 25, 0.8);
    border-radius: 16px;
    overflow: hidden;
    box-shadow: 0 15px 35px rgba(0, 0, 0, 0.35);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(60, 60, 60, 0.5);
    position: relative;
  }
  
  .about-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 3px;
    background: linear-gradient(to right, transparent, #B87333, transparent);
  }
  
  .about-content {
    padding: 3.5rem;
    color: #e0e0e0;
  }
  
  .intro-text {
    font-size: 1.2rem;
    line-height: 1.7;
    margin-bottom: 3rem;
    max-width: 800px;
    margin-left: auto;
    margin-right: auto;
  }
  
  .highlight {
    color: #B87333;
    font-weight: 600;
    position: relative;
  }
  
  .highlight::after {
    content: '';
    position: absolute;
    left: 0;
    bottom: -2px;
    width: 100%;
    height: 2px;
    background: rgba(184, 115, 51, 0.4);
  }
  
  .tabs-container {
    border-radius: 12px;
    overflow: hidden;
    background: rgba(30, 30, 30, 0.5);
    border: 1px solid rgba(60, 60, 60, 0.6);
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
  }
  
  .tab-nav {
    display: flex;
    background: rgba(20, 20, 20, 0.7);
    border-bottom: 1px solid rgba(60, 60, 60, 0.6);
  }
  
  .tab-btn {
    padding: 1.2rem 1.5rem;
    background: transparent;
    border: none;
    color: #e0e0e0;
    font-size: 1rem;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.3s ease;
    flex: 1;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  
  .tab-btn::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(to bottom, rgba(255, 255, 255, 0.05), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }
  
  .tab-btn:hover::before {
    opacity: 1;
  }
  
  .tab-btn:after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    width: 0;
    height: 3px;
    background: #B87333;
    transition: all 0.3s ease;
    transform: translateX(-50%);
  }
  
  .tab-btn:hover {
    color: #ffffff;
  }
  
  .tab-btn.active {
    color: #B87333;
    background: rgba(184, 115, 51, 0.1);
  }
  
  .tab-btn.active:after {
    width: 80%;
  }
  
  .tab-content {
    padding: 2.5rem;
    min-height: 300px;
  }
  
  .tab-panel {
    height: 100%;
  }
  
  /* Skills Tab */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 2rem;
  }
  
  .skill-card {
    background: rgba(40, 40, 40, 0.7);
    padding: 1.8rem;
    border-radius: 12px;
    border: 1px solid rgba(70, 70, 70, 0.6);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.15);
    transition: all 0.3s ease;
  }
  
  .skill-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.2);
    border-color: rgba(184, 115, 51, 0.4);
    background: linear-gradient(145deg, rgba(50, 50, 50, 0.7), rgba(40, 40, 40, 0.7));
  }
  
  .skill-card h3 {
    font-size: 1.25rem;
    margin-bottom: 1rem;
    color: #B87333;
    position: relative;
    display: inline-block;
    padding-bottom: 0.5rem;
  }
  
  .skill-card h3::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 40px;
    height: 2px;
    background: rgba(184, 115, 51, 0.6);
  }
  
  .skill-card p {
    font-size: 1rem;
    line-height: 1.6;
    color: #e0e0e0;
  }
  
  /* Tech Stack Tab */
  .tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
    gap: 1.8rem;
    justify-items: center;
  }
  
  .tech-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.8rem;
    transition: all 0.3s ease;
    width: 100%;
  }
  
  .tech-item:hover {
    transform: translateY(-5px);
  }
  
  .tech-icon {
    width: 60px;
    height: 60px;
    background: rgba(40, 40, 40, 0.8);
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0.8rem;
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
    border: 1px solid rgba(70, 70, 70, 0.6);
    transition: all 0.3s ease;
  }
  
  .tech-item:hover .tech-icon {
    background: rgba(184, 115, 51, 0.2);
    border-color: rgba(184, 115, 51, 0.4);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.25);
  }
  
  .tech-icon img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
  
  .tech-item span {
    font-size: 0.9rem;
    text-align: center;
    font-weight: 500;
  }
  
  /* Education Tab */
  .education-timeline {
    position: relative;
    padding-left: 2rem;
    max-width: 800px;
    margin: 0 auto;
  }
  
  .education-timeline:before {
    content: '';
    position: absolute;
    top: 10px;
    bottom: 10px;
    left: 8px;
    width: 2px;
    background: linear-gradient(to bottom, rgba(184, 115, 51, 0.8), rgba(184, 115, 51, 0.2));
    border-radius: 1px;
  }
  
  .education-item {
    position: relative;
    padding-bottom: 2.5rem;
  }
  
  .education-item:last-child {
    padding-bottom: 0;
  }
  
  .timeline-dot {
    position: absolute;
    left: -2rem;
    top: 0;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    background: #B87333;
    box-shadow: 0 0 0 4px rgba(184, 115, 51, 0.2);
    transform: translateX(0);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .education-item:hover .timeline-dot {
    transform: scale(1.2);
    box-shadow: 0 0 0 6px rgba(184, 115, 51, 0.3);
  }
  
  .education-content {
    background: rgba(40, 40, 40, 0.7);
    padding: 1.8rem;
    border-radius: 12px;
    border-left: 3px solid #B87333;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
    transition: all 0.3s ease;
  }
  
  .education-item:hover .education-content {
    transform: translateX(5px);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.25);
    background: linear-gradient(145deg, rgba(50, 50, 50, 0.7), rgba(40, 40, 40, 0.7));
  }
  
  .education-content h3 {
    font-size: 1.2rem;
    color: #B87333;
    margin-bottom: 0.8rem;
    font-weight: 600;
  }
  
  .education-content p {
    font-size: 1rem;
    line-height: 1.6;
    color: #e0e0e0;
  }
  
  @media (max-width: 992px) {
    .about-content {
      padding: 2.5rem;
    }
    
    .tab-content {
      padding: 2rem;
    }
    
    .skills-grid {
      grid-template-columns: 1fr;
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
    .about-section {
      padding: 5rem 1rem;
    }
    
    .section-header h2 {
      font-size: 2.2rem;
    }
    
    .section-header h2::before,
    .section-header h2::after {
      display: none;
    }
    
    .about-content {
      padding: 2rem 1.5rem;
    }
    
    .intro-text {
      font-size: 1.1rem;
      margin-bottom: 2rem;
    }
    
    .tab-nav {
      flex-direction: column;
    }
    
    .tab-btn {
      padding: 0.8rem;
    }
    
    .tab-btn.active:after {
      width: 40%;
    }
    
    .tab-content {
      padding: 1.5rem 1rem;
    }
    
    .tech-grid {
      grid-template-columns: repeat(2, 1fr);
      gap: 1.2rem;
    }
    
    .education-content {
      padding: 1.2rem;
    }
    
    .skill-card {
      padding: 1.5rem;
    }
  }
</style>