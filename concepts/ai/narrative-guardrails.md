# Narrative Guardrails

## What it is
A post-processing layer that scans AI-generated text for deprecated, wrong, or misleading numbers and either replaces them with correct values or removes them entirely. It runs after the AI produces its response but before the response reaches the user.

## Tourism Translation
**The manager who proofreads the listing before it goes live.**

Your marketing team writes a beautiful listing: "This stunning 5-bedroom villa sleeps 12 guests with a heated pool." But the property was recently renovated and now has 4 bedrooms, sleeps 10, and the pool heater was removed. The manager catches these outdated claims before the listing goes live and replaces them with current facts.

Narrative guardrails do the same thing for AI-generated reports. The AI might reference an old metric ("962 unanswered inquiries") that was computed wrong months ago. The guardrail catches it and replaces it with the current verified number (48).

## Why it matters
AI models have a tendency to reference memorable or dramatic numbers even when the underlying data has changed. If your system once computed "$2.4M in commission leakage" (which was wrong), the AI might keep citing it in summaries because it's a striking figure. Narrative guardrails make this impossible by actively scanning and replacing known-bad values.

## Key principles
1. **Replace, don't just warn** — a warning in the server log doesn't protect the user; replacement in the output does
2. **Scan all text fields** — not just the summary; check insights, action items, tooltips, PDF sections
3. **Use locked values as replacements** — don't replace wrong numbers with other guesses; use the pre-computed truth
4. **Maintain a deprecated number registry** — every time a metric is corrected, add the old value to the blocklist

## Related concepts
- [Locked Values](./locked-values.md)
- [Trust Gate](./trust-gate.md)
