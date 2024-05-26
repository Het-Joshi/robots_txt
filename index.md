---
layout: default
---

# $ cat about.txt <span class="blinking-cursor"></span>
{:id="about"}

Namaste, welcome to my blog **robots.txt**! I started this blog in an effort to document my cybersecurity projects and all the things I learn in this field. Whether you're a newbie just dipping your toes into the vast ocean of cybersecurity or a seasoned pro looking to sharpen your skills, this blog is for you. My goal is to share knowledge, tips, and tricks that will be useful to everyone, from beginners to experts. So, grab a cup of coffee (or tea, if that's your thing), get comfy, and let's explore the fascinating world of cybersecurity together.
<br>
**Happy hacking!**

# $ cat latest-posts.txt <span class="blinking-cursor"></span>

<ul>
{% for post in site.categories.posts limit:4 %}
  <li>
    <h2>{{ post.title }}</h2>
    <p>{{ post.description }}</p>
    <p>{{ post.excerpt }}</p>
    <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.description }}">Read more</a>
  </li>
{% endfor %}
</ul>

<a href="{{ site.baseurl }}/library">View All Posts</a>



# $ cat contact.txt <span class="blinking-cursor"></span>
{:id="contact"}

If you have any questions, suggestions, or just want to say hello, feel free to reach out to me! I'm always excited to connect with fellow cybersecurity enthusiasts, share knowledge, and collaborate on projects. You can contact me via the following channels:

- **Email**: [het.matrix@gmail.com](mailto:het.matrix@gmail.com)
- **GitHub**: [github.com/het-joshi](https://github.com/het-joshi)
- **LinkedIn**: [Het-Joshi](https://www.linkedin.com/in/hetjoshi/)

Whether you have feedback on my posts, want to discuss a cybersecurity topic, or need help with something, don't hesitate to get in touch. Let's make the cybersecurity community stronger together!

# $ cat projects.txt <span class="blinking-cursor"></span>
{:id="projects"}

<ul>
{% for project in site.categories.projects %}
<li><a href="{{ project.link }}">{{ project.title }}</a> - {{ project.description }}</li>
{% endfor %}
</ul>

# $ cat tools.txt <span class="blinking-cursor"></span>
{:id="tools"}

<ul>
{% for tool in site.categories.tools %}
<li><a href="{{ tool.link }}">{{ tool.title }}</a> - {{ tool.description }}</li>
{% endfor %}
</ul>

# $ cat talks.txt <span class="blinking-cursor"></span>
{:id="talks"}

<ul>
{% for talk in site.categories.talks %}
<li><a href="{{ talk.link }}" title="{{ talk.description }}">{{ talk.title }}</a> at {{ talk.where }}</li>
{% endfor %}
</ul>
