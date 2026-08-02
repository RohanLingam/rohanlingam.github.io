# Your website — how to edit it

Plain HTML and CSS. No build step, no framework, no npm. You edit a file, save it,
refresh the browser. That's the whole workflow.

---

## 1. What's in here

```
index.html                     ← the homepage (bio, links, Updates, Miscellaneous)
projects.html                  ← the project list, one row per project
stylesheet.css                 ← all styling. You rarely need to touch this.
README.md                      ← this file
images/
  profile.jpg                  ← your headshot
  projects/                    ← every project image and video goes here
data/
  RohanLingam-CV.pdf           ← your CV
  example-project-report.pdf   ← any PDF you want to link or embed
projects/
  _TEMPLATE.html               ← copy this to start a new project page
  example-project.html         ← a full example (images, PDF, table, code)
  second-project.html          ← a short example
```

Three levels: the homepage introduces you, `projects.html` lists everything you've built,
and each file in `projects/` is one project written up in full.

Every file currently in `images/` and `data/` is a grey placeholder. Overwrite them
with your own files, keeping the same names, and the site updates with no HTML edits.

---

## 2. Preview it locally

Double-click `index.html` — it opens in your browser and works.

One exception: the embedded PDF viewer inside project pages sometimes gets blocked
when opening files directly. If you want that to work locally, run a tiny server
from this folder:

```
cd path/to/this/folder
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

---

## 3. First things to change

Your name, email, and GitHub are already filled in. Still to do, in `index.html`:

| Find | Replace with |
|---|---|
| `goodreads.com/user/show/000000000` | your Goodreads profile URL |
| the bio paragraph | your bio, 3–5 sentences |
| the Updates bullets | real updates (see below) |
| the Miscellaneous bullets | real activities, and `#` links with real URLs |

Drop your headshot in as `images/profile.jpg` — square crops look best, since the CSS
rounds it into a circle. Replace `data/RohanLingam-CV.pdf` with your real CV, keeping
the filename.

### The Updates section

A running list, newest at the top. One line each. To add one, copy a single line:

```html
<li><strong>Aug 2026</strong> &mdash; What happened. <a href="#">Link if there is one.</a></li>
```

Keep it to roughly the last year and delete old entries as you go. A stale updates list
reads worse than no updates list.

---

## 4. Adding a project

Two steps: make the page, then link to it from the homepage.

### Step A — make the project page

1. Copy `projects/_TEMPLATE.html` and rename the copy, e.g. `projects/rf-amplifier.html`.
   Use lowercase and hyphens, no spaces — the filename becomes part of the URL.
2. Open it and change the title, the meta line, and the links at the top.
3. Delete every block in the body you don't need. Keep the ones you do and fill them in.
   The blocks are all labeled with comments like `<!-- ---------- BLOCK: hero image ---------- -->`.
4. Put your images in `images/projects/` and your PDFs in `data/`, then point the
   `src` and `href` attributes at them.

### Step B — add the row to `projects.html`

Open `projects.html`, find the section marked:

```
<!-- ===================== PROJECT ENTRY START ===================== -->
```

Copy one entire block from `PROJECT ENTRY START` to `PROJECT ENTRY END`, paste it
where you want the project to appear (newest at the top is the convention), and edit:

- the thumbnail path
- the title and the `href` pointing to your new page
- the names line, the context line (`<em>Course project</em>, 2025`)
- the small link row underneath
- the one-paragraph description

There are three flavors of entry already in the file — copy whichever fits:

1. **Highlighted + hover swap** — pale yellow background, image changes on mouseover.
2. **Plain** — one static thumbnail. Use this for most projects.
3. **External link** — points at a repo or paper instead of a project page.

### The hover swap

If you copy the hover-swap entry, rename the JavaScript functions and the element `id`
so they're unique. Every project that hovers needs its own name — pick something and
replace `biologger` everywhere it appears in that block:

```
onmouseout="biologger_stop()" onmouseover="biologger_start()"
id="biologger_image"
function biologger_start() { document.getElementById('biologger_image')...
```

If two projects share a name, both will break. If you don't want the effect, use the
plain entry instead — it's much less to keep track of.

### The highlight

The pale yellow background comes from `bgcolor="#ffffd0"` on the `<tr>`. Add it to
highlight a project, delete it to un-highlight.

---

## 5. Blocks you can use on a project page

