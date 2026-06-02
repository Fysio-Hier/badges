# Fysio-Hier — Test-health badges

Deze **publieke** repo host de [shields.io endpoint](https://shields.io/endpoint)-JSON's voor de
test-health-badges van Fysio-Hier-projecten. De meeste consumer-repos zijn **privé**, waardoor
shields.io / GitHub hun badge-data niet anoniem kunnen ophalen (`raw` van een private repo geeft
404). Door de JSON's hier (publiek) te hosten, renderen de badges wél in de README's van die repos.

> ⚙️ **Auto-gegenereerd — niet handmatig bewerken.** De `<project>/<component>.json`-bestanden worden
> bij elke `push: main` van een consumer geschreven door de centrale reusable workflow
> [`ci-pipeline-test-health-badges`](https://github.com/Fysio-Hier/ai-ops/blob/main/docs/test-health-badges.md)
> in [`ai-ops`](https://github.com/Fysio-Hier/ai-ops). Handmatige wijzigingen worden bij de volgende run overschreven.

Legenda: 🟢 alle tests groen · 🔴 failures · ⚪️ 0 tests / nog niet gemeten · 🟡 run kon niet bepaald worden.
Coverage toont een percentage zodra de runner-image een coverage-driver (pcov) heeft; anders grijs `n/a`.

---

## Aangesloten projecten

### gym-planner

Leden- en lesbeheer (Laravel). Repo: [`Fysio-Hier/fit-hier-gym-planner`](https://github.com/Fysio-Hier/fit-hier-gym-planner) (privé).

**Coverage (hele suite):** ![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/Fysio-Hier/badges/main/gym-planner/coverage.json)

| Onderdeel | Status |
|---|---|
| Recurring payments (Mollie) | ![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/Fysio-Hier/badges/main/gym-planner/mollie.json) |
| Class types | ![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/Fysio-Hier/badges/main/gym-planner/classtype.json) |
| Invoicing | ![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/Fysio-Hier/badges/main/gym-planner/invoicing.json) |
| Auth | ![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/Fysio-Hier/badges/main/gym-planner/auth.json) |
| Bookings | ![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/Fysio-Hier/badges/main/gym-planner/bookings.json) |

---

## Een project aansluiten

1. Voeg in de consumer-repo een wrapper toe die de reusable `-mysql`/base workflow aanroept, met:
   ```yaml
   with:
     badges_repo: Fysio-Hier/badges
     badges_branch: main
     badges_path: <project-naam>      # eigen submap hier
     components: |
       [{ "label": "...", "test_path": "tests/Feature/...", "badge_file": "....json" }]
   ```
2. De ops-app moet op deze repo `contents: write` hebben (org-wide install dekt dat).
3. Voeg dit project hierboven toe aan **Aangesloten projecten** met zijn badge-tabel.

Volledige handleiding: [ai-ops/docs/test-health-badges.md](https://github.com/Fysio-Hier/ai-ops/blob/main/docs/test-health-badges.md).
