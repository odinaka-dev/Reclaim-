# Reclaim — Webhook Receiver (starter)

This is the smallest possible version of the part that listens for
Nomba's payment notifications. Right now it just receives a notification
and logs it — it doesn't create Recovery Cases yet, that's the next step.

## What this is for

Nomba needs a public URL to send payment notifications to. This project
gives you that URL once deployed. Get this live first, submit the URL
on Nomba's form, and we'll start seeing real events immediately —
even before the rest of the system is built.

## Run it on your machine first

```
npm install
npm start
```

Then open `http://localhost:3000/health` in a browser — if you see
`{"status":"ok", ...}` it's working.

## Deploy it (so it has a real public URL)

Use **Render** — it's free for this and gives you a URL that doesn't
change every time you restart your laptop (unlike ngrok).

1. Push this folder to a GitHub repo.
2. Go to render.com → New → Web Service → connect that repo.
3. Build command: `npm install`
   Start command: `npm start`
4. Click deploy. Wait a minute or two.
5. Render gives you a URL like `https://reclaim-webhook.onrender.com`

## What to submit on Nomba's form

Take the Render URL and add `/webhooks/nomba` to the end:

```
https://reclaim-webhook.onrender.com/webhooks/nomba
```

That exact link goes in the "webhook URL" field on Nomba's form, along
with our sub-account ID.

## How to check it's actually receiving real events

Once deployed, visit:

```
https://reclaim-webhook.onrender.com/webhooks/recent
```

This shows the last 50 notifications received, so you can see real
Nomba data land without digging through server logs.

## What's next (don't build this yet, just know it's coming)

- Saving each event into a real database instead of memory
- Checking the transaction ID against ones we've already seen, so we
  never act on the same notification twice
- Turning a `payment_success` (or failure) event into an actual
  Recovery Case in our system
