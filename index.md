---
layout: default
---

<div class="wrap">

  <!-- ===== HERO ===== -->
  <section class="hero section-top">
    <div class="hero-grid">
      <div>
        <div class="kicker">field notes · since 2024</div>
        <h1>Notes from the night shift.</h1>
        <p class="lede">A security scrapbook &mdash; writeups, the tools I build, and the
           half-formed thoughts I have at 1&nbsp;a.m. I write things down so I actually understand them.</p>
        <p class="now">currently poking at: <b>smart TVs</b>, <b>tunnels</b>, and <b>AI agents</b>.</p>
      </div>

      <div class="file" aria-label="robots.txt directives">
        <div class="file-bar">
          <span class="dot r"></span><span class="dot y"></span><span class="dot g"></span>
          <span class="file-name">~/robots.txt</span>
        </div>
<pre class="file-body"><span class="c"># what the crawlers may index</span>
<span class="k">User-agent:</span> <span class="v">*</span>
<span class="k">Allow:</span>      <span class="v"><a href="#posts">/posts</a></span>
<span class="k">Allow:</span>      <span class="v"><a href="#tools">/tools</a></span>
<span class="k">Allow:</span>      <span class="v"><a href="#thoughts">/thoughts</a></span>
<span class="k">Disallow:</span>   <span class="no">/secrets</span>
<span class="k">Crawl-delay:</span> <span class="v">grab a coffee</span>
<span class="c"># happy hacking — Het</span></pre>
      </div>
    </div>
  </section>

  <!-- ===== POSTS ===== -->
  <section id="posts">
    <div class="sec-label">
      <span class="path">/posts</span>
      <h2>Latest</h2>
      <span class="sec-note">newest first</span>
    </div>

    {%- comment -%} build a unique tag list scoped to the posts category {%- endcomment -%}
    {% assign tag_list = "" %}
    {% for post in site.categories.posts %}{% for t in post.tags %}{% unless tag_list contains t %}{% assign tag_list = tag_list | append: t | append: "," %}{% endunless %}{% endfor %}{% endfor %}
    {% assign tags = tag_list | split: "," %}
    {% if tags.size > 0 %}
    <div class="chips" role="group" aria-label="Filter posts by tag">
      <button class="chip" data-filter="all" aria-pressed="true">all</button>
      {% for t in tags %}<button class="chip" data-filter="{{ t }}" aria-pressed="false">{{ t }}</button>{% endfor %}
    </div>
    {% endif %}

    <div id="postlist">
      {% for post in site.categories.posts limit:5 %}
      <a class="post" href="{{ site.baseurl }}{{ post.url }}" data-tags="{{ post.tags | join: ' ' }}">
        <div class="post-meta">
          {% for t in post.tags %}<span class="tag">#{{ t }}</span>{% endfor %}
          <span>{{ post.date | date: "%b %-d, %Y" }}</span>
          <span>~{{ post.content | number_of_words | divided_by: 200 | plus: 1 }} min</span>
        </div>
        <h3>{{ post.title }}</h3>
        <p>{{ post.excerpt | default: post.description | strip_html | truncate: 180 }}</p>
      </a>
      {% endfor %}
    </div>

    <a class="viewall" href="{{ site.baseurl }}/library/">view all posts &rarr;</a>
  </section>

  <!-- ===== TOOLS / BUILDS ===== -->
  <section id="tools">
    <div class="sec-label">
      <span class="path">/tools</span>
      <h2>Things I built</h2>
      <span class="sec-note">small, sharp, open source</span>
    </div>
    {% assign builds = "" | split: "" %}
    {% if site.categories.projects %}{% assign builds = builds | concat: site.categories.projects %}{% endif %}
    {% if site.categories.tools %}{% assign builds = builds | concat: site.categories.tools %}{% endif %}
    <div class="grid">
      {% for b in builds %}
      <div class="tool">
        <div class="top">
          <svg class="ic" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M6 3 L14 3 L19 8 L19 21 L6 21 Z"/><path d="M14 3 L14 8 L19 8"/></svg>
          <h3>{{ b.title }}</h3>
        </div>
        <p>{{ b.description }}</p>
        {% if b.link %}<div class="lk"><a href="{{ b.link }}" target="_blank" rel="noopener">repo &uarr;</a></div>{% endif %}
      </div>
      {% endfor %}
      <div class="empty" aria-hidden="true">
        <svg class="ic" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 5 L12 19 M5 12 L19 12"/></svg>
        next tool, compiling&hellip;
      </div>
    </div>
  </section>

  <!-- ===== THOUGHTS ===== -->
  <section id="thoughts">
    <div class="sec-label">
      <span class="path">/thoughts</span>
      <h2>Half-formed</h2>
      <span class="sec-note">opinions subject to refactor</span>
    </div>
    {% assign thoughts = site.categories.posts | where_exp: "p", "p.tags contains 'thoughts'" %}
    {% if thoughts.size > 0 %}
      {% for post in thoughts limit:3 %}
      <a class="post" href="{{ site.baseurl }}{{ post.url }}">
        <div class="post-meta"><span class="tag">#thoughts</span><span>{{ post.date | date: "%b %-d, %Y" }}</span></div>
        <h3>{{ post.title }}</h3>
        <p>{{ post.excerpt | default: post.description | strip_html | truncate: 180 }}</p>
      </a>
      {% endfor %}
    {% else %}
      <div class="empty">tag a post <code>thoughts</code> and it shows up here.</div>
    {% endif %}
  </section>

  <!-- ===== TALKS ===== -->
  {% if site.categories.talks.size > 0 %}
  <section id="talks">
    <div class="sec-label">
      <span class="path">/talks</span>
      <h2>On stage</h2>
    </div>
    {% for talk in site.categories.talks %}
    <div class="talk">
      <a href="{{ talk.link }}">{{ talk.title }}</a>
      <span class="where">{{ talk.where }}</span>
    </div>
    {% endfor %}
  </section>
  {% endif %}

  <!-- ===== ABOUT ===== -->
  <section id="about" class="about">
    <div class="sec-label">
      <span class="path">/about</span>
      <h2>$ whoami</h2>
    </div>
    <p>Namaste &mdash; I'm Het. I'm a security researcher who learns by taking things apart, and this
       blog is where I write down the journey: the writeups, the tools, the dead ends, and the
       occasional idea worth keeping. Beginner or veteran, you're welcome here. Grab a coffee.</p>
    <div class="doodle-row" aria-hidden="true">
      <svg class="doodle" viewBox="0 0 64 54" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M24 26 C 23 25, 41 25, 40 26 C 42 32, 41 38, 40 40 C 30 42, 25 41, 24 40 C 22 34, 23 28, 24 26 Z"/>
        <path d="M24 30 C 14 26, 10 18, 6 14 M24 36 C 12 36, 8 42, 4 46 M40 30 C 50 26, 54 18, 58 14 M40 36 C 52 36, 56 42, 60 46"/>
        <circle cx="29" cy="31" r="1.6" fill="currentColor"/><circle cx="35" cy="31" r="1.6" fill="currentColor"/>
      </svg>
      <svg class="doodle" viewBox="0 0 44 54" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M8 22 C 7 21, 37 21, 36 22 C 38 32, 37 44, 36 46 C 22 48, 10 47, 8 46 C 6 36, 7 24, 8 22 Z"/>
        <path d="M13 22 C 11 8, 33 8, 31 22"/><path d="M22 31 L22 38"/>
      </svg>
      <svg class="doodle" viewBox="0 0 60 50" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M6 8 C 5 7, 55 7, 54 8 C 56 20, 55 40, 54 42 C 30 44, 10 43, 6 42 C 4 28, 5 10, 6 8 Z"/>
        <path d="M14 18 L22 24 L14 30 M28 30 L40 30"/>
      </svg>
    </div>
  </section>

  <!-- ===== CONTACT ===== -->
  <section id="contact">
    <div class="sec-label">
      <span class="path">/contact</span>
      <h2>Say hello</h2>
    </div>
    <div class="addr">
      <div><span class="k">email</span> <a href="mailto:het.matrix@gmail.com">het.matrix@gmail.com</a></div>
      <div><span class="k">github</span> <a href="https://github.com/het-joshi" target="_blank" rel="noopener">github.com/het-joshi</a></div>
      <div><span class="k">linkedin</span> <a href="https://www.linkedin.com/in/hetjoshi/" target="_blank" rel="noopener">in/hetjoshi</a></div>
    </div>
  </section>

</div>

<script>
  // tag filter — accessible, in-memory only
  (function(){
    var chips = Array.prototype.slice.call(document.querySelectorAll('.chip'));
    var posts = Array.prototype.slice.call(document.querySelectorAll('#postlist .post'));
    function apply(f){
      posts.forEach(function(p){
        var tags = (p.getAttribute('data-tags')||'').split(' ');
        p.style.display = (f==='all' || tags.indexOf(f)>-1) ? '' : 'none';
      });
    }
    chips.forEach(function(c){
      c.addEventListener('click', function(){
        chips.forEach(function(x){ x.setAttribute('aria-pressed','false'); });
        c.setAttribute('aria-pressed','true');
        apply(c.getAttribute('data-filter'));
      });
    });
  })();
</script>
