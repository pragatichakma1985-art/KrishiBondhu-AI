# KrishiBondhu AI

**KrishiBondhu** ("Farmer's Friend") is a single-file, mobile-first web app that gives small farmers an AI crop doctor, local weather and crop-risk alerts, and a farmers' marketplace. It is built for Bangladesh and South Asia first, but works for farmers in 190+ countries.

- One Python file: `krishibondhu_v4_fixed.py`
- No pip packages needed (Python standard library only)
- Runs on a phone with Pydroid 3, or on any server
- Installable as a PWA (add to home screen) and partly works offline

---

## What it is used for

| Who | What they do with it |
|---|---|
| Farmers | Check a sick crop with photos, see weather and disease risk, sell produce, find buyers |
| Buyers / traders | Post what they want to buy, find farmers' lots in their country |
| Extension workers | Show farmers simple first-step advice and local problem reports |

---

## Features

### 1. AI Crop Doctor
- Choose country, crop, symptom, add up to **5 photos** (camera or gallery) and notes
- AI replies with: alert level (green / yellow / red), simple summary, up to 2 likely causes with confidence, what it is, treatment, prevention, today's steps, questions to sharpen the answer, and when to see an agricultural officer
- Checks if the photo really matches the selected crop and warns if not
- Tells the farmer how to retake a blurry or dark photo
- **80+ crops** with built-in reference lists of common diseases and pests (rice, wheat, maize, potato, tomato, chilli, eggplant, jute, sugarcane, cotton, fruits, vegetables, pulses, tea, spices and more), plus an "Other" option for any crop
- Answers in **17 languages**
- Speak your notes (voice typing) and listen to the answer (text-to-speech)
- Share advice as text or as a picture card, or copy it
- Saves your last 10 checks **on your phone only**
- Thumbs up / down feedback
- Demo mode that works with no key and no photo

### 2. Weather and Crop Risk
- 7-day forecast and current weather for the chosen country, quick-pick cities, typed village/town name, or "My location"
- Alerts for heavy rain, extreme heat, frost and strong wind
- "Check crop risk (AI)": uses real humidity, rain and temperature numbers to name only the problems the weather actually favours, with signs to look for
- If the weather is not risky, it says so instead of inventing problems

### 3. Problems Reported in Your Country
- After advice, a farmer can warn neighbours by reporting crop, problem name and place
- Only crop, problem and place are stored (no photo, name or phone)
- Shows the last 14 days, grouped and counted

### 4. Marketplace (Krishi Haat)
- Tabs: **Buyer needs**, **Sellers**, **My lots**, **RFQ**
- Post "I will sell" or "I want to buy" with crop, quantity, price, place, country and phone
- Posts are visible per country for 30 days
- Up to **12 photos** per selling lot
- Contact details are hidden until the buyer taps "Show contact"
- Call or WhatsApp buttons
- Message in your own language with **AI translation**, and translate any post
- Report spam or unsafe posts (3 reports hides a post)
- Seller trust badge (new, active, trusted, reported)
- Price statistics from real posts (min, max, median)
- Search, crop filter, sort by price
- Sample posts are clearly labelled "Sample"

### 5. Sell and Share Your Produce
- AI writes a short, honest sales post (no invented claims, no private data sent to the AI)
- One tap "Post everywhere": posts to the Marketplace with photos and opens the phone share menu (Facebook, WhatsApp, Instagram, etc.)
- Save your Facebook / Instagram / WhatsApp / Telegram / website once (kept on your phone)
- Optional **Telegram channel auto-post** with photos
- **AI price suggestion** from real posts in your country
- **Auto buyer match**: shows buyer needs for your crop as you type
- Quick buttons to search Facebook Marketplace, Facebook groups, Instagram, Google, Alibaba and IndiaMART

### 6. Find Buyers on the Internet
- Opens public searches on Facebook, Instagram, LinkedIn, Alibaba, Tridge and Google, plus local sites (for example Bikroy, IndiaMART, OLX, Jiji)
- Optional **AI buyer finder with scam check** (needs a free Serper key): finds web leads, extracts crop, quantity and place, and rates scam risk (low / medium / high)

### 7. Impact Dashboard and Setup Status
- Live counts of crop checks, market posts, area reports, countries and helpful ratings
- Setup card shows which keys are missing

---

## Countries

The app supports **190+ countries and territories**:

