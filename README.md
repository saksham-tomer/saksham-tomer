<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Saksham Tomar - Interactive Profile</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/particles.js/2.0.0/particles.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/gsap.min.js"></script>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #0f0c29;
      background: linear-gradient(to right, #24243e, #302b63, #0f0c29);
      color: white;
      overflow-x: hidden;
      line-height: 1.6;
    }
    
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 2rem;
      position: relative;
      z-index: 2;
    }

    #particles-js {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 0;
    }

    .hidden {
      opacity: 0;
      transform: translateY(30px);
      transition: all 1s;
    }

    .show {
      opacity: 1;
      transform: translateY(0);
    }

    header {
      text-align: center;
      padding: 2rem 0;
      margin-bottom: 2rem;
      position: relative;
      background: rgba(15, 12, 41, 0.7);
      border-radius: 10px;
      backdrop-filter: blur(10px);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
      border: 1px solid rgba(255, 255, 255, 0.1);
    }

    h1 {
      font-size: 3rem;
      margin-bottom: 0.5rem;
      background: linear-gradient(to right, #fc466b, #3f5efb);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }

    .intro {
      font-size: 1.2rem;
      max-width: 800px;
      margin: 0 auto;
    }

    .wave {
      display: inline-block;
      animation: wave 1.5s infinite;
    }

    @keyframes wave {
      0% { transform: rotate(0deg); }
      20% { transform: rotate(15deg); }
      40% { transform: rotate(0deg); }
      60% { transform: rotate(15deg); }
      100% { transform: rotate(0deg); }
    }

    .rocket {
      display: inline-block;
      animation: rocket 3s infinite;
    }

    @keyframes rocket {
      0% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
      100% { transform: translateY(0); }
    }

    section {
      background: rgba(15, 12, 41, 0.7);
      border-radius: 10px;
      padding: 2rem;
      margin-bottom: 2rem;
      backdrop-filter: blur(10px);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
      border: 1px solid rgba(255, 255, 255, 0.1);
      transition: transform 0.3s, box-shadow 0.3s;
    }

    section:hover {
      transform: translateY(-5px);
      box-shadow: 0 12px 40px rgba(0, 0, 0, 0.4);
    }

    h2 {
      font-size: 2rem;
      margin-bottom: 1.5rem;
      position: relative;
      display: inline-block;
    }

    h2::after {
      content: '';
      position: absolute;
      left: 0;
      bottom: -5px;
      width: 100%;
      height: 3px;
      background: linear-gradient(to right, #fc466b, #3f5efb);
      transform: scaleX(0);
      transform-origin: left;
      transition: transform 0.5s;
    }

    section:hover h2::after {
      transform: scaleX(1);
    }

    .about-me-list {
      list-style: none;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1rem;
    }

    .about-me-item {
      display: flex;
      align-items: center;
      background: rgba(255, 255, 255, 0.1);
      padding: 0.75rem;
      border-radius: 5px;
      transition: all 0.3s;
    }

    .about-me-item:hover {
      background: rgba(255, 255, 255, 0.2);
      transform: translateX(5px);
    }

    .about-me-item i {
      margin-right: 10px;
      font-size: 1.2rem;
    }

    .skills-container {
      display: flex;
      flex-wrap: wrap;
      gap: 0.75rem;
      margin-top: 1rem;
    }

    .skill-badge {
      background: rgba(0, 0, 0, 0.3);
      border-radius: 5px;
      padding: 0.5rem 1rem;
      display: inline-flex;
      align-items: center;
      gap: 0.5rem;
      font-size: 0.9rem;
      transition: all 0.3s;
      cursor: pointer;
    }

    .skill-badge:hover {
      transform: translateY(-3px);
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
      background: rgba(63, 94, 251, 0.3);
    }

    .projects {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
      gap: 2rem;
    }

    .project-card {
      background: rgba(0, 0, 0, 0.2);
      border-radius: 10px;
      overflow: hidden;
      transition: all 0.3s;
      height: 100%;
      display: flex;
      flex-direction: column;
    }

    .project-card:hover {
      transform: translateY(-10px);
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.4);
    }

    .project-content {
      padding: 1.5rem;
      flex-grow: 1;
    }

    .project-title {
      font-size: 1.5rem;
      margin-bottom: 1rem;
      color: #fc466b;
    }

    .tech-stack {
      display: flex;
      flex-wrap: wrap;
      gap: 0.5rem;
      margin-top: 1rem;
    }

    .tech-tag {
      background: rgba(255, 255, 255, 0.1);
      padding: 0.25rem 0.5rem;
      border-radius: 3px;
      font-size: 0.8rem;
    }

    .stats-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
    }

    .stat-card {
      background: rgba(0, 0, 0, 0.2);
      border-radius: 10px;
      padding: 1.5rem;
      text-align: center;
      transition: all 0.3s;
    }

    .stat-card:hover {
      background: rgba(0, 0, 0, 0.3);
      transform: scale(1.03);
    }

    .tech-categories {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1.5rem;
    }

    .tech-category {
      background: rgba(0, 0, 0, 0.2);
      border-radius: 10px;
      padding: 1.5rem;
    }

    .tech-category h3 {
      margin-bottom: 1rem;
      color: #3f5efb;
    }

    .tech-list {
      list-style: none;
    }

    .tech-list li {
      margin-bottom: 0.5rem;
      display: flex;
      align-items: center;
    }

    .tech-list li::before {
      content: '▹';
      color: #fc466b;
      margin-right: 0.5rem;
    }

    .achievements {
      list-style: none;
    }

    .achievement-item {
      background: rgba(0, 0, 0, 0.2);
      margin-bottom: 1rem;
      padding: 1rem;
      border-radius: 5px;
      border-left: 4px solid #3f5efb;
      transition: all 0.3s;
    }

    .achievement-item:hover {
      background: rgba(0, 0, 0, 0.3);
      transform: translateX(5px);
    }

    footer {
      text-align: center;
      padding: 2rem;
      margin-top: 3rem;
      background: rgba(15, 12, 41, 0.7);
      border-radius: 10px;
      backdrop-filter: blur(10px);
    }

    .social-links {
      display: flex;
      justify-content: center;
      gap: 1.5rem;
      margin-top: 1rem;
    }

    .social-link {
      font-size: 1.5rem;
      color: white;
      opacity: 0.7;
      transition: all 0.3s;
    }

    .social-link:hover {
      opacity: 1;
      transform: translateY(-3px);
    }

    #canvas-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
    }

    @media (max-width: 768px) {
      .projects {
        grid-template-columns: 1fr;
      }
      
      .tech-categories {
        grid-template-columns: 1fr;
      }
      
      .stats-container {
        grid-template-columns: 1fr;
      }
      
      .about-me-list {
        grid-template-columns: 1fr;
      }
    }

    /* Glowing effect for special elements */
    .glow {
      text-shadow: 0 0 10px rgba(63, 94, 251, 0.7);
    }

    /* Floating animation */
    .float {
      animation: float 6s ease-in-out infinite;
    }

    @keyframes float {
      0% { transform: translateY(0px); }
      50% { transform: translateY(-20px); }
      100% { transform: translateY(0px); }
    }

    /* Rotating animation */
    .rotate {
      animation: rotate 10s linear infinite;
    }

    @keyframes rotate {
      from { transform: rotate(0deg); }
      to { transform: rotate(360deg); }
    }

    /* Typing effect */
    .typing-text {
      white-space: nowrap;
      overflow: hidden;
      border-right: 3px solid #fc466b;
      animation: typing 3.5s steps(40, end), blink 0.75s step-end infinite;
    }

    @keyframes typing {
      from { width: 0; }
      to { width: 100%; }
    }

    @keyframes blink {
      from, to { border-color: transparent; }
      50% { border-color: #fc466b; }
    }
  </style>
</head>
<body>
  <div id="particles-js"></div>
  <div id="canvas-container"></div>
  
  <div class="container">
    <header class="hidden">
      <h1><span class="wave">👋</span> Hello, I'm Saksham Tomar</h1>
      <p class="intro"><span class="rocket">🚀</span> A Full Stack Developer with over 3 years of experience, specializing in modern web and blockchain technologies. Passionate about creating efficient, scalable, and maintainable solutions that solve real-world problems.</p>
    </header>

    <section id="about" class="hidden">
      <h2>💼 About Me</h2>
      <ul class="about-me-list">
        <li class="about-me-item">
          <i>📧</i> 
          <a href="mailto:sakshamtomerdevs@gmail.com" style="color: white; text-decoration: none;">sakshamtomerdevs@gmail.com</a>
        </li>
        <li class="about-me-item">
          <i>🔗</i> 
          <a href="https://www.linkedin.com/in/saksham-tomar-8090b22b7/" style="color: white; text-decoration: none;">LinkedIn: Saksham Tomar</a>
        </li>
        <li class="about-me-item">
          <i>🌐</i> 
          <a href="https://port-one-brown.vercel.app/" style="color: white; text-decoration: none;">Saksham's Portfolio</a>
        </li>
        <li class="about-me-item">
          <i>🏢</i> 
          <a href="https://greymatterfi.tech" style="color: white; text-decoration: none;">GreyMatterFi</a>
        </li>
      </ul>
    </section>

    <section id="skills" class="hidden">
      <h2>🔧 Core Skills</h2>
      <div class="skills-container">
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="JavaScript" />
          JavaScript
        </div>
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="TypeScript" />
          TypeScript
        </div>
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="React" />
          React
        </div>
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="Next.js" />
          Next.js
        </div>
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="Node.js" />
          Node.js
        </div>
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="Solidity" />
          Solidity
        </div>
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="Rust" />
          Rust
        </div>
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="Kubernetes" />
          Kubernetes
        </div>
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="AWS" />
          AWS
        </div>
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="GraphQL" />
          GraphQL
        </div>
        <div class="skill-badge">
          <img src="/api/placeholder/24/24" alt="Docker" />
          Docker
        </div>
      </div>
    </section>

    <section id="stats" class="hidden">
      <h2>📈 GitHub Stats</h2>
      <div class="stats-container">
        <div class="stat-card float">
          <h3>GitHub Activity</h3>
          <div class="github-stats">
            <img src="/api/placeholder/400/200" alt="GitHub Stats" />
          </div>
        </div>
        <div class="stat-card float" style="animation-delay: 1s;">
          <h3>Top Languages</h3>
          <div class="github-stats">
            <img src="/api/placeholder/400/200" alt="Top Languages" />
          </div>
        </div>
      </div>
    </section>

    <section id="projects" class="hidden">
      <h2>🌟 Projects</h2>
      <div class="projects">
        <div class="project-card">
          <div class="project-content">
            <h3 class="project-title">GreyMatter - Cross-Chain Aggregator Platform</h3>
            <p>A cross-chain aggregator platform using Wormhole for token bridging and DeFi protocol integration. GreyMatter retrieves yield farming data from DeFiLlama and other sources, providing an AI chatbot interface for an enhanced user experience.</p>
            <div class="tech-stack">
              <span class="tech-tag">Web3.js</span>
              <span class="tech-tag">React</span>
              <span class="tech-tag">Node.js</span>
              <span class="tech-tag">Solidity</span>
            </div>
          </div>
        </div>
        
        <div class="project-card">
          <div class="project-content">
            <h3 class="project-title">Multi-Threaded Proxy Server in C</h3>
            <p>Developed a highly efficient, multi-threaded proxy server with an LRU caching mechanism, utilizing pthreads for handling concurrent requests. Achieved a 40% improvement in response times and 30% reduction in data inconsistencies with mutexes and semaphores.</p>
            <div class="tech-stack">
              <span class="tech-tag">C</span>
              <span class="tech-tag">pthreads</span>
              <span class="tech-tag">Systems Programming</span>
            </div>
          </div>
        </div>
        
        <div class="project-card">
          <div class="project-content">
            <h3 class="project-title">E-Health SaaS Platform</h3>
            <p>An e-health app developed for SRMS Hospital, built with Next.js and WebRTC for online consultations. Deployed with Docker and Kubernetes for scalability, using Redis for message queuing and Kafka for real-time notifications.</p>
            <div class="tech-stack">
              <span class="tech-tag">Next.js</span>
              <span class="tech-tag">WebRTC</span>
              <span class="tech-tag">Docker</span>
              <span class="tech-tag">Kubernetes</span>
              <span class="tech-tag">Redis</span>
              <span class="tech-tag">Kafka</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="technologies" class="hidden">
      <h2>🛠️ Technologies I Use</h2>
      <div class="tech-categories">
        <div class="tech-category">
          <h3>Frontend</h3>
          <ul class="tech-list">
            <li>React</li>
            <li>Next.js</li>
            <li>JavaScript</li>
            <li>TypeScript</li>
            <li>Three.js</li>
          </ul>
        </div>
        
        <div class="tech-category">
          <h3>Backend</h3>
          <ul class="tech-list">
            <li>Node.js</li>
            <li>Go</li>
            <li>Python</li>
            <li>GraphQL</li>
            <li>Redis</li>
            <li>RabbitMQ</li>
            <li>Kafka</li>
          </ul>
        </div>
        
        <div class="tech-category">
          <h3>Blockchain</h3>
          <ul class="tech-list">
            <li>Solidity</li>
            <li>Rust</li>
            <li>Anchor (Solana)</li>
            <li>Web3.js</li>
          </ul>
        </div>
        
        <div class="tech-category">
          <h3>DevOps</h3>
          <ul class="tech-list">
            <li>Docker</li>
            <li>Kubernetes</li>
            <li>CI/CD (GitHub Actions, Jenkins)</li>
            <li>AWS</li>
            <li>Terraform</li>
          </ul>
        </div>
        
        <div class="tech-category">
          <h3>Databases</h3>
          <ul class="tech-list">
            <li>MongoDB</li>
            <li>PostgreSQL (Prisma ORM)</li>
          </ul>
        </div>
      </div>
    </section>

    <section id="achievements" class="hidden">
      <h2>🏆 Achievements</h2>
      <ul class="achievements">
        <li class="achievement-item">Hackathon Winner 🏅</li>
        <li class="achievement-item">Boosted API response times by 40% and reduced infrastructure costs by 20% through optimized microservices and CI/CD pipeline setup.</li>
      </ul>
    </section>

    <footer class="hidden">
      <p class="typing-text">Let's connect and build something amazing together!</p>
      <div class="social-links">
        <a href="mailto:sakshamtomerdevs@gmail.com" class="social-link">📧</a>
        <a href="https://www.linkedin.com/in/saksham-tomar-8090b22b7/" class="social-link">🔗</a>
        <a href="https://github.com/saksham-tomer" class="social-link">🐙</a>
      </div>
    </footer>
  </div>

  <script>
    // Particles.js configuration
    particlesJS('particles-js', {
      "particles": {
        "number": {
          "value": 80,
          "density": {
            "enable": true,
            "value_area": 800
          }
        },
        "color": {
          "value": "#ffffff"
        },
        "shape": {
          "type": "circle",
          "stroke": {
            "width": 0,
            "color": "#000000"
          },
          "polygon": {
            "nb_sides": 5
          }
        },
        "opacity": {
          "value": 0.5,
          "random": false,
          "anim": {
            "enable": false,
            "speed": 1,
            "opacity_min": 0.1,
            "sync": false
          }
        },
        "size": {
          "value": 3,
          "random": true,
          "anim": {
            "enable": false,
            "speed": 40,
            "size_min": 0.1,
            "sync": false
          }
        },
        "line_linked": {
          "enable": true,
          "distance": 150,
          "color": "#ffffff",
          "opacity": 0.4,
          "width": 1
        },
        "move": {
          "enable": true,
          "speed": 2,
          "direction": "none",
          "random": false,
          "straight": false,
          "out_mode": "out",
          "bounce": false,
          "attract": {
            "enable": false,
            "rotateX": 600,
            "rotateY": 1200
          }
        }
      },
      "interactivity": {
        "detect_on": "canvas",
        "events": {
          "onhover": {
            "enable": true,
            "mode": "grab"
          },
          "onclick": {
            "enable": true,
            "mode": "push"
          },
          "resize": true
        },
        "modes": {
          "grab": {
            "distance": 140,
            "line_linked": {
              "opacity": 1
            }
          },
          "bubble": {
            "distance": 400,
            "size": 40,
            "duration": 2,
            "opacity": 8,
            "speed": 3
          },
          "repulse": {
            "distance": 200,
            "duration": 0.4
          },
          "push": {
            "particles_nb": 4
          },
          "remove": {
            "particles_nb": 2
          }
        }
      },
      "retina_detect": true
    });

    // Three.js background effect
    const container = document.getElementById('canvas-container');
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer({ alpha: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    container.appendChild(renderer.domElement);

    // Create floating 3D objects
    const geometry = new THREE.TorusKnotGeometry(10, 3, 100, 16);
    const material = new THREE.MeshBasicMaterial({ 
      color: 0x3f5efb, 
      wireframe: true,
      transparent: true,
      opacity: 0.3
    });
    const torusKnot = new THREE.Mesh(geometry, material);
    scene.add(torusKnot);

    // Add additional objects
    const geometry2 = new THREE.IcosahedronGeometry(15, 0);
    const material2 = new THREE.MeshBasicMaterial({ 
      color: 0xfc466b, 
      wireframe: true,
      transparent: true,
      opacity: 0.2
    });
    const icosahedron = new THREE.Mesh(geometry2, material2);
    icosahedron.position.set(-30, 0, -50);
    scene.add(icosahedron);

    camera.position.z = 50;

    // Animation loop
    function animate() {
      requestAnimationFrame(animate);
      
      torusKnot.rotation.x += 0.003;
      torusKnot.rotation.y += 0.005;
      
      icosahedron.rotation.x += 0.005;
      icosahedron.rotation.y += 0.003;
      
      renderer.render(scene, camera);
    }
    animate();

    // Resize event handler
    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    // Scroll animation
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('show');
        }
      });
    }, { threshold: 0.2 });

    document.querySelectorAll('.hidden').forEach(el => observer.observe(el));

    // Add hover effects for skill badges
    document.querySelectorAll('.skill-badge').forEach(badge => {
      badge.addEventListener('mouseover', () => {
        gsap.to(badge, { 
          y: -10, 
          backgroundColor: 'rgba(63, 94, 251, 0.5)', 
          boxShadow: '0 10px 20px rgba(0,0,0,0.4)',
          duration: 0.3 
        });
      });
      
      badge.addEventListener('mouseout', () => {
        gsap.to(badge, { 
          y: 0, 
          backgroundColor: 'rgba(0, 0, 0, 0.3)', 
          boxShadow: 'none',
          duration: 0.3 
        });
      });
    });

    // Project cards hover animation
    document.querySelectorAll('.project-card').forEach(card => {
      card.addEventListener('mouseover', () => {
        gsap.to(card, { 
          y: -15, 
          boxShadow: '0 20px 40px rgba(0,0,0,0.5)',
          duration: 0.4 
        });
      });
      
      card.addEventListener('mouseout', () => {
        gsap.to(card, { 
          y: 0, 
          boxShadow: '0 8px 30px rgba(0,0,0,0.3)',
          duration: 0.4 
        });
      });
    });

    // Header text animation
    const headerText = document.querySelector('header h1');
    gsap.fromTo(headerText, 
      { y: -100, opacity: 0 }, 
      { y: 0, opacity: 1, duration: 1.5, delay: 0.5, ease: "elastic.out(1, 0.5)" }
    );

    // Intro text animation
    const introText = document.querySelector('.intro');
    gsap.fromTo(introText, 
      { y: 50, opacity: 0 }, 
      { y: 0, opacity: 1, duration: 1, delay: 1.2, ease: "back.out(1.7)" }
    );
  </script>
</body>
</html>
