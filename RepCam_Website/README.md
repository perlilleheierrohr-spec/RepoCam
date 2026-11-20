# RepCam website + launch checklist

Static site: landing page, `/privacy/`, `/terms/`, `/support/`. No build step, no cookies, no tracking.

## 1. Domain
The App Store already has an app called **RepCam** (by Carson Tyler), so the App Store name must be different,
e.g. **"RepCam: AI Rep Counter"**. Pick a domain that is free, e.g. `repcam.app`, `getrepcam.com`, `repcamapp.com`.
Buy it at Domeneshop, Cloudflare or Namecheap (~150–300 kr/year).

## 2. Host it free on GitHub Pages
1. Create a public repo `repcam-site` on github.com (account perlilleheierrohr-spec).
2. Upload everything in this folder (drag and drop on github.com works).
3. Repo › Settings › Pages › Source: *Deploy from a branch*, branch `main`, folder `/ (root)`.
4. Custom domain: type your domain (e.g. `repcam.app`) and save. Tick *Enforce HTTPS* once it is offered.
5. At your domain shop, add DNS records:
   - `A` @ → 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153
   - `CNAME` www → `perlilleheierrohr-spec.github.io`
6. Wait 10 min – a few hours. Check `https://<domain>/privacy/` loads.

## 3. Point the app at the domain
`RepCam/Services/AppLinks.swift` → change `site` to your domain. Everything else follows.

## 4. App Store Connect
**Subscriptions** (Features › Subscriptions), one group "RepCam Pro":
| Product ID | Duration | Price (Norway base) | Offer |
|---|---|---|---|
| com.perhansen.repcam.pro.yearly | 1 year | 349 kr | Introductory offer: free, 3 days, new subscribers |
| com.perhansen.repcam.pro.weekly | 1 week | 59 kr | – |

Put both on the same level in the group (same service, different length). Each needs a display name, description and a review screenshot of the paywall.

**App Information / App Privacy**
- Privacy Policy URL: `https://<domain>/privacy/`
- Support URL: `https://<domain>/support/`
- Marketing URL: `https://<domain>/`
- App Privacy: **Data Not Collected**
- EULA: Apple's standard EULA, and add to the end of the App Store description:
  `Terms of use: https://<domain>/terms/ · Privacy: https://<domain>/privacy/`
- Paid Apps Agreement + bank and tax info must be signed under Business, or subscriptions won't load.

## 5. Test purchases in Xcode
Product › Scheme › Edit Scheme › Run › Options › StoreKit Configuration → `RepCam.storekit`.
Then the paywall shows 349 kr / 59 kr and you can buy, cancel and restore in the simulator or on your iPhone without paying.
