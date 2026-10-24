# Build Your Resume

A free, single-file resume builder website designed for GitHub Pages.

## Features
- Live resume preview
- Personal details, summary, multiple work roles and education entries
- Skills and projects/achievements
- Basic job-description keyword check
- Print / Save as PDF using the browser's print dialog
- Saves draft data in the current browser's local storage
- Responsive layout for desktop and mobile

## Publish using GitHub Pages
1. Create a GitHub repository (for example, `resumecraft-ai`).
2. Upload `index.html` to the repository root.
3. Open **Settings → Pages**.
4. Under build and deployment, choose **Deploy from a branch**.
5. Choose branch `main` and folder `/ (root)`, then Save.
6. Wait for GitHub Pages to publish the site; the URL will appear on the Pages settings screen.

## Important notes
- This is a static website and does not call a real AI model yet. The writing helper gives guided templates, and the keyword checker is a simple text match—not a guaranteed ATS score.
- Do not put a private AI API key in `index.html`, because anyone can inspect a public website's code. To add genuine AI generation, use a backend or serverless function that keeps the API key secret.
- Resume information is saved in the browser's local storage on the device. Avoid using a shared computer and clear data when done.
- PDF export uses the browser print dialog. Choose **Save as PDF**.
