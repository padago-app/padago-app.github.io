# padago-site

The public website for padago. Plain static files, no build step, served by
GitHub Pages from the root of `main`.

    index.html              the one page: claim and download, then the app's two halves,
                            Notizen and Noten, each a screenshot per feature with its name
                            and one line under it, then the data
    datenschutz/            the privacy policy — its URL is in App Store Connect and in the
                            app's Einstellungen, so it never moves
    anleitung/              the guide, and the Support URL for App Store Connect; one page,
                            chapters down the side
    css/site.css            every page's styles, one file
    screenshots/            the six on the start page

Everything is linked relatively, so the site works at padago.org and at a
github.io sub-path alike. Nothing is loaded from another server — the
Datenschutz page says so, and it has to stay true.

The app itself lives in its own private repository; anything the site borrows
from it (logo, fonts, screenshots) is copied across by hand:

    logo/    from padago/logo/          the three SVGs, favicon-64, icon-180, icon-512
    fonts/   from padago/public/fonts/  IBM Plex Sans 400 and 600, with its OFL licence

The exception is `logo/padago-wordmark-*.svg`, which is drawn here: the mark's
p and g, spelled out to padago on the same circle grid.

## Writing

German as written in Switzerland: ss for ß, «Guillemets», *Lehrperson*,
*Lektion*. Most lines need no address at all; where one does, it is *du*
(«Auf deinem Gerät»). The words for things in the app are the app's own,
down to «Synchronisierung». Each line says what a feature gains a teacher,
not how it works: that is the Anleitung's job.

## Screenshots

The six in `screenshots/` are stand-ins, rendered from the app's test
suite (`test/palettes.sh` in the app repository, light palette), each from
a frame of its `test/preview.html`: «2» the Stundenplan, «3h» the Lektion,
«12» the Stücke, «17» the Anmerkungen, «10v» and «10w» the tools, «11y» the
whiteboard. The pupils there are named out of `test/preview/composers.txt`,
and the Notizen screens are all of one moment, in the middle of a lesson on
a Dienstag. Stücke, Anmerkungen and the tools show a real score, Chrétien's
«Sérénade sous Bois», kept in `test/preview/` there with the markings drawn
on it on an iPad (the file the app saved); the rest of that library is
placeholders, the pupil's other pieces with covers drawn after Bärenreiter's
and Henle's by `test/preview/covers.mjs`, colours and layout only, no name
or mark of theirs. The whiteboard is D-Dur and h-Moll, written by
`test/preview/scales.mjs`. Each is the frame's 760×1010 iframe, cut out of
the shot at +14+44:

    magick 17____Anmerkungen-light.png -crop 760x1010+14+44 +repage -quality 85 screenshots/anmerkungen.webp

The real ones come from an iPad:
portrait, **light theme**, real music. The light screens stand apart from
the page's own white on black; a dark one would read as more of the page.

The page crops each screen to 4:5 from the top and fades the last of it
into the black behind its caption, so what a screenshot is about has to be
in the upper three quarters or so of the screen. Where it is lower, `--at`
on the `<img>` moves the crop down (`style="--at: 75%"`).

Bring each down to 1200 px wide and write it over its stand-in:

    magick IMG_0001.PNG -resize 1200x -quality 85 screenshots/lektion.webp

then set the `width` and `height` on its `<img>` in `index.html` to the new
size, which keeps the page from jumping while it loads.

The tools are one picture made of two screens, since the app opens one
panel at a time: the left half of a screen with the Stimmgerät open, which
stands at the left, and the right half of one with the Metronom open, at
the right, over the same page of the same score. The stand-in's frames are
840×1050, the shape the page crops to, and wide enough that each panel ends
short of the middle:

    OUT=shots ./test/palettes.sh "10v ·" "10w ·"
    magick \( shots/10v-light.png -crop 420x1050+14+44 +repage \) \
      \( shots/10w-light.png -crop 420x1050+434+44 +repage \) \
      +append -quality 85 screenshots/werkzeuge.webp

From an iPad the same, both screenshots cut to 4:5 from the foot of the
screen, where the panels are, and joined at the middle (here for one of
1640×2360):

    magick \( IMG_0002.PNG -gravity south -crop 1640x2050+0+0 +repage \
              -gravity northwest -crop 820x2050+0+0 +repage \) \
      \( IMG_0003.PNG -gravity south -crop 1640x2050+0+0 +repage \
              -gravity northwest -crop 820x2050+820+0 +repage \) \
      +append -resize 1200x -quality 85 screenshots/werkzeuge.webp

## App Store

Until the app is live, the start page says «Bald im App Store» in a plain
outline. Apple's badge is only for apps that can be downloaded; once it can,
replace the outline with the German badge («Laden im App Store», the black
one) from Apple's marketing tools, linked to the app's page.

## Preview locally

    python3 -m http.server 8000

`.nojekyll` stops GitHub Pages running the files through Jekyll.
