# SCE Web Dev Lab — Recipe Book (HTML + CSS)

## Objective

- [ ] Build a 4-page site: one Home page (table of contents) and three Recipe pages
- [ ] Use only HTML and CSS
- [ ] Finish with clean styling and basic responsiveness

## Setup (Terminal & Editor)

- [ ] Open your terminal
- [ ] Navigate to a working folder of your choice

```
cd your/folder/path
```

- [ ] Create a new project folder named `sce-web-dev-recipe-book`

```
mkdir sce-web-dev-recipe-book
```

- [ ] Change into the new project folder

```
cd sce-web-dev-recipe-book
```

- [ ] Open the project folder in your code editor

```
code .
```

- [ ] Create a file named `index.html` in the root

```
touch index.html
```

- [ ] Create a file named `styles.css` in the root

```
touch styles.css
```

- [ ] Create a folder named `recipes`

```
mkdir recipes
```

cd into recipes

```
cd recipes
```

- [ ] Inside `recipes`, create three files: `pasta.html`, `tacos.html`, `pancakes.html`

```
touch pasta.html
```

```
touch tacos.html
```

```
touch pancakes.html
```

- [ ] Create a folder path `assets/images` for three recipe images

## Global Requirements

- [ ] Use semantic HTML where appropriate (`header`, `main`, `footer`, `nav`, `section`, `article`)
- [ ] Reuse the same header and footer on all pages
- [ ] Home page links to each recipe page; each recipe page links back to Home
- [ ] Use CSS classes (avoid inline styles)
- [ ] Provide readable text hierarchy with headings and paragraphs
- [ ] Add descriptive alt text to all images
- [ ] Ensure site is usable and visually consistent across pages

### For now we are just going to add the elements, we will style them later.

## Checkpoint 1 — Home Page
#### Open your index page on your browser
  - [ ] If on MAC use:
```
open index.html
```
  - [ ] If on Windows use:
```
start index.html
```
- [ ] First lets connect your styles sheet to your html page
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Homepage</title>
        <link rel="stylesheet" href="styles.css">
    </head>
    <body>
        
    </body>
</html>
```
- [ ] In index.html add a site header with a clear site title and optional subtitle
- [ ] Add a main section titled “Table of Contents”
- [ ] For each recipe card include: title, one-sentence blurb, and link to its recipe page
- [ ] Add a site footer with your name or a simple message
- [ ] Confirm navigation works: clicking a card opens the correct recipe page

### Should look something like this:
<img width="391" height="788" alt="Screenshot 2025-09-10 at 2 20 53 PM" src="https://github.com/user-attachments/assets/bc03a2ec-5c90-42ee-963f-cc21c2f80c1c" />


## Checkpoint 2 — Recipe Pages

#### For this checkpoint we will implement on the 3 recipes pages.

- [ ] Include the same header and footer as the Home page
- [ ] Add a clear page title matching the recipe
- [ ] Place one image of the dish near the top
- [ ] Add a short description paragraph
- [ ] Add an unordered list of ingredients
- [ ] Add an ordered list of step-by-step instructions
- [ ] Add a “Back to Home” link

### Should look something like this:
<img width="468" height="907" alt="Screenshot 2025-09-10 at 2 21 10 PM" src="https://github.com/user-attachments/assets/8f3dbbd7-33e7-40a4-b925-aac68b524730" />


## Checkpoint 3 — Styling & Responsiveness

- [ ] Apply consistent colors, fonts, and spacing in `styles.css`
- [ ] Use CSS Grid for the homepage recipe cards
- [ ] Style recipe pages with margins, headings, and image sizing
- [ ] Add hover effects to links or recipe tiles
- [ ] Make the layout responsive (e.g., single column on small screens)
- [ ] Verify the site looks good on both desktop and mobile

### This is the end result

<img width="1920" height="934" alt="Screenshot 2025-09-10 at 2 16 33 PM" src="https://github.com/user-attachments/assets/f65a6b70-6f26-40c8-a1df-0a54b818b7b6" />
<img width="630" height="773" alt="Screenshot 2025-09-10 at 2 18 48 PM" src="https://github.com/user-attachments/assets/a5f81309-983e-447e-9494-82e380bf7477" />
