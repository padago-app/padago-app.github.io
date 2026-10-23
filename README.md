# padago-site

The public website for padago. Plain static files, no build step, served by
GitHub Pages from the root of `main`.

The app itself lives in its own private repository; anything the site borrows
from it (logo, fonts, screenshots) is copied across by hand.

Preview locally:

    python3 -m http.server 8000

`.nojekyll` stops GitHub Pages running the files through Jekyll.
