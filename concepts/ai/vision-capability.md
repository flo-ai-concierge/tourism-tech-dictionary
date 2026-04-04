# AI Vision (Image Reading)

## What it is
The ability for an AI assistant to see and understand images — screenshots, photos, documents. The AI receives the image alongside the text message and can describe what it sees, read text in the image, and respond with full context.

## Tourism translation
Before vision: Your concierge can only read written notes. If a guest holds up a photo of a broken faucet, the concierge says "I can't see that, can you describe it?"

After vision: Your concierge looks at the photo, sees the broken faucet handle, identifies it as a Moen cartridge issue, and creates a maintenance task — all from seeing the image.

For operations teams, this means field staff can snap photos of issues (propane gauges, broken fixtures, stains, maintenance needs) and send them directly to the AI. The AI reads the photo and takes action.

## How it works
1. User sends a message with an image attachment (Slack, chat, etc.)
2. System detects the image file, downloads it
3. Image is converted to base64 encoding and sent to the AI model
4. AI "sees" both the text message AND the image
5. AI responds with context from both sources
6. Image is stripped from session history after processing (saves memory)

## Constraints
- Only processes image types: PNG, JPEG, GIF, WebP
- Maximum file size: ~4MB (AI model limit)
- If image download fails, AI still processes the text and notes it couldn't read the image
- Images are not stored in conversation history (too large) — replaced with a text placeholder

## When you'll encounter it
- Field team sends photo of a maintenance issue → AI creates task with details from the photo
- Manager sends screenshot of a report → AI reads and discusses the numbers shown
- Cleaner sends photo of a supply level → AI logs the inventory data

## Related concepts
- [Data Integrity Rules](data-integrity-rules.md) — even with vision, verify before stating facts
