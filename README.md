# padago-site

The public website for padago. Plain static files, no build step, served by
GitHub Pages from the root of `main`.

The app itself lives in its own private repository; anything the site borrows
from it (logo, fonts, screenshots) is copied across by hand:

    logo/    from padago/logo/          the three SVGs, favicon-64, icon-180, icon-512
    fonts/   from padago/public/fonts/  IBM Plex Sans 400 and 600, with its OFL licence

The exception is `logo/padago-wordmark-*.svg`, which is drawn here: the mark's
p and g, spelled out to padago on the same circle grid.

Preview locally:

    python3 -m http.server 8000

`.nojekyll` stops GitHub Pages running the files through Jekyll.
