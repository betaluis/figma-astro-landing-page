# Creating design in figma

- Start by creating a new design and naming it "landing page."

- Create a frame and choose the largest one which will be "desktop."

- Drag it down to give yourself some space to work.

- Usually you'd want to start with a mobile design first, then tablet, then desktop, but in this tutorial Chris went with just the desktop version.

## Setting up the base (colors and types)

The reason we do this is because then we can reference these colors and types later on and it'll be much more effecient.

- Create a new page on the left and call it "style guide"

- Add a frame where we can gather our colors and types.

- Choose the circle shape and hold shift as you drag it out.

    - Click on the four dots on the right side panel to create a new color style.

    - Call it background. Now, if we want to update this color and we used it in multiple different places, then we can update all the elements using this color at once instead of manually.

    - Create another circle (command and drag), detach the previous color style, and then click on the four dots again to add another color.

### Here are the different color sets that you'll need to create

- #0F172A : Background
- #5957E9 : Accent 1
- #EC4899 : Accent 2
- #F87171 : Accent 3
- #8D98CD : Text-alt
- #ACB3CA : Muted
- #E0E7FF : Text
- #FAFBFF : White

### Now we need to set up the types

- Go to type-scale.com
- The font will be "Inter"
- Base font size will be "22px" for desktop
- Scale will be "Perfect Fourth"
- Weight is 400

Now create a new frame where we'll create the types. Call it text.

- "1" and change the font to "inter" 
- font-size 92.59px
- font-weight bold
- Right click on the "1" and select "add auto layout." (you can also hit shift+a)
- Under "constraints and resizing, click the center of the box to center.
- padding = 0
- Copy the text down and change the font-size 69.46 and change "1" to "2"

### Create component set

- Grab both of the text items
- Click the icon with four squares at the top in the center of the menu bar.
- Select "create component set"
- You're going to want to name it something like "text-scale"

This allows us to reference this as an asset anywehre in the site. That's helpful because we don't have to choose the font-size every time we have text. All we have to choose is the component we want.

- Rename the component variant to "Size" instead of "Property 1." This is found on the right side menu.
- Now grab the components on the left and change the size to "4xl and 3xl."

### Add the third text item.

- With the entire component selected click the bottom plus button.
- Add the size - 2xl
- Add the font size to the actual text - 52.11
- Repeat this process.

Now the section might be getting a bit long so try rearranging the numbers horizontally.

- Do this by dragging the component out and then dragging the numbers.

- Also, you can select multiple fonts, hold command, and drag down to create new ones.

- Create 4, 5, 6, 7, and 8. All will be bold.
    
    - 4 = 39.09px / xl 
    - 5 = 29.33px / lg
    - 6 = 22.00px / md 
    - 7 = 16.50px / sm 
    - 8 = 12.38px / xs

The reason we've created these components is because Figma stores them as assets. We can then grab any of the fonts later on and use them without having to manually type out the size, font, etc.

The assets are found on the left side pannel at the top, next to "Layers", or you can use Shift + i. 

## Create button components

- Make the frame and call it buttons.
- Grab one of the text components (shift + i)
- Fill the background color
- "Button Text" and it will be medium size.
- Hit shift + a to create an auto layout. Now we have padding. Play around with the padding for the button. 10 at the top/bottom and 25 left/right works well.
- Change the background to the primary
- Copy the button and change the backgroudn to accent
- Highlight both of them and create component set at the top.
- Change the variant to Color and give each button a value "Accent 1 and Accent 2"

What if you wanted to add a hover state?

- Create a new primary button by choosing the component and place it below the first one.
- Change the background color to whatever you want.
- Go back to the component state itself and add a new property called hover. You do that on the right side panel.
- Now all of the buttons have a hover button
- Set the values for the hover property to be either true or false for each button
- Copy the button and create the second hover state
- Create 2 more buttons and repeat the steps above. The last button with be a transparent button with the text changing colors when hovered.

Create gradient color

- Change the background for the second button to a gradient color.  
- Start by creating a new color in the colors component. 
- Unlink it.
- Create gradient.
- Then select the button and change the variant value.
- Change the hover state as well.

## Edits 

- Create a new variant of the text components. So select all of them and drag them next to the original.

- Create the new property called colors.

- The second variant should have the muted gray as a the text color. Remember to give a value to the variant for each.