All of these are in `_TEMPLATE.html`, ready to copy.

**Image with caption**
```html
<figure>
  <img src="../images/projects/yourphoto.jpg" alt="what it shows">
  <figcaption>Caption text.</figcaption>
</figure>
```

**Two or three images side by side** (they stack automatically on phones)
```html
<div class="imgrow">
  <figure><img src="../images/projects/a.jpg" alt="a"><figcaption>Left.</figcaption></figure>
  <figure><img src="../images/projects/b.jpg" alt="b"><figcaption>Right.</figcaption></figure>
</div>
```

**Embedded PDF**
```html
<iframe class="doc-embed" src="../data/your-report.pdf" title="Report"></iframe>
<p><a href="../data/your-report.pdf">Download the PDF</a></p>
```
Always keep the download link. Mobile browsers often can't render the embed.

**Word doc, spreadsheet, or anything else** — browsers can't display these inline, so
just link them. Exporting to PDF first is usually nicer for the reader.
```html
<p><a href="../data/your-notes.docx">Design notes (DOCX)</a></p>
```

**Video file**
```html
<figure>
  <video controls muted loop width="100%">
    <source src="../images/projects/demo.mp4" type="video/mp4">
  </video>
  <figcaption>Caption.</figcaption>
</figure>
```

**YouTube** — use the `/embed/` URL form, not `/watch?v=`
```html
<iframe width="100%" height="400" src="https://www.youtube.com/embed/VIDEO_ID"
        frameborder="0" allowfullscreen></iframe>
```

**Spec table**
```html
<table class="spec">
  <tr><th>Supply</th><td>3.3 V</td></tr>
</table>
```

**Callout box**
```html
<blockquote>The one thing you want people to remember.</blockquote>
```

**Code**
```html
<pre><code>your_code_here();</code></pre>
```

**Section heading, sub-heading, divider**
```html
<h2>Big heading</h2>
<h3>Small heading</h3>
<hr>
```

### A note on paths

Project pages live one folder down, so they reach back up with `../`:

- from `index.html`: `images/projects/photo.jpg`
- from `projects/anything.html`: `../images/projects/photo.jpg`

If an image doesn't show up, this is almost always why. Capitalization counts too —
`Photo.JPG` and `photo.jpg` are different files once the site is online.

---

## 6. Editing the Miscellaneous section

Bottom of `index.html`. It's one bullet list. Each top-level bullet is a category, with
the bold lead-in doing the labeling, and optional sub-bullets underneath:

```html
<li><strong>Category.</strong> One-line summary.
  <ul style="padding-left:22px">
    <li>A detail.</li>
    <li>Another detail.</li>
  </ul>
</li>
```

To add a category, copy that whole block. To drop the sub-bullets, delete the inner
`<ul>` and leave a single line. Keep each bullet to one line — this section reads as a
quick sketch of who you are outside the projects, not a second resume.

---

## 7. Putting it online (GitHub Pages, free)

1. Make a new GitHub repo named exactly `yourusername.github.io`.
2. Upload everything in this folder to the root of that repo — `index.html` must be at
   the top level, not inside a subfolder.
3. Repo → Settings → Pages → Source: `main` branch, `/ (root)`. Save.
4. Wait a minute or two. Your site is at `https://yourusername.github.io`.

After that, editing is: change a file, commit, push. GitHub redeploys automatically.
You can even edit files directly in the GitHub web editor if you're away from your laptop.

---

## 8. Practical tips

- **Resize images before uploading.** A 6 MB phone photo makes the page slow. Aim for
  under 400 KB each; 1200 px wide is plenty for a full-width photo, 320 px for a thumbnail.
- **Thumbnails should be square.** The layout reserves a 160×160 box. Non-square images
  get squished.
- **Write the project page like a blog post, not a lab report.** What is it, why did you
  build it, what was hard, what happened. Attach the formal report as a PDF if you have one.
- **Filenames with spaces cause problems online.** Use hyphens.
- **Add a favicon** by dropping a `favicon.ico` into `images/` — the HTML already points at it.
- **Nothing here tracks anyone.** There's no analytics, no fonts loaded from a third party
  beyond the Google Fonts `@font-face` block already in the CSS, and no cookies.

---

Layout and stylesheet adapted from [Jon Barron's website](https://github.com/jonbarron/jonbarron_website),
which he offers freely. The analytics tags from his live site are not included here.
