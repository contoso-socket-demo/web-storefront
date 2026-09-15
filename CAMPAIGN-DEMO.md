# Why this repo declares seven malicious packages

This repo exists to make the **Threat Intel → Campaigns** page show real
impact. Without it every campaign reads "Not detected" with N/A impact,
which is a weak look on the page that showcases Socket's threat research.

## Every one of them is inert

All seven have **already been removed from npm** and return 404, verified
2026-09-15 immediately before committing:

| Package | Campaign |
|---|---|
| `tailwindcss-contact-forms@0.5.6` | **[5] Contagious Interview** and **[29] PolinRider** |
| `tailwind-form-kit@0.6.4` | [5] Contagious Interview |
| `hardhat-base@2.2.2` | [5] Contagious Interview |
| `pinochiomathm@2.3.5` | [5] Contagious Interview |
| `@antv/f2-vue@4.1.33` | [22] Mini Shai-Hulud |
| `@servicetitan/eslint-config@38.1.6` | [33] keyv and cacheable compromise |
| `bpm-foundation-app-configs@35.9.4` | [34] Flooding Dropper |

`npm install` physically cannot fetch any of them, which is the only reason
this is acceptable in a **public** repo. Declaring a *live* malicious
package here would compromise anyone who cloned and installed.

Campaign detection still works because the badge is a live Postgres
intersection of campaign IOC artifact IDs against current head SBOMs, and it
applies **no `removed_at` filter** — unpublished versions remain valid IOCs.

## How the badge actually works, which matters when demoing

- **Current heads only.** Default branch, latest scan. Remediate and rescan
  and the badge correctly flips back to Not detected.
- **It never consults firewall telemetry or the Alerts page.** A firewall
  block does not light up a campaign. Only a package present in a scanned
  manifest does. This is what bit a customer who ran their firewall in a
  separate Socket org and expected campaign impact to appear.
- **No history.** You cannot retroactively prove what the badge showed on a
  past date.

## The story to tell

The odd mix of packages is not arbitrary, and it is the best part of this
demo. **North Korea's Contagious Interview campaign** works by having
operators pose as recruiters and hand a developer a take-home coding
assignment whose dependencies are malicious. A victim's `package.json` ends
up looking exactly like this: plausible-sounding Tailwind helpers, a charting
library, a Hardhat plugin, all pulled in to complete a fake interview task.

So the narrative is: *a developer took a coding test, and this is what landed
in our storefront.* Then pivot to the campaign page and show it is not one
bad package but a tracked, ongoing operation with thousands of linked
artifacts.

## If a badge stops showing impact

The version may have been relinked or the campaign retired. Re-pick an IOC:

1. `GET /v1/orgs/contoso/threat-campaigns?per_page=100` for the campaign list
2. `GET /v1/orgs/contoso/threat-campaigns/{id}/packages?per_page=1000` for purls
3. Keep only versions that return **404** on the npm registry
4. Add to `package.json`, push to `main`, wait for the App scan

Needs the `threat-campaigns:list` token scope.
