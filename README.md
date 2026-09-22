# Style — Personal Outfit Editor

Style is a mobile-friendly wardrobe and outfit-planning project for young women. My original idea was to let a user upload photos of her clothes, describe her body and preferred style, save outfits from fashion creators, and then receive a recommendation for a specific day and social situation. I wanted the experience to feel like a personal stylist rather than a random outfit generator, while keeping the visual design playful and dopamine-inspired.

## Live project

[Open Style on GitHub Pages](https://fengtinglu1020-bot.github.io/mystyle/)

For the installable experience, open the link in Safari on iPhone or Chrome/Edge on Android and use **Add to Home Screen** or **Install app**. The hosted HTTPS version is required for installation and offline caching.

## How to open or run it

No build tools, accounts, API keys, or external services are required.

1. Download or clone this repository.
2. For a quick desktop preview, open `index.html` in a browser.
3. For the full PWA behavior, serve the folder with any local static server and open the local URL it provides. For example: `python3 -m http.server 8000`, then visit `http://localhost:8000`.

All of the interface, styling, and application logic are contained in `index.html`. `manifest.webmanifest`, `sw.js`, and `icon.svg` provide the installable web-app experience. Wardrobe photos, preferences, inspirations, and feedback stay in the current browser using IndexedDB/local storage. Users should export a wardrobe backup before clearing browser data or changing devices.

## AI tool and selected prompts

I used **ChatGPT/Codex** to help plan, write, debug, and refine the single-page HTML/CSS/JavaScript prototype. Selected prompts that shaped the project included:

> “Build a clothing coordination website for women aged 18–28. Users should be able to upload photos of all their clothes and enter information about their body shape and preferred styles. When someone asks what to wear today and describes the day’s social needs, the website should provide an outfit recommendation. Use one index.html file with CSS and JavaScript inside it. Do not use external services.”

> “The page content is good, but I do not like the design. I want it to have a dopamine-inspired style.”

> “The current outfit logic is confusing and only keeps generating combinations. It does not consider the occasion or the styles of creators I like. Rework the logic so that the priorities are: 1. weather and required formality, 2. occasion, and 3. favorite creator outfits.”

> “Some contrasting color combinations are too abrupt. Most of the outfit should use coordinated colors, with contrast limited to a small area such as an accessory or bag.”

I also used iterative testing prompts based on visible problems, including incorrect clothing categories and colors, repeated recommendations, relaxed clothes appearing in formal looks, an inflated outfit count, confusing backup downloads, and a mobile installation button that was difficult to find.

## Reflection

The final project matches my intention most clearly in its structure and priorities: it starts with a real wardrobe, asks about the day’s weather, formality, and occasion, and only then uses saved creator outfits and personal preferences to influence the result. The colorful dopamine-style interface and the ability to upload inspiration images also match the experience I imagined. However, the automatic photo analysis does not yet match the reliability of a real stylist. For example, early tests labeled a navy top and a beige plaid skirt with the wrong colors and categories, so I changed the flow to show confidence labels and make every important clothing attribute editable. I also tested recommendations with only five garments and found that the app incorrectly claimed it could make 60 outfits and kept showing the same look. I changed the counting logic to use only valid combinations, added recent-look rotation, and made weather/formality hard filters before occasion and creator-style ranking. I further adjusted color logic so that a look stays mostly coordinated and reserves strong contrast for a smaller accessory rather than combining several competing colors.

AI helped me turn ideas and visual feedback into working HTML, CSS, and JavaScript quickly, and it was especially useful for proposing scoring rules, finding state-management bugs, adding local backup/feedback tools, and converting the site into an installable PWA. I still had to decide what “good styling” meant for this product: which constraints should be mandatory, how formal and relaxed clothing should be separated, when creator inspiration should influence a result, and which interface explanations would make the recommendation trustworthy. The largest unresolved issue is image understanding. Because this version uses no external services, its browser-only color/category estimation is limited and still depends on manual correction; it cannot understand fabric, garment construction, or a full outfit as accurately as a trained multimodal model. Data also stays on one device unless the user exports a backup, and the recommendation quality remains uncertain until more users test it with larger, more varied wardrobes and provide feedback.

## Privacy and limitations

This prototype does not upload photos to a server. Data remains in the browser, which supports privacy and low-cost testing but means there is no automatic cross-device sync. The project is a decision-support prototype, not a production fashion-recognition system.
