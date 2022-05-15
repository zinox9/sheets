![Cover Image](./images/htmlcss.png)

#### Table Of Contents

**[HTML , CSS & Responsiveness Reference Sheet](#html--css--responsiveness-reference-sheet)**

- **[HTML](#HTML)**
  - [Basic HTML](#basic-html)
  - [Useful Elements](#useful-elements)
- **[CSS](#CSS)**
  - [Basic CSS](#basic-css)
  - [Positioning](#Positioning)
  - [Animations](#Animations)
  - [Images & Transformation](#images--transformation)
  - [Styling Forms](#styling-forms)
  - [Useful Properties](#useful-properties)
- **[Responsiveness](#Responsiveness)**
  - [Screen Width Usage](#screen-width-usage)
  - [Order to apply Media queries](#order-to-apply-media-queries)
  - [Handling Images](#handling-images)
  - [Feature Queries](#feature-queries)
- **[Other Useful Concepts](#other-useful-concepts)**

# HTML , CSS & Responsiveness Reference Sheet

> **This sheet contains all the HTML & CSS references that can be used to keep track of everything on their path. This sheet also has explanation & usage of Responsiveness in a website.**

## HTML

- **[CHEATSHEET](https://websitesetup.org/html5-cheat-sheet/)** 

### Basic HTML

- **All Tags -** [**Reference**](https://htmlreference.io/)
- **Class & ID -** [Usage](https://css-tricks.com/the-difference-between-id-and-class/)
- **Adding CSS & other files -** [Link Tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link) 
- **Adding JS -** [Script](https://www.tutorialsteacher.com/javascript/script-tag)

### Useful Elements

- [Forms](https://htmlreference.io/element/form/) & [Form Elements](https://htmlreference.io/forms/)
- [Tables](https://css-tricks.com/complete-guide-table-element/)
- [Figure](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figure), [iFrames](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Other_embedding_technologies)

---

## CSS

- **[CHEATSHEET](https://websitesetup.org/css3-cheat-sheet/)**
- All Properties [**Reference**](https://tympanus.net/codrops/css_reference/)

### Basic CSS

- **Box Model -** [Explained](https://css-tricks.com/box-sizing/)
- **Selectors -** [All Pseudo Selectors](https://css-tricks.com/pseudo-class-selectors/) & [Common 30 Cheatsheet](https://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048)
- **Positioning -** [Relative, Absolute & Other](https://css-tricks.com/almanac/properties/p/position/)
- **States -**  [Link](https://css-tricks.com/almanac/selectors/l/link/) | [Visited](https://css-tricks.com/almanac/selectors/v/visited/) | [Hover](https://css-tricks.com/almanac/selectors/h/hover/) | [Active](https://css-tricks.com/almanac/selectors/a/active/) | [Focus](https://css-tricks.com/almanac/selectors/f/focus/)
- **After & Before Elements -**   [Reference](https://css-tricks.com/almanac/selectors/a/after-and-before/) | [Applications](https://bryanlrobinson.com/blog/2018/08/07/top-3-uses-of-after-and-before-css-pseudo-elements/)
- **Pseudo Class Selectors -** [:not](https://css-tricks.com/almanac/selectors/n/not/) | [:nth-child](https://css-tricks.com/almanac/selectors/n/nth-child/) | [others](https://css-tricks.com/pseudo-class-selectors/)
- **Special Functions -** [calc()](https://css-tricks.com/a-complete-guide-to-calc-in-css/) | [others](https://www.sitepoint.com/8-clever-tricks-with-css-functions/)
- **Variables -**  [Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)

### Positioning

- **Floats -** [All About Floats](https://css-tricks.com/all-about-floats/)
- **Display -** [block, inline, inline-block, tables](https://css-tricks.com/almanac/properties/d/display/)
- **Flexbox -** [Explanation](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) , [Cheatsheet](http://flexbox.malven.co/)
- **Grids -** [Explanation](https://css-tricks.com/snippets/css/complete-guide-grid/) , [Cheatsheet](http://grid.malven.co/)

### Animations

- **Creating Animations -** [Reference](https://css-tricks.com/almanac/properties/a/animation/)
- **Using Animations -**[Transition](https://css-tricks.com/almanac/properties/t/transition/)
- **Cubic Bezier**: [Create Your Own](http://cubic-bezier.com/#.63,-0.94,.55,1.87) or [Premade](https://easings.net/#)

### Images & Transformation

- **Background Images & Gradients -** [Reference](https://css-tricks.com/almanac/properties/b/background-image/)
- **Transformation -** [Transform](https://css-tricks.com/almanac/properties/t/transform/)
- **Clipping & Masking -**   [Reference](https://css-tricks.com/clipping-masking-css/), [Clipping Tool](http://bennettfeely.com/clippy/)

### Styling Forms

- **Styling Inputs -** [Reference](https://css-tricks.com/styling-texty-inputs-only/)  
- **Selectors -** [:input-placholder](https://css-tricks.com/almanac/selectors/p/placeholder/) | [:input-placeholder-shown](https://css-tricks.com/almanac/selectors/p/placeholder-shown/) | [:valid](https://css-tricks.com/almanac/selectors/v/valid/)  | [:invalid](https://css-tricks.com/almanac/selectors/i/invalid/) | [:focus](https://css-tricks.com/almanac/selectors/f/focus/) 
- **Other Inputs -** [Radio Button, Checkbox, Toggle Styling](https://css-tricks.com/custom-styling-form-inputs-with-modern-css-features/)
- **Dropdown -** [Reference](https://tympanus.net/codrops/2012/10/04/custom-drop-down-list-styling/)

### Useful Properties

- [Target](https://developer.mozilla.org/en-US/docs/Web/CSS/:target) - to target an element having ID 
- [Background-clip](https://developer.mozilla.org/en-US/docs/Web/CSS/background-clip) - to clip background with text or content
- [Perspective](https://3dtransforms.desandro.com/perspective) - change the perspective of 3d animations
- [Backface visibility](https://developer.mozilla.org/en-US/docs/Web/CSS/backface-visibility) - for the elements behind
- [Overflow](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow) - for overflowing content
- [Background-blend-mode](https://css-tricks.com/almanac/properties/b/background-blend-mode/), [Mix-blend-mode](https://css-tricks.com/almanac/properties/m/mix-blend-mode/) - blend background with some color , or blend text with background
- [Box Decoration Break](https://developer.mozilla.org/en-US/docs/Web/CSS/box-decoration-break) - to fix the decoration for multiline text
- [Shape Outside](https://css-tricks.com/almanac/properties/s/shape-outside/) - to align paragraph according to the shape of  image with it
- [Image Filter](https://css-tricks.com/almanac/properties/f/filter/) - to add filters to images
- [Object fit](https://css-tricks.com/almanac/properties/o/object-fit/) - to fit images and videos  in containers
- [Hyphens](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens) - for multiline content
- [backdrop-filter](https://css-tricks.com/almanac/properties/b/backdrop-filter/) - gives filter to the background 

---

## Responsiveness

- **[Media Queries](https://css-tricks.com/css-media-queries/)**

- **Meta Tag -** `<meta name='viewport' content="width=device-width, initial-scale=1.0">`

### Screen Width Usage

- **Desktop First :** use max-width; (higher to lower)
- **Mobile First :** use min-width (lower to higher)

### Order to apply Media queries

1. base + typography
2. general layout
3. grid
4. page  layout
5. components 

### Handling Images

- **Density Switching -**  high-res (2px for 1px) & low-res(1px for 1px)
  
  - `<img srcset="img1x.png 1x, img2x.png 2x" alt="Image">`

- **Art directions -** different images for different screen
  
  ```html
  <picture>
      <!-- when lower than 600px -->
      <source srcset="imgsmall1x.png 1x, imgsmall2x.png 2x" media="(max-width: 37.5em)"> 
      <!-- using density switching with art directions -->
      <img srcset="img1x.png 1x, img2x.png 2x" alt="img">
  </picture>
  ```

- **Resolution Switching -** large & small screen
  
  ```html
  <!-- in srcset , the images are specified with their original width-->
  <img srcset="img1.png 300w, img1-large.png 1000w" 
       sizes="(max-width: 900px) 20vw, (max-width: 600px) 30vw, 300px">
  <!-- in sizes , the screen size is speicified with the image width to be used, last one being the default size -->
  ```

- **Handling Images in CSS -** media queries combined with screen res & width
  
  ```css
  // for resolution greater than 1px and 600px width or webkit is for safari browser
  @media (min-resolution: 192pi) and (min-width:600px) ,
      (-webkit-min-device-pixel-ratio: 2) and (min-width:600px){
      // image you want to set
      }
  ```

### Feature Queries

- **Browser**
  
  ```css
  @supports (-webkit-backdrop-filter: blur(10px)) or (backdrop-filter: blur(10px)){
      -webkit-backdrop-filter: blur(10px);
      backdrop-filter: blur(10px);
      //use only if the browser supports these properties
  }
  ```

- **Touch Capability -** This will apply for small screen OR non hover screen.
  `@media only screen and (max-width: 56.25em),  only screen and (hover:none){}`

---

## Other Useful Concepts

- **Optimizing Images -** By **cropping** or using [Optimizilla](https://imagecompressor.com/)

- **Search Engine Optimization -** By using [Meta tags](https://searchenginewatch.com/sew/how-to/2067564/how-to-use-html-meta-tags)

- **Class Naming Convention -** [BEM](https://css-tricks.com/bem-101/)

- **Global Reset**
  
  ```css
  * {
      margin: 0;
      padding: 0;
      box-sizing: inherit; //from body element
  } 
  html{
      font-size: 62.5%; //defines 1rem everywhere as 10px
  }
  body{
      box-sizing: border-box;
      /*
      Define project wide font family and size in body selector
      */
  }
  ```

---