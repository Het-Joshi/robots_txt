---
layout: default
---

<div id="terminal">
  <div id="terminal-header">
    <div class="button red"></div>
    <div class="button yellow"></div>
    <div class="button green"></div>
  </div>
  <div id="terminal-body">
    <div id="terminal-content"></div>
    <div id="terminal-prompt">
      <span class="prompt-user">guest@robots.txt:</span><span class="prompt-symbol">~$</span>
      <input type="text" id="terminal-input" autofocus>
    </div>
  </div>
</div>

<script>
// JavaScript for the interactive terminal
const terminalContent = document.getElementById('terminal-content');
const terminalInput = document.getElementById('terminal-input');

const commands = {
  'about': `
    <h2>$ cat about.txt</h2>
    <p>Namaste, welcome to my blog <strong>robots.txt</strong>! I started this blog in an effort to document my cybersecurity projects and all the things I learn in this field. Whether you're a newbie just dipping your toes into the vast ocean of cybersecurity or a seasoned pro looking to sharpen your skills, this blog is for you. My goal is to share knowledge, tips, and tricks that will be useful to everyone, from beginners to experts. So, grab a cup of coffee (or tea, if that's your thing), get comfy, and let's explore the fascinating world of cybersecurity together.</p>
    <p><strong>Happy hacking!</strong></p>
  `,
  'posts': `
    <h2>$ cat latest-posts.txt</h2>
    <ul>
      {% for post in site.categories.posts limit:4 %}
        <li>
          <h3>{{ post.title }}</h3>
          <p>{{ post.description }}</p>
          <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.description }}">Read more</a>
        </li>
      {% endfor %}
    </ul>
    <a href="{{ site.baseurl }}/library">View All Posts</a>
  `,
  'contact': `
      <h2>$ cat contact.txt</h2>
      <p>If you have any questions, suggestions, or just want to say hello, feel free to reach out to me! I'm always excited to connect with fellow cybersecurity enthusiasts, share knowledge, and collaborate on projects. You can contact me via the following channels:</p>
      <ul>
          <li><strong>Email:</strong> <a href="mailto:het.matrix@gmail.com">het.matrix@gmail.com</a></li>
          <li><strong>GitHub:</strong> <a href="https://github.com/het-joshi" target="_blank">github.com/het-joshi</a></li>
          <li><strong>LinkedIn:</strong> <a href="https://www.linkedin.com/in/hetjoshi/" target="_blank">Het-Joshi</a></li>
      </ul>
  `,
    'help': `
    <h2>$ help</h2>
    <p>Available commands:</p>
    <ul>
      <li><strong>about</strong> - learn more about this blog</li>
      <li><strong>posts</strong> - view the latest posts</li>
      <li><strong>contact</strong> - get in touch with me</li>
      <li><strong>clear</strong> - clear the terminal</li>
    </ul>
  `,
    'clear': ''
};

terminalInput.addEventListener('keydown', function(event) {
  if (event.key === 'Enter') {
    const command = terminalInput.value.trim().toLowerCase();
    const output = commands[command];

    if (command === 'clear') {
        terminalContent.innerHTML = '';
    } else if (output) {
      terminalContent.innerHTML += \`<div class="terminal-line"><span class="prompt-user">guest@robots.txt:</span><span class="prompt-symbol">~$</span> ${command}</div>\`;
      terminalContent.innerHTML += \`<div class="terminal-line">${output}</div>\`;
    } else {
      terminalContent.innerHTML += \`<div class="terminal-line"><span class="prompt-user">guest@robots.txt:</span><span class="prompt-symbol">~$</span> ${command}</div>\`;
      terminalContent.innerHTML += \`<div class="terminal-line">Command not found: ${command}. Type 'help' for a list of commands.</div>\`;
    }

    terminalInput.value = '';
    terminalContent.scrollTop = terminalContent.scrollHeight;
  }
});

// Initial greeting
terminalContent.innerHTML += \`<div class="terminal-line">Welcome to robots.txt! Type 'help' to see a list of available commands.</div>\`;
</script>