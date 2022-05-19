   #                                          Browser Rendering
Have you ever thought how browsers display content to us ? We all know that every web page contains a HTML , CSS and most of the times there is a JavaScript file as well. How  does a Browser renders HTML, CSS and JavaScript files ? What is the mechanism behind it ? Through the following article I will take you through the Browser Rendering Process.

## Introduction
 **Browser**  is a rendering engine whose main task is to provide users with the requested content in a human readable way. As discussed earlier if the browser simply displays the content present in HTML file (Considered as Skeleton for a web page) , a layman may not understand what's displayed on screen.
 Now Lets look into how a browser works with these files.The browser reads the data present in HTML,CSS and JavaScript files in the form of raw bytes not the actual text. And these raw bytes undergo several transformations and at last a DOM tree creation starts after parsing HTML file. Then where is our CSS file ? During the parsing of HTML file whenever the browser comes across `<link>`tag it  fetches the CSS file and  starts creating a CSSOM ( CSS Object Model).  And here comes the game changer JavaScript file. We all know that it is possible to alter the HTML and CSS files through JavaScript. So what browser does is it stops the creation of DOM and CSSOM tree until the JavaScript file is completely parsed.Here I have given a gist of rendering mechanism and now I shall take through Critical Rendering Path (CRP).

## Critical Rendering Path
Critical rendering path is a sequence steps the browser take to display the content from HTML,CSS and JavaScript file to the screen in a meaningful way. CRP includes creation of Document Object Model (DOM) , CSS Object Model, Rendering Tree and Layout.

### Creation of Document Object Model (DOM)
As discussed earlier the browser cannot read (understand) the text present in the `.html` file. The text has to undergo certain transformations to be understood by the rendering engine. 
Different steps taken to create a DOM Tree :

 - First the engines reads the data present in the HTML file as raw bytes and these raw bytes are converted into characters.

- These characters are converted into tokens. Still they are not readable by the browser for creation of DOM.
- During tokenization (process of creating tokens) every start tag and end tag is considered. After tokens are created , these tokens are converted into Nodes which are considered as building blocks of DOM tree. 
- After nodes are created they are linked in a tree establishing relations between nodes like Parent-child relation(Main container - Sub container) and Adjacent Sibling relation( HTML elements with a common container. For Example two paragraph elements in a `<>div>` container ).

![tion here](https://www.tutorialstonight.com/assets/js/dom-tutorial.webp) *An image depicting a skeleton of DOM Tree*

### Creation of CSS Object Model
During the creation of DOM tree whenever the browser comes across the `<link>` it requests for the `main.css` file. CSS files change the way we look at a website. All the styling and colors are due to the presence of CSS.  The raw bytes of data in CSS files undergo similar transformation like that  of DOM. After this some new tree structure called CSS Object Model construction begins.

### Executing a JavaScript file
As we know most of the web applications use JavaScript and that we can change or access the HTML and CSS through JavaScript. DOM provides different methods through which we can change or remove HTML Elements. Same goes with CSS as well. So our browser pauses the DOM and CSSOM building processes until the JavaScript file is completely executed because which can alter the Position or Style of trees structures.

JavaScript file is placed at bottom lines of HTML file because to alter the changes there should be DOM and CSSOM already under process. If we place in the beginning i.e between`<head>` it will not make any changes because the HTML and CSS files are not parsed yet and there is no DOM and CSSOM.

### Render Tree
At this step we have a DOM and CSSOM tree structures which are independent. The DOM contains content of HTML file whereas the CSSOM has styles related to the HTML content. Now the browser joins both these independent tree structures to form something called **Render Tree**. 
While creating render tree the browser finds each node in DOM tree from starting and matches them styles to be added to them. 
After this Render Tree the browser moves on next step i.e Layout.

### Layout
Now we have all the content and their respective styles. In layout the size and position of elements are determined as per screen size. We have different types of screen sizes and as per Responsive design the screen sizes are divided into -   
-   Small (smaller than 640px)
-   Medium (641px to 1007px)
-   Large (1008px and larger)

After computing the width and positions of elements  as per screen size the browser now paint the pixels on the screen and now the elements are rendered on the screen. Optimizing a website means Optimizing this CRP so that resources are rendered fast on screen without blocking any resources.

I have tried to present the Browser Rendering Process here and you are free to add any changes or corrections to this page.
 
 ### Ref :
 - [Tutorials Tonight](https://www.tutorialstonight.com/js/js-dom-introduction.php)
 - [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/Performance/Critical_rendering_path#optimizing_for_crp)
 - [FreeCodeCamp](https://www.freecodecamp.org/news/web-application-security-understanding-the-browser-5305ed2f1dac/)
 - [Log Rocket](https://blog.logrocket.com/how-browser-rendering-works-behind-scenes/)
 - [Windows App Development](https://docs.microsoft.com/en-us/windows/apps/design/layout/screen-sizes-and-breakpoints-for-responsive-design)



 

