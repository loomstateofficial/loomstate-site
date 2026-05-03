# Loomstate site

Static landing site for Loomstate, the solo-operator agent-ops audit service. Single purpose right now: satisfy Stripe's website requirement for the Founder Agent-Ops Audit Payment Link, and give cold-DM recipients a public reference page for the offer.

## Files

- `index.html` &mdash; landing page (offer, deliverables, pricing, contact, honest risks).
- `terms.html` &mdash; Terms of Service.
- `privacy.html` &mdash; Privacy Policy.
- `refund.html` &mdash; Refund Policy (tiered: pre-kickoff / post-kickoff / post-delivery).
- `404.html` &mdash; not-found page.
- `robots.txt` &mdash; allow indexing.

(No `CNAME` file is included; create one only when you've purchased a custom domain &mdash; an empty `CNAME` will break GitHub Pages.)

No JS, no analytics, no external CDN. Plain HTML + inline CSS so Stripe's website review can fingerprint it instantly and so the page loads under 100 ms.

## Deploy to GitHub Pages (free)

1. Create a new public GitHub repo. Suggested name: `loomstate-site`.
2. Copy this folder's contents to the repo root and push to `main`.
   ```
   cd loomstate-site
   git init
   git remote add origin git@github.com:<your-user>/loomstate-site.git
   git add .
   git commit -m "Loomstate site v1 (R27.709 scaffold)"
   git branch -M main
   git push -u origin main
   ```
3. In the repo on GitHub: **Settings &rarr; Pages**.
4. Set **Source** = `Deploy from a branch`, **Branch** = `main`, folder = `/ (root)`. Save.
5. Wait 1&ndash;3 minutes. GitHub will publish at `https://<your-user>.github.io/loomstate-site/`.
6. Open that URL and confirm the four pages render and the contact mailto opens.

That URL is what you give Stripe in the website field during onboarding.

## Connect a custom domain (optional, later)

Stripe accepts the `github.io` subdomain &mdash; you don't need a custom domain to launch. When you do buy one (e.g., `loomstate.so`):

1. Edit the `CNAME` file: replace its contents with the bare domain, e.g. `loomstate.so`. Commit and push.
2. At the registrar, set DNS:
   - For an apex domain: four `A` records pointing to GitHub Pages IPs (`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`).
   - For a subdomain (e.g. `www.loomstate.so`): a `CNAME` record pointing to `<your-user>.github.io.`
3. Back in **Settings &rarr; Pages**, enter the custom domain and tick **Enforce HTTPS** once the certificate provisions.

## Stripe onboarding checklist

When you create the Stripe account for Loomstate:

- **Business type**: Individual / sole proprietor (unless you've registered an LLC).
- **Business website**: the GitHub Pages URL (or custom domain) from above.
- **Industry / category**: Professional services &mdash; consulting / IT services.
- **Statement descriptor**: `LOOMSTATE` (max 22 chars).
- **Description of products/services**: paste the first paragraph of `index.html`.
- **Pricing**: USD 750 flat per engagement, single-purchase (not subscription).
- **Refund policy URL**: link to `refund.html` on the live site.
- **Terms URL**: link to `terms.html`.
- **Privacy URL**: link to `privacy.html`.

After approval, create one **Payment Link** in Stripe for "Founder Agent-Ops Audit &mdash; USD 750", set fulfilment to manual, and save the link URL. That URL goes into the kickoff-call email template you send paying clients &mdash; not on the public site.

## Editing

Plain HTML &mdash; open in any editor and edit the markup. Keep the inline CSS in sync across pages (the four files share the same `:root` palette and structural rules).

If the offer changes, update both this site and the canonical scope doc at `ai-security-platform/.ai/revenue/productized-service-offers/founder-agent-ops-audit-scope-v2.md` so they stay aligned.
