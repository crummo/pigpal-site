# Website brief — paste this into a site builder

The site in this folder is hand-written static HTML for GitHub Pages. If you ever want it
redesigned — by a designer, by v0 / Lovable / Claude, by anyone — hand over the prompt below
rather than describing the app from memory. Everything in it is true of the shipped app, which
matters: a generated site that invents features is worse than no site.

Screenshots live in `assets/` and are regenerated from the simulator, not mocked up.

---

## The prompt

> Build a marketing site for **Pig Pal**, an iPhone and iPad app that handles chores, allowance
> and savings goals for a family. Static HTML and CSS in a single file, no framework, no build
> step, no external requests — it's hosted on GitHub Pages at `pigpal.app`.
>
> **What the app actually does.** Parents set up chores worth money and a weekly allowance. Kids
> tick chores off on their own screen; a parent approves, and only then does the money move. Kids
> split their allowance toward savings goals and watch them fill. Parents can offer rewards that
> aren't money — a day out for thirty chores — either pooled between the kids or each on their
> own. Everything syncs privately between both parents' devices over iCloud. A device can be
> tagged: a kid's own phone opens straight to their screen and needs the parent PIN to leave it,
> while the family iPad opens to a "Who's here?" picker with a face for each child.
>
> **What it does not do, and must not be implied.** There is no web app, no Android version, no
> bank connection, no real debit card, no investing, no chores marketplace, no AI. Money in Pig
> Pal is a ledger of what a parent owes a child, not actual funds.
>
> **Privacy is a selling point and it is literally true.** No account, no server, no analytics,
> no advertising, no third-party SDKs. Family data lives on the device and, optionally, in the
> user's own iCloud, which the developer cannot read. The App Store privacy label is
> "Data Not Collected". Say this plainly and don't dress it up.
>
> **Voice.** Warm, plain, specific. Short sentences. Concrete nouns — "a kid ticks it off, a
> parent approves, the money lands" rather than "seamless family financial empowerment". Never
> use: seamless, empower, revolutionize, gamify, journey, solution. American spelling and US
> date format throughout, to match the app. No exclamation marks except in the app's own UI copy.
>
> **Look.** Soft pink, rounded, friendly, generous whitespace — the app's own palette. Background
> `#fdf0f2`, cards `#fff7f8`, ink `#2b1b20`, accent pink `#e0688c`, darker pink for links
> `#c8466b`. Full dark-mode support via `prefers-color-scheme` with background `#1a1114`, cards
> `#241a1e`, ink `#f6eaee`. System font stack; no web fonts. Corner radius 18–26px. Soft shadows,
> never hard borders.
>
> **Structure.** One page: a hero with the pig mark, the line "The piggy bank, all grown up", a
> one-sentence description, and a call to action; three device screenshots with captions; a
> feature grid of six; a short privacy section; a footer with privacy, support and copyright.
> Plus a second page for the privacy policy.
>
> **Must-haves for the App Store listing to be valid:** a working privacy policy page, a support
> contact, and an `og:image` so shared links preview properly.
>
> **Copy comes from the app, not from imagination.** The headline and the first three feature
> cards are the app's own onboarding text, word for word — "Kids check things off the list and
> earn real dollars. You approve, the money lands." Keep them identical: someone who sees the site
> and then opens the app should read the same sentences. New copy goes in that voice.
>
> **Use the real app icon** (`assets/icon.png`, from the asset catalog) in the hero, as the
> favicon and as the Apple touch icon. Never an emoji stand-in.
>
> **Assets:** `assets/shot-kid.png`, `assets/shot-parent.png`, `assets/shot-gate.png`,
> `assets/shot-rewards.png` — real screenshots at 620px wide. Use the kid screen as the hero and
> the social preview image.
>
> **Accessibility:** real alt text describing what each screenshot shows, contrast of at least
> 4.5:1 for body text in both color schemes, and a layout that works at 375px wide with no
> horizontal scrolling.

---

## Regenerating the screenshots

They come from the headless preview harness on the Pro Max simulator (the App Store's 6.9" size),
so the same captures work for the store listing:

```sh
PM=6F7EF7BA-86BA-47F7-A11D-35B51132B2E4
SIMCTL_CHILD_PREVIEW_SCREEN=kidview SIMCTL_CHILD_PREVIEW_KID=k_maya \
  xcrun simctl launch $PM com.slowdustsoftware.PigPalApp
xcrun simctl io $PM screenshot docs/assets/shot-kid.png
sips --resampleWidth 620 docs/assets/shot-kid.png    # web size; skip for App Store Connect
```

Screens worth capturing: `gate`, `kidview`, `parentview`, `rewardcard`, `family`. Cold launches
render black — launch twice and wait a few seconds, and keep the Simulator app frontmost.
