# Building a CSS Stylesheet (Simplified Version)


## Part 1: Color Palette

### Color Palette

Please go to [color.adobe.com](https://color.adobe.com) and upload an image with a color palette that you like. 

Open your CSS stylesheet from your theme, copy the color codes from the Adobe site and paste them into the stylesheet. Assign each color a CSS variable name.

From now on, only refer to colors in your CSS by their name. Over time, this will let you refine and perfect your palette.

You can use names that explain the color, or you can use names that explain the use of the color in the interface. Your choice.

#### Example 1

    :root {
      --palest-blue: #D0E5F2;
      --pale-orange: #F2A679;
      --dark-orange:  #D95A2B;
      --dark-gray: #474441;
      --deep-red: #8C2D18;
    }

Or:

#### Example 2

    :root {
      --main-bg-color: #D0E5F2;
      --main-fg-color: #F2A679;
      --titles-color:  #D95A2B;
      --bodytext-color: #474441;
      --accent-color: #8C2D18;
    }

## Part 2: Choosing & Importing Fonts

### Find a good font pair

Seek inspiration here: [Ultimate Guide to Font Pairing](https://www.canva.com/learn/the-ultimate-guide-to-font-pairing/)

### Find a good set of Google Fonts

Look on [fonts.google.com](https://fonts.google.com) (or on other sites where you can legally download fonts for web use) for a good font combination. Find at least two fonts:

- One font face for titles and subtitles
- One font face for body text

Download the fonts to your computer.


### Or use a good font pair from Adobe 

See this [Adobe Help Page](https://helpx.adobe.com/ca/fonts/using/add-fonts-website.html) for instructions on how to use Adobe fonts in your web projects.




    Is self-hosting your fonts better than linking to them?

    It used to be best practice to link to fonts hosted by big companies like Google and Adobe. Their servers were always much faster. However nowadays almost all web servers (except free or really inexpensive ones) are more than fast enough to host your own fonts. 



### Follow these steps if not using Adobe fonts

#### Convert the fonts for web use

Go to [https://transfonter.org/](https://transfonter.org/)

Use these settings to convert your fonts to WOFF and WOFF2 formats:

![Transfonter.org settings screenshot](./img/transfonter.png)




#### Move the font files

1. Create a "fonts" folder inside your theme/default/ theme folder.
2. Move the font files into the fonts folder. (There is no need to add them into subfolders.)

#### Copy the CSS @font-face rules

Copy the font face rules from the Transfonter stylesheet.css to your theme's stylesheet. (Note that the path to the fonts is relative to the CSS file.)

     @font-face {
    font-family: 'Anton';
    src: local('Anton Regular'), local('Anton-Regular'),
        url('fonts/Anton-Regular.woff2') format('woff2'),
        url('fonts/Anton-Regular.woff') format('woff');
    font-weight: normal;
    font-style: normal;
    font-display: swap;
    }
    
    
    
    @font-face {
      font-family: 'Raleway';
      src: local('Raleway Regular'), local('Raleway-Regular'),
          url('fonts/Raleway-Regular.woff2') format('woff2'),
          url('fonts/Raleway-Regular.woff') format('woff');
      font-weight: normal;
      font-style: normal;
      font-display: swap;
    }
    
    
    @font-face {
      font-family: 'Raleway';
      src: local('Raleway Bold'), local('Raleway-Bold'),
          url('fonts/Raleway-Bold.woff2') format('woff2'),
          url('fonts/Raleway-Bold.woff') format('woff');
      font-weight: bold;
      font-style: normal;
      font-display: swap;
    }






## Part 3: Font Basics

### EM vs REM

An EM is a value equal to the height of a lowercase letter m in the chosen font.

An em can have different values if you are looking at the letter m in a paragraph, an H1 tag or an h4 tag. An em is ***context-sensitive***.

A REM is a "Root EM". It is a value equal to the height of a lowercase letter m in the chosen font ***of the root element***. **The value of a REM never changes.**

### Use a Typographic Scale

There is a science behind choosing fonts sizes that work well together. Very much like music, it all depends on which notes you choose to place into a chord. In the case of type, the size of glyphs is equivalent to the note in the chord.

See: [https://spencermortensen.com/articles/typographic-scale/](https://spencermortensen.com/articles/typographic-scale/)  Scroll down to the bottom and experiment with the scale selector. Notice sometimes it gives the name of a musical chord structure.

Experiment with the R value (size contrast ratio) to different ratios (ex: 1.6 or 1.2 or 1.618 - whatever), and the height of the base font F0 (body font size). Note **1.618** is the [golden ratio used in classic art](https://www.adobe.com/creativecloud/design/discover/golden-ratio.html). 

Your only concern is not having type so big that many words will need to be hyphenated on mobile sized screens.


    /* ==================  EXAMPLE TYPOGRAPHIC SCALE ============================= */
    
     h1 { font-size: 3.6rem; }
     h2 { font-size: 2.9977rem; }
     h3 { font-size: 2.4961rem; }
     h4 { font-size: 2.0785rem; }
     h5 { font-size: 1.7307rem; }
     h6 { font-size: 1.4411rem; }
     p, li { font-size: 1.2rem; }
     footer { font-size: .9992rem; }
    
     /* ==================  END EXAMPLE TYPOGRAPHIC SCALE ============================= */



Copy the result into your stylesheet.



## Part 4: Web Typography

### Remember Mobile First

The main technique for creative responsive web designs is to start with the mobile scale design first. It is the easiest because it is (mostly) a single column design.

Mobile first defines the following list of design decisions:

- Color palette
- Font choices
- Typographic scale
- Typographic white space
- Margins
- Padding
- List decoration (bullets)
- Link states (LoVeHA Rule)
- Order of content priority (most important content is shown at the top of the page, less important content is towards the bottom)


### Add some basic text font rules

In web typography, always have **multiple fallbacks** in case your preferred fonts do not load as expected. This means you must write "preferred font, preferred alternate font, generic alternate font".

    h1, h2, h3, h4, h5, h6, label {
      font-family: Anton, 'Helevetica Neue', Arial, sans-serif;
    }
    
    p, li, figcaption, a {
      font-family: 'Raleway Regular', 'Helevetica Neue', Arial, sans-serif;
    }

Always **limit the width of your text content** so that on very large screens your text looks like a column not one extremely wide sentence.

    p, li {
        max-width: 65ch;
    }



### LoVeHA! Rule

The "Link Visited Hover Active"  CSS rules for links and their different states must be written in this order:

    a:link {}
    a:visited {}
    a:hover {}
    a:active {}

If not written in the order above, the effects on one or several states may not be visible.
    


### Body Padding vs Child Margins

One of the first decisions that must be taken is <u>whether or not you want the background colors of the content to reach the edge of the browser window</u>. In that case, do not give the body any padding.

![Body Tag Has Padding](./img/body-padding.png)

If the body tag has padding, the contents of the page will be surrounded by white space.

![Body Tag Has No Padding](./img/body-no-padding.png)

If the body tag has no padding, the contents of the page will touch the edge of the browser window.




### Typographic Margins

#### Vertical rhythm (margins)

Define the amount of vertical margin for each type of text content. There should always be more space above than below an item.

Example:

    h2 {
      margin-top: 3rem;
      margin-bottom: 1.5rem;
    }



### Sectional Margins

Separate the different sections of the page with generous amounts of white space. 

Negative space will help the reader understand that a certain section of the page is different from others because it appears "alone" in its area. This will let you avoid having to place boxes, borders and backgrounds just to make the area (for example: header) stand out.

      header {
        margin-bottom: 5em;
      }
    
      main {margin: 3em 0 4em 0;}  
      /* CSS shorthand: clockwise starting at noon */
    
      footer {
        margin-top: 5em;
      }



### Prepare for larger viewport designs

#### Wrapper DIV

One of the most useful **non-semantic elements** (an element not used to define the structure of the text content) is a box that wraps all the page content. Hence, we call it a "wrapper".


Set the wrapper div to be centered and with a fixed width on larger viewports.

    @media screen and (min-width: 1025px) {
        
     .wrapper {
        margin: 3em auto;  
       /* 3em can be any value; auto L/R margins do the actual centering */
        width: 960px;
     }  
    }
