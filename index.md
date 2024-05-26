---
layout: default
---

# $ cat about.txt
{:id="about"}

Namaste, welcome to my blog **robots.txt**! I started this blog in an effort to document my cybersecurity projects and all the things I learn in this field. Whether you're a newbie just dipping your toes into the vast ocean of cybersecurity or a seasoned pro looking to sharpen your skills, this blog is for you. My goal is to share knowledge, tips, and tricks that will be useful to everyone, from beginners to experts. So, grab a cup of coffee (or tea, if that's your thing), get comfy, and let's explore the fascinating world of cybersecurity together.
<br>
**Happy hacking!**

# $ cat contact.txt
{:id="contact"}

I think that all about this theme is intuitive, but if you want help, please, contact me: [gjuniioor](https://github.com/gjuniioor).

# $ cat team.txt
{:id="team"}

<ul>
{% for member in site.categories.team reversed %}
<li id="{{ member.title }}">{{ member.title }}
  <ul>
    <li>{{ member.mail }}</li>
    <li><a href="https://github.com/{{ member.github }}">https://github.com/{{ member.github }}</a></li>
    <li><a href="{{ member.site }}">{{ member.site }}</a></li>
  </ul>
</li>
{% endfor %}
</ul>

# $ cat projects.txt
{:id="projects"}

<ul>
{% for project in site.categories.projects %}
<li><a href="{{ project.link }}">{{ project.title }}</a> - {{ project.description }}</li>
{% endfor %}
</ul>

# $ cat tools.txt
{:id="tools"}

<ul>
{% for tool in site.categories.tools %}
<li><a href="{{ tool.link }}">{{ tool.title }}</a> - {{ tool.description }}</li>
{% endfor %}
</ul>

# $ cat talks.txt
{:id="talks"}

<ul>
{% for talk in site.categories.talks %}
<li><a href="{{ talk.link }}" title="{{ talk.description }}">{{ talk.title }}</a> at {{ talk.where }}</li>
{% endfor %}
</ul>

# $ cat posts.txt
{:id="posts"}

<ul>
{% for post in site.categories.posts %}
  <li>{{ post.title }} :: <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.description }}">en</a></li>
{% endfor %}
</ul>

# $ cat articles.txt
{:id="articles"}

<ul>
{% for post in site.categories.articles %}
  <li>{{ post.title }} :: <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.description }}">en</a></li>
{% endfor %}
</ul>
