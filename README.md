<h1 align="center">
  <img src="kiro.jpg" alt="Kiro" width="220" />
  <br />
  Surfn
</h1>

![Last-Commit](https://img.shields.io/github/last-commit/erikdubois/surfn?style=for-the-badge)

<img alt="GitHub followers" src="https://img.shields.io/github/followers/erikdubois?style=flat">&nbsp;&nbsp;<img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/erikdubois/surfn">&nbsp;&nbsp;<img alt="GitHub forks" src="https://img.shields.io/github/forks/erikdubois/surfn">

<img alt="YouTube Channel Subscribers" src="https://img.shields.io/youtube/channel/subscribers/UCJdmdUp5BrsWsYVQUylCMLg">&nbsp;&nbsp;<img alt="YouTube Channel Views" src="https://img.shields.io/youtube/channel/views/UCJdmdUp5BrsWsYVQUylCMLg">

---

**Surfn** is a colourful flat icon theme. It started as a blend of four icon sets — Ultra Flat,
Super Flat Remix, Yltra Flat and Numix (Circle) — with many icons reworked to personal taste.
The name comes from rearranging the letters of its original name, **S**uper **U**ltra **F**lat
**N**umix **R**emix → *SUFNR* → **Surfn** (pronounced *surfing*).

This is the **base** theme. Every other Surfn theme ships only its recoloured folders and inherits
all remaining icons from here, so the base `surfn-icons-git` is required by all of them.

## Installation (Arch / Kiro — nemesis_repo)

```bash
# Everything — the whole Surfn collection (base + all variants)
sudo pacman -S surfn-icons-meta

# Just the base Surfn icon set
sudo pacman -S surfn-icons-git
```

## Manual

Copy `usr/share/icons/Surfn` into `~/.icons` (or `~/.local/share/icons` on Plasma),
then select **Surfn** in your appearance settings.

## How it is managed

`Surfn` is the main icon set; all variants inherit their icons from it. A variant only overrides
folder colours (and the odd accent), so fixing an app icon here fixes it across the whole family —
and it keeps every variant small instead of duplicating thousands of icons.

## Variants

Each variant is its own package and pulls in `surfn-icons-git` automatically:

| Variant | Package |
|---------|---------|
| [Surfn Arc](https://github.com/erikdubois/surfn-arc) | `surfn-arc-icons-git` |
| [Surfn Arc Breeze](https://github.com/erikdubois/surfn-arc-breeze) | `surfn-arc-breeze-icons-git` |
| [Surfn Arch Blue](https://github.com/erikdubois/surfn-arch-blue) | `surfn-arch-blue-icons-git` |
| [Surfn Breeze Arc](https://github.com/erikdubois/surfn-breeze-arc) | `surfn-breeze-arc-icons-git` |
| [Surfn Breeze Dark](https://github.com/erikdubois/surfn-breeze-dark) | `surfn-breeze-dark-icons-git` |
| [Surfn Dracul](https://github.com/erikdubois/surfn-dracul) | `surfn-dracul-icons-git` |
| [Surfn Luv](https://github.com/erikdubois/surfn-luv) | `surfn-luv-icons-git` |
| [Surfn Luv Red](https://github.com/erikdubois/surfn-luv-red) | `surfn-luv-red-icons-git` |
| [Surfn Majestic](https://github.com/erikdubois/surfn-majestic) | `surfn-majestic-icons-git` |
| [Surfn Mint-X-Grey](https://github.com/erikdubois/surfn-mint-x-grey) | `surfn-mint-x-grey-icons-git` |
| [Surfn Numix](https://github.com/erikdubois/surfn-numix) | `surfn-numix-icons-git` |
| [Surfn Numix Misty](https://github.com/erikdubois/surfn-numix-misty) | `surfn-numix-misty-icons-git` |
| [Surfn Numix Polo](https://github.com/erikdubois/surfn-numix-polo) | `surfn-numix-polo-icons-git` |
| [Surfn Numixs](https://github.com/erikdubois/surfn-numixs) | `surfn-numixs-icons-git` |
| [Surfn Orange](https://github.com/erikdubois/surfn-orange) | `surfn-orange-icons-git` |
| [Surfn Papirus Blue](https://github.com/erikdubois/surfn-papirus-blue) | `surfn-papirus-blue-icons-git` |
| [Surfn Papirus Casablanca](https://github.com/erikdubois/surfn-papirus-casablanca) | `surfn-papirus-casablanca-icons-git` |
| [Surfn Papirus Grey](https://github.com/erikdubois/surfn-papirus-grey) | `surfn-papirus-grey-icons-git` |
| [Surfn Plasma Dark](https://github.com/erikdubois/surfn-plasma-dark) | `surfn-plasma-dark-icons-git` |
| [Surfn Plasma Dark Breeze](https://github.com/erikdubois/surfn-plasma-dark-breeze) | `surfn-plasma-dark-breeze-icons-git` |
| [Surfn Plasma Dark Qogir](https://github.com/erikdubois/surfn-plasma-dark-qogir) | `surfn-plasma-dark-qogir-icons-git` |
| [Surfn Plasma Flow](https://github.com/erikdubois/surfn-plasma-flow) | `surfn-plasma-flow-git` |
| [Surfn Plasma Light](https://github.com/erikdubois/surfn-plasma-light) | `surfn-plasma-light-icons-git` |
| [Surfn Qogir](https://github.com/erikdubois/surfn-qogir) | `surfn-qogir-icons-git` |
| [Surfn Tela](https://github.com/erikdubois/surfn-tela) | `surfn-tela-icons-git` |
| [Surfn Vertexed](https://github.com/erikdubois/surfn-vertexed) | `surfn-vertexed-icons-git` |
| [Surfn Vimix Black](https://github.com/erikdubois/surfn-vimix-black) | `surfn-vimix-black-icons-git` |

## License

[LICENSE](./LICENSE) — Attribution-NonCommercial-ShareAlike 4.0 International.
