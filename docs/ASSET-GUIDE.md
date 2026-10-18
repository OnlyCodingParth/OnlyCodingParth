# Asset Guide

This guide explains how to add your own images to the profile README and how to turn on the contribution snake.

The README is built so that **nothing shows a broken image**. Every image that does not exist yet is wrapped in an HTML comment, and a text version is shown instead. When you upload an image, you switch it on by deleting two marker lines (or one small piece of text).

---

## How the "switch on" markers work

In `README.md` you will see blocks like this:

```html
<!-- ENABLE-HEADER-IMAGE
<div align="center">
  <img src="assets/header/github-header.png" width="100%" alt="..." />
</div>
ENABLE-HEADER-IMAGE-END -->
```

Everything between those two marker lines is hidden. To switch it on, **delete the first line and the last line** (the ones containing `ENABLE-...`). The image code in the middle then becomes live.

Single-line items use this shape:

```html
<!-- ENABLE: <img src="assets/projects/infinity-guide.png" width="100%" alt="..." /> -->
```

To switch one of these on, delete `<!-- ENABLE: ` at the start of the line and ` -->` at the end.

> Only enable an image **after** the file is uploaded to the repository. Enabling it earlier is what causes a broken image.

---

## 1. Header image

- **Upload to:** `assets/header/github-header.png`
- **Size:** 1600 x 450 pixels
- **Suggested content:** an AI microchip with a neural network, a dark background, blue and purple lighting, the name PARTH GAVALI and the tagline "Exploring AI, ML & Data Science".

To enable it:

1. Upload the file to `assets/header/`.
2. In `README.md`, find `ENABLE-HEADER-IMAGE` and delete the two marker lines.
3. Delete the text header block above it (it is marked `HEADER-TEXT-FALLBACK`), so the name does not appear twice.

## 2. Footer image

- **Upload to:** `assets/footer/github-footer.png`
- **Recommended size:** 1600 x 300 pixels (any wide, short banner works)
- **Suggested content:** the same dark navy, blue and purple look as the header, with subtle circuit lines.

To enable it:

1. Upload the file to `assets/footer/`.
2. In `README.md`, find `ENABLE-FOOTER-IMAGE` and delete the two marker lines.
3. Keep the text footer ("Keep Learning. Keep Building. Keep Exploring.") if your image does not contain that text. If your image already contains it, delete the `FOOTER-TEXT-FALLBACK` block.

## 3. Certificate images

Upload to `assets/certifications/` using exactly these names:

| File | Certificate |
|---|---|
| `01-nptel.png` | NPTEL, Python for Data Science |
| `02-be10x.png` | Be10x, AI Tools and ChatGPT Workshop |
| `03-isro-hackathon.png` | Bharatiya Antariksh Hackathon 2026 |
| `04-cyber-security.png` | Cyber Security Workshop |
| `05-music-night.png` | Music Night |

To enable a preview, find its `<!-- ENABLE: <img ... /> -->` line under that certificate in `README.md` and remove the comment markers. You can enable them one at a time.

Before uploading, hide or crop any personal details you do not want public (for example a roll number, QR code or certificate ID).

## 4. Project banners (optional)

- **Upload to:** `assets/projects/`
- **Expected names:** `infinity-guide.png`, `c-programming.png`, `dsa-in-c.png`, `agriculture-notes.png`
- **Recommended size:** 1200 x 630 pixels

Each project in `README.md` has a commented-out banner line. Remove the comment markers once the file is uploaded.

## 5. Recommended dimensions and formats

| Image | Recommended size |
|---|---|
| Header | 1600 x 450 |
| Footer | 1600 x 300 |
| Certificates | about 1200 px wide |
| Project banners | 1200 x 630 |

- **Formats GitHub displays:** PNG, JPG/JPEG, GIF, WebP and SVG.
- The README expects `.png`. If you upload a `.jpg`, change the extension in the matching `src="..."` too.
- Keep each file under about 1 MB so the profile loads quickly.
- File names are **case-sensitive** on GitHub. `01-nptel.png` and `01-NPTEL.png` are different files.

