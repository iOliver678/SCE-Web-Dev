# Lab 1 - Javascript for begineers

### Goals:

- Be able to understand how to write a function
- How to manipulate the DOM

## Lab Overview
SCE needs your help, there is a hidden message sent from an unknown source that claims our president is hiding a massive secret, we need to uncover it.
You are already given starter code `index.html` and `styles.css`. You're job is going to be to create a file called `script.js` for out javascript. This script will allow us to decrypt a secret message! So it will take in an input we output the result.

## Step 0: Setting up
Navigate to your folder of choice using your terminal and create a new folder called week2_lab
```
mkdir week2_lab
```
Open that using your terminal by cding into it and using code . to open your ide. Once you are inside the IDE create a `index.html`, `styles.css` and `script.js`. Copy over the **MY** `index.html` and  `styles.css` code into **YOUR** files. 
Now lets link your `script.js` to your html page, easily do this by adding `script src="script.js"></script>` at the bottom of the body of the page.

Once that is there open the index file in your browser and you should see this:
<img width="530" height="274" alt="Screenshot 2025-09-14 at 4 19 51 PM" src="https://github.com/user-attachments/assets/c3c81510-60e5-4c1a-902e-fba9cf49a0e8" />

**Checkpoint:**
- [ ] Have your `index.html` and  `styles.css` set up and see the page
- [ ] Have an **EMPTY** `script.js`
- [ ] Linked to your html page

## Step 1: Manipulating the DOM
All of our work moving forward will be done in the `script.js` file, but we will need to refrence the `index.html` file. So right now go and take a look at `index.html` and familiarize yourself. 

We are first going to set up the DOM functionality. There are 3 elements we need to to interact with, can you identify those?

The 3 elements are the button, the input field, and our output field. In our `index.html` those elements all have their own id's. We can see those here:
```html
    <input type="text" id="encodedInput">

    <button id="decodeButton">Decode!</button>

    <p>Decoded Message:</p>
    <div id="decodedOutput"></div>
```
The way you interact with elements is by using the DOM. Using `document.getElementById('element_name')` and you can assign that to a variable so you can easily work with.
So go ahead and do that for the 3 elements.

Once you have those 3 elements assigned to variables we can now set up an action listener, using the var you assigned the button element to you can create it. Remeber what type of input will the users be using for this? `click`!

```js
var.addEventListener('click' () => {
  //logic
}
```
Easily set up an event listener using an arrow function! We dont need to pass in any arguments for this. For now lets make sure it works so we are just going to simply render our message, do this by assiging our var (the one you assigned from the output element) `textContent` to the **_value_** of our var of the input element.

```js
var.addEventListener('click' () => {
  outputvar.textContent = inputelementvar.value;
}
```

Now on click of the button it will output the input. That tells us our button works we succesfully manipulated the DOM. Once you confirm it works remove this logic.

Now in your eventlistner we want to clean the input and remove it of any whitespaces to make sure logic runs smoothly, do so by assiging a var called `raw` to the trimmed value of our input element.

```javascript
var.addEventListener('click' () => {
  const raw = (inputvar.value || ' ').trim() // || ' ' is just a saftey check for when its empty
}
```
## Step 2:
The unknow source has told us that the way we can decode this is by first translating some chars. They gave us this map:
| Symbol | Letter |
|--------|--------|
| #      | a      |
| %      | e      |
| ^      | o      |
| &      | s      |
| *      | m      |

Knowing this we can now translate some chars! 

The way we are going to do this is by creating a function that takes in a string and is able to replace chars with other chars.

Create a function called translateChares.

```javascript
function translateChars(message){
  //logic here
}
```
Once created we can actually use a built in method called replaceAll(arg1, arg2) where it replaces arg1 with arg2! You use this method with dot notation, and you can also chain these!

Ill show an example:
```javascript
function translateChars(message){
  return message.replaceAll('#', 'a').replaceAll('%','e')
}
```
Do this for the rest of the chars!

## Step 3:
The unknown source says to also reverse the words! 

Create a new function called reverseEachWord. 
```javascript
function reverseEachWord(message){
  //logic here
}
```
Okay so lets think about this, what are we going to input into the function... a string! So we can just used `reverse()` on it! **WRONG**, we were told to just reverse the words not the entire sentance! So this makes it a bit more tricky. One simple approach is we can do the following:
1. Split up the string by its words and store as an array with elements -> Hello world !-> ['Hello', 'World', '!']
2. Create an empty array where we will store our reversed words
3. Now we can loop through our array that is holding our words and reverse each word individually and add them to the empty array we created!
4. Then we can just return that array as a string!

This wont be easy to implement if you have never leetcoded, otherwise this is a simple technique. So dont worry if this is a bit hard to find intuative 

```javascript
function reverseEachWord(message){
  //logic
}
```
Now we are almost done! we just need to use these methods on click!

## Step 4:
We need to call our methods in order and manipulate the DOM to show our out similar to the way we just showed the default input


```javascript
var.addEventListener('click' () => {
  const raw = (inputvar.value || ' ').trim(); // || ' ' is just a saftey check for when its empty
  const step1 = translateChars(raw); //calls first method
  const decoded = reverseEachWord(step1); // pass in first method result 
  outputvar.textContent = decoded; //show our output by manipulating the DOM
}
```

After you do this you can now paste our secret message `r%vil^ &%vol #hct#*` into our program!
What is it ?!
