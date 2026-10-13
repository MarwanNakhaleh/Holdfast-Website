# Holdfast — canonical site content

Single source of truth for all pages. Copy may be lightly adapted for voice,
but **commands, URLs, ports, and steps must be used verbatim.**

## Brand architecture (locked)

- **Brand / company name:** Holdfast.
- **Product name (the device):** Holdfast Brick. The device is genuinely a
  brick — small, solid, lives on a shelf. Existing visuals (brick-red
  palette, brick-shaped step icons, the `tangible-brick` design direction)
  stay.
- **Domain:** holdfastbrick.com.
- **In running copy**, "Holdfast" is the brand; "the brick" is the device.
  First mention in a section may read "Holdfast Brick" for clarity;
  afterwards "the brick" reads naturally and is now literally correct.

## Product truth

- Holdfast is a small device (a Raspberry Pi) that plugs into your home
  router and blocks ads and trackers for **every device on your network** —
  phones, TVs, laptops, guests. No app installs per device, no subscriptions,
  no cloud account. Your data never leaves your home.
- It runs AdGuard Home (ad blocking) + Unbound with DNS-over-TLS (private,
  encrypted lookups) + an iOS companion app that finds the brick
  automatically and pairs with a 6-digit code.
- Honest limitation (must appear in the guide, not buried): in-stream video
  ads on streaming services (Disney+, Hulu, YouTube) are stitched into the
  video server-side and **can't be reliably blocked by DNS** — sometimes a
  blocklist catches them, sometimes it doesn't. We won't promise streaming
  ads are gone. What works dependably: web ads, in-app banners, trackers,
  telemetry, smart-TV home-screen ads.
- Repos: https://github.com/MarwanNakhaleh/HoldfastBrickAPI (runs on the Pi),
  https://github.com/MarwanNakhaleh/HoldfastBrickUI-iOS (the app).

## Kit teaser (future product — "coming soon", no checkout)

Pre-built Holdfast Brick kit: pre-flashed, pre-configured — plug it into your
router, open the app, scan the pairing code, done. Pricing promise:
**the cost of the parts plus $50 flat.** Email-me-when-ready is fine as a
placeholder CTA (mailto: link acceptable, no fake forms).

## Setup guide — exact steps

### What you need (~$70–90)
- Raspberry Pi 5 (2 GB is plenty) — older models with an Ethernet port
  (Pi 4, 3B+) work too
- microSD card, 16 GB or larger
- The official Pi 5 power supply (27 W USB-C)
- One Ethernet cable
- A phone or computer on the same WiFi

### Step 1 — Flash the SD card
1. Install Raspberry Pi Imager (rpi.org) on your computer.
2. Choose **Raspberry Pi OS Lite (64-bit)** (DietPi also works).
3. In the Imager's settings (gear icon): **enable SSH**, set a username and
   password, and set the hostname if you like.
4. Write the card, then put it in the Pi.

### Step 2 — Plug the brick into your router
Connect the Ethernet cable from the Pi to any LAN port on your router, then
plug in power. Give it a minute to boot. Wired is required — the brick will
serve your whole network and must not depend on WiFi.

### Step 3 — Install the Holdfast software
Find the Pi's address in your router's device list (or try
`ssh <username>@raspberrypi.local`), then:

```
ssh <username>@<pi-address>
git clone https://github.com/MarwanNakhaleh/HoldfastBrickAPI.git
cd HoldfastBrickAPI
sudo bash deploy/provision.sh
```

The script installs and wires everything: AdGuard Home, Unbound with
encrypted DNS (DNS-over-TLS to Cloudflare/Quad9), Tailscale (optional remote
access), ntopng, and the Holdfast API. It's safe to re-run any time.

### Step 4 — Finish AdGuard's one-time wizard
Open `http://<pi-address>:3000` in a browser. Choose web port **3000** and
DNS port **53**, create an admin login, finish the wizard — then run
`sudo bash deploy/provision.sh` once more. The re-run wires AdGuard to the
encrypted DNS chain and creates the app's credentials automatically.

### Step 5 — Connect the app
Build HoldfastBrickUI-iOS from Xcode onto your iPhone/iPad (App Store release
coming). On first launch the app finds the brick on your WiFi by itself.
Enter the 6-digit pairing code — it's printed at the end of the install, or
run `sudo holdfastbrick-pair` on the Pi for a fresh one. Allow the "local
network" permission when iOS asks.

### Step 6 — Protect every device
In the app: **Ad Blocking → Whole-home protection**. The guided flow checks
your network, walks you through turning off your router's DHCP (with a
direct link to your router's admin page), and flips the brick to handing out
addresses — after that, every device on the network is protected
automatically, including guests.

Xfinity note: xFi gateways can't turn DHCP off. Workaround the app will walk
you through: shrink the gateway's DHCP range to a single address (e.g.
10.0.0.253–10.0.0.253); devices then migrate to the brick as their leases
renew.

### Troubleshooting quick hits
- App can't find the brick → same WiFi? Local Network permission on?
  (Settings → Privacy & Security → Local Network). VPN off?
- Ads still showing on a device → it may still hold an old DHCP lease;
  toggle its WiFi off/on.
- Streaming ads still showing → expected; see the honest limitation above.

## Voice
Plain, direct, warm. Never "revolutionary/seamless/empower". The reader owns
their network; the brick works for them. Sentence case everywhere.


## Reservation offer (deposit test, October 2026)

- Product: Holdfast Brick, prebuilt (Intel N150, 16GB RAM, 512GB SSD, 2.5GbE)
- Price: $299 one-time, no subscription
- Reservation: $15 via Stripe, fully refundable anytime, counts toward purchase
- No ship date is promised anywhere; refund terms live on terms.html
- Savings math and approved claims: Holdfast/docs/marketing-claims-substantiation.md
  (YouTube Premium $15.99/mo individual, $26.99/mo family; Google One / iCloud+
  storage $35.88-$119.88/yr; 1Password Families $71.88/yr — all dated October 2026)
- Honest limits that MUST stay on the page: in-stream streaming ads, Spotify
  audio ads, and sponsored content are not blockable; photo backups are the
  user's responsibility until a backup feature ships
- Files: reserve.html, privacy.html, terms.html; deposit flow is a Stripe
  payment link (PAYMENT_LINK_URL placeholder in reserve.html)
