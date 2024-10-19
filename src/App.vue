<template>
  <div id="app">
    <!-- Splash Screen Section -->
    <div class="splash-screen" id="startscreen">
      <h1>{{ title }}</h1>
      <p>{{ intro }}</p>
      <div class="btn-container">
        <button class="btn-custom" @click="scrollToSection('about')">About Me</button>
        <button class="btn-custom" @click="scrollToSection('portfolio')">Portfolio</button>
        <button class="btn-custom" @click="scrollToSection('skills')">Skills</button>
        <button class="btn-custom" @click="scrollToSection('contact')">Contact</button>
        <button class="btn-custom" @click="scrollToSection('chatbot')">Ask the AI</button>
      </div>
    </div>

    <!-- About Me Section -->
    <section id="about">
      <h2>About Me</h2>
      <p>{{ aboutMe }}</p>
    </section>

    <!-- Portfolio Section -->
    <section id="portfolio">
      <h2>Portfolio: Work Experience</h2>
      <ul>
        <li><strong>Floor & Decor</strong> (Sep 2023 - Present)<br>
          Sales Specialist - Responsible for assisting customers in selecting flooring, managing inventory, and ensuring a clean work environment.
        </li>
        <li><strong>LL Flooring</strong> (Sep 2022 - Sep 2023)<br>
          Sales Specialist - Handled showroom and warehouse responsibilities, assisted customers with flooring choices, managed inventory, and maintained daily follow-ups with customers.
        </li>
      </ul>
    </section>

    <!-- Skills Section -->
    <section id="skills">
      <h2>Skills</h2>
      <ul>
        <li>Proficient in Java programming</li>
        <li>Proficient in Python for data analysis and scripting</li>
        <li>Experienced with SQL for database management</li>
        <li>Familiar with web development technologies like HTML, CSS, and Vue.js</li>
      </ul>
    </section>

    <!-- Contact Section -->
    <section id="contact">
      <h2>Contact Me</h2>
      <p>Email: <a :href="'mailto:' + email">{{ email }}</a></p>
    </section>

    <!-- AI Chatbot Section -->
    <section id="chatbot">
      <h2>Ask the AI</h2>
      <<iframe width="350" height="430" allow="microphone;" src="https://console.dialogflow.com/api-client/demo/embedded/410b57e8-df9e-4ccb-a17b-62fc75849001"></iframe>
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
          description: "Responsible for assisting customers in selecting flooring, managing inventory, and ensuring a clean work environment."
        },
        {
          company: "LL Flooring",
          dates: "Sep 2022 - Sep 2023",
          role: "Sales Specialist",
          description: "Handled showroom and warehouse responsibilities, assisted customers with flooring choices, managed inventory, and maintained daily follow-ups with customers."
        }
      ],
      userInput: "",
      aiResponse: ""
    };
  },
  methods: {
    scrollToSection(sectionId) {
      const section = document.getElementById(sectionId);
      if (section) {
        section.scrollIntoView({ behavior: 'smooth' });
      }
    },
    async getResponse() {
      const apiKey = "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"; // Replace with your OpenAI API key
      const prompt = this.userInput;

      try {
        const response = await fetch("https://api.openai.com/v1/completions", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${apiKey}`
          },
          body: JSON.stringify({
            model: "gpt-4",
            prompt: prompt,
            max_tokens: 100
          })
        });

        const data = await response.json();
        this.aiResponse = data.choices[0].text.trim();
      } catch (error) {
        console.error("Error getting AI response:", error);
        this.aiResponse = "There was an error connecting to the AI.";
      }
    }
  }
};
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  background: linear-gradient(to right, #f8f9fa, #d1e8e2);
  color: #333;
  scroll-behavior: smooth;
}

.splash-screen {
  text-align: center;
  min-height: 100vh;
  padding: 20px;
  background: #6b5b95;
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

section {
  padding: 40px 20px;
  background-color: #f0f0f0;
  border-radius: 10px;
  margin: 20px auto;
  max-width: 800px;
}

h1 {
  font-size: 3em;
  color: #ff6f61;
}

h2 {
  text-align: center;
  color: #88b04b;
}

p {
  font-size: 1.2em;
  text-align: center;
  margin: 20px auto;
  max-width: 100%;
  word-wrap: break-word;
  overflow-wrap: break-word;
}

.btn-container {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.btn-custom {
  padding: 10px 20px;
  background-color: #ff6f61;
  border: none;
  color: #fff;
  border-radius: 5px;
  font-size: 1em;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-custom:hover {
  background-color: #ff847c;
}

#skills {
  padding: 20px;
  background-color: #d1e8e2;
  border-radius: 10px;
  text-align: center;
}

#portfolio ul, #skills ul {
  list-style-type: none;
  padding: 0;
}

#portfolio li, #skills li {
  margin-bottom: 20px;
}

#chatbot {
  padding: 20px;
  background-color: #ffe0b2;
  border-radius: 10px;
  text-align: center;
}

iframe {
  border: 2px solid #88b04b;
  border-radius: 10px;
}
</style>
