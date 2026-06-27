# Changelog

## 2026.06.27 — Clipboard Manager Settings: full-colour clipboard icon (XFCE clipman)

### What Changed

The **Clipboard Manager Settings** entry in XFCE Settings showed a faint white
wireframe instead of a real icon. `xfce4-clipman-settings.desktop` looks up
`Icon=xfce4-clipman-plugin`, and Surfn's `apps/scalable/xfce4-clipman-plugin.svg`
was a symlink to `klipper.svg` — a monochrome symbolic line-icon
(`fill:currentColor`, `.ColorScheme-Text` = `#eff0f1`). On the dark theme that
near-white outline reads as a broken/empty glyph next to the colour icons around it.

Repointed the symlink to `com.github.davidmhewitt.clipped.svg`, Surfn's full-colour
circular clipboard (teal disc, orange clip, white note), so the settings entry now
matches the rest of the grid.

### Technical Details

- Changed in both the deployed tree and the `_src` master so a re-deploy keeps the fix:
  - `usr/share/icons/Surfn/apps/scalable/xfce4-clipman-plugin.svg`
  - `_src/Surfn/scalable/apps/scalable/xfce4-clipman-plugin.svg`
- The panel/tray `status/*/clipman.svg` icons are intentionally monochrome and were
  left untouched — only the apps-context settings icon was wrong.

### Files Modified

- usr/share/icons/Surfn/apps/scalable/xfce4-clipman-plugin.svg (symlink → com.github.davidmhewitt.clipped.svg)
- _src/Surfn/scalable/apps/scalable/xfce4-clipman-plugin.svg (symlink → com.github.davidmhewitt.clipped.svg)

## 2026.06.24 — Settings/System menu categories: restore the colour icons (XFCE)

### What Changed

In the XFCE (Whisker) menu the **Settings** and **System** categories showed the
wrong art — Settings a teal monitor-with-sliders, System a grey monochrome glyph —
instead of Surfn's colour icons (blue cog, green magnifier). The artwork was never
lost; GTK's icon lookup was resolving `preferences-desktop` (Settings) and
`applications-system` (System) to **duplicate copies** that outrank the intended
`categories/scalable` versions:

- `apps/scalable/preferences-desktop.svg` (coloured sliders) and
  `apps/scalable/applications-system.svg` (cyan magnifier) — same name, different
  art, in a directory listed before `categories/scalable`.
