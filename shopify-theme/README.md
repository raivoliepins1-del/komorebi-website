# Shopify theme changes

Section group settings deployed to the Komorebi Impulse theme on komorebiworld.com.

These are theme editor settings files, not code. They are kept here so each change
to the live store has a reviewable diff and a rollback reference.

## 2026-09-16 — email capture (popup + footer)

Before this change the storefront had **no email capture at all**: no popup, no footer
signup form, and no Klaviyo script loading. Verified by fetching the live homepage.

**`sections/popup-group.json`**
- `newsletter-popup` flipped from `disabled: true` to `disabled: false`.
- Copy rewritten. The previous draft promised "Save 10% off with our Newsletter" and a
  discount code, but nothing in the store could send that code. Replaced with an early
  access offer that needs no delivery mechanism.
- `button_label` cleared. It was "Lets explore" with an empty `button_link`, which would
  have rendered a button linking to the current page.
- Fires 5s after landing, once per 30 days, hidden from logged in customers.

**`sections/footer-group.json`**
- Added block `footer-2`, type `newsletter`, to the `footer` section.
- Widths rebalanced to sum to 100% on one row: menu 45, newsletter 35, logo 20.
- The newsletter snippet also renders the social icons, which the footer did not have before.

Both forms post to Shopify's native `{% form 'customer' %}` with tags `prospect,newsletter`,
so signups land in Shopify Customers and sync onward if an email app is connected later.

Copy is French because French is the site source language. It has not yet been read by a
native French speaker.
