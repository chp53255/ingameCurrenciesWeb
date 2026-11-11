# Gem Store

A one-page loot box demo for COP 4910 Presentation 4. Each player gets a pretend $20 and buys one gem bundle. They open loot boxes until the presenters announce a code, then their phone shows a receipt in real dollars along with the true odds.

No real money changes hands. There is no backend and no tracking, and the page loads nothing from other sites. Everything runs on the player's phone.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: HTML, CSS and JavaScript in one file. |
| `README.md` | This file. Optional on GitHub Pages. |

## Put it on GitHub Pages

1. Create a new **public** repository on GitHub, for example `gem-store`. Pages on a free account requires a public repo.
2. Upload `index.html` (and this README) to the root of the default branch. Use **Add file › Upload files**, or `git push`.
3. Go to **Settings › Pages**. Under **Build and deployment**, set Source to **Deploy from a branch**, the branch to `main`, and the folder to `/ (root)`. Save.
4. Wait a minute or two. The site appears at `https://<your-username>.github.io/gem-store/`.
5. Open that URL on your phone and play once to confirm it works.

## Make the QR code

Generate the code from the final URL, and keep the trailing slash:

```bash
qrencode -s 12 -m 2 -o qr.png 'https://<your-username>.github.io/gem-store/'
```

`qrencode` is in most Linux package managers and in Homebrew. Any offline QR generator also works. Avoid "free QR" sites that send scans through their own redirect links, because some of those links expire or show ads.

Put the QR code **and** the plain URL on the cover slide, since some phone cameras won't scan from a projector.

## Running it in class

- **Reveal code:** `RECEIPT`, and it isn't case-sensitive. Presenter B says it out loud at 3:00. To change it, edit `revealCode` near the top of the script.
- **One purchase per player.** Each bundle leaves leftover gems on its own: 160, 180 and 220. Allowing a second purchase would break that, because 500 + 1,200 gems is exactly five boxes.
- **Refreshing doesn't reset a phone.** Progress is saved in the browser, so a reload doesn't give anyone a second purchase.
- **To start over** (rehearsals, testing): add `?reset` to the URL, e.g. `https://<you>.github.io/gem-store/?reset`.
- **The odds really are disclosed,** but only behind the tiny "Probability disclosure" link at the bottom. That's deliberate. At the reveal, ask who tapped it. The fine print also calls 0.5% "boosted" from a standard 0.25%, so the claim was technically true.
- **The "offer ends" timer is fake.** It restarts every two minutes, and the receipt says so.

## Numbers the page uses

These match the presentation doc and the slides. All of them are in `CONFIG` at the top of the script.

| Bundle | Price | Boxes (340 💎 each) | Real cost per box | Gems left over |
| --- | --- | --- | --- | --- |
| 500 💎 | $4.99 | 1 | $4.99 | 160 ($1.60) |
| 1,200 💎 | $9.99 | 3 | $3.33 | 180 ($1.50) |
| 2,600 💎 | $19.99 | 7 | $2.86 | 220 ($1.69) |

Each box draws a number from 1 to 1,000 using the browser's cryptographic random number generator: Legendary 1–5 (0.5%), Epic 6–50 (4.5%), Rare 51–210 (16%), Common 211–1,000 (79%). If you change the odds, change the `max` and `pct` values together.

## Before presenting

- [ ] Play through once on an iPhone and once on an Android phone.
- [ ] Test on the classroom Wi-Fi **and** on cellular data.
- [ ] Run `?reset` on any phone you rehearsed with.
- [ ] Bring the paper fallback (roll table and volunteer cards) in case the network fails.