- `categories/symbolic/applications-system.svg` (grey glyph) — wins the size tie
  (`Size=16` vs the colour bucket's `Size=48`).
- Breeze-overlaid `preferences/<size>/preferences-desktop.svg` (teal monitor,
  `Type=Fixed`) — an exact pixel-size match beats the `Scalable` colour bucket.

Removing those duplicates leaves a single `categories/scalable` winner per name, so
both categories now show the blue cog and green magnifier.

### Technical Details

- [rearrange.sh](./rearrange.sh): new `prune_shadow_duplicates()` step (in `main()`
  after `make_hidpi`, before `prune_dangling` so any alias left pointing at a removed
  file is swept up as a dead link). Deletes the two `apps/scalable` duplicates, the
  `categories/symbolic/applications-system.svg`, and `preferences/*/preferences-desktop.svg`.
  Regenerated `usr/share/icons/Surfn` + `index.theme` — pruned 6 duplicates.
- Fixed in the generator (not `_src`, not a hand-edit) so it survives every rebuild.
- Verified with a screenless `Gtk.IconTheme` lookup against the regenerated tree:
  `preferences-desktop` and `applications-system` both resolve to
  `categories/scalable/`; the other `applications-*` categories are unchanged.
- Side effect (intended): any launcher using `Icon=preferences-desktop` /
  `Icon=applications-system` now shows the cog / green magnifier consistently.

### Files Modified

- `rearrange.sh` (new `prune_shadow_duplicates` step)
- `usr/share/icons/Surfn/**` (regenerated; 6 shadowing duplicates pruned, `index.theme` rebuilt)

## 2026.06.23 — White `?` for the Kickoff Help category

**Install docs:** the README install section now lists the meta packages (top-level `*-icons-meta`, plus the group meta where applicable) alongside the per-variant `*-icons-git` package — replacing the outdated single `pacman -S` line.

### What Changed

The **Help** category in the Plasma Kickoff menu showed a gray `?` that clashed
with the colorful sibling category icons. Root cause (verified live): the Kickoff
Help group is defined in `plasma-applications.menu` via `kf5-help.directory`, whose
`Icon=help-about-symbolic`. Surfn's own `actions/symbolic/help-about-symbolic.svg`
is a bare `?` hard-coded to gray (`#555555`), rendered literally by Kickoff — so the
glyph showed gray. Recoloured it to pure **white** (`#ffffff`).

Also added (completeness, separate from the visible bug): `applications-help`, the
one `applications-*` category icon base Surfn was missing relative to its siblings —
a bare white `?` for any launcher that requests that name.

### Technical Details

- `help-about-symbolic.svg`: changed the glyph `fill` from `#555555` → `#ffffff`
  (path unchanged). This is the actual fix for the menu — confirmed via
  `kiconfinder6` that the Help category resolves to this file through the active
  theme's `Inherits=Surfn` chain.
- `applications-help.svg`: new bare white `?` (scalable `#ffffff`, symbolic
  `#4d4d4d`), based on the existing Surfn bare-`?` glyph path.
- Edited the published tree and the local `_src` source directly (no regen).
- `check-icons.sh` clean (gtk-update-icon-cache passes).

### Files Modified

- `usr/share/icons/Surfn/actions/symbolic/help-about-symbolic.svg` (gray → white) — the fix
- `usr/share/icons/Surfn/categories/scalable/applications-help.svg` (new, completeness)
- `usr/share/icons/Surfn/categories/symbolic/applications-help.svg` (new, completeness)

## 2026.06.21 — Surfn rebuilt from the Surfing work (context-first layout)

### What Changed

The Surfn theme was replaced with the rearranged, fixed theme developed in the
sister `Surfing` repo — same generator, renamed back to **Surfn**. The old
size-first Surfn theme was removed (backed up separately). Surfn now ships the
Breeze-style context-first layout with all the fixes below, generated by the same
`rearrange.sh`/`check-icons.sh` (kept local, not published).

### Technical Details

- Source snapshot `_src/Surfn` + `rearrange.sh`/`check-icons.sh` copied in
  (gitignored — local only). `rearrange.sh` `OUT` and `index.theme`
  `Name=`/`Comment=` set to **Surfn**; everything else identical to Surfing.
- Regenerated `usr/share/icons/Surfn` (Name=Surfn). `check-icons.sh` clean.
- The dated entries below document each fix as developed under the Surfing name;
  they all apply to this Surfn theme.

## 2026.06.21 — Klipper: use Breeze's clipboard icon (white)

### What Changed

The tray clipboard (Klipper) showed Surfn's brown clipboard — Surfn's
`klipper.svg` is a symlink to `evolution-tasks.svg`. Replaced just the klipper
icon with Breeze's clipboard in the same white/recolorable monochrome as the
other tray icons; `evolution-tasks` is left alone.

### Technical Details

- [rearrange.sh](./rearrange.sh) `overlay_breeze_clipboard()` (after
  `overlay_breeze_status_icons`): replaces each `klipper.svg` (a Surfn symlink →
  `evolution-tasks`) with Breeze's `klipper-symbolic`, recoloured
  `#232629`/`#31363b → #eff0f1` (Breeze's light and dark ColorScheme-Text
  defaults) so it renders white like the other tray icons. Only `klipper` is
  touched. `check-icons.sh` clean.

## 2026.06.21 — White system-tray expander arrow (recolour Surfn arrows)

### What Changed

Plasma's system-tray expander (the ▼) showed Surfn's olive arrow. Breeze ships
no `arrow-*` icons (only `go-down`/`pan-down`), so rather than swap the shape,
recoloured Surfn's whole `arrow-*` family to a white, recolorable monochrome so
it tints with the panel like the volume/brightness icons.

### Technical Details

- [rearrange.sh](./rearrange.sh) `flatten_arrow_icons()` (after
  `make_hamburger_menu`): rewrites Surfn's `actions/**/arrow-*.svg` olive fill
  (`#859900`) to `currentColor` + a `.ColorScheme-Text` light default
  (`#eff0f1`), tagging the paths so KDE recolours them — **32** icons
  (`arrow-up/down/left/right` and `-double`). `check-icons.sh` clean.

## 2026.06.21 — Thunar icon: use the blue file-manager folder

### What Changed

Surfn's `thunar` icon was a purple/yellow folder, out of step with the blue
file-manager folder `Thunar.svg` already used (it links to `nautilus.svg`).
Pointed `thunar` at the same blue icon so every Thunar name matches.

### Technical Details

- [rearrange.sh](./rearrange.sh) `preferred_app_aliases()` (after
  `preferred_place_aliases`): symlinks `apps/<size>/{thunar,Thunar,org.xfce.Thunar}.svg
  → nautilus.svg` (which resolves to the blue `system-file-manager.svg`), matching
  the existing `Thunar.svg → nautilus.svg` convention. `org.xfce.thunar.svg`
  (→ `thunar.svg`) follows automatically. Capital-T variants are aliased
  explicitly since some launchers/.desktop files request that casing and Surfn
  ships only lowercase. Symlink over copy to keep one source of truth.
- `check-icons.sh` clean.

## 2026.06.21 — Ship Breeze battery + network + audio icons (light default)

### What Changed

Relying on `Inherits=` to supply Plasma's tray Networks/Battery/Volume icons
proved unreliable, so they're now shipped as Surfing's own icons. Copied Breeze's
`battery*`, `network*` and `audio-volume*` icons into Surfing and switched their
recolour default to a light tone (Erik runs dark panels/menus, where Breeze's
dark `#232629` default would be near-invisible in any context that doesn't
recolour).

### Technical Details

- [rearrange.sh](./rearrange.sh) `overlay_breeze_status_icons()` (after
  `overlay_breeze_contexts`): copies Breeze `battery*` + `network*` +
  `audio-volume*` from the `status`/`devices`/`actions` contexts (`cp -a`,
  preserving the many alias symlinks) — **1269** icons incl.
  `network-wired-activated`, `battery-000…100` (charging/symbolic/profile),
  `audio-volume-high/-medium/-low/-muted` (± symbolic). `network-workgroup*` is
  skipped to keep Surfn's grey globe. Then rewrites the recolour stylesheet
  default `color:#232629`/`#31363b → #eff0f1` on the real SVGs so they read on dark menus;
  KDE still recolours to the panel text colour.
- `check-icons.sh` clean; perms `0644` (via `normalize_permissions`).

## 2026.06.21 — Inherits: breeze after Numix so Plasma tray icons resolve

### What Changed

On Plasma the system-tray **Networks** and **Power & Battery** icons were blank.
Plasma uses Breeze's granular status names (`network-wired-activated`,
`battery-000…100` with charging/symbolic/profile variants) that Surfn doesn't
ship, so they fall through `Inherits=`. The chain reached breeze too late — a
partial status set earlier in the list shadowed it — so the icons came up empty.
Moved breeze up to just after the two Numix themes, and dropped Sardi.

