# Wood River PTA Website

## Project overview

This repository contains the public website for the Wood River Parent Teacher
Association in Corpus Christi, Texas. It is a small static site hosted by GitHub
Pages at `https://woodriverpta.org`.

There is no framework, build system, package manager, backend, database, or CMS.
The site consists of HTML, CSS, a logo, and small inline JavaScript snippets.

## Repository structure

- `index.html` — homepage
- `mission.html` — mission, vision, and core values
- `impact.html` — programs and community impact
- `about.html` — organization overview and history
- `get-involved.html` — membership, volunteering, and contact information
- `style.css` — shared styles and responsive behavior
- `logo.png` — shared site logo
- `CNAME` — GitHub Pages custom domain configuration
- `README.md` — short public repository overview

The header, footer, mobile-menu script, and page-reveal script are duplicated
across the HTML pages. When changing one of these shared elements, update every
page and verify that the active navigation state remains correct on each page.

## General working rules

- Keep the site static and dependency-free unless the user explicitly requests
  an architectural change.
- Prefer small, focused edits using the existing HTML and CSS conventions.
- Preserve the maroon visual identity and the existing `Outfit` typography
  unless a redesign is requested.
- Preserve `CNAME`; removing or changing it can disconnect the custom domain.
- Do not replace the external membership, volunteer, school, or Facebook links
  without confirming the new destinations.
- Do not invent dates, officers, contact information, event details, statistics,
  or PTA claims. Ask for missing factual content when it cannot be inferred
  safely from the repository.
- Preserve unrelated user changes in the working tree.
- Do not force-push, rewrite history, or use destructive Git commands.

## Editing workflow

1. Check the working tree before editing:

   ```sh
   git status --short
   ```

2. Read the complete file being changed and inspect related pages or selectors.

3. Make the smallest coherent change. For shared navigation, footer, or script
   changes, apply the update consistently across all five HTML pages.

4. Review the resulting diff:

   ```sh
   git diff --check
   git diff
   ```

5. Preview and verify the site locally before considering the work complete.

## Local preview

This site does not need a build command or local server. Open the relevant HTML
file directly in a browser, starting with `index.html` for the homepage. Relative
links, `style.css`, `logo.png`, and the inline JavaScript should work from the
local files.

When working in Codex, prefer the in-app browser's local-file preview if that
surface permits it. The automated in-app browser may reject `file://` URLs under
its security policy. If that happens, do not introduce a server or new tooling
just for previewing: validate the source, clearly report that visual preview was
blocked, and let the user open the HTML file directly. After an explicitly
requested publish, the agent can verify the result at
`https://woodriverpta.org`.

At minimum, check:

- The edited page at a normal desktop width.
- The edited page at a mobile width below `900px`.
- Header navigation and the mobile menu.
- Internal links and any external link changed by the update.
- Text wrapping, spacing, and footer layout.
- The browser console for errors when JavaScript was changed.

For site-wide style, navigation, or footer changes, spot-check every page.

## Implementation conventions

- Use semantic HTML and retain the existing page structure where practical.
- Put reusable styling in `style.css`; avoid adding more inline styles unless the
  existing component is already intentionally defined inline.
- Reuse the CSS custom properties under `:root` for brand colors and common
  values.
- Keep responsive behavior in the existing media-query sections.
- Provide useful `alt` text for meaningful images.
- Keep interactive controls keyboard accessible and give icon-only buttons an
  accessible label.
- If a link opens a new tab with `target="_blank"`, also add
  `rel="noopener noreferrer"`.
- Avoid adding third-party scripts, trackers, or dependencies without explicit
  approval.

## Completion checklist

Before reporting an edit as complete:

- The requested content or behavior is present.
- `git diff --check` passes.
- The relevant pages were previewed directly when browser access was available;
  otherwise, the preview limitation was reported accurately.
- Desktop and mobile layouts remain usable.
- Shared content is consistent across pages.
- `CNAME` is intact.
- No unrelated files were modified.

Clearly report what changed, what was verified, and whether the changes are only
local or have been published.

## Publishing through GitHub Pages

GitHub Pages publishes this site from the `main` branch. A normal push to
`origin/main` is the deployment mechanism.

Only publish when the user explicitly asks to push, deploy, or publish. Before
publishing:

1. Confirm the current branch and working-tree state:

   ```sh
   git branch --show-current
   git status --short
   ```

2. Confirm that only the intended changes will be included:

   ```sh
   git diff
   ```

3. Stage the intended files explicitly:

   ```sh
   git add path/to/file
   ```

4. Create a concise commit:

   ```sh
   git commit -m "Describe the website update"
   ```

5. Push the `main` branch:

   ```sh
   git push origin main
   ```

Do not commit or push unrelated local changes. If the current branch is not
`main`, or if remote changes prevent a normal push, inspect the situation and
explain it rather than forcing the update.

After a successful push, report the commit and note that GitHub Pages deployment
may take a short time. If deployment verification is requested, check
`https://woodriverpta.org` after the published revision becomes available.
