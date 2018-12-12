<!--
    Author: Baseline Curriculum 2.0
    Edited: Ben Hulan, John Barela
    Market: SF, Den

-->

<!--Time is still tight here. -->

<!--10:40 WDI6 -->
<!--10:15 5 minutes -->

<!-- Hook: Raise your hand if you have played Tetris before. Think about trying to fit all those pieces together. Fifteen pieces have come through, and you just need that 4-blocks-in-a-line, but you keep getting those Ls. Now you understand the frustration of the CSS Box Model and Positioning in web development. -->

# CSS Box Model and Positioning

Web pages, at a base level, are made out of boxes. As we've already seen with HTML, our website is basically a reverse game of tetris, in which each rectangular element stacks to the upper left based on how its shaped. Obviously, this is functional, but not organized in the slightest. Today we're gonna look into one of the crucial ways to reshape these boxes into a more functional layout - the CSS Box Model. It will be a necessary cornerstone for almost every project you undertake.

### Objectives
*After this lesson, students will be able to:*

- **Describe** the difference between block, inline, and inline-block elements
- **Adjust** element spacing using padding and margin
- **Create** floating elements to position content removed from the standard document flow
- **Explain** the difference between and use cases of static, relative, fixed, and absolute positioning
- **Create** a page with multi-column layout

### Preparation
We're going to be building off a couple of tools we already know: HTML and CSS. 
Before starting, we should be clear on the following questions: 
- What do we use HTML for? 
- How does CSS augment HTML?

## An Intro to The Box Model

All HTML elements can be considered boxes. Even if you see a circle, it's living within a box. In fact, we can literally think of them as a series of moving boxes, sitting in an empty living room on your moving day - they have the same properties:

- **Width/Height**: How big is your box? This will determine how much of your crap you can stuff into it.
- **Padding**: Let's say you were moving something fragile; you'd probably want to line your box with some packing peanuts or something simliar, to keep it away from the edges.
- **Content**: How much stuff you're trying to cram into your box.
- **Margin**: How far away from other boxes you want this particular box to be. For the sake of our metaphor, imagine that you were creating space between boxes with packing blankets.

The sum of all these properties looks a little like this:

![box-model](http://web.simmons.edu/~grovesd/comm244/notes/week6/box-model.gif)


<!--10:20 10 minutes -->

## Box Model Demo

Let's make some boxes to practice with. We're going to make a digital living room and arrange our boxes in a way that makes sense to us.

- Create a new directory called `box-model-work`
- Create an html page called `index.html` with an externally linked css stylesheet called `main.css`
- Inside your html page create a "livingRoom" div holding four divs within. Change the background color to whatever color you want your carpet to be.
- Inside our CSS page, make the container a 800px square containing 100px squares within that are red, blue, green, and yellow.
- Write some content in your boxes to denote what's inside each box.

<!-- Ask devs to fight checking the solution like they may fight a tiger to protect their first-born child -->

Check below when you are finished:

<details>
<summary>Looking at the html...</summary>

```html
<link rel="stylesheet" type="text/css" href="main.css">

<div id="livingRoom">
    <div id="box1">Books</div>
    <div id="box2">Dishes</div>
    <div id="box3">Closet Junk</div>
    <div id="box4">Towels</div>
</div>
```
</details>

<details>
<summary>And the CSS...</summary>

```css
#livingRoom {
    height: 800px;
    width: 800px;
    background-color: gray;
}
#box1 {
    background-color: red;
    height: 100px;
    width: 100px;
}
#box2 {
    background-color: blue;
    height: 100px;
    width: 100px;
}
#box3 {
    background-color: green;
    height: 100px;
    width: 100px;
}
#box4 {
    background-color: yellow;
    height: 100px;
    width: 100px;
}
```
</details>

<!--WDI6 11:00 -->

### Layers of the Box Model

Let's get go into some more detail and practice with each of these elements of The Box Model.

#### Margin

The margin is the space around the element. The larger the margin, the more space between our element and the elements around it. We can adjust the margin to move our HTML elements closer to or farther from each other. Adjusting our margins not only moves our element relative to other elements on the page, but also relative to the "walls" of the HTML document.

For instance, if we take an HTML element with a specific width (such as any one of our `<div>` elements in the editor) and set its margin to `auto`, this tells the document to automatically put equal left and right margins on our element, centering it on the page.

If you want to specify the margin of a particular side, you can do it like this:

```css
div {
    margin-top: /*some value*/
    margin-right: /*some value*/
    margin-bottom: /*some value*/
    margin-left: /*some-value*/
}

```

You can also set an element's margins all at once. You just start from the top margin and go around clockwise (going 
from top to right to bottom to left). For instance:

```css
div {
    margin: 1px 2px 3px 4px;
}
```

You can even do top-bottom and side-side:

```css
div {
    margin: 0 auto;
}
```

##### Moving day Activity: 
Whatever was in your your green box has begun to smell. Adjust its margin so that it's at least 40px away from all other boxes.

<!--11:09 WDI6 -->

#### Border

We've talked briefly about borders, which refers to the edges of the element. It's what we've been making visible every time we set the border property.

The border property accepts three values: thickness, pattern, and color:

```css
div {
    border: 5px solid black;
}
```

##### Moving day Activity:
Your red box is full of heavy stuff, so make the borders extra thick to prevent our metaphorical cardboard from ripping.

<!--WDI6 11:14 -->

#### Padding and Content

The padding is our packing peanuts - the spacing between the content and the border of the box. Unlike in real life, adding more padding to your box will increase it's size to accomdate the contents of the box. If, however, the height and width are explicitly set, it will only affect the area around the content portion of the box, leaving the size of the content unaffected. If those properties aren't set, it will manipulate the content area.

Padding accepts the same value types as margin:

```css
div {
    padding: 2px;
}
```
##### Moving day Activity:
- Your blue box is full of breakable objects. Make the padding at least 30px, because we don't want anything getting broken!
- Your yellow box is WAY too full. Put at least 175 characters in it. Keep in mind, you might have to make your box bigger.

<!--WDI6 11:24  -->
<!--10:45 10 minutes -->

## Display

Our boxes are looking just about ready to move. Now, let's learn some CSS tools that can't be used on physical boxes. In the CSS box model, you can further augment how your boxes are laid out with the `display` property. It has four main properties:

<!--Whip-around while listing on white board -->

* A **block** element takes up the full width of its container by default, regardless of the content inside of it. It doesn't allow any other elements to sit next to it. It's best for large containers and other sizeable page content.

* An **inline** element takes up only as much space as the content requires, and sits in the same line as preceeding elements. Margin and padding only affect the left and right sides of the elements. This display style is great for elements that should not disrupt the surrounding content; for example, a link within the text of a paragraph.

* An **inline-block** element maintains the properties of an inline element, but allows a width and height to be applied to it (as well as side margin/padding). This display style is good for wrapping lists of elements that are still block-like, such as a grid of products on amazon.

* If you assign **none** as the value of the display, this will make the element and its content disappear from the page entirely!

Here's a visual example:
![Block vs. Inline Example](images/boxmodel-block-vs-inline.png)

To illustrate this, if we had this HTML:

```html
<div class="inline">
    <div class="inline">Content</div>
    <div class="inline">Content</div>
    <div class="inline">Content</div>
</div>

<div class="block">
    <div class="block">Content</div>
    <div class="block">Content</div>
    <div class="block">Content</div>
</div>

<div class="inline-block">
    <div class="inline-block">Content</div>
    <div class="inline-block">Content</div>
    <div class="inline-block">Content</div>
</div>

```

With this CSS:

```css
.inline {
    display: inline;
}

.block {
    display: block;
}

.inline-block {
    display: inline-block;
}
```

We would end up with something like this:

![display](https://i.imgur.com/zeD1f2m.png)

<!--CFU: Catch-phrase with block, inline, inline-block -->

<!--10:55 10 minutes -->
<!--WDI6 11:30 -->

## Position

Another CSS property, `position`, affects how our elements interact with other elements on the page. It can take a `relative`, `absolute`, `fixed`, or `static` value.

#### Static Positioning

`position:static` is the default value for position. You won't need to declare this value unless you're overriding a previous declaration.

#### Relative Positioning

Declaring `position:relative` allows you to position the element top, bottom, left, or right, **relative to where it would normally occur**.  Let's add some CSS and see what happens:

```css
#box1 {
    background-color: red;
    height: 100px;
    width: 100px;
    position:relative;
    top: 0;
    left: 40px;
}
```
In our moving boxes metaphor, this is akin to saying "move the red box 40px to the right of where it currently is."

#### Absolute Positioning

Specifying `position:absolute` _removes the element from the document flow_ and places it exactly where you tell it to be, relative to its parent container.

```css
#box2 {
    background-color: red;
    height: 100px;
    width: 100px;
    position:absolute;
    top: 0;
    right: 0;
}
```

There's no physical metaphor for this rule, because it allow your elements to overlap and intersect eachother. Sadly, real boxes do not work this way!

![](https://media.giphy.com/media/NOsfNQGivMFry/giphy.gif)


#### Fixed Positioning

An element with fixed position is positioned relative to the browser window. It will not move even if the window is scrolled - it's good for headers and footer that you want to remain stationary even as the user scrolls. 

```css
#box3 {
    position: fixed;
    width: 100px;
    height: 100px;
    background-color: blue;
    top: 0;
    left: 0;
}
```

<!--11:05 5 minutes -->
<!--WDI6 11:35 -->

## Floats and Clears

The float property specifies whether or not a box (or an element) should float; essentially, it left and right aligns block-level elements. Non-floated elements, like text, will be wrapped around the floated elements.

<!--This also works with inline elements why do we say block? -->

![](https://cloud.githubusercontent.com/assets/40461/8234489/3b61ef02-15d4-11e5-8864-435fb6e0c3cc.png)

> Note that "absolutely positioned" elements ignore the float property as they are removed from the normal document flow. Floated elements remain a part of the flow of the web page. This is distinctly different than page elements that use absolute positioning.

There are four valid values for the float property: 
- **`left`** and **`right`** float elements in those directions, respectively. 
- **`none`** (the default) ensures the element will not float.
- **`inherit`** will assume the float value of the parent element.

#### Clear

Elements will wrap up next to floated items until they are specifically cleared. When you put a `clear` on an element, you are essentially telling it perform a line break, and create a new row.

![](https://cloud.githubusercontent.com/assets/40461/8234478/287c1156-15d4-11e5-9901-ba9090a5bf70.png)

<!-- 11:10 15 minutes -->

## Using position, floats, and clears to create columns

Now that we have the basics of relative and absolute positioning, let's turn our living room full of moving boxes into a two-column layout. Start by changing the heights; then we'll investigate how to use floats and clears for a more effective approach.

Change the heights of "box1" and "box2" to 200px and absolutely position the two squares like so:


```css
#livingRoom {
    background-color: gray;
    position: relative;
    height: 800px;
    width: 800px;
}
#box1 {
    background-color: red;
    height: 200px;
    width: 100px;
    position:absolute;
    top: 0;
    right: 0;
}
#box2 {
    background-color: blue;
    height: 200px;
    width: 100px;
    position: absolute;
    top: 0;
    left: 0;
}
```

Note how our "box2" div is positioned to the top left of the container and "box1" to the top right. This was done to illustrate that absolute positioning doesn't care what order the elements appear in your html.

Also, notice how we can't see "box3" or "box4"? They are being covered up by our absolute-positioned "box2" div (remember, absolute positioning removes the element from the document flow).

We can move those divs back into our field of view by declaring that they originate at `0px` off of the `bottom`, `left`, and `right` of our container:

<!--WDI6 11:47 -->

```css
#box3 {
    background-color: green;
    height: 100px;
    width: 100px;
    position: absolute;
    bottom: 0;
    left: 0;
}
#box4 {
    background-color: yellow;
    height: 100px;
    width: 100px;
    position: absolute;
    bottom: 0;
    right: 0;
}
```

This works fine when we know the exact sizes of our elements - but what if we were building something like a blog and we had text in those columns or surrounding them? We won't always know the exact amount of text or their font sizes. This is where floats can help us.

#### Floats to create multicolumn layouts

If our element sizes are variable or dynamic we can use floats to allow text/other elements to wrap around the floated element.  To illustrate this, lets first go to a favorite ipsum generator and grab four paragraphs of text.

Now, let's venture back to our html page and add this text after the closing tag of our `box2` div and before the 
opening tag of our `box3` div.

Your html should like this:

```html

    <div id="livingRoom">
        <div id="box1"></div>
        <div id="box2"></div>
        <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Praesent rutrum lectus eget nunc auctor, non convallis ligula pretium. Sed eget orci ipsum. Fusce felis erat, semper sit amet erat in, dictum sagittis leo. Nullam eget lobortis dolor, ut sagittis eros. Aenean varius augue ac diam sollicitudin faucibus. Aenean posuere ante leo, in vehicula est dictum in. Donec mattis diam mauris, a pretium turpis gravida vitae. Nullam et ultricies magna.
        </p>
        <p>
            Proin turpis nisl, faucibus eget varius vel, ultrices sit amet lorem. Donec quis nunc sed libero varius tempor sit amet eu mi. Morbi maximus tincidunt eros eu mattis. Phasellus dapibus sollicitudin diam, ut dapibus neque facilisis a. Curabitur mi justo, ornare sed risus vel, ullamcorper hendrerit dolor. Etiam id tincidunt quam, vel imperdiet leo. Aenean sed turpis aliquet, tristique est non, placerat eros.
        </p>
        <p>
            Donec vitae tincidunt elit. Praesent faucibus nisi ex, sed varius metus fringilla sed. Duis tempus est id fermentum dignissim. Praesent vel felis in diam aliquet dictum eget sed eros. Proin tempus tellus sem. Maecenas eget lectus justo. Aliquam a eros iaculis, condimentum velit a, porttitor odio. Vestibulum pharetra enim nunc, pretium fermentum tellus venenatis sed. Sed feugiat rutrum accumsan. Suspendisse quis ipsum vel lorem vestibulum eleifend. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas mollis, nulla non interdum cursus, libero ex vehicula enim, a hendrerit lacus odio nec est. In in lobortis neque, ac aliquet risus. Vivamus tempus placerat enim, nec laoreet nulla suscipit eget. Morbi quis euismod tellus, in sollicitudin lorem. Sed ut orci vitae massa elementum tristique in nec massa.
        </p>
        <p>
            Fusce et nibh et odio malesuada dignissim vel at eros. Donec nec nunc fermentum, volutpat lacus in, ultrices ex. Nam non cursus arcu. Praesent nisl sem, fermentum eu pharetra quis, cursus eget magna. Donec ultrices lorem et quam pretium, vitae luctus ante commodo. Pellentesque tincidunt aliquet justo, in ultricies nisi pellentesque ac. Aenean porta ligula nec lacus viverra efficitur. Sed bibendum ornare urna eget scelerisque. Vestibulum bibendum turpis et nibh dapibus, in accumsan lacus dapibus. Maecenas vitae tortor eleifend, aliquam elit id, hendrerit magna. Donec placerat hendrerit dolor, ut dapibus purus mollis in. Aliquam erat volutpat. Fusce ultricies libero et scelerisque condimentum. Nunc sem ex, pretium id enim nec, facilisis luctus ligula. Morbi hendrerit ipsum in dolor tincidunt convallis ut a neque.
        </p>
        <div id="box3"></div>
        <div id="box4"></div>
    </div>

```

As expected, our text falls behind our absolute positioned columns. Now let's make our elements aware of each other with floats.

Back in our CSS, remove the absolute positioning from our `box2` div and replace it with `float:left`:

```css
#box2 {
    background-color: blue;
    height: 200px;
    width: 100px;
    float: left;
}
```

Note that our text is aware that our "box2" div wants to be as far left as possible, and kindly wraps it in a nice text hug!

#### Floats with clears

While floats make other elements aware of their location and give them text hugs, clears tell other elements to leave them some space (i.e. no hugs).

![](http://s2.quickmeme.com/img/73/73da31728b13520117e2dab7447b8f37c29071dbd452f21f7377969d08949463.jpg)


Lets go back to our CSS and change our "box2" div's positioning from `float:left;` to `clear:right;`.

`Clear` is saying "I'm not sure how much space I'm going to take, but whatever it is, clear off my right side". Our text respects its wishes and drops to the line below.

<!--11:25 5 minutes -->

## Conclusion
<!--Think-pair-share -->
- Compare the elements of The Box Model - margin, border, padding, content.
- Compare inline-block, block, and inline.
- How do floats work with clears to create a multicolumn layout?

## Positioning Excercise - Living Box Model

Let's recap the CSS box model. It's main properties are:

- Display
- Float
- Clear
- Position
- Margin
- Padding*
- Border*

To make sure we still remember these, we're going to act them out. Half of the class will get a pad of post-its to write CSS properties on, and the other half has to act them out.
> Note - Padding and Border might be hard to act out. Let's stick with the first 5 properties.

If you have post-its, take two of them and write one CSS property/value on each. Hand each of your two post-its to a different person.

<!--12:15 WDI6 -->

## Licensing
All content is licensed under a CC­BY­NC­SA 4.0 license.
All software code is licensed under GNU GPLv3. For commercial use or alternative licensing, please contact legal@ga.co.