---

## 6. How to add images (beginner steps)

**On github.com**

1. Open your `OnlyCodingParth` repository and go into the correct folder (for example `assets/header`).
2. Click **Add file → Upload files**, drag your image in and click **Commit changes**.
3. Open `README.md`, click the pencil icon and switch the image on as described above.

**On your computer**

1. Copy the image into the matching folder of your local clone.
2. Edit `README.md`.
3. Run `git add .`, `git commit -m "Add images"` and `git push`.

---

## 7. Enable the contribution snake

The snake needs a one-time workflow run before its images exist, so the README section for it is switched off.

1. **Allow Actions to write.** In the repository go to **Settings → Actions → General → Workflow permissions**, choose **Read and write permissions** and click **Save**.
2. **Run the workflow.** Open the **Actions** tab, choose **Generate Contribution Snake** in the left list, click **Run workflow** and confirm. It starts only when you click.
3. **Wait for a green check.** This usually takes under a minute.
4. **Confirm the output files exist** (see section 9).
5. **Enable the section.** In `README.md`, find `ENABLE-SNAKE` and delete the two marker lines. The heading and the snake images then appear.

The workflow also re-runs every 12 hours. GitHub pauses scheduled workflows in a public repository after 60 days without repository activity. If the snake stops updating, run the workflow manually once to restart it.

---

## 8. Troubleshooting broken images

**An image I uploaded does not show**

- Check the path and spelling in `src="..."`. It must match the file name exactly, including capital letters.
- Check the file is in the right folder and is committed (visible on github.com, not only on your computer).
- Make sure the repository is public.
- Hard refresh the page (Ctrl+Shift+R, or Cmd+Shift+R on Mac). GitHub caches images for a few minutes.

**A statistics card says "Something went wrong" or shows an error**

- These cards come from free third-party services (github-readme-stats, streak-stats, github-readme-activity-graph) that sometimes hit rate limits or go down.
- Wait a few minutes and reload. It usually recovers without any change from you.
- If a card keeps failing, remove that one `<img>` line. The rest of the README is unaffected.

**The snake does not show**

- The `ENABLE-SNAKE` markers are probably still in place, or the workflow has not succeeded yet.
- If the workflow ran but the `output` branch was not created, create it once by hand and run the workflow again:

```bash
git switch --orphan output
git commit --allow-empty -m "Initialize output branch"
git push origin output
git switch main
```

- If the run fails with a permissions error, re-check step 1 of section 7. An organization policy can also block write access.

---

## 9. Verify the GitHub Actions output

1. Open the **Actions** tab and click the latest **Generate Contribution Snake** run. Both steps should have a green check.
2. Switch to the `output` branch (the branch menu on the repository's main page). It should contain `github-snake.svg` and `github-snake-dark.svg`.
3. Open these addresses in a browser. Each should display an animated snake:
   - `https://raw.githubusercontent.com/OnlyCodingParth/OnlyCodingParth/output/github-snake.svg`
   - `https://raw.githubusercontent.com/OnlyCodingParth/OnlyCodingParth/output/github-snake-dark.svg`
4. Only then enable the section in `README.md`.

---

## 10. Preview the README before pushing

**In VS Code**

1. Open `README.md`.
2. Press `Ctrl+Shift+V` (or `Cmd+Shift+V` on Mac) to open the Markdown preview.
3. Your local images in `assets/` show immediately. Cards from third-party services need an internet connection.

**On GitHub, without publishing to your profile**

1. Create a new branch, for example `readme-preview`: `git switch -c readme-preview`.
2. Commit and push that branch: `git push -u origin readme-preview`.
3. Open `README.md` on that branch on github.com to see exactly how GitHub renders it.
4. When you are happy, merge it into `main`. The profile shows the `main` version.

VS Code's preview is close to GitHub but not identical. Check the final result on github.com, on both desktop and a phone, before you finish.
