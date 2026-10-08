# Customer's Canvas — Website Phase 1 prototype

Clickable, responsive **website and customer journey prototype** for the Phase 1 redesign of customerscanvas.com.

**Repository:** Aurigma/website-update

## What is here

- Homepage that presents Customer's Canvas as one connected offering, rather than a Hub-first homepage.
- **Products:** Customer's Canvas Portal (ready-to-configure B2B ordering) and Customer's Canvas Hub (APIs, embedded components and rendering).
- **Solutions:** Print Service Providers, Marketing Services, Software Vendors & Platforms, Business Printing, Direct Mail, Packaging, Large Format and Promotional Products.
- **Capabilities:** Offer Flexible Personalization Flows; Turn Designs into Production-Ready Files; Keep Orders Moving from Intake to Production; Integrate With Your Systems.
- Online Demo entry and Contact Sales paths.
- Interactive **Test a journey** tool in the lower-right corner. Three suggested starting points help reviewers walk through different customer journeys.

The prototype is written in English for the future website. Its product claims are intentionally conservative and should still be validated with Product before publication.

## Run locally

This is a build-free static website:

```sh
python3 -m http.server 8080
```

Open http://localhost:8080. Routes use hash navigation (e.g. `#/solutions/direct-mail`) because this is a portable prototype, **not a final production URL strategy**.

## Smoke tests

```sh
node --check app.js
node tests/smoke.cjs
```

The test checks 19 routes (homepage, 14 product/solution/capability landing pages, 2 index routes and 2 conversion paths), a minimum set of CTAs and the CJM tester.

## Gitea Actions

`.gitea/workflows/prototype.yml` runs checks on push and packages `dist/` as an Actions artifact. It also supports an optional preview deployment webhook. A public website is **not** deployed until a host (for example Coolify) and the webhook have been configured.

A static web server only needs to serve `index.html`, `styles.css` and `app.js` from the same directory.

For Coolify: create a service from this private repository using its `Dockerfile` (Nginx on port 80), then configure its deploy webhook as the repository Actions secret `WEBSITE_PREVIEW_DEPLOY_WEBHOOK`. After the workflow checks and package step succeed, Actions will call that webhook. No production credentials or URL are committed here.

## Safe prototype boundaries

- The Demo and Contact forms are **simulated**. They neither transmit nor save email or customer information.
- The final step in the Demo simulation links to the existing external live demo at `https://portal-public.customerscanvas.com/`.
- Resources, public documentation and Company link to the **existing** customerscanvas.com site and are not rewritten in Phase 1.
- The visual presentation is a testable Phase 1 **concept**, not the final Digital Ink design and not a production-ready CMS theme.
- No live tracking, CRM writes, real lead forms, authentication, payments or redirects.
- For launch: preserve high-value existing URLs, assign production URL mappings, implement accessibility/SEO QA, track demo events and wire forms and leads.

## CJM test scripts

1. **Commercial printer:** Solution / Print Service Providers → Portal → Order Flows and Production Output → Demo → Contact Sales.
2. **Software platform:** Solution / Software Vendors & Platforms → Hub → Integrations → Demo → Contact Sales.
3. **Marketing services:** Solution / Marketing Services → Personalization Flows → Demo.
4. **Direct mail:** Solution / Direct Mail → Hub → File Generation → Demo.
5. **Packaging:** Solution / Packaging → Production Files → Hub or Portal → Contact Sales.

During testing, note any missing context, confusing product distinction, over-promised capability, orphaned route, and unclear CTA. Related tasks live in Plane Marketing `WEB26`.

## Sources

- Internal Phase 1 concept and Product Knowledge Bricks (Capabilities, Line of Business).
- Website landing-page creation guidelines and the existing customerscanvas.com content.

## GitHub Pages preview

Publishing mirror: https://github.com/alexeykozyavkin/website-update

After enabling **Settings → Pages → Deploy from a branch → main → / (root)**, the static prototype is available at:

https://alexeykozyavkin.github.io/website-update/

Gitea (`Aurigma/website-update`) remains the canonical source. This GitHub copy is for browser review; synchronization is currently performed explicitly, not automated. Avoid editing the GitHub mirror independently.
