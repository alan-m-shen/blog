# Alan’s Blog

A small static personal site: Hugo, PaperMod, Markdown, and custom CSS.

## Run locally

Use Hugo **0.146.0** (also recorded in `.hugo-version`). The version file is a
reference for local and hosting configuration; Hugo itself does not enforce it.
PaperMod is pinned by the Git submodule commit. Initialize it after cloning:

```sh
git submodule update --init --recursive
hugo server
```

Use `hugo server -D` to preview draft posts.

## Build

```sh
hugo --environment production --cleanDestinationDir
```

Publish `public/`. This directory is generated output only; the build command
removes stale output such as old RSS feeds. Configure the hosting provider to
use the same Hugo version and initialize submodules before building.

## Keep customization small

- Articles live in `content/posts/`; image URLs remain external.
- Styling lives in `assets/css/extended/custom.css`.
- Fonts load through `layouts/partials/extend_head.html`.
- The custom home, cover, image, and minimal footer templates preserve the design.
- The theme header handles automatic dark mode. The minimal footer intentionally
  omits theme scripts for disabled features (theme toggle, back-to-top, code copy).
- RSS output is disabled. No Node build step is required.

## Images

Ordinary Markdown images keep their normal appearance:

```markdown
![Description](https://example.com/image.png)
```

Opt into the monochrome print treatment for an individual image:

```go-html-template
{{< image src="https://example.com/image.jpg" alt="Description" style="print" >}}
```

The image shortcode also accepts `caption`, `width`, and `height`. Omitting
`style="print"` leaves it unfiltered. Icons and the avatar have separate styles.
For a post's cover, set `cover.style: print` in its front matter; omit that field
for an untreated cover.

The home page retains PaperMod’s single-column list and original entry margins.
Only the top padding scales continuously with viewport width using
`clamp(1rem, 3vw, 2rem)`; bottom padding remains zero. No breakpoints or custom
home-page layout are needed.

## Citations

Essays use Chicago 18th-edition notes: a full first citation within each essay,
shortened later citations, and note markers after punctuation. Books without
stable page numbers use chapter, section, or book-and-line locators. Legal notes
identify the instrument and relevant articles. No separate bibliography is needed
for these short essays because the notes supply the full source details.

The lost original references were reconstructed from sources checked on October 9,
2026; they are not a recovered bibliography. The original publication dates remain
(with Paradise Lost dated June 2, 2022), and `lastmod` records the revision date.

When deliberately upgrading Hugo or PaperMod, build first and check the home
page and an article at narrow and wide widths, in both light and dark mode.
