# Immutable State Update

## What it is
Creating a fresh copy of data with changes applied, rather than modifying the original. React detects the new object reference and updates the screen. This is the correct pattern for state management in React — always return new objects, never mutate existing ones.

## Tourism Translation
**"Writing a brand new room assignment card instead of erasing the old one."**

When a guest switches rooms, you don't erase their old card — you write a completely new one and hand it to the front desk. They see a new card, immediately update their system. No confusion, no missed updates.

## Why it matters
The fix for the FLO Analyze display bug. Instead of mutating `prev.groups` directly, the code now creates a new `groups` object with `{ ...prev, groups: newGroups }`. React sees a new reference at every level and re-renders the card with the analysis result visible.
