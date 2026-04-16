# Field Name Mismatch

## What it is
When the frontend sends data using one field name (like "body") but the backend expects a different name (like "content"), causing the request to silently fail validation. The data is there, but the server can't find it because it's looking under the wrong key.

## Tourism Translation
**Like a guest filling out a check-in form where the "Phone" field is labeled "Mobile" on the app but "Phone Number" in the PMS.** The guest typed their number, but the property management system can't find it because it's looking for "Phone Number" and the app sent "Mobile." The data never arrives — not because it's missing, but because the two systems call it different things.

## When you'll encounter it
- When a form submission returns a "field required" error even though you filled it in
- When frontend and backend were built at different times or by different people
- When an API was updated but the calling code wasn't updated to match
