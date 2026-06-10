# robots.txt — revamp (v2, include-based)

This version plugs into your existing theme structure instead of replacing it wholesale.
It reuses your `_includes` architecture and keeps the `assets/css/style.css` filename, so
`head.html`'s stylesheet link keeps working with no edits elsewhere.

**Use this instead of the earlier `robots_txt_theme` package** (that one used a self-contained
layout + `main.css`; this is cleaner and matches how your repo is organized).

## Files to replace / add

```
robots_txt/
├── _includes/
│   ├── head.html        ← replace (adds fonts, fixes viewport + theme-color)
│   ├── header.html      ← replace (now the sticky nav bar; pulls in nav.html)
│   ├── nav.html         ← replace (link list)
│   └── footer.html      ← replace (global footer; comments moved to post.html)
├── _layouts/
│   ├── default.html     ← replace (clean head/body, keeps Konami egg)
│   └── post.html        ← replace (reading view; reuses your disqus.html)
├── assets/css/
│   └── style.css        ← replace (the new dark theme)
├── index.md             ← replace
└── library.md           ← replace
```

## Left untouched (keep yours)

`_includes/disqus.html`, `_includes/open_graph_cards.html`, `_includes/share_buttons.html`,
`_config.yml`, `_posts/`, `rss.xml`, `atom.xml`, `Gemfile`, `assets/LICENSE`, `assets/img/`.

Note: comments now render inside the article (via your `disqus.html`) rather than in the
footer, so `footer.html` no longer calls disqus — that's intentional.

## One-time content tweaks

1. **Tags drive the filter + /thoughts.** Add a `tags:` line to posts (topic, separate from
   the `categories:` content-type). Suggested for your existing three:
   - `2024-12-10-Hacker-post.md`  → `tags: [thoughts]`
   - `2024-07-26-fileGen-post.md` → `tags: [tools, journey]`
   - `2024-05-26-init-1-post.md`  → `tags: [journey]`
2. **Code fences:** use ` ```python ` (not `python3`) so Rouge colors them.

## Preview

```
bundle exec jekyll serve   # → http://localhost:4000/robots_txt/
```

## Extras kept / changed

- Konami code (↑↑↓↓←→←→ b a) now flips the accent to the classic phosphor green — a nod to
  the old theme. Press again to toggle back.
- Old ASCII banner + `$ cat about.txt` framing is gone; the identity is the robots.txt
  directive block in the hero. Say the word if you want the `$ cat` motif reintroduced.
- The `og:image` tags in `open_graph_cards.html` use relative paths; if you want proper
  link-preview thumbnails, make `site.cover` an absolute URL. Left as-is for now.
```
