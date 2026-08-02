Desk — install
A working app you can put on your phone today. Position sizing, the risk gate,
tilt detection, thesis capture, journal, and the adherence score — the whole
discipline layer, running entirely on your device.

It does not connect to a broker. You place orders in your broker app as
usual and log them here. That's deliberate: the discipline half is the part
that changes your results, and it needs no API keys, no server, and no approval
from anyone.

Fastest route — GitHub Pages (about 5 minutes)
Service workers need HTTPS, and phone home-screen install needs a service
worker. Any static host works; Pages is free.

Create a public repo, e.g. desk.
Upload all five files — index.html, manifest.json, sw.js, icon-192.png, icon-512.png — to the repo root.
Settings → Pages → Source: Deploy from a branch, branch main, folder /.
Wait a minute, then open https://<your-username>.github.io/desk/ on your phone.
Android (Chrome): menu → Add to Home screen → Install.
iPhone (Safari): Share → Add to Home Screen. Must be Safari; Chrome on
iOS can't install PWAs.

It then launches full-screen with no browser chrome, and works with the network
off entirely.

Netlify Drop (drag the folder onto netlify.com/drop) and Cloudflare Pages both
work identically if you'd rather not use GitHub.

Try it on a laptop first
cd desk-pwa
python3 -m http.server 8000
Then http://localhost:8000. Localhost counts as a secure origin, so the
service worker registers and you can test install behaviour.

Opening index.html by double-clicking also works — everything runs except
offline caching and install.

First five minutes
Rules tab — set your real capital, risk per trade, daily loss cap, and minimum R:R. Everything downstream keys off these.
Ticket — type a symbol, entry, and stop. Leave quantity blank and tap away; it fills in the size that risks exactly your percentage.
Notice what the gate refuses. That's the app working.
Log a trade, then close it from Open with the honest exit reason.
Process becomes useful at around 20 closed trades, and the per-setup feedback switches on at 30 trades in a single tag.
Coach (optional AI review)
Rules → Coach, paste an Anthropic API key from console.anthropic.com. Two
buttons then appear under the Coach tab: a weekly review and a pattern read
across your whole journal, plus a "check this against my record" button on the
ticket once a setup has 10 closed trades.

It only ever receives your closed trades with prices stripped — tag, wording,
weekday, rupee result, and whether you exited at plan. It has no market data
and no open positions, so it structurally cannot suggest a trade. It tells you
what you have been doing, not what to do next.

The key is stored in this browser and goes directly to Anthropic. It never
reaches me or any server of mine. Calls cost a fraction of a rupee each. Skip
it entirely and everything else works unchanged.

Exit reminders
The app has no broker connection and cannot close a position. It can nudge you
at the two moments exits get forgotten: the intraday square-off window (default
15:12, editable) and the instant your daily loss cap is breached. Enable
notifications under Rules.

Real automated exits — GTT stops attached on fill, trailing, forced square-off —
need the server build, a broker Algo-ID, and a static-IP VPS. That's the other
zip.

What's stored, and where
Everything lives in your browser's local storage on that one device. Nothing is
uploaded, there is no account, and there is no server to breach. The flip side:
clearing site data erases it, and it doesn't sync between phone and laptop.
Export to JSON from the Rules tab now and then.

Notes
Charge rates are hardcoded defaults (STT, GST, stamp duty, SEBI, exchange,
and Zerodha-style brokerage). They change with circulars and Finance Acts.
Check the net P&L on your first logged trade against the real contract note,
and edit the R table near the top of the script in index.html if it drifts.
The daily lock and tilt pause are honest, not enforced. Nothing stops you
opening your broker app anyway. The friction is the whole mechanism; if you
find yourself routing around it, that's data about your process too.
Options: enter premium per unit as the price and total units (lots ×
lot size) as quantity — not notional. STT and exchange charges apply to
premium turnover, and getting this wrong is the most common F&O costing error.
Informational record-keeping only. Not investment advice, not a recommendation
to buy or sell any security.