### Technical Details

- [rearrange.sh](./rearrange.sh) `generate_index_theme()` now emits a curated
  `Inherits=Numix,Numix-Circle,breeze,Paper,Papirus,Moka,gnome,hicolor` (was
  pulled verbatim from Surfn, which buried breeze and included Sardi). Surfing's
  own icons still win over every inherited theme; this only changes which theme
  fills the gaps. `check-icons.sh` clean.

## 2026.06.21 — Stop flattening go-home (Thunar Home was turning dark)

### What Changed

Thunar's "Home" shortcut icon went from white to dark after the nav-flatten
work. Surfn's `go-home` is already a clean white (`#ffffff`) house that GTK shows
correctly on a dark sidebar; flattening it pinned the fill to
`currentColor`/`#4d4d4d`, forcing it dark. Removed `go-home` from the flatten
set so the white original is kept.

### Technical Details

- [rearrange.sh](./rearrange.sh): `go-home` dropped from `NAV_FLAT_ICONS`
  (`flatten_nav_actions`). Back/forward/up/down/reload stay flat + recolorable;
  `go-home` keeps Surfn's white house. `check-icons.sh` clean; perms `0644`.

## 2026.06.21 — Generated icons no longer ship owner-only (0600 → 0644)

### What Changed

`check-icons.sh` flagged 45 nav/menu icons as "not world-readable" — they were
mode `0600`, so the installed theme would be unreadable for other users. Root
cause: every flagged file is one the script *generates* (recoloured nav art,
vertical arrows, hamburger menu), written via `cp` from a `mktemp` temp file —
and `mktemp` creates its temp file `0600`, which `cp` (no `-p`) propagated to
the icon. Copied (`cp -a`) icons were fine because `-a` preserves upstream
`0644`.

