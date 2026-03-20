# npm install

## What it is
A command that downloads and installs all the software packages (dependencies) that your application needs to run. It reads a file called `package.json` that lists everything required, then downloads them into a `node_modules` folder.

## Tourism Translation
**Stocking the property before guest arrival.** Before a guest checks in, you load the property with everything they need: linens, towels, toiletries, kitchen supplies, welcome basket. `npm install` does the same for your app — it loads all the "supplies" the code needs to function.

`package.json` is your **property checklist** — it lists exactly what supplies to stock. `node_modules` is the **storage closet** where everything gets stored.

## When you'll encounter it
- Setting up a project for the first time
- After cloning a repository from GitHub
- When a teammate adds a new package you don't have yet
- During deployment (Render runs this automatically before building)

## The dev vs production distinction
Some supplies are only for staff (cleaning chemicals, maintenance tools) — guests never see them. These are **devDependencies**. Others are for the guest experience (linens, amenities) — these are **production dependencies**.

When deploying to production, you can skip devDependencies with `npm install --omit=dev` — just like you wouldn't put cleaning chemicals in the guest bedroom.

## Related concepts
- [DevDependencies](./dev-dependencies.md)
- [package.json](./package-json.md)
