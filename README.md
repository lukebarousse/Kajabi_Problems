# GitHub Pages Setup for Kajabi Content

This repository hosts HTML lesson content that can be embedded into Kajabi courses. This workaround is necessary because Kajabi blocks certain keywords (like `COALESCE` in SQL) when pasted directly into lesson content.

## Overview

By hosting your HTML content on GitHub Pages and embedding it via JavaScript, you can bypass Kajabi's content restrictions and maintain full control over your lesson materials. This setup supports multiple courses, with each course having its own folder (e.g., `SQL_DE/` for SQL Data Engineering).

---

## Adding New Problems/Lessons

### Step 1: Create Your HTML File

1. Create your HTML file in the appropriate course folder (e.g., `SQL_DE/`) using your numbering system:
   ```bash
   touch SQL_DE/1.13.4.html
   ```
   Use your standard numbering convention (e.g., `1.13.4.html`, `2.5.1.html`)

2. Open the file in your editor and paste your HTML content

3. Save the file

### Step 2: Push to GitHub

```bash
git add SQL_DE/1.13.4.html
git commit -m "Add problem 1.13.4"
git push origin main
```

**Note:** Wait 1-2 minutes after pushing for GitHub Pages to update. You can check deployment status in your repo Settings → Pages.

### Step 3: Get Your Live URL

Your file will be live at:

```
https://lukebarousse.github.io/Kajabi_Problems/SQL_DE/1.13.4.html
```

**Test it:** Paste that URL in your browser—you should see your HTML rendered. ✅

**Note:** Replace `1.13.4.html` with your actual filename (using your numbering system) and `SQL_DE` with your course folder name if different.

---

## Embedding Content in Kajabi

### The Script to Paste

In your Kajabi lesson, add a **Custom HTML** block and paste this script:

```html
<div id="lesson-container">
  <p style="padding: 40px; text-align: center; background: #f0f0f0; border: 2px dashed #ccc; color: #666; font-family: monospace; margin: 0;">📝 EDIT CONTENT IN KAJABI_PROBLEMS REPO<br />To edit this lesson content, update the HTML file in the Kajabi_Problems repository<br /></p>
</div>

<script>
  fetch('https://lukebarousse.github.io/Kajabi_Problems/<course-folder>/<filename>.html')
    .then(response => response.text())
    .then(html => {
      document.getElementById('lesson-container').innerHTML = html;
    })
    .catch(error => console.error('Error loading lesson:', error));
</script>
```

**Customize the script:**
- Replace `<course-folder>` with your course folder (e.g., `SQL_DE`)
- Replace `<filename>` with your HTML filename (e.g., `1.13.4.html`, `2.5.1.html`)

### Example

For a file named `2.5.1.html` in the `SQL_DE` folder:

```html
<div id="lesson-container">
  <p style="padding: 40px; text-align: center; background: #f0f0f0; border: 2px dashed #ccc; color: #666; font-family: monospace; margin: 0;">📝 EDIT CONTENT IN KAJABI_PROBLEMS REPO<br />To edit this lesson content, update the HTML file in the Kajabi_Problems repository<br /></p>
</div>

<script>
  fetch('https://lukebarousse.github.io/Kajabi_Problems/SQL_DE/2.5.1.html')
    .then(response => response.text())
    .then(html => {
      document.getElementById('lesson-container').innerHTML = html;
    })
    .catch(error => console.error('Error loading lesson:', error));
</script>
```

---

## Updating Existing Content

When you update an existing HTML file:

```bash
git add SQL_DE/1.13.4.html
git commit -m "Update problem 1.13.4"
git push origin main
```

The changes deploy automatically within 1-2 minutes. Kajabi will pull the latest version automatically—no need to update the script in Kajabi.

---

## Folder Structure

```
Kajabi_Problems/
├── README.md
└── SQL_DE/
    ├── 1.13.4.html
    ├── 2.5.1.html
    └── ... (add more files as needed)
```

You can add additional course folders as needed (e.g., `Python_Basics/`, `Data_Analysis/`, etc.).

---

## Troubleshooting

- **Page not loading?** Wait a few minutes after pushing—GitHub Pages can take 1-2 minutes to update.
- **404 error?** Make sure your file path in the URL matches the actual file location in the repo.
- **Content not showing in Kajabi?** Check the browser console (F12) for JavaScript errors.
- **Script not working?** Verify:
  1. The URL in the `fetch()` call matches your GitHub Pages URL exactly
  2. The file exists and has been pushed to GitHub
  3. GitHub Pages deployment is successful (check Settings → Pages)

---