### Technical Details

- [rearrange.sh](./rearrange.sh): fixed at the write sites — `flatten_nav_actions`
  and `make_hamburger_menu` now `chmod 644` the `mktemp` temp before `cp`, and
  `derive_vertical_arrows` `chmod 644`s its redirect outputs (redirect mode is
  umask-dependent). Each generated icon is `0644` the moment it's written.
- `normalize_permissions()` (called from `main()` after `generate_index_theme`)
  runs `find "${OUT}" -type f -exec chmod 644 {} +` as a catch-all backstop, so
  any future generation path that forgets the per-site `chmod` still ships
  world-readable. Verified: zero non-`0644` files; `check-icons.sh` clean.

## 2026.06.21 — Match up/down arrow weight to back/forward

### What Changed

After flattening the nav icons, the up arrow looked too thick next to
back/forward — Surfn's symbolic `go-up`/`go-down` are a heavier design than
`go-previous`/`go-next`. Now the vertical arrows are derived by rotating the
thin `go-previous` arrow, so the whole nav family shares one weight.

### Technical Details

- [rearrange.sh](./rearrange.sh) `derive_vertical_arrows()` (after
  `flatten_nav_actions`): builds `go-up` (`rotate(90 8 8)`) and `go-down`
  (`rotate(-90 8 8)`) from the flat `go-previous` across
  `actions/{16,22,24,32,scalable}` (**10** files); `go-up` removed from
  `NAV_FLAT_ICONS` so it's no longer flattened from its heavier symbolic art.
- Rendered + recolor-checked; `check-icons.sh` clean.

## 2026.06.21 — Hamburger menu icon for Dolphin's open-menu button

### What Changed

Dolphin's hamburger (⋮/≡) menu button rendered blank: it requests
`application-menu`, but Surfn ships only a *gear* (`open-menu` and the
`*-symbolic` variants) with no colored `application-menu`, so KDE fell back to
nothing usable. Shipped a proper flat ≡ hamburger so the button keeps its
expected look.

### Technical Details

- [rearrange.sh](./rearrange.sh) `make_hamburger_menu()` (after
  `flatten_nav_actions`): writes a clean three-bar ≡ SVG (fill `currentColor` +
  `.ColorScheme-Text` stylesheet, so KDE recolours it light-on-dark /
  dark-on-light) as `application-menu` **and** `open-menu` across
  `actions/{16,22,24,32,scalable}` (**10** files), replacing the Surfn gear.
- Rendered + recolor-checked with `rsvg-convert`; `check-icons.sh` clean.

## 2026.06.21 — Flat navigation icons in Dolphin (match Thunar)

### What Changed

Plasma/Dolphin's toolbar showed the colored blue-circle navigation icons while
XFCE/Thunar showed flat monochrome arrows — same theme, but the apps pull
different files (GTK uses `actions/symbolic/<n>-symbolic`, KDE the colored
`actions/<size>/<n>`). Made Dolphin match Thunar's flat arrows for the
navigation set (back/forward/up/home/reload), auto-recolored to the toolbar
text colour.

### Technical Details

- [rearrange.sh](./rearrange.sh) `flatten_nav_actions()` (after `repair_osb_svgs`):
  builds each colored nav action icon from the symbolic artwork, converting the
  fill to `currentColor` + a `.ColorScheme-Text` stylesheet so KDE recolours it
  (light on dark, dark on light). Writes to `actions/{16,22,24,32,scalable}`,
  replacing the blue-circle versions. GTK keeps using the untouched symbolic
  icons. Set: `go-previous/next/up/home`, `view-refresh`, `go-previous/next-rtl`
  (**35** files).
- Verified with `rsvg-convert`: flat render in default grey and (simulated)
  light recolor; `check-icons.sh` clean.

## 2026.06.21 — Fix Plasma/GTK rendering: folder aliases + broken symbolic SVGs

### What Changed

Two rendering bugs surfaced after installing on real desktops:

1. **Plasma — Downloads folder rendered in a foreign style** (different colour)
   instead of the Surfn blue. Surfn ships alternate folder names
   (`folder-downloads`, `folder-text`, `folder-image(s)`, `folder-sound(s)`, …)
   only under `scalable/`, so a desktop requesting one at a **fixed pixel size**
   missed and fell through `Inherits=` (Numix first) to a foreign theme.
