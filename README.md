# Kembali Basah

> **Concept project.** Kembali Basah is a fictional peatland restoration foundation, built by [Aftar Fadilah](https://aftarfadilah.com) as a frontend case study. It is not a real organisation, takes no donations, and is not affiliated with any real foundation, agency or company.

*Kembali basah* means "wet again". Peat burns when it is dry and mostly does not when it is wet, so the name is the intervention: block the drainage canals, keep the water in the ground.

**Gambut basah, api padam.** · Keep the peat wet. Keep the fire out.

## What's here

| | |
|---|---|
| [`docs/brand-profile.md`](docs/brand-profile.md) | Idea, mission, programmes, audiences, personality, voice, trust rules |
| [`docs/design-guidelines.md`](docs/design-guidelines.md) | Colour (with computed contrast), type, logo, layout, motion, components, accessibility, performance budget, i18n |
| [`src/styles/tokens.css`](src/styles/tokens.css) | Design tokens, light and dark |
| [`design/index.html`](design/index.html) | Static concept page of the visual direction (open in a browser; uses the tokens) |
| [`public/brand/logo-mark.svg`](public/brand/logo-mark.svg) | The mark |

## Plan

1. Brand profile and design guidelines (this PR)
2. Next.js scaffold, tokens, fonts, Indonesian and English routing, CI with Lighthouse budgets
3. Home page and the Rewet interaction, built on real NASA FIRMS (VIIRS S-NPP) detections
4. Fire Watch page with an accessible table alternative to the map
5. Deploy to `kembali-basah.aftarfadilah.com`

## Working agreement

- Work happens on a branch and lands through a pull request.
- Pull requests are **squash-merged**, so `main` has one clean commit per change. The PR title becomes the commit message, so write it as one.
