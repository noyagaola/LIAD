# LIAD migration plan

## Safety rules

- `main` preserves the original static site.
- The tag `backup/original-2026-11-07` identifies the untouched imported baseline.
- React migration work happens only on `migration/react-tailwind-foundation` until it is reviewed.
- Each completed milestone receives a Git tag and is pushed to GitHub before the next milestone starts.

## Confirmed first-release scope

- Product catalogue, product pages, cart and wishlist remain available.
- Courses are enquiry-only: the primary call to action opens WhatsApp or collects contact details.
- No payment, checkout, account registration, database, inventory sync, CRM integration or admin panel is included in this release.
- The future architecture must allow those systems to be added without rebuilding the public site.

## Problems in the imported site

1. The source has no React project, package manifest, build pipeline or automated validation.
2. The active site is split between root redirect pages, `original/`, and `liad-shop/`; ownership of the active version is unclear.
3. Styling is spread across many overlapping files (`v2` through `v5`, `overrides`, and several page-specific systems), producing conflicts and inconsistent design.
4. Product, course and article data are embedded in browser JavaScript instead of typed, reusable application data.
5. Several navigation links reference an old GitHub Pages deployment and will break outside that domain.
6. Contact and content routing mixes pathname and hash logic, so some routes cannot be reached as written.
7. Cart and favourites rely only on local browser storage. This is acceptable for the temporary catalogue but must be made deliberate and tested.
8. The current checkout is an email-request flow. It should be replaced by an explicit, non-payment enquiry path until payments are introduced.

## Migration sequence

1. Create a Vite React TypeScript project with Tailwind CSS, ESLint and a testable build command.
2. Preserve all approved brand assets in a clear asset library; remove duplicate page copies only after visual verification.
3. Convert catalogue, courses and editorial content to typed local data modules. Do not change prices or product content during conversion.
4. Build one reusable RTL application shell: typography, colours, spacing, buttons, navigation, footer, cards and motion rules.
5. Rebuild the public routes: home, catalogue, product, courses, course detail, journal, contact and legal information.
6. Rebuild cart and favourites with a single client-side store; make the non-payment checkout an enquiry flow.
7. Add WhatsApp course enquiry actions and a contact form boundary that can later submit to a CRM/database.
8. Run desktop and mobile visual review, keyboard navigation checks, route checks and production build validation.
9. Tag the reviewed React baseline before any Lovable-led design work.

## Lovable workflow

Lovable may be used for design exploration after the React/Tailwind baseline exists. GitHub remains the source of truth: Lovable changes must return through a dedicated branch, be reviewed, validated locally and tagged before merging. Never overwrite `main` from Lovable directly.

## Deferred systems

- Database and inventory source of truth.
- LIAD lead/opportunity management sync.
- Admin panel for Liad.
- Payment provider, invoices, order lifecycle and shipping integration.
- Customer accounts and course access.