2. **Thunar (GTK) — back/forward toolbar buttons showed a missing-icon "?"**.
   ~29 Surfn symbolic icons (`go-previous`, `go-next`, `pan-*`, `zoom-*`,
   `media-*`, `open-menu`, …) carry a dead `<linearGradient osb:paint="solid">`
   Inkscape swatch but never declare the `osb:` namespace — so librsvg (used by
   GTK) aborts parsing the **whole file** and the icon disappears.
3. **Plasma sidebar — Network was a plain folder, Recent Files a foreign icon**.
   Dolphin's "Network" uses `folder-network` (Surfn maps it to a plain folder);
   pointed it at the `network-workgroup` globe instead — the same icon XFCE's
   "Browse Network" shows. "Recent Files" uses `document-open-recent` (Surfn
   ships it only as a scalable SVG → fell back at fixed sizes); aliased to
   `folder-recent`, matching "Recent Locations".

All fixed in the generator so regeneration stays reproducible.

### Technical Details

- [rearrange.sh](./rearrange.sh) `propagate_place_aliases()` (after
  `overlay_breeze_contexts`): for each same-directory alias symlink in
  `places/scalable`, recreates it at every fixed size where the target exists —
  `folder-downloads.png → folder-download.png` now lives at 16–128, not just
  `scalable/`. **416** aliases propagated.
- [rearrange.sh](./rearrange.sh) `repair_osb_svgs()` (after
  `overlay_breeze_contexts`): injects
  `xmlns:osb="http://www.openswatchbook.org/uri/2009/osb"` into every SVG that
  uses `osb:` without declaring it. **29** SVGs repaired; afterwards all 190
  symbolic action icons parse (`rsvg-convert` clean, 0 failures).
- [rearrange.sh](./rearrange.sh) `preferred_place_aliases()` (after
  `propagate_place_aliases`): forces specific names to the expected Surfn icon,
  overriding the generic propagation — `folder-network → network-workgroup`
  (globe), `document-open-recent → folder-recent`. **18** aliases applied.
- `index.theme` group count unchanged (aliases/repairs land in already-declared
  directories). `check-icons.sh` clean; `gtk-update-icon-cache` builds.

### Files Modified

- `rearrange.sh` (new `propagate_place_aliases`, `repair_osb_svgs` steps)
- `usr/share/icons/Surfing/**` (regenerated — fixed-size folder aliases, repaired
  symbolic SVGs)

## 2026.06.21 — Initial Surfing theme + repo

### What Changed

Created the **Surfing** icon theme: the Surfn icon set rearranged from its
non-standard size-first, triple-nested layout into a clean **Breeze-style
context-first** layout, with Breeze's `applets` and `preferences` contexts
overlaid so Surfing carries the full Breeze context set. Stood the repo up with
flow scripts and a package recipe.

### Technical Details

- [rearrange.sh](./rearrange.sh) deterministically rebuilds the theme from a
  read-only Surfn source snapshot (`_src/`, gitignored):
  - `<size>/<context>/` → `<context>/<size>/`; `scalable/<context>/{scalable,symbolic}/`
    → `<context>/{scalable,symbolic}/`; flat scalable → `<context>/scalable/`.
  - Whole-context redirect symlinks dropped (the real `<context>/scalable`
    bucket, declared `Type=Scalable`, serves every size).
  - 33 cross-context `../` aliases rewritten to the new paths; per-context `@2x`
    HiDPI symlinks recreated.
  - Breeze `applets` (259 svg) + `preferences` (413 svg) overlaid; 38 dead Breeze
    cross-context aliases pruned (they fall back through `Inherits=`).
  - `index.theme` regenerated from the tree on disk (102 groups) — zero
    declared-but-missing, zero undeclared.
- Verified: 13,013 → 13,013 real files (no icon loss), 0 broken symlinks,
  `gtk-update-icon-cache` builds, `check-icons.sh` reports all themes clean.
- Flow: [setup.sh](./setup.sh) (git remote), [up.sh](./up.sh) (validate via
  check-icons.sh, then commit/push). Package recipe `surfing-icons-git`
  (PKGBUILD + build.sh) lives in `KIRO-PKG-BUILD-ICONS/surfing/`.

### Files Modified

- `rearrange.sh`, `check-icons.sh`, `setup.sh`, `up.sh` (new)
- `usr/share/icons/Surfing/**` (generated theme)
- `README.md`, `CHANGELOG.md`, `.gitignore` (new)
