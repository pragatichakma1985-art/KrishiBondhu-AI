# KrishiBondhu — AI crop doctor + farmer marketplace with PayPal checkout

**PayPal AI Hackathon submission.** Single-file Python app (`fa_ai_v15.py`), runs on a phone (Pydroid 3) or a server.

## The problem
Small farmers in Bangladesh and South Asia lose crops to diseases they cannot identify, and have no safe, simple way to sell their produce or pay for orders online.

## What it does
- **AI crop doctor** (Bangla, English and 100+ languages): the farmer picks a crop, adds leaf photos and symptoms, and gets a short diagnosis, safe first steps and when to see the agricultural officer. Model: Meta Muse Spark Open via Baseten. It never gives pesticide doses.
- **Krishi Haat marketplace**: buyers' needs, sellers' lots, RFQs, buyer–seller matching, phone-verified badges.
- **PayPal checkout (new)**: a buyer can pay a seller's lot with PayPal. The server creates the order with the **PayPal Orders API v2**, sends the buyer to PayPal to approve, then **captures the payment on the server**, checks that the captured amount and currency match our order, and only then marks it paid. The platform records a small commission per order.

## PayPal integration (central to the app)
| Step | Where |
|---|---|
| OAuth token (client credentials, cached) | `_pp_token()` |
| Create order (`intent=CAPTURE`, `PAY_NOW`) | `pay_start()` -> `POST /v2/checkout/orders` |
| Buyer approves on PayPal | redirect to `payer-action` link |
| Capture + verify amount/currency | `pp_capture()` -> `POST /v2/checkout/orders/{id}/capture` |
| Idempotency | `PayPal-Request-Id` header, `ORDER_ALREADY_CAPTURED` handled |
| UI | "Pay with PayPal" button on every marketplace lot, plus the `/pay` page |

Runs against the **free PayPal Sandbox** (`PAYPAL_LIVE=1` switches to live).

## What changed during the submission period
Started as a crop-diagnosis demo; during the hackathon we added the multi-language marketplace, buyer–seller matching, verified badges, security hardening and the PayPal checkout flow above.

## Run it
```
PAYPAL_CLIENT_ID=...   # PayPal Sandbox app
PAYPAL_SECRET=...
LLM_API_KEY=...        # Baseten key (Muse Spark Open)
PUBLIC_URL=https://your-public-url
python fa_ai_v15.py
```
Open `PUBLIC_URL`, sign in, tap **Haat**, open a lot, tap **Pay with PayPal**, and pay with a Sandbox *Personal* test account. Never commit keys to the repo.

## Limits (honest)
Payments are a Sandbox demo. The app does not hold funds or guarantee delivery; farmers are told to verify buyers. AI advice is not a confirmed diagnosis.

## 3-minute demo video outline
1. 0:00 Problem in one sentence. 2. 0:20 Photo + symptoms -> AI answer in Bangla. 3. 1:00 Haat -> a lot -> Pay with PayPal -> approve in Sandbox -> "Payment received". 4. 2:00 Show code: Orders API + server-side capture. 5. 2:40 Impact for farmers.
