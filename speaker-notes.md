#1: WOW CSS!
Hello and welcome to WOW! So CSS. 


#2: WHY DO THIS WITH CSS?
Some of you may be wondering: why would you want to do this with CSS when it's pretty easy to just do it with javaScript? Or, even easier, jQuery... 

Well, I found myself wondering from the opposite end of the spectrum...
- Why do I need to do these trivial things with javaScript or jquery?
- Why should I have to include js, and the extra kilobytes, additional complexity and all the things that can go wrong when relying on js for what is really -just a simple on click change to manipulate styling?
- It isn't progressive and in the case of many, many custom jquery plugins and widgets, it isn't accessible.
- It seems like overkill for simple things such as custom styled inputs, simple slide toggles or tabs
- In addition to my js doubt, we also have the rising power and awesomeness of CSS3, which includes some really powerful selectors and combinators, 
- I'd seen pure CSS solutions mentioned before on the interwebs and I thought here's a challenge! 
- Let's investigate this, try make things work and make them work well for the user, the pure HTML5 and CSS3 way…

So lets take a quick look at the different ways we can go PURE CSS...


#3:USING CSS PSEUDO SELECTORS TO DETECT CLICK EVENTS

##:TARGET
- :target llows us to set styles for when an element linked to an anchor tag is clicked
- On click, if there is a match, the :target style is triggered
- Only works with anchor tags with a #URL
- Only works once, so no toggling...
- Unless you add another anchor tag with #URL to go back to the previous state

So that's how I created these slides, using anchor tags and the :target pseudo selector to style the elements targeted on click of the link


#4:USING CSS PSEUDO SELECTORS TO DETECT CLICK EVENTS

##:FOCUS
- This method relies on the user focusing on an element in order to take effect
- Only works with elements that are focusable, or that have been given the "tabindex" attribute
- Clicking anywhere else reverts the element to its default styling
- Not so great in terms of the behaviour this one allows


#5:USING CSS PSEUDO SELECTORS TO DETECT CLICK EVENTS

##:ACTIVE
- This relies on storing a style in an almost infinite transition (9,999,999s or 116 days)
- On click of an element with this transition, the style for the :active state is triggered
- The :active style has a transition of 0s, which temporarily overrides the "infinite" transition and allows any additional styles declared on :active to take effect
- When the element is no longer :active, the "infinite" transition kicks in again, preserving any :active styles applied
- While this is insanely clever, it isn't really feasible
- It only works once and with transitionable values


#6:USING CSS PSEUDO SELECTORS TO DETECT CLICK EVENTS

##:CHECKED
- And finally there is the :checked method, aka the "checkbox hack" as it is popularly known.
- This is the method I ended up choosing to explore as it is the most flexible 
- It allows us to detect and style around a boolean, :checked and not :checked
- There is also the added bonus of NO PAGE JUMPING (which can happen with :target if you’re not using fixed or absolute positioning)

#7: INPUT AND LABEL = AWESOME the HMTL
- At its most basic, we start with HTML that consists of an input and a label
- By keeping the value of the "for" attribute the same as the "name" or "id" attributes we tie the two together
- A click on the <label> will target the <input>


#8: INPUT AND LABEL the DEMO
- A linked label and input allows us to check an input by clicking on the label is associated with
- This opens up a whole range of possibilities...
- The most obvious being a big boost to usability as we can now target either the input or its label!
- What user wants to pinpoint a tiny checkbox when they could just take a wild stab at a larger target?


#9: INPUT AND LABEL the CSS
-Still pretty simple at this stage


#10: CUSTOM STYLED CHECKBOXES the HTML
Now that we don't need to show that ugly default checkbox in order for people to interact with it...
- We can hide it and still be able to check it reliably via its label
- With the input hidden we can then go wild with styling the label itself
- Or use ::before or ::after pseudo elements to add styles to the label


#11: CUSTOM STYLED CHECKBOXES the DEMO

##Display: none vs Opacity: 0
- I used a combination of opacity: 0 and absolute positioning off the viewport to hide the checkbox as setting its display to none means we can no longer tab to it using the keyboard 
- With the help of the :focus selector for the hidden input, I then set up a focus style for the label it's tied to, to assist keyboard surfers
- Not too much CSS to set this up and we have a keyboard friendly component


#12: CUSTOM STYLED CHECKBOXES the CSS
There are a few key things to note here about the CSS:

##::before:
- The ::before pseudo element is used to create the location pin and add it before the label element

