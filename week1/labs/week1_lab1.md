# Lab 1 — Profile Card (HTML/CSS From Scratch)

> Build a single **profile card** webpage using only **HTML + CSS**. No libraries. No starter code.

---

## 🎯 Objectives

- Create a minimal HTML document and link a stylesheet
- Structure a small UI component (profile card) with semantic elements
- Practice core CSS (box model, spacing, borders, typography, hover/focus states)
- Keep layout responsive and centered

## Outcome
<img width="1440" height="750" alt="Screenshot 2025-09-08 at 3 39 50 PM" src="https://github.com/user-attachments/assets/7daf652a-ff0a-423b-ac1d-fc8448aee05b" />

---

## ⏱ Timebox

**15–30 minutes**

- Setup (3) • Structure (5) • Style (7–15) • Verify (3) • Polish (2)

---

## What You Produce

- `index.html`
- `styles.css`
- One screenshot of the final result

---

## Acceptance Criteria

- Single card centered on the page
- Card contains: avatar image, name (heading), role (paragraph), three skill tags, and one call-to-action button
- Avatar appears circular
- Tags render as “pills” (inline chips)
- Button has a visible hover state
- Basic focus styles for keyboard accessibility
- No external frameworks

---

## Step-by-Step

### Step 1 — Project Setup

- Create a new folder named `lab1-profile-card`
- Inside the folder, create two files: `index.html` and `styles.css`
- Plan to open `index.html` directly in the browser to test

**Checkpoint**

- [ ] Folder exists
- [ ] Both files created
- [ ] You can open `index.html` in a browser

---

### Step 2 — HTML Skeleton

- In `index.html`, outline a valid HTML document (doctype, html, head, body)
- Link `styles.css` in the document head
- In the body, add a **single page wrapper** that will center content
- Inside the wrapper, add a **card container** (semantic choice is yours)

**Card content (top to bottom):**

- Profile **image** element (use any image source you have)
- **Name** as a main heading
- **Role** as a short paragraph (e.g., “Student • Web Dev”)
- **Skills** as a short list of three items
- A **primary button** (CTA), e.g., “Connect”

**Checkpoint**

- [ ] Wrapper and card containers exist
- [ ] Image, heading, paragraph, list (3 items), and button added
- [ ] No inline styles yet (CSS will handle visuals)

---

### Step 3 — Base CSS

- In `styles.css`, define base styles:
  - Reset box sizing
  - Set body font family and background color
  - Ensure the page wrapper can center the card both vertically and horizontally

**Checkpoint**

- [ ] Body uses a readable sans-serif stack
- [ ] Page wrapper will center content on all screens

---

### Step 4 — Card Styling

- Give the card a **max width** (around 320–360px) and make it responsive
- Add **padding**, **rounded corners**, a **subtle border** or **shadow**
- Center text inside the card

**Checkpoint**

- [ ] Card width stays comfortable on mobile and desktop
- [ ] Card has clear visual separation from the page background

---

### Step 5 — Avatar Styling

- Ensure the profile image displays as a **perfect circle**
- Constrain its size (consistent width/height)
- Keep it centered inside the card

**Checkpoint**

- [ ] Avatar is circular and not distorted
- [ ] Avatar is centered above the text

---

### Step 6 — Typography

- Increase **name** size and make it bold
- Reduce and mute **role** color slightly for contrast
- Maintain clear vertical spacing between elements

**Checkpoint**

- [ ] Visual hierarchy: name > role
- [ ] Clean, readable spacing

---

### Step 7 — Skill Tags

- Render the list inline (skills in one line or two, depending on width)
- Add background color, rounded edges, and compact padding to each tag
- Add small gap between tags

**Checkpoint**

- [ ] Three tags appear as pill-shaped chips
- [ ] Tags wrap naturally on smaller screens

---

### Step 8 — Button Interaction

- Style the button with a solid background and white text
- Add rounded corners and comfortable padding
- Add a **hover** effect (e.g., slight brightness change)
- Ensure a visible **focus** outline for keyboard users

**Checkpoint**

- [ ] Hover feedback is obvious
- [ ] Focus ring is visible and accessible

---

### Step 9 — Final Verification

Open `index.html` in a browser and confirm:

- [ ] The card is centered on the page
- [ ] The avatar is circular
- [ ] The name and role are styled with clear hierarchy
- [ ] Tags look like pills with spacing
- [ ] Button has hover + focus feedback
- [ ] No external CSS libraries used

## To view get the go live vscode extension and open your project

## 🌟 Stretch (Optional, 2–5 min)

- Add a **subtle hover effect** to the card (slight lift or stronger shadow)
- Alternate a **second tag color** (e.g., every other tag)
- Swap the avatar to your own image and adjust sizes to fit cleanly

---

## 📤 Submission

- Turn in `index.html`, `styles.css`, and a screenshot of the page
- Briefly note anything you customized (name, role, color choices)

---
