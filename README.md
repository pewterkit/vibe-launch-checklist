# vibe-launch-checklist

A pre-launch checklist for apps built with AI app builders (Lovable, Bolt, Replit, v0, Cursor). Each item is one thing to confirm on your live site before you share the link, with a guide that explains the check and the fix.

Copy this file into your repo, or open an issue in your own project with it, and tick items off as you go.

## Security

- [ ] No Stripe secret or restricted key (`sk_live_`, `rk_live_`) in the JavaScript your site ships. [Guide](https://pewterkit.com/guides/stripe-secret-key-exposed)
- [ ] No OpenAI API key in browser code; OpenAI calls go through your own server function. [Guide](https://pewterkit.com/guides/openai-api-key-exposed-frontend)
- [ ] No Supabase `service_role` key in the frontend; the browser uses the publishable or `anon` key. [Guide](https://pewterkit.com/guides/supabase-service-role-key-frontend)
- [ ] Source maps (`.map` files) are not served on the live site. [Guide](https://pewterkit.com/guides/source-maps-in-production)
- [ ] `Strict-Transport-Security` header is sent on HTTPS responses. [Guide](https://pewterkit.com/guides/hsts-header-missing)
- [ ] Framing is restricted with `Content-Security-Policy: frame-ancestors` (plus `X-Frame-Options`). [Guide](https://pewterkit.com/guides/x-frame-options-frame-ancestors)
- [ ] `X-Content-Type-Options: nosniff` is set. [Guide](https://pewterkit.com/guides/x-content-type-options-nosniff)

## Payments

- [ ] The live site uses Stripe live keys (`pk_live_`), not `pk_test_`, and live-mode prices, Payment Links and webhooks. [Guide](https://pewterkit.com/guides/stripe-test-mode-live-site)
- [ ] Checkout `success_url` and `cancel_url` point at your live domain, not `localhost` or a preview address. [Guide](https://pewterkit.com/guides/stripe-success-url-localhost)

## Sign-in

- [ ] Supabase Site URL is your production domain, and your `redirectTo` URLs are on the Redirect URLs list. [Guide](https://pewterkit.com/guides/supabase-google-oauth-redirects-to-localhost)
- [ ] Google's sign-in screen names your domain, not `*.firebaseapp.com` or `*.supabase.co`. Guides: [Firebase](https://pewterkit.com/guides/change-firebase-authdomain), [Supabase](https://pewterkit.com/guides/supabase-google-sign-in-custom-domain)
- [ ] Every domain your app signs in from is on Firebase's Authorized domains list. [Guide](https://pewterkit.com/guides/firebase-authorized-domains)
- [ ] Your Google OAuth app is published "In production", not left in Testing. [Guide](https://pewterkit.com/guides/app-has-not-completed-google-verification)

## Email & domain

- [ ] One SPF record at the root of your domain, ending in `~all`. [Guide](https://pewterkit.com/guides/spf-record-missing)
- [ ] A DMARC record at `_dmarc.yourdomain.com`, starting with `p=none`. [Guide](https://pewterkit.com/guides/dmarc-record-missing)
- [ ] `http://` redirects to `https://`. [Guide](https://pewterkit.com/guides/http-to-https-redirect)
- [ ] Both `yourdomain.com` and `www.yourdomain.com` resolve, and one redirects to the other. [Guide](https://pewterkit.com/guides/www-not-working)
- [ ] Domain auto-renew is on and the expiry date isn't close. [Guide](https://pewterkit.com/guides/domain-expiry-auto-renew)
- [ ] Your HTTPS certificate is renewing automatically. [Guide](https://pewterkit.com/guides/ssl-certificate-expiry)

## Privacy, rules & accessibility

- [ ] A privacy policy is linked from the homepage, with an effective date and a Do Not Track statement (US). [Guide](https://pewterkit.com/guides/privacy-policy-for-app-us)
- [ ] Ad pixels and other non-exempt trackers wait for consent from UK and EU visitors. [Guide](https://pewterkit.com/guides/cookie-banner-before-trackers)
- [ ] Sites running ad pixels have a "Do Not Sell or Share" or "Your Privacy Choices" link (US). [Guide](https://pewterkit.com/guides/do-not-sell-or-share-link)
- [ ] Subscriptions show auto-renew terms before payment and offer online cancellation (US). [Guide](https://pewterkit.com/guides/subscription-auto-renew-disclosure)
- [ ] Every meaningful image has `alt` text; decorative images use `alt=""`. [Guide](https://pewterkit.com/guides/image-alt-text-missing)
- [ ] Every form field has a label. [Guide](https://pewterkit.com/guides/form-elements-must-have-labels)
- [ ] Icon-only buttons and links have an accessible name. [Guide](https://pewterkit.com/guides/buttons-must-have-discernible-text)

## Search & launch day

- [ ] The page title is your product, not "Lovable App" or "Vite + React". [Guide](https://pewterkit.com/guides/page-title-still-lovable-app)
- [ ] The meta description is your own, not a template default. [Guide](https://pewterkit.com/guides/meta-description-missing)
- [ ] The favicon is your icon, not `/vite.svg` or the builder's default. [Guide](https://pewterkit.com/guides/default-vite-favicon)
- [ ] Shared links show your own `og:image`, title and description. [Guide](https://pewterkit.com/guides/og-image-link-preview-not-showing)
- [ ] No `noindex` meta tag, `X-Robots-Tag: noindex` or `Disallow: /` on production. [Guide](https://pewterkit.com/guides/noindex-left-on)
- [ ] A `sitemap.xml` with absolute URLs on your own domain. [Guide](https://pewterkit.com/guides/sitemap-xml-missing)
- [ ] The canonical URL points at your domain, not `*.lovable.app` or `*.vercel.app`. [Guide](https://pewterkit.com/guides/canonical-points-to-lovable-app)
- [ ] Deep links such as `/pricing` load when opened or refreshed directly (no 404). [Guide](https://pewterkit.com/guides/spa-refresh-404)

## How to check automatically

Most items can be checked by hand in a minute with browser developer tools, `curl` or `dig`; each guide shows how.

To run many of them at once, [Pewterkit](https://pewterkit.com) has a free check: paste your live URL and it reads public information only (your homepage, the scripts it loads, response headers and DNS records), then lists what it found with the line, header or record behind each finding. Disclosure: this checklist is maintained by Pewterkit, which also sells filled-in fixes; nothing in this list requires them.

## Contributing

Issues and pull requests are welcome. For a new item, please:

- keep it to one line that says what "done" looks like on the live site;
- link a public source (official docs or a guide) that explains the check and the fix;
- avoid claims about how often a problem occurs unless you can link the data.

## License

Content: CC BY 4.0. Share and adapt with attribution.
