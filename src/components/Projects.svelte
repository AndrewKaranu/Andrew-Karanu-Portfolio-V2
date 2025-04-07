<script>
  import { onMount, tick } from 'svelte';
  import { fade, fly, slide } from 'svelte/transition';
  import { crossfade } from 'svelte/transition';
  
  // Create crossfade transition for smooth switching between projects
  const [send, receive] = crossfade({
    duration: 400,
    fallback(node) {
      return { 
        duration: 400,
        css: t => `opacity: ${t}`
      };
    }
  });

  let projects = [
    {
      id: 1,
      title: "Match A Wish",
      description: "Developed a full-stack app to match toy donors with hospitals, using a matching algorithm powered by OpenAI embeddings. Won 1st place for Best Use of Databricks.",
      image: "path/to/match-a-wish.jpg", // Replace with your image path
      video: "",
      techStack: ["React", "Node.js", "Express", "Databricks SQL", "Auth0", "OpenAI Embeddings"],
      githubLink: "https://devpost.com/software/match-a-wish",
      siteLink: "",
      category: "Full-Stack"
    },
    {
      id: 2,
      title: "Melody",
      description: "MERN app offering AI-powered tools for Spotify: playlist generation from prompts, images, and listening history. Used OpenAI + Spotify APIs.",
      image: "path/to/melody.jpg",
      video: "",
      techStack: ["Node.js", "Express", "React", "MongoDB", "Amazon S3", "OpenAI", "Spotify API"],
      githubLink: "https://github.com/AndrewKaranu/MELODY-Playlist-App",
      siteLink: "",
      category: "Web Development"
    },
    {
      id: 3,
      title: "Touch Trust Bank",
      description: "Accessible banking app with facial authentication and voice commands. Built for visually impaired users, featuring a JavaFX interface and RAG system using Gemini.",
      image: "path/to/touch-trust.jpg",
      video: "",
      techStack: ["Java", "JavaFX", "OpenCV", "Google TTS", "CMU Sphinx", "MySQL", "Gemini"],
      githubLink: "https://github.com/AndrewKaranu/Touch-Trust-Bank/tree/main",
      siteLink: "",
      category: "Software"
    },
    {
      id: 4,
      title: "Byte Sized Tech News",
      description: "Automated tech mailing list with React sign-up frontend and Flask backend. Scraped and summarized articles using ML and NLP with Gemini.",
      image: "path/to/byte-sized.jpg",
      video: "",
      techStack: ["React", "Flask", "Python", "Selenium", "AWS SES", "SQL", "NLP", "Machine Learning"],
      githubLink: "https://github.com/AndrewKaranu/Byte-Size-Tech-News",
      siteLink: "",
      category: "Data & ML"
    },
    {
      id: 5,
      title: "Job Salary Predictor",
      description: "Built ML model to predict job salaries using web-scraped data and regression. Used LLaMA 8B model via Ollama to augment missing data.",
      image: "path/to/job-salary.jpg",
      video: "",
      techStack: ["Python", "Pandas", "Web Scraping", "Machine Learning", "AutoML", "Ollama"],
      githubLink: "",
      siteLink: "",
      category: "Data & ML"
    }
  ];

  // Add unique IDs if not already present
  projects = projects.map((p, i) => ({...p, id: p.id || i+1}));
  
  let featuredProjectId = 1; // Start with first project featured
  let hoveredProject = null;
  let isLoaded = false;
  let isChangingFeatured = false;

  // Function to set featured project
  function setFeaturedProject(project) {
    if (isChangingFeatured || project.id === featuredProjectId) return;
    
    isChangingFeatured = true;
    // Short delay for animation
    setTimeout(() => {
      featuredProjectId = project.id;
      isChangingFeatured = false;
    }, 200);
  }
  
  // Computed properties
  $: featuredProject = projects.find(p => p.id === featuredProjectId);
  $: otherProjects = projects.filter(p => p.id !== featuredProjectId);

  onMount(() => {
    setTimeout(() => {
      isLoaded = true;
    }, 300);
  });
