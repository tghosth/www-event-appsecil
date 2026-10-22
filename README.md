# AppSec-Israel

Jekyll repo for hosting the website for AppSec Israel Conference.   
Viewable live at https://appsecil.org/ . 

### Contributing
Feel free to contribute anything that will improve the Conference site via PR - especially design :-)   
- If you're not familiar with Jekyll: https://jekyllrb.com/docs/home/  
- Jekyll tips: http://cheat.jekyll.tips/

### 2026 photo album

The album page is `2026/photos.md`, published at `/photos.html` (linked as
`./photos`, following the other 2026 pages). It shows a coming-soon message
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

Open `http://127.0.0.1:4000/photos.html`. The preview rebuilds when files change;
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
equal prominence. Chapter pages use `_layouts/chapter.html` and
`assets/css/chapter.css`, independently of yearly conference layouts.

- `/`: shared landing page
- `/conference.html`: existing 2026 conference overview
- `/conference/` and `/2026/`: aliases to the conference overview
- `/chapter/`: mailing list, meetup information, and ways to participate
- `/chapter/meetups/`: historical meeting records and recordings
- `/chapter/about/`: chapter people and Hebrew resources
- `/conferences/`: annual conference history

Existing root conference detail URLs (registration, agenda, sponsors, photos,
and code of conduct) are preserved. Conference navigation anchors now point
explicitly to the conference overview. Historical 2023 and 2025 sites are unchanged.

Chapter content was adapted from OWASP/www-chapter-israel. Keep mailing list,
forms, contacts, and resources in the chapter pages current. Past Meetup links
are retained as historical references; announcements use the mailing list.
Legacy meeting conflicts are preserved with an archive note. The invalid
“May 26–39, 2019” conference date is shown as “May 2019” pending verification.
Historical sponsor graphics and stale announcements were not imported.

For a preview under a project URL, build with a base URL:
`bundle exec jekyll build --baseurl /www-event-appsecil`.
Check the landing page, chapter pages, conference overview, and both conference
navigation menus. In particular, verify images and existing root detail links.
