# Slack Block Kit

## What it is
Slack's structured message format for rich, visual posts. Instead of plain text, you send a JSON payload describing blocks (headers, sections, buttons, dividers, images, colored accents) and Slack renders it as a beautiful card with links, actions, and formatting.

## Tourism Translation
**"A welcome amenity card at check-in — not just a note."**

A plain note says: "Welcome. Wifi: FLOHOM_Guest, password: flohom2026. Pool closes at 9. Checkout at 10."

An amenity card version has a logo at the top, a photo of the pool, a QR code for the Wi-Fi, a map of the property, a tear-off coupon for breakfast, and an SOS number in a colored box. Same information, infinitely better experience.

Block Kit is the amenity card version of a Slack message.

## Why it matters

### Plain text Slack messages are cluttered
If the `#reviews` bot posted plain text, every review would look like a wall of characters. The team's eyes would glaze over. With Block Kit, each review is a clean card with:
- Colored left accent bar (platform color)
- Bold header with emoji + stars + platform + property
- Secondary line with guest name + date
- Indented quote block showing the review text
- A prominent "Respond in FLO Bridge" button at the bottom
- A thin divider underneath

### Buttons that do things
Block Kit supports interactive action buttons. The "Respond in FLO Bridge" button isn't just a link — it's a Block Kit action element that opens the review detail page in a new tab. The team can click directly from Slack into the FLO workflow without copying URLs.

### Attachment color for left accent
The `color` field on an attachment sets a colored bar on the left side of the card. We use this for platform identification:
- `#FF5A5F` (Airbnb red)
- `#245ABE` (VRBO blue)
- `#34A853` (Google green)
- `#759A9B` (FLOHOM teal for direct)

### Real FLOHOM example
```js
{
  text: "New review from Kat Jones",  // fallback for notifications
  attachments: [{
    color: "#34A853",  // Google green
    blocks: [
      { type: "section", text: { type: "mrkdwn", text: "🟢 ⭐⭐⭐  *Google* · FLOHOM 10 — Rudee Retreat\nKat Jones · Apr 7, 2026" }},
      { type: "section", text: { type: "mrkdwn", text: "> I had a difficulty turning on the firepit..." }},
      { type: "actions", elements: [{ type: "button", text: { type: "plain_text", text: "Respond in FLO Bridge" }, url: "https://flohom-guest.onrender.com/admin/reputation/719", style: "primary" }] },
      { type: "divider" }
    ]
  }]
}
```

## In simpler terms
It's the difference between a plain-text email and a branded HTML email with images, buttons, and colored sections. Same message, way more useful.