</script>

<section id="projects" class:loaded={isLoaded}>
  <div class="section-header">
    <h2 transition:fade={{duration: 400, delay: 100}}>My Projects</h2>
    <div class="section-line" transition:slide={{duration: 600, delay: 200}}></div>
    <p class="section-description" transition:fade={{duration: 400, delay: 300}}>
      Here's a selection of projects I've worked on. Click any project to see more details.
    </p>
  </div>

  <!-- Featured Project -->
  {#if featuredProject}
    <div class="featured-project" 
         class:changing={isChangingFeatured} 
         in:receive={{key: `featured-${featuredProject.id}`}}
         out:send={{key: `featured-${featuredProject.id}`}}>
      <div class="featured-content">
        <div class="featured-text">
          <div class="featured-label">Featured Project</div>
          <h3>{featuredProject.title}</h3>
          <div class="featured-description">
            <p>{featuredProject.description}</p>
          </div>
          <ul class="tech-stack">
            {#each featuredProject.techStack as tech}
              <li>{tech}</li>
            {/each}
          </ul>
          <div class="project-links">
            {#if featuredProject.githubLink}
              <a href={featuredProject.githubLink} target="_blank" class="btn-link">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
                Code
              </a>
            {/if}
            {#if featuredProject.siteLink}
              <a href={featuredProject.siteLink} target="_blank" class="btn-link">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path><polyline points="15 3 21 3 21 9"></polyline><line x1="10" y1="14" x2="21" y2="3"></line></svg>
                Live Demo
              </a>
            {/if}
          </div>
        </div>
        <div class="featured-image">
          <div class="image-container" 
               on:mouseenter={() => hoveredProject = featuredProject} 
               on:mouseleave={() => hoveredProject = null}>
            <img src={featuredProject.image} alt={featuredProject.title} />
            {#if featuredProject.video && hoveredProject === featuredProject}
              <video src={featuredProject.video} autoplay loop muted></video>
            {/if}
          </div>
        </div>
      </div>
    </div>
  {/if}

  <!-- Project Cards -->
  <div class="projects-heading" transition:fade={{duration: 400, delay: 500}}>
    <h3>All Projects</h3>
    <p>Click on any project to feature it</p>
  </div>

  <!-- Project Grid -->
  <div class="projects-grid">
    {#each otherProjects as project, i (project.id)}
      <!-- Using key function to animate project cards while handling crossfade -->
      <div class="project-card" 
           in:receive={{key: `card-${project.id}`}}
           out:send={{key: `card-${project.id}`}}
           on:mouseenter={() => hoveredProject = project} 
           on:mouseleave={() => hoveredProject = null}
           on:click={() => setFeaturedProject(project)}
           on:keydown={e => e.key === 'Enter' && setFeaturedProject(project)}
           tabindex="0"
           role="button"
           aria-label={`Feature ${project.title} project`}>
        <div class="card-image">
          <img src={project.image} alt={project.title} />
          {#if project.video && hoveredProject === project}
            <video src={project.video} autoplay loop muted></video>
          {/if}
          <div class="card-overlay">
            <div class="overlay-content">
              <span>Click to feature</span>
            </div>
          </div>
        </div>
        <div class="card-content">
          <div class="card-header">
            <h4>{project.title}</h4>
            <span class="category-tag">{project.category}</span>
          </div>
          <p>{project.description}</p>
          <div class="card-footer">
            <div class="tech-pills">
              {#each project.techStack.slice(0, 3) as tech}
                <span class="tech-pill">{tech}</span>
              {/each}
              {#if project.techStack.length > 3}
                <span class="tech-pill">+{project.techStack.length - 3}</span>
              {/if}
            </div>
            <div class="card-links">
              {#if project.githubLink}
                <!-- Using on:click|stopPropagation instead of onclick which is not recommended in Svelte -->
                <a href={project.githubLink} target="_blank" class="icon-link" aria-label="GitHub" on:click|stopPropagation>
                  <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
                </a>
              {/if}
              {#if project.siteLink}
                <a href={project.siteLink} target="_blank" class="icon-link" aria-label="Live site" on:click|stopPropagation>
                  <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path><polyline points="15 3 21 3 21 9"></polyline><line x1="10" y1="14" x2="21" y2="3"></line></svg>
                </a>
              {/if}
            </div>
          </div>
        </div>
      </div>
    {/each}
  </div>
</section>

<style>
  section {
    padding: 4rem 0;
    opacity: 0;
    transition: opacity 1s ease;
  }
  
  section.loaded {
    opacity: 1;
  }
  
  .section-header {
    text-align: center;
    margin-bottom: 3rem;
  }
  
  h2 {
    font-size: 2.5rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
    color: #ffffff;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  }
  
  .section-line {
    height: 4px;
    width: 60px;
    background: #B87333;
    margin: 0 auto 1.5rem;
    border-radius: 2px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  }
  
  .section-description {
    max-width: 650px;
    margin: 0 auto;
    color: #e0e0e0;
    font-size: 1.1rem;
    line-height: 1.6;
  }
  
  /* Projects Heading */
  .projects-heading {
    text-align: center;
    margin: 3rem 0 2rem;
  }
  
  .projects-heading h3 {
    font-size: 1.5rem;
    font-weight: 600;
    color: #ffffff;
    margin-bottom: 0.5rem;
  }
  
  .projects-heading p {
    color: #B87333;
    font-size: 0.95rem;
  }
  
  /* Featured Project */
  .featured-project {
    margin-bottom: 3rem;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    background: rgba(30, 30, 30, 0.75);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(60, 60, 60, 0.5);
    transition: opacity 0.3s ease, transform 0.3s ease;
  }
  
  .featured-project.changing {
    opacity: 0.6;
    transform: translateY(10px);
  }
  
  .featured-content {
    display: flex;
    align-items: stretch;
  }
  
  .featured-text {
    flex: 1;
    padding: 2.5rem;
    display: flex;
    flex-direction: column;
  }
  
  .featured-label {
    display: inline-block;
    background: rgba(184, 115, 51, 0.2);
    color: #B87333;
    padding: 0.3rem 0.8rem;
    border-radius: 20px;
    font-size: 0.85rem;
    font-weight: 600;
    margin-bottom: 1rem;
    border: 1px solid rgba(184, 115, 51, 0.3);
  }
  
  .featured-text h3 {
    font-size: 1.8rem;
    font-weight: 700;
    margin-bottom: 1rem;
    color: #ffffff;
  }
  
  .featured-description {
    flex-grow: 1;
  }
  
  .featured-description p {
    font-size: 1rem;
    line-height: 1.6;
    color: #e0e0e0;
  }
  
  .featured-image {
    flex: 1;
    min-height: 400px;
    position: relative;
  }
  
  .image-container {
    position: absolute;
    inset: 0;
    overflow: hidden;
  }
  
  .image-container img, 
  .image-container video {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.5s ease;
  }
  
  .image-container:hover img,
  .image-container:hover video {
    transform: scale(1.05);
  }
  
  .tech-stack {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    list-style: none;
    padding: 0;
    margin: 1.5rem 0;
  }
  
  .tech-stack li {
    background: rgba(40, 40, 40, 0.8);
    padding: 0.3rem 0.7rem;
    border-radius: 5px;
    font-size: 0.85rem;
    font-weight: 500;
    color: #e0e0e0;
    border: 1px solid rgba(60, 60, 60, 0.8);
  }
  
  .project-links {
    display: flex;
    gap: 1rem;
  }
  
  .btn-link {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem 1rem;
    background: rgba(40, 40, 40, 0.8);
    color: #ffffff;
    border-radius: 6px;
    font-weight: 500;
    text-decoration: none;
    transition: all 0.2s ease;
    border: 1px solid rgba(60, 60, 60, 0.8);
  }
  
  .btn-link:hover {
    background: rgba(184, 115, 51, 0.8);
    transform: translateY(-2px);
  }
  
  /* Projects Grid */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 1.5rem;
    transition: opacity 0.3s ease;
  }
  
  .project-card {
    border-radius: 12px;
    overflow: hidden;
    background: rgba(30, 30, 30, 0.75);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    height: 100%;
    display: flex;
    flex-direction: column;
    border: 1px solid rgba(60, 60, 60, 0.5);
    backdrop-filter: blur(5px);
    cursor: pointer;
  }
  
  .project-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
    border-color: rgba(184, 115, 51, 0.3);
  }
  
  .card-image {
    height: 180px;
    position: relative;
    overflow: hidden;
  }
  
  .card-image img,
  .card-image video {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.5s ease;
  }
  
  .project-card:hover .card-image img,
  .project-card:hover .card-image video {
    transform: scale(1.05);
  }
  
  .card-overlay {
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  
  .project-card:hover .card-overlay {
    opacity: 1;
  }
  
  .overlay-content {
    background: rgba(184, 115, 51, 0.8);
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 20px;
    font-size: 0.9rem;
    font-weight: 500;
    transform: translateY(10px);
    transition: transform 0.3s ease;
  }
  
  .project-card:hover .overlay-content {
    transform: translateY(0);
  }
  
  .card-content {
    padding: 1.5rem;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
  }
  
  .card-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 0.8rem;
  }
  
  .card-header h4 {
    font-size: 1.25rem;
    font-weight: 600;
    margin: 0;
    color: #ffffff;
  }
  
  .category-tag {
    font-size: 0.75rem;
    background: rgba(184, 115, 51, 0.2);
    color: #B87333;
    padding: 0.2rem 0.5rem;
    border-radius: 4px;
    font-weight: 500;
    border: 1px solid rgba(184, 115, 51, 0.3);
  }
  
  .card-content p {
    font-size: 0.95rem;
    line-height: 1.5;
    margin-bottom: 1.2rem;
    color: #e0e0e0;
    flex-grow: 1;
  }
  
  .card-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: auto;
  }
  
  .tech-pills {
    display: flex;
    gap: 0.4rem;
    flex-wrap: wrap;
  }
  
  .tech-pill {
    background: rgba(40, 40, 40, 0.8);
    padding: 0.2rem 0.5rem;
    border-radius: 4px;
    font-size: 0.75rem;
    color: #e0e0e0;
    border: 1px solid rgba(60, 60, 60, 0.8);
  }
  
  .card-links {
    display: flex;
    gap: 0.8rem;
  }
  
  .icon-link {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 32px;
    height: 32px;
    border-radius: 50%;
    background: rgba(40, 40, 40, 0.8);
    color: #e0e0e0;
    transition: all 0.2s ease;
    border: 1px solid rgba(60, 60, 60, 0.8);
    z-index: 5;
  }
  
  .icon-link:hover {
    background: rgba(184, 115, 51, 0.8);
    color: white;
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }

  @media (max-width: 992px) {
    .featured-content {
      flex-direction: column-reverse;
    }
    
    .featured-image {
      min-height: 300px;
    }
    
    .projects-grid {
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    }
  }

  @media (max-width: 768px) {
    section {
      padding: 3rem 1rem;
    }
    
    h2 {
      font-size: 2rem;
    }
    
    .featured-text {
      padding: 1.5rem;
    }
    
    .featured-text h3 {
      font-size: 1.5rem;
    }
    
    .projects-grid {
      grid-template-columns: 1fr;
    }
  }
</style>