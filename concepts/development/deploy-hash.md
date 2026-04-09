# Deploy Hash / Build Marker

## What it is
A unique identifier attached to each new version of your deployed app. When you push new code, your hosting provider (Render, Vercel, Netlify) generates a new build with a new hash. You can use that hash to verify which version is actually running in production.

## Tourism Translation
**"The revision number stamped at the bottom of each new print run of the room-service menu."**

You print 500 menus on March 1. Bottom-right corner says `Rev 3.1`. On March 15, you update the prices and reprint. New menus say `Rev 3.2`. Now if a guest complains "the price on the menu doesn't match what I was charged," you look at the menu in their hand, check the revision number, and instantly know whether they had the old version or the new one.

## Why it matters

### Verifies the deploy actually happened
Pushing code to GitHub doesn't mean it's live. Render has to build and deploy it, which takes 2-5 minutes. Before that finishes, the old version is still running. Checking the deploy hash tells you definitively whether the new code is serving traffic yet.

### Catches stale caches
Sometimes a deploy succeeds but a CDN serves an old cached copy. The hash being the same tells you the cache hasn't refreshed. The hash being different confirms the new build is live.

### Enables safe polling
During deploys, we poll the app's HTML every 15 seconds and look at the embedded build marker:
```html
<!--AINzsMA8k82JkTMaM85Vx-->
```
That comment is Next.js's build ID. When it changes from the previous value, we know the new deploy is live and safe to start testing.

### Real FLOHOM example
```bash
PREV="<!--3E9oblb_JucU9DgBL5nRH-->"
for i in 1 2 3 4 5 6 7 8 9 10 11 12; do
  HASH=$(curl -sS https://flohom-guest.onrender.com/admin/reputation | grep -oE '<!--[A-Za-z0-9_-]{15,30}-->' | head -1)
  if [ "$HASH" != "$PREV" ]; then
    echo "NEW DEPLOY LIVE: $HASH"
    break
  fi
  sleep 15
done
```
This polls until the hash changes, then declares the deploy ready. We used this pattern all day during the #reviews build.

## In simpler terms
It's the "version number" on the bottom of a document. If two people are looking at documents with different version numbers, they're not looking at the same thing, no matter how much they agree on what it says.
