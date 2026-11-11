# Gem Store

A one-page loot box demo for COP 4910 Presentation 4. Every player starts with the same 2,000-gem Starter Pack and picks one of two modes:

- **High Roller:** double the Legendary odds, fewer boxes.
- **Standard:** standard odds, more boxes.

Players open boxes one at a time until the presenters announce a code. Their phone then shows a receipt in real dollars, compares the two modes honestly, and reveals the odds.

No real money changes hands. There is no backend and no tracking, and the page loads nothing from other sites. Everything runs on the player's phone.

## Files and dependencies

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: HTML, CSS and JavaScript in one file. |
| `img/*.jpg` | The 15 portrait images, named exactly as listed below. |
| `README.md` | This file. Optional on GitHub Pages. |

There are **no code dependencies**: no npm packages, no frameworks, no build step, no external fonts or scripts. The only other files are the portraits.

## The portraits

Every loot box drops one portrait. Rarity follows how recently each person served, with the most recent rarest. Within a tier, each portrait is equally likely.

| Tier | Portraits | File names in `img/` |
| --- | --- | --- |
| Legendary | Trump, Biden | `trump.jpg`, `biden.jpg` |
| Epic | Obama, George W. Bush, Clinton | `obama.jpg`, `bush.jpg`, `clinton.jpg` |
| Rare | Reagan, Carter, Kennedy, Theodore Roosevelt | `reagan.jpg`, `carter.jpg`, `jfk.jpg`, `teddy-roosevelt.jpg` |
| Common | Grant, Lincoln, Jackson, Jefferson, Washington, Franklin | `grant.jpg`, `lincoln.jpg`, `jackson.jpg`, `jefferson.jpg`, `washington.jpg`, `franklin.jpg` |

- File names are **case-sensitive** on GitHub Pages: `Carter.JPG` will not load as `carter.jpg`. A missing or misnamed image doesn't break the game; that portrait just shows its name without a picture.
- **Size:** keep each image about 600 px tall or less. A phone decodes a 1920×2062 image to about 16 MB of memory, and the page preloads all 15.
- **Rights:** a public GitHub Pages site republishes these images to anyone with the link. Check the artist's license or ask permission, and credit them in this README.
- To change who is in which tier, edit `items` in `CONFIG` near the top of the script.

## Put it on GitHub Pages

1. Create a new **public** repository on GitHub, for example `gem-store`. Pages on a free account requires a public repo.
2. Upload `index.html` (and this README) to the root of the default branch. Use **Add file › Upload files**, or `git push`.
3. Go to **Settings › Pages**. Under **Build and deployment**, set Source to **Deploy from a branch**, the branch to `main`, and the folder to `/ (root)`. Save.
4. Wait a minute or two. The site appears at `https://<your-username>.github.io/gem-store/`.
5. Open that URL on your phone and play once to confirm it works.

If you update `index.html` later, Pages republishes on its own within a minute or two.

## Make the QR code

Generate the code from the final URL, and keep the trailing slash:

```bash
qrencode -s 12 -m 2 -o qr.png 'https://<your-username>.github.io/gem-store/'
```

`qrencode` is in most Linux package managers and in Homebrew. Any offline QR generator also works. Avoid "free QR" sites that send scans through their own redirect links, because some of those links expire or show ads.

Put the QR code **and** the plain URL on the cover slide, since some phone cameras won't scan from a projector.

## Running it in class

- **Reveal code:** `RECEIPT`, and it isn't case-sensitive. Presenter B says it out loud at 3:00. To change it, edit `revealCode` near the top of the script.
- **One mode per player.** The choice is locked once confirmed. Progress is saved in the browser, so refreshing doesn't reset the phone or let a player switch modes.
- **One box at a time.** There is no "open all" button. Each tap opens a single box, and rarer pulls shake a little longer.
- **To start over** (rehearsals, testing): add `?reset` to the URL, e.g. `https://<you>.github.io/gem-store/?reset`.
- **The odds really are disclosed,** but only behind the tiny "Probability disclosure" link at the bottom. That's deliberate. At the reveal, ask who tapped it.
- **The "offer ends" timer is fake.** It restarts every two minutes, and the receipt says so.

## Numbers the page uses

These match the presentation doc and the slides. All of them are in `CONFIG` at the top of the script. The Starter Pack is 2,000 💎, and its hidden price is $19.99.

| | High Roller | Standard |
| --- | --- | --- |
| Box price | 850 💎 | 340 💎 |
| Boxes per pack | 2 | 5 |
| Gems left over | 300 ($3.00) | 300 ($3.00) |
| Real cost per box opened | $9.99 | $4.00 |
| Legendary / Epic / Rare / Common | 1 / 9 / 25 / 65% | 0.5 / 4.5 / 16 / 79% |
| Chance of at least one Legendary per pack | 2.0% | 2.5% |
| Average cost of one Legendary | about $1,000 | about $800 |

High Roller doubles the odds per box but costs 2.5× as much per box, so it **lowers** the chance of a Legendary across a whole pack. That's the twist the receipt reveals.

Each box draws a number from 1 to 1,000 using the browser's cryptographic random number generator. A tier wins when the roll is at or below its `max`, checked from Legendary down. If you change the odds, change `max` and `pct` together.

## Before presenting

- [ ] Play through both modes on an iPhone and on an Android phone.
- [ ] Test on the classroom Wi-Fi **and** on cellular data.
- [ ] Run `?reset` on any phone you rehearsed with.
- [ ] Bring the paper fallback (both roll tables and volunteer cards) in case the network fails.