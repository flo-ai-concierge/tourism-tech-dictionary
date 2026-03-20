# DevDependencies

## What it is
Software packages that are only needed during development and testing — not when the app is actually running in production. Examples: testing frameworks, code linters, build tools, documentation generators.

## Tourism Translation
**Back-of-house supplies.** Cleaning chemicals, maintenance tools, staff uniforms, the inventory clipboard, the training manual. Guests never see or use these items, but the hotel can't operate without them behind the scenes.

When you're "opening the hotel to guests" (deploying to production), you don't need the training manuals in every room. You only need what guests actually use. Keeping back-of-house supplies out of guest areas saves space and keeps things clean.

## When you'll encounter it
- When your build is running out of memory — removing heavy devDependencies before the build can free up space
- When reviewing `package.json` — dependencies are "guest supplies," devDependencies are "staff supplies"
- When optimizing deployment size

## Real example
Puppeteer (a browser automation tool) is 200+ MB. If it's only used for internal scripts and never by the live website, it should be a devDependency. Leaving it as a regular dependency is like storing the industrial floor polisher in the guest suite — it takes up space and serves no purpose there.

## Related concepts
- [npm install](./npm-install.md)
- [OOM — Out of Memory](../infrastructure/oom-out-of-memory.md)
