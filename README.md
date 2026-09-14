# shadowknight9284.github.io

My personal site. Two pages, no build step, no framework.

**[`index.html`](index.html)** — the landing page. Name, tagline, and a way to reach me.

**[`resume.html`](resume.html)** — the actual point of the site: my résumé presented as a
working LaTeX editor. Three documents (`main.tex`, `about_me.tex`, `cv.tex`) in a file
tree, a real editor pane on the left, a rendered page on the right, and a compile-log
drawer underneath. Edit the source and it recompiles as you type. Break the syntax and the
log drawer tells you what broke, the way a real one would.

## ResumeTeX

The renderer is not a screenshot and not a PDF embed — it's a small LaTeX interpreter
written from scratch in vanilla JS, living in `resume.html`. It tokenizes the source and
walks it directly, handling the subset a résumé actually needs:

- `\section`, `\begin{center}`, `\begin{itemize}`, paragraph breaks
- text commands: `\textbf`, `\textit`, `\emph`, `\texttt`, `\underline`, size switches
- `\href`, `\url`, `\includegraphics` (renders the real image, falls back to a
  placeholder frame when the path doesn't resolve)
- inline `$...$` math, `--`/`---` dashes, escaped specials
- the `\resumeSubheading` / `\resumeItem` macro family from the standard résumé template

Unsupported commands are skipped rather than thrown, so an unknown macro degrades to its
argument instead of blanking the page. The document outline in the sidebar is derived by
scanning the raw source for `\section{...}`.

## Running it

Open `index.html` in a browser. That's the whole dev loop — there's nothing to install and
nothing to compile. The only external dependency is CodeMirror from a CDN, and the editor
falls back to a plain `<textarea>` if it fails to load.

Deployed via GitHub Pages from `main`.