##:checked
- The :checked pseudo selector matches elements when they are in their selected states
- This selected state is only applicable to <inputs> of type radio and checkbox
- If they are not selected (or checked) there is no match
- So we can set up default styles for when the input is unchecked
- Using :checked and sibling combinators, we can create selectors that target and set up styles on sibling elements for when an input is :checked

##+ Adjacent Sibling Combinator:
- In this example, the adjacent sibling combinator is to select the label that is the immediate sibling of the input.


#13: CUSTOM STYLED RADIO TOGGLE the HTML 
- Pretty much the same HTML here...
- Inputs and labels, except with radio selects this time
- And we have a switch or toggle


#14: CUSTOM STYLED RADIO TOGGLE the DEMO


#15: CUSTOM STYLED RADIO TOGGLE the CSS
- Slightly different styling for this one, but the same principle
- Using the adjacent sibling combinator to select the label to apply styles on :checked status


#16: CHECKBOX SLIDE TOGGLE the HTML
- Here we have our trusty linked label and input PLUS
- an additional div to hold the contents to be toggled
- The structure of the HTML here is important as all of the elements must be children of the same parent in order for this to work


#17: CHECKBOX SLIDE TOGGLE the DEMO
Neat! A super simple slidetoggle that's just waiting to be styled into whatever you need it to be!


#18: CHECKBOX SLIDE TOGGLE the CSS
The CSS for this isn't getting too hectic yet, but there are a few important things to note:

##Max-height:
- Firstly, the default state of <div> to be toggled has a max-height of 0 
- No margin or padding along the top or bottom
- Overflow-y is set to hidden 
- Basically, anything that can add vertical height is set to 0.
- The reason I went with max-height rather than transform translate-y is that transitioning height will affect and push the rest of the elements down
- This is not the case with translate-y, which takes the element translated out of the box model and floats it over everything else
- The transition is set to all, and waiting on our default style, that way it's triggered on both states, when the element is :checked and unchecked

##Will-change:
- I’ve added an additional little tweak to performance with the "will-change" property is added on :hover of the label that triggers the toggle
- will-change is the successor to the long standing transform: 3d() hack aka null transform hack, which, when applied to an element tricks the browser into using hardware acceleration to handle CSS animations and transforms rather than relying on the CPU
- By declaring the will-change property on an element, we can inform the browser ahead of time that a transformation or animation will occur, allowing it to perform certain optimizations ahead of time
- I've applied will-change specifically to the :hover state of the label that triggers the toggle, so that the optimization is set up just before the click. That's all the time it needs
-There is no need to have will-change hanging around on the default styling of the element, as we would use transition, as this would waste memory
- Sadly, the support for will-change isn't great, but give it a little time.

##~ General sibling combinator:
- Here I use the general sibling combinator to select the div with the class of details and style it for when the checkbox is :checked


#19: SO WHADDA YA’LL THINK SO FAR?

-Is this making sense?
-Does it seem like something you would use?
-Does it feel like this is crossing the line of what HTML and CSS should be doing?


#20: RADIO SELECT TABS the HTML
- The "checkbox hack" with radio select inputs work beautifully for this simple tab component
- As you can see, the basic structure for this is the same as the slide toggle, a hidden input, a label and a div to hold the contents of the tab to be toggled.
- I specifically chose radio selects for this rather than checkboxes as one radio select can be selected at a time
- This ties in well with the expected behaviour of tabs, which are also only active one at a time


#21: RADIO SELECT TABS the DEMO 


#22: RADIO SELECT TABS the CSS 

##Vertical-height: gotcha
- One gotcha to beware of with this particular example, is that you will need to set either a height, or a max-height on the parent that contains the tab component 
- The vertical height of the parent would collapse otherwise 
- This is because the tabs are floated and the tab content is absolutely positioned, everything inside the parent has been taken out of the normal flow of the box model

##Absolutely positioned container divs
- The key things that make these tabs work are the absolutely positioned tab content divs
- :checked status toggles their z-index 
- The tab label’s z-index is also toggled on :checked, but that’s just to make sure the borders respond accordingly 


#23: CHECKBOX ACCORDION MENU the HTML
- Using the same principle, except with checkboxes this time rather than radio selects and different styling...
- We have a simple accordion menu with HTML and CSS only
- Checkboxes chosen rather than radio selects to be able to toggle more than one submenu at a time


#24: CHECKBOX ACCORDION MENU the DEMO


