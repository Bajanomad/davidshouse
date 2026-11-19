# David's House

David's whole web presence in one repo, built the night of
Nov 18/19 2026 when he ordered the OurSpace demo turned into the
live site. Hosted on GitHub Pages.

## Layout
- `/index.html` — the front door: David's glyph wheel on the
  OurSpace space background, blue instead of orange, hacker
  branding retired. Center button opens OurSpace (a room inside
  this repo). Orbit doors: crown = GitHub, K = his Facebook,
  bars = Vercel. Flag, house and bowtie doors are unwired.
- `/ourspace/` — OurSpace, the closed little network for his
  circle (Section 13 team plus Miles and Scott, invite only,
  about 50 people max, ever). One standard template, 12 themes,
  username + password accounts (no email), an admin panel for
  David, and a gate that opens on the COOL bar (sign-in exists
  but is not required yet, by his order).
- `/ourspace/profile.html?id=<member>` — a real standalone
  profile page per person, same design, reads and writes the
  same shared data.
- `/ourspace/config.js` — the database connection (Supabase
  project URL + public anon key). Empty means local-only mode.

## The database
Supabase (free tier). David's account was already at the free
plan limit of two projects ("411 Apps" and "Bajanomad's
Project", both left untouched), so OurSpace lives as its own
table, `ourspace_state`, inside the existing "411 Apps"
project. It holds a single JSON document with the shared slices of the app
state: posts, walls, edits, accounts, custom members, deleted
ids. Every device reads it on load and re-checks every 30
seconds; every change is pushed back within about a second.
Which member you are acting as stays on your own device.
A public storage bucket, `pics`, is reserved for picture
uploads. Security is demo grade on purpose for now (open
policies, passwords in the shared doc): David ordered the real
security phase separately, later.

## Decisions
- v8 of the OurSpace demo is the design keeper; this repo's app
  is that build plus accounts, admin, and the database sync.
- All music is off OurSpace for now; embedded YouTube players
  come later.
- The old 411 / Clandestino site on Vercel is a closed chapter
  and is not part of this repo.