- **South Asia:** Bangladesh, India, Nepal, Pakistan, Sri Lanka, Afghanistan, Bhutan, Maldives
- **East and Southeast Asia:** Indonesia, Vietnam, Thailand, Philippines, Malaysia, Myanmar, Cambodia, China, Japan, South Korea, Laos, Mongolia, Singapore, Taiwan, Brunei, Timor-Leste, North Korea
- **Central Asia:** Kazakhstan, Uzbekistan, Kyrgyzstan, Tajikistan, Turkmenistan
- **Middle East:** Turkey, Iran, Saudi Arabia, UAE, Iraq, Syria, Jordan, Lebanon, Israel, Palestine, Yemen, Oman, Qatar, Kuwait, Bahrain, Armenia, Azerbaijan, Georgia
- **Africa:** Nigeria, Kenya, Ethiopia, Ghana, Tanzania, Uganda, South Africa, Egypt, Morocco and all other African countries
- **Americas:** USA, Canada, Mexico, Brazil, Argentina, Colombia, Peru, Chile, Cuba and all other countries of North, Central and South America and the Caribbean
- **Europe:** UK, France, Germany, Spain, Italy, Netherlands, Poland, Ukraine, Russia and all other European countries
- **Oceania:** Australia, New Zealand, Papua New Guinea, Fiji and the Pacific islands
- **Other country** option for anything not listed

Each country gets its own Marketplace board, reports, weather city list and default answer language.

## Answer languages (17)

Bangla, English, Hindi, Urdu, Nepali, Spanish, Portuguese, French, Arabic, Simplified Chinese, Indonesian, Vietnamese, Thai, Swahili, Russian, Tamil, Sinhala.

The interface itself is fully translated in Bangla and English, with Hindi, Urdu and Nepali for main labels.

---

## What it uses

| Part | Used for | Needed? |
|---|---|---|
| Python 3 (standard library only) | Web server and all logic | Yes |
| **Baseten** inference API (OpenAI-compatible), default model `meta-models/muse-spark-open` | Crop doctor, risk, sales post, translation, price tip, buyer finder | Yes, for AI features |
| **Open-Meteo** (free, no key) | Weather and geocoding | Built in |
| **Serper.dev** (free key) | AI buyer finder and scam check | Optional |
| **Telegram Bot API** | Post to a Telegram channel | Optional |
| Browser Web Speech API | Voice typing and listen aloud | Built in (Chrome recommended) |
| Browser Share API, Geolocation, Service Worker | Share menu, My location, offline use | Built in |
| Google Fonts (Noto Sans Bengali) | Bangla text display | Built in |

---

## How to run

### On a phone (Pydroid 3)
1. Open `krishibondhu_v4_fixed.py` in Pydroid 3 and run it.
2. When asked, paste your Baseten API key and press Enter.
3. Open `http://localhost:8000` in Chrome.

### On a computer or server
```bash
export LLM_API_KEY="your-baseten-key"
python krishibondhu_v4_fixed.py
```
Then open `http://localhost:8000`.

### Environment variables

| Variable | Meaning | Default |
|---|---|---|
| `LLM_API_KEY` | Baseten API key | none |
| `LLM_BASE_URL` | AI API base URL | `https://inference.baseten.co/v1` |
| `LLM_MODEL` | Model name | `meta-models/muse-spark-open` |
| `SERPER_KEY` | serper.dev key for AI buyer finder | none |
| `TG_TOKEN` | Telegram bot token | none |
| `TG_CHAT` | Telegram channel, for example `@mychannel` (bot must be admin) | none |
| `PORT` | Server port | `8000` |
| `TRUST_PROXY` | Set to `1` behind a reverse proxy to read the real client IP | off |

**Never commit real keys to GitHub.** Keep them in environment variables or paste them when the app asks.

The Marketplace, weather and demo work without any AI key.

---

## Data stored on the server

Created automatically next to the script (do not commit these):

- `board.json`: marketplace posts (30 days)
- `photos/`: lot photos
- `reports.json`: area problem reports
- `feedback.json`: helpful / not helpful counts
- `checks.json`: crop check counter

Farmer history, saved accounts and settings stay in the **phone's own browser storage**.

---

## Safety and privacy

- The AI never gives pesticide doses or mixing amounts. It tells farmers to read the label and ask the local agricultural officer.
- Outside South Asia the AI does not name any pesticide at all, only cultural and organic steps.
- Farmer-typed text is treated as data, with protection against prompt-injection.
- Rate limiting on all API routes.
- Photos sent for diagnosis are used for analysis only and not saved. Marketplace lot photos are saved only if the farmer posts them.
- Contact numbers are not sent to the AI.
- The app does not handle payments. People on the Marketplace are **not verified**: never send money in advance, check the buyer, and meet in a public place.
- Impact numbers come from real use of the app; early numbers come from demo and test use.

---

## Disclaimer

Advice is AI-generated and is **not a confirmed diagnosis**. Always consult a local agricultural extension officer before using any pesticide. Marketplace prices marked "Sample" are examples only.
