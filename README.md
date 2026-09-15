# web-storefront

Contoso customer-facing storefront. Vue 3, Vite, Tailwind.

## What this repo demos

The **Threat Intel → Campaigns** page. It declares seven packages that are
linked IOCs across five tracked campaigns, so the page shows real impact
instead of "Not detected" on every row.

| Campaign | Lit by |
|---|---|
| [5] North Korea's Contagious Interview | `hardhat-base`, `pinochiomathm`, `tailwind-form-kit`, `tailwindcss-contact-forms` |
| [29] PolinRider | `tailwindcss-contact-forms@0.5.6` |
| [22] Mini Shai-Hulud | `@antv/f2-vue@4.1.33` |
| [33] keyv and cacheable compromise | `@servicetitan/eslint-config@38.1.6` |
| [34] Flooding Dropper | `bpm-foundation-app-configs@35.9.4` |

Every one has **already been removed from npm** (404), so `npm install`
cannot fetch them and nothing can be compromised. Campaign detection still
works because the badge applies no `removed_at` filter.

Rationale, mechanics and the talk track: **[CAMPAIGN-DEMO.md](CAMPAIGN-DEMO.md)**.

`npm install` in this repo **will fail**. That is expected. Nothing in CI
runs it: the Socket CLI uploads manifests rather than installing them.

## Required secrets

- `SOCKET_SECURITY_API_TOKEN`
