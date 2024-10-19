<template>
  <div id="app">
    <!-- Splash Screen Section -->
    <div class="splash-screen">
      <h1>{{ title }}</h1>
      <p>{{ intro }}</p>
      <div class="btn-container">
        <button class="btn-custom" @click="scrollToSection('about')">About Me</button>
        <button class="btn-custom" @click="scrollToSection('chatbot')">Ask The Ai</button>
        <button class="btn-custom" @click="scrollToSection('portfolio')">Portfolio</button>
        <button class="btn-custom" @click="scrollToSection('skills')">Skills</button>
        <button class="btn-custom" @click="scrollToSection('contact')">Contact</button>
      </div>
    </div>

    <!-- About Me Section -->
    <section id="about">
      <h2>About Me</h2>
      <p>{{ aboutMe }}</p>
    </section>

    <section id="chatbot">
            <h2>Ask the AI</h2>
            <iframe width="350" height="430" allow="microphone;" src="https://console.dialogflow.com/api-client/demo/embedded/410b57e8-df9e-4ccb-a17b-62fc75849001"></iframe>
        </section>

    <!-- Portfolio Section -->
    <section id="portfolio">
      <h2>Portfolio: Work Experience</h2>
      <ul>
        <li v-for="job in jobs" :key="job.company">
          <strong>{{ job.company }}</strong> ({{ job.dates }})<br />
          {{ job.role }} - {{ job.description }}
        </li>
      </ul>
    </section>

    <!-- Skills Section -->
    <section id="skills">
      <h2>Skills</h2>
      <ul>
        <li v-for="skill in skills" :key="skill">{{ skill }}</li>
      </ul>
    </section>

    <!-- Contact Section -->
    <section id="contact">
      <h2>Contact Me</h2>
      <p>Email: <a :href="'mailto:' + email">{{ email }}</a></p>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "Welcome to My Portfolio",
      intro: "Explore my journey as an IT professional. From networking to desktop support to web development, I blend technology with creativity.",
      aboutMe: "Hello! I'm Matthew Martins, a junior at Kean University, studying Information Technology. My education covers programming, database management, networking, and cybersecurity. I'm passionate about solving problems and creating innovative tech solutions. Currently, I am seeking internship opportunities to apply my knowledge in practical settings. Let's connect to discuss potential opportunities or explore the ever-growing world of IT!",
      email: "Matthew.M.Martins@gmail.com",
      jobs: [
        {
          company: "Floor & Decor",
          dates: "Sep 2023 - Present",
          role: "Sales Specialist",
          description: "Responsible for assisting customers in selecting flooring and ensuring a clean work environment.",
        },
        {
          company: "LL Flooring",
          dates: "Sep 2022 - Sep 2023",
          role: "Sales Specialist",
          description: "Handled showroom and warehouse responsibilities, assisted customers with flooring choices, managed inventory, and maintained daily follow-ups with customers.",
        },
      ],
      skills: [
        "Proficient in Java programming",
        "Proficient in Python for data analysis and scripting",
        "Experienced with SQL for database management",
        "Familiar with web development technologies like HTML, CSS, and Vue.js",
      ],
    };
  },
  methods: {
    scrollToSection(sectionId) {
      const section = document.getElementById(sectionId);
      if (section) {
        section.scrollIntoView({ behavior: "smooth" });
      }
    },
  },
};
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  background: #f8f9fa;
  color: #333;
  scroll-behavior: smooth;
}
.splash-screen {
  text-align: center;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
section {
  padding: 60px 20px;
  min-height: 100vh;
}
h1,
h2 {
  text-align: center;
}
p {
  font-size: 1.2em;
  text-align: center;
  margin: 20px auto;
  max-width: 800px;
}
.btn-container {
  display: flex;
  justify-content: center;
  gap: 10px;
}
.btn-custom {
  padding: 10px 20px;
  background-color: #f0f0f0;
  border: none;
  color: #333;
  border-radius: 5px;
  font-size: 1em;
  cursor: pointer;
  transition: background-color 0.3s ease;
}
.btn-custom:hover {
  background-color: #ddd;
}
#skills {
  padding: 20px;
  background-color: #edafaf;
  border-radius: 10px;
  text-align: center;
}
</style>
