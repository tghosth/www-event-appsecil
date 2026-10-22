# AppSec-Israel

Jekyll repo for hosting the website for AppSec Israel Conference.   
Viewable live at https://appsecil.org/ . 

### Contributing
Feel free to contribute anything that will improve the Conference site via PR - especially design :-)   
- If you're not familiar with Jekyll: https://jekyllrb.com/docs/home/  
- Jekyll tips: http://cheat.jekyll.tips/

### 2026 photo album

The album page is `2026/photos.md`, published at `/2026/photos.html`. It shows a coming-soon message
until photos are added.

Copy photos into `assets/img/2026/album/` and rebuild the site. Jekyll discovers
them automatically; no YAML entries or plugins are needed. JPG, JPEG, PNG, GIF,
WebP and AVIF files are supported, including uppercase extensions. Non-image
files are ignored.

Photos appear in filename order (including any subfolders). Photos with known
capture times use a `YYYY-MM-DD_HH-MM-SS_` filename prefix so they appear from
earliest to latest. Photos without a known capture time use an `undated_`
prefix and appear afterward. The website does not need the original files or
read capture timestamps from image metadata.

You can also use prefixes such as `001-keynote.jpg` to control order. Descriptive
filenames provide the image alt text, with hyphens and underscores replaced by
spaces. Images are displayed as lazy-loaded thumbnails and open at full size.
Resize very large originals before adding them to keep the page quick to load.

The album reuses the site's `ImgPopUp.js` viewer, with previous/next buttons,
left/right arrow keys, a photo counter, and a close button (or Escape).

### Local preview with Ruby 4 on Windows

From a terminal in this repository, run:

```powershell
.\preview.bat
```

Open `http://127.0.0.1:4000/2026/photos.html`. The preview rebuilds when files change;
refresh the browser to see updates. Press Ctrl+C to stop it. To only build the
site, run `.\preview.bat -Build`. To use another port, run
`.\preview.bat -Port 4001`.

No arguments are needed: the launcher checks dependencies, installs any missing
ones, builds the site, and starts the server each time. It runs Ruby directly,
so PowerShell script execution settings do not affect it. It uses
`_tools/Gemfile.preview` to run Jekyll 3.10 and Liquid 4.0.4 with Ruby 4's shipped
JSON and BigDecimal libraries. This avoids the incompatible older Liquid
version selected by the full GitHub Pages bundle on Ruby 4. The production
`Gemfile` is separate from this local preview configuration.

### Chapter and conference landing page

The homepage (`index.html`) gives the annual conference and year-round chapter
equal prominence. The homepage and chapter pages use the original conference design: Poppins,
`style-2026.css`, the photo hero, existing button styles, and shared header/footer
includes. `assets/css/chapter.css` adds only chapter-specific layout and archive
formatting; it does not define a separate visual theme.

- `/`: shared landing page
- `/conference.html`: upcoming 2027 conference overview
- `/conference/` and `/2027/`: aliases to the upcoming conference
- `/2026/`: archived 2026 overview and year-specific detail pages
- `/chapter/`: mailing list, meetup information, and ways to participate
- `/chapter/meetups/`: historical meeting records and recordings
- `/chapter/about/`: chapter people and Hebrew resources
- `/conferences/`: annual conference history

Current root agenda, registration, sponsors, and CFP pages are 2027 placeholders.
The old root photo URL redirects to `/2026/photos.html`. 2026 records now live
under `/2026/`; archive layouts, year-specific navigation and relative asset paths follow the
existing 2025 archive pattern. The full 2026 homepage is preserved, with its
own 2026 logo, menu, content sections and footer. The shared menu belongs to
the current chapter/2027 site.
2026 page content is preserved verbatim from the original conference site,
including its original labels, forms, calls to action and photo messages. Only
layout/asset paths and routing change for the year-specific location, as with
2025. Historical 2023 and 2025 sites are unchanged. `current_year` is 2027; upcoming dates and venue are
maintained in `_data/year-2027/config.yml`. The visual design still uses the
existing 2026 stylesheet, independently of the conference's current year.

Chapter content was adapted from OWASP/www-chapter-israel. Keep mailing list,
forms, contacts, and resources in the chapter pages current. Past Meetup links
are retained as historical references; announcements use the mailing list.
Imported meeting and conference records retain the source wording and dates.
Only local navigation links and display formatting are adapted. No editorial
warnings or provenance notes are added to the published chapter pages.
Historical sponsor graphics and stale announcements were not imported.

For a preview under a project URL, build with a base URL:
`bundle exec jekyll build --baseurl /www-event-appsecil`.
Check the landing page, chapter pages, conference overview, and both conference
navigation menus. In particular, verify images and existing root detail links.

### 2027 conference maintenance

The 2027 overview uses `custom-2027`, matching the original 2026 section
structure, photo hero, typography, colors, buttons and gallery. It uses the
shared current-site header and footer. Detail pages use `layout-2027`.
The shared design assets remain in their original paths; reusing them does not
change the archived site's files.

Edit `_data/year-2027/config.yml` for confirmed dates and venue, and
`2027/index.md` for the section copy. Until confirmed, registration, CFP,
sponsorship, agenda and team information remain placeholders. The gallery is
explicitly labelled as 2026 highlights; no 2026 speakers, sponsors, prices,
registration forms or dates are presented as 2027 information.

2025 and 2026 retain year-specific navigation and historical page content.
Changes to the current shared menu should be made in `_data/site-menu.yml`.

### GitHub Pages workflow

`.github/workflows/pages.yml` builds the same site using the Pages Jekyll
builder and current checkout, configuration, artifact-upload and deployment
actions. The upload action uses the Node.js 24-compatible artifact action,
replacing the Node.js 20 dependency in GitHub's generated branch workflow.

To activate it, select **GitHub Actions** as the build source in
**Settings → Pages**. The old **Deploy from a branch** source uses a workflow
maintained by GitHub; repository changes cannot update its action versions.
The workflow runs on pushes to `main` and `feature/chapter-conference-landing`,
and supports manual runs. Configure the `github-pages` environment to allow
the branch being previewed. Once this feature is merged, remove its branch
entry if it should no longer deploy.
