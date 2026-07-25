# Posting templates

Copy-paste snippets for adding a post to domineoeffect.uk.
Edit on GitHub, commit, and it is live in about a minute.

- Homepage: `index.html` (edit at `/edit/main/index.html`)
- New article: `/new/main`, name it `take-something.html`
- All styling lives in `style.css` - never paste CSS into a page.

New cards go DIRECTLY UNDER `<div class="cards">` so newest is first.

---

## 1. FIND card (homepage only)

```html
      <article class="card find">
        <span class="badge"><span class="tile tile-sm" aria-hidden="true"><span class="face f2"></span><span class="face f4"></span></span></span>
        <span class="date">FIND &#183; 26 JUL</span>
        <h4><a href="REVIEW_URL" target="_blank" rel="noopener">Your headline here</a></h4>
        <p>Two or three sentences on why it is worth knowing about.</p>
        <p class="links"><a href="REVIEW_URL" target="_blank" rel="noopener">read the review &#8594;</a></p>
      </article>
```

## 2. WATCH card (homepage only)

```html
      <article class="card watch">
        <span class="badge"><span class="tile tile-sm" aria-hidden="true"><span class="face f3"></span><span class="face f2"></span></span></span>
        <span class="date">WATCH &#183; 26 JUL</span>
        <div class="embed"><iframe src="https://www.youtube-nocookie.com/embed/VIDEO_ID" title="Video" loading="lazy" allowfullscreen referrerpolicy="strict-origin-when-cross-origin"></iframe></div>
        <h4>Your headline here</h4>
        <p>Why this one is worth an evening.</p>
        <p class="links"><a href="https://www.youtube.com/watch?v=VIDEO_ID" target="_blank" rel="noopener">watch on YouTube &#8594;</a></p>
      </article>
```

VIDEO_ID is the part after `v=` in a YouTube URL.
Embeds only play on the live https site, never from a local file.

## 3. TAKE card (points at your article)

```html
      <a class="card take" href="take-something.html">
        <span class="badge"><span class="tile tile-sm" aria-hidden="true"><span class="face f1"></span><span class="face f0"></span></span></span>
        <span class="date">TAKE &#183; 26 JUL</span>
        <h4>Your headline</h4>
        <p>The hook - one or two sentences.</p>
      </a>
```

Takes use `<a class="card take">` so the whole card is clickable.
Finds and watches use `<article class="card ...">`.

For the article itself: open `take-hinton.html`, copy it, and swap the text.
It already links `style.css`, so it inherits the theme.

---

## The four things that break the page

**1. Close the tag.** Every find/watch card needs `</article>`.
Missing closers make cards NEST inside each other - that is what caused
the overlapping cards. Takes need `</a>`.

**2. Use a domino nobody else has.** Top face = the stream:
`f1` take, `f2` find, `f3` watch. Bottom face is free - pick an unused one.

**3. Use entity codes, not typed punctuation.** This is what stops the
`A-tilde` garbling coming back:

| Want | Type this |
|---|---|
| dot separator | `&#183;` |
| em dash | `&#8212;` |
| pound | `&#163;` |
| arrow | `&#8594;` |
| quote marks | `&quot;` or plain " |

Never paste curly quotes or dashes straight from Word or a webpage.

**4. Trim the oldest card** when the feed gets long.

---

## Dominoes still free

As of 25 Jul 2026 (26 tiles in use, all unique):

- **Take** (`f1` top): `f1/f0`, `f1/f1`, `f1/f2`, `f1/f3`, `f1/f6`
- **Find** (`f2` top): `f2/f2`, `f2/f4`
- **Watch** (`f3` top): `f3/f2`, `f3/f3`, `f3/f4`, `f3/f6`

To re-check what is taken, open the live site and paste this into the
browser console (F12):

```js
[...document.querySelectorAll('.tile')].map(t=>[...t.querySelectorAll('.face')]
  .map(f=>f.className.replace('face ','')).join('/')).sort().join(', ')
```

Finds run low first. When `f2` pairs run out, reuse a number on a card
that has since been trimmed, or let a find carry a second-face repeat -
uniqueness is a nice-to-have, not structural.

---

## Before you commit

Click the **Preview** tab and check the diff. A healthy new post shows
ONE small hunk of added lines. If you see a hunk adding 200+ lines, the
paste has duplicated the file - do not commit, reload and try again.

After it goes live, hard-refresh with Ctrl+Shift+R (Cmd+Shift+R on Mac).

---

## When this gets tedious

At one post a day, hand-editing `index.html` every time is the bottleneck,
and every edit is a chance to break the grid. The fix is converting to
Astro: each post becomes its own file and the homepage builds its own card
list, so you never touch `index.html` again. Worth doing once you have four
or five posts up and the format has settled.
