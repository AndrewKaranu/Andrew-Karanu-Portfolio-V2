<script>
    let name = '';
    let email = '';
    let message = '';
  
    function handleSubmit() {
      // Add your form submission logic here
      console.log('Form submitted:', { name, email, message });
      // Reset form fields
      name = email = message = '';
    }
  </script>
  
  <section id="contact">
    <div class="container">
      <h2 class="subtitle">Contact Me</h2>
      <div class="row">
        <div class="contact-left">
          <p><i class="fas fa-paper-plane"></i> email@example.com</p>
          <p><i class="fas fa-phone-square-alt"></i> 1234567890</p>
          <div class="social-icons">
            <a href="#"><i class="fab fa-facebook"></i></a>
            <a href="#"><i class="fab fa-twitter-square"></i></a>
            <a href="#"><i class="fab fa-instagram"></i></a>
            <a href="#"><i class="fab fa-linkedin"></i></a>
          </div>
          <a href="path/to/your-cv.pdf" download class="btn btn1">Download CV</a>
        </div>
        <div class="contact-right">
          <form on:submit|preventDefault={handleSubmit}>
            <input type="text" bind:value={name} placeholder="Your Name" required>
            <input type="email" bind:value={email} placeholder="Your Email" required>
            <textarea bind:value={message} rows="6" placeholder="Your Message"></textarea>
            <button type="submit" class="btn btn2">Submit</button>
          </form>
        </div>
      </div>
    </div>
  </section>
  
  <style>
    /* Add your existing CSS here */
  </style>