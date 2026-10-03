# Website brief

The site in this folder is hand-written static HTML, served by Cloudflare Pages at `pigpal.app`.
If it is ever redesigned — by a designer, by a site builder, by Claude — hand over the prompt
below rather than describing the app from memory. A generated site that invents features is
worse than no site.

**The screenshots are the source of truth.** They come from the current build, so when this file
and a screenshot disagree, the screenshot wins and this file is the thing to fix.

---

## The prompt

> Build a marketing site for **Pig Pal**, an iPhone app that handles chores, allowance
> and savings goals for a family. Static HTML and CSS, no framework, no build step, no external
> requests. Four pages: home, support, privacy policy, terms.
>
> **What the app actually does.** Parents set up chores worth money and a weekly allowance.
> Kids tick chores off on their own screen; chores marked *approval* wait for a parent before
> the money moves. Kids can also ask to buy something or ask for money to be added, and those
> requests wait for a parent too — a parent says yes or sends it back. Kids put money aside
> toward savings goals, or let part of their allowance save itself each week; saved money is
> kept apart from money to spend. Parents can offer rewards that aren't money — a day at the
> zoo for forty chores between everyone, or pizza and a film for a few chores each. Each kid has
> a history of what was earned, spent and saved. Everything syncs privately between the family's
> devices over iCloud. A device can be tagged: a kid's own phone opens straight to their screen
> and needs the parent PIN to leave it, while a shared phone opens to a "Who's here?" picker
> with a face for each child.
>
> **What it does not do, and must not be implied.** There is no web app, no Android version, no
> bank connection, no real debit card, no investing, no chores marketplace, no AI. Money in Pig
> Pal is a ledger of what a parent owes a child, not actual funds. Version 1.0 is iPhone only:
> no iPad version and no wall mode yet — both are coming, and the support FAQ says the iPad one
> is on the way. Don't show or promise either in the pitch. There is no backup or restore
> feature and no data export for users yet — sync is not a backup, and the app says so.
>
> **Privacy is a selling point and it is literally true.** No account, no server, no analytics,
> no advertising, no third-party SDKs. Family data lives on the device and, if sync is on, in the
> user's own iCloud, where Apple's privacy policy governs it and Slow Dust Software cannot read
> it. The App Store privacy label is "Data Not Collected". Say this plainly and don't dress it
> up. Don't claim encryption beyond what Apple promises.
>
> **Voice.** Warm, plain, specific. Short sentences. Concrete nouns — "a kid ticks it off, a
> parent approves, the money lands" rather than "seamless family financial empowerment". Never
> use: seamless, empower, revolutionize, gamify, journey, solution. American spelling and US
> date format throughout, to match the app. No exclamation marks except in the app's own UI copy.
>
> **Copy agrees with the screenshots.** Don't describe anything they don't show. Where the app
> has its own words for a thing — *Waiting for you*, *Money to spend*, *Auto-saving*, *Who's
> here?* — use them.
>
> **Look.** Soft pink, rounded, friendly, generous whitespace — the app's own palette.
> Background `#fdf0f2`, cards `#fff7f8`, ink `#2b1b20`, accent pink `#e0688c`, darker pink for
> links `#c8466b`. Full dark mode via `prefers-color-scheme`: background `#1a1114`, cards
> `#241a1e`, ink `#f6eaee`. System font stack; no web fonts. Corner radius 18–26px. Soft
> shadows, never hard borders.
>
> **Structure.** A sticky translucent nav on every page (How it works · Not a bank · Privacy ·
> Support), identical in position on all four. Home: a hero with the app icon, "The piggy bank,
> all grown up.", a one-line description, a "See how it works" button and an App Store badge;
> a row of three phone screenshots (kid's goals, parent overview, kid's money and requests),
> with a note under it that the screenshots show sample data; a feature grid of six; three feature details cut from the
> real screens (savings, today's chores, approvals); a rewards showcase; "Not a bank"; "Privacy,
> honestly"; a footer with privacy policy, terms, support and "© Slow Dust Software". Support
> carries the contact email and an FAQ with FAQPage structured data.
>
> **Must-haves for the App Store listing:** a working privacy policy page, a support page with a
> contact address, and an `og:image` so shared links preview properly.
>
> **Use the real app icon** (`assets/icon.png`) in the hero, as the favicon and as the Apple
> touch icon. Never an emoji stand-in.
>
> **Accessibility:** real alt text describing what each screenshot shows, contrast of at least
> 4.5:1 for body text in both color schemes, and a layout that works at 375px wide with no
> horizontal scrolling.

---

## Assets

| File | What it is |
|---|---|
| `shot-kid.png` | Kid's Goals screen (Theo). Also the `og:image`. 620px wide. |
| `shot-parent.png` | Parent overview with requests waiting (Finn, Theo, Wren). 620px wide. |
| `shot-money.png` | Kid's My money screen: ask to add money, ask to buy, history (Mina). 620px wide. |
| `shot-rewards.png` | Rewards screen (Finn, Wren). 620px wide. |
| `detail-goal.png` | Crop: money to spend and a savings goal with auto-save. |
| `detail-chores.png` | Crop: today's chores, one marked approval. |
| `detail-approve.png` | Crop: a kid's page on the parent's phone (Kofi) with a request waiting. |
| `shot-gate.png`, `shot-gate-ipad.png` | Old gate captures. Not used; the iPad one is for when iPad ships. |

Phone shots are resized to 620px wide and have the Dynamic Island filled with the status-bar
pink — shown without a device frame, the black pill is the loudest thing on the page. Leave the
App Store Connect captures as they are. Crops are cut from the full-resolution captures
(1320×2868) and left at that scale. The captures live in
`PigPay/incoming/ASC/shots/build50_shots/`, with dark-mode versions in `build50-dark/`.

The site shows one household through most of the story (Finn, Theo, Wren), with Mina and Kofi
from two other families. Keep it to a few coherent families rather than
a different family in every screenshot — a lineup reads as staged.

## Regenerating the screenshots

**The children in the fixtures are generated, not photographed.** Keep it that way — never put a
real child's face on the site or in the store listing. The site says so under the shot row, and
says it reason-first, because "we generated these" next to app screenshots can read as "there is
AI in this app", which there isn't. If the fixtures change, that line has to stay true. Face
crops for the fixtures are 512×512 head-and-shoulders, in `PigPay/incoming/ASC/faces/`.

Captures come from the app's preview harness on the iPhone 17 Pro Max simulator (the App
Store's 6.9" size), and the 13-inch iPad Pro once iPad ships. Screen names change between builds — check the
harness rather than this file. Cold launches can render black; launch twice and wait.

A capture taken with the simulator rotated to landscape comes back in the portrait pixel frame —
`simctl io screenshot` ignores the rotation. Fix it afterwards with `sips -r 270`.

## Hosting

- **Cloudflare Pages**, building from `main` of `crummo/pigpal-site`. There is no build step;
  a push deploys in under a minute or two.
- **Domain** registered at Porkbun; **DNS** on Cloudflare. `www.pigpal.app` 301s to the apex via
  a Cloudflare redirect rule.
- **URLs are extensionless.** Pages 308s `/privacy.html` to `/privacy`, so link to `/privacy`,
  `/terms`, `/support`, and keep canonicals extensionless. Unknown paths serve the homepage
  with a 200, not a 404.
- **support@pigpal.app** is a Cloudflare Email Routing forward to the support Gmail inbox, which
  also sends as that address.
- **App Store Connect:** support URL `https://pigpal.app/support`, privacy policy
  `https://pigpal.app/privacy`, marketing URL `https://pigpal.app`.

## At launch

- Replace the hero's "Coming soon to the App Store" placeholder with Apple's official badge,
  unmodified, linking to the listing. The markup has a `LAUNCH` comment at the spot.
- The terms promise their date changes whenever they do. Update it with any edit.