#25: CHECKBOX ACCORDION MENU the CSS
- The CSS here that makes it all work is exactly the same as the simple slide toggle 
- Max-height initially set to 0 and increased on :checked. 
- There’s will-change on hover of the label that triggers the toggle 
- And a transition for max-height waiting on the default styling to transition the height change smoothly both ways


#26: CHECKBOX DROPDOWN MENU BY SOMEONE ELSE
So my initial dropdown menu paled in comparison to this cleverly done one by Chris Coyier of CSS tricks: [Super Awesome Dropdown Menu by Chris Coyier](http://dabblet.com/gist/1507175) This is based on a previous version by Paull Ferguson. I knew the behaviour I wanted was for only one dropdown to be active at a time, yet also be able to close one if it was open. I was experimenting with additional radio buttons when I found this one, well formed and ready to go.

- The really cool trick here is an additional radio input and label that, on initial :checked status, gets bumped in front of the original label that triggers the dropdown. 
- Clicking on this then triggers the :checked style change to change the opacity of the submenu back to 0 as well as bump the initial label to toggle it open back to the front as the closing label goes back to z-index: -1


#27: CHECKBOX EXPAND/COLLAPSE ALL the HTML
- Extend the basic "checkbox hack" principle further we can do all sorts of interesting things
- One toggle that toggles a number of components open and closed
- While also being able to toggle them individually


#28: CHECKBOX EXPAND/COLLAPSE ALL the DEMO


#29: CHECKBOX EXPAND/COLLAPSE ALL the CSS
- Ok, I'll admit this is starting to go overboard, especially if your CSS selectors start looking like this...
- Still, it was super fun to figure out


#30: CONS. WHADDAYA THINK?


#31: TOTALLY IMPARTIAL CONS
- :checked does not have deepest browser support:
-- Internet Explorer up to 8
-- Some versions of Firefox on Linux
-- Android Stock Browser
-- Opera Mini
-- BlackBerry Browser
-- Nokia Xpress Browser
-- UC Browser
-- Firefox Android
- In some cases, extra markup needed to make it work, so not as semantically correct as it could be. The HTML structure required is very specific, elements involved have to share the same parent
- Using CSS to do what is traditionally seen as javaScripts job, interactivity, is bad, Mkay
- Not fully accessible: Even though we can declare aria-roles and initial aria-expanded values on elements,there is no way for us to change them using CSS
- CSS selectors can get overly complex and unreadable


#32: PROS. WHADDAYA THINK?


#33: TOTALLY IMPARTIAL PROS
- Wide support: good to go from IE9 and up!
- Only requires a small amount of additional markup to make it work
- No javascript required!
- It will work no matter what, totes progressive enhance
- More accessible than jquery ui options as components created using the checkbox hack are fully keyboard surfable
- This is CSS badassery at its finest


#34: HOW FAR SHOULD YOU GO?


##35: HOW FAR WOULD I TAKE THIS?

In some instances it makes perfect sense, for example:
-Checkboxes and radio selects that require custom styling
-Simple tabs
-Simple slide toggles
-Possibly even accordion accordion menu

If your CSS selectors start looking monstrous, maybe it's time to reconsider? But then who are we writing our code for? Do I choose to steer away from pure CSS solutions because it makes my CSS more difficult for other devs to read? My users sure as hell don't care what my CSS selectors look like.

Is the benefit of a leaner, js free site outweighed by the fact that I have to add extra lines of markup to make pure CSS solutions work?

Or do I compromise? If my ui needs to be fully accessible, a teeny bit of javaScript will need to be included to correctly manage aria-expanded values...

As with any creative discipline, there are many forms of expression and there are many, many means of achieving an end. It really does come down to you where to draw the line.


#36: WHAT DOES THE FUTURE HOLD? 
Tab Atkins, who writes CSS specs, thinks display: stack is probably the future for a tabbed user interface through CSS.

#37: NOW GO FORTH AND RECONSIDER CSS!


#38: USEFUL LINKS
- [CSS Click Events](http://tympanus.net/codrops/2012/12/17/css-click-events/)
- [Quirksmode CSS Selectors](http://www.quirksmode.org/css/selectors/)
- [Dev Opera: will-change](https://dev.opera.com/articles/css-will-change-property/)
- [Caniuse: will-change](http://caniuse.com/#feat=will-change)
- [Tab Atkins Jr: display: stack](http://www.xanthir.com/blog/b4DV0)