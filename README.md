# We Can’t Code Well — Project Site

A lightweight single-page website for our CISC322/CISC326 group project.  
It showcases the team, an embedded **PDF report**, a **video demo**, and **presentation slides** (PowerPoint) with an Office Online viewer and a Google Docs fallback. Built on the HTML5 UP **Story** template and deployable as a static site (e.g., GitHub Pages).

---

## Features

- **Team section** with roles and smooth in-page navigation.
- **PDF embed** (`assets/A1.pdf`) with a full-screen/open-in-tab button and a fallback link.
- **Video demo** (YouTube) embedded responsively.
- **Presentation slides** (`assets/Void.pptx`) embedded via **Office Online**, with a **Google Docs Viewer** toggle.
- **Responsive, animated layout** using HTML5 UP transitions (onscroll fades, smooth scrolling).

---

## Project Structure

```
.
├─ index.html
├─ images/
│  ├─ banner.jpg
│  └─ spotlight01.jpg
└─ assets/
   ├─ A1.pdf
   ├─ Void.pptx
   ├─ css/
   │  ├─ main.css
   │  └─ noscript.css
   ├─ js/
   │  ├─ jquery.min.js
   │  ├─ jquery.scrollex.min.js
   │  ├─ jquery.scrolly.min.js
   │  ├─ browser.min.js
   │  ├─ breakpoints.min.js
   │  ├─ util.js
   │  └─ main.js
   └─ (optional fonts/icons)
```

---

## Deploying to GitHub Pages

1. Push the project to a **public** GitHub repo.
2. **Settings → Pages**  
   - Source: *Deploy from a branch*  
   - Branch: `main` (or `master`) • Root
3. Wait for the Pages URL.

**Important:** Office/Google viewers must fetch `assets/Void.pptx` via a **public absolute URL**. The script in `index.html` builds this automatically:
```js
var pptxUrl = new URL('assets/Void.pptx', window.location.href).href;
```

---

## Configuration

### Video (YouTube)
Update the embed to your video (current demo ID is `KykVLshQq_g`):
```html
<div class="embed embed-16x9">
  <iframe
    src="https://www.youtube-nocookie.com/embed/KykVLshQq_g"
    title="Void — The Video Overview"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen
    loading="lazy"></iframe>
</div>
```

### Images
Replace `images/banner.jpg` and `images/spotlight01.jpg` with your assets.

### Copy/Labels
Edit section headings, roles, and button text directly in `index.html`.

---

## Embeds — How They Work

### PDF (`assets/A1.pdf`)
```html
<object
  data="assets/A1.pdf#view=page-width"
  type="application/pdf"
  class="pdf-embed"
  aria-label="A1 PDF">
  <iframe
    src="assets/A1.pdf#view=page-width"
    class="pdf-embed"
    title="A1 PDF"></iframe>
  <p>Can’t display the PDF. <a href="assets/A1.pdf" target="_blank" rel="noopener">Open it</a>.</p>
</object>
```
- `#view=page-width` gives a friendly default zoom.
- `<p>` provides a fallback link if PDFs aren’t supported (e.g., some mobile browsers).

### Slides (`assets/Void.pptx`)
Office viewer by default; toggle to Google viewer if needed:
```html
<div class="pptx-embed">
  <iframe id="void-pptx" title="Void.pptx slides" allowfullscreen></iframe>
</div>

<script>
(function () {
  var pptxUrl = new URL('assets/Void.pptx', window.location.href).href;

  var office = 'https://view.officeapps.live.com/op/embed.aspx?src='
               + encodeURIComponent(pptxUrl)
               + '&wdAr=1.77777777777778'; // 16:9
  var gview = 'https://docs.google.com/gview?embedded=true&url='
               + encodeURIComponent(pptxUrl);

  var iframe = document.getElementById('void-pptx');
  iframe.src = office;

  var toggle = document.getElementById('toggle-viewer');
  var hint   = document.getElementById('pptx-hint');
  if (toggle) {
    toggle.addEventListener('click', function (e) {
      e.preventDefault();
      iframe.src = iframe.src.includes('view.officeapps.live.com') ? gview : office;
      if (hint) hint.hidden = false;
    });
  }
})();
</script>
```

---

## Testing

- **Mobile/Responsive:** Use dev tools to verify embeds scale and text remains readable.
- **Safari/iOS:** If PDFs don’t render inline, the fallback download link should appear.
- **Slides viewer:** If Office shows a blank page, click **“Try alternate viewer”**.


---

## Credits

- Base theme: **HTML5 UP – Story** (free for personal and commercial use under **CCA 3.0**).  
  <https://html5up.net/story>

---

## License

- Site content (report, slides, copy, images): © the project authors.  
- Theme and third-party assets: under their respective licenses (see HTML5 UP CCA 3.0).


---

## Maintainers

- **David Balan** — Team Leader  
- **Mark Nistor** — Presenter  
- **Ameek Bains** — Presenter  
- **Maxim Logunov** — Team Member  
- **Radmehr Vafadarfalavarjani** — Team Member  
- **Luca Del Sorbo** — Team Member

Questions or improvements? Open an issue or PR.
