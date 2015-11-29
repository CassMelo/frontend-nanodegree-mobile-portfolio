#Udacity FrondEnd Developer Class 
Version 1.0 11/28/2015


##General Usage Notes
This project is part of the Udacity FrontEnd Developer Course. In this project we had to work on on some optimization to make the app load faster and pizza.html run at 60FPS when scrolling.

## Installing
To install just copy all files under the directory dist and run the file index.html

##How to run the application


This is Cameron Pittman's portfolio used for the Udacity Optimization Class.
There are 4 projects on this portfolio.

* **Build Your Own 2048**

    In this page Cameron created the Udacity website's version in 2048. 

* **Website Performance Optimization**

    This class is really important and everyone should invest time and effort. 

* **Mobile Web Development**

    Here is a recommendation to take the Mobile Web Development.
 
* **Cam's Pizzeria**

    This is a fake pizzeria where the pizzas are created randomically. You can change the pizza's sizes and everytime you do so, the layout will change. It has 3 pizza's sizes: small, meduim and large.

## Optimizations to run index.html

###  index.html

1 - Downloaded the image files (BuildYourOwn2048.jpg, WebsitePerformanceOptimization.jpg, MobileWebDevelopment.jpg)

2 - Resized the file (pizzeria.jpg) using Shrink-o-matic

3 - Added media on `<link href="css/print.css" rel="stylesheet" media="print">`

4 - Added async `<script async src="http://www.google-analytics.com/analytics.js"></script>`

5 - Updated my  Google Analytics profile ID. `ga('create', 'UA-70397381-1');`

6 - Commented the line below

`<!--<link href="//fonts.googleapis.com/css?family=Open+Sans:400,700" rel="stylesheet"> -->`


###  style.html

1 - Minified style.css 


## Optimizations to run pizza.html
###  pizza.html

1 - Divided the .css file considering the media queries


```
  <link rel="stylesheet" href="css/bootstrap-grid.css">
  <link rel="stylesheet" href="css/bootstrap-grid-768px.css" media="(min-width:786px)">
  <link rel="stylesheet" href="css/bootstrap-grid-992px.css" media="(min-width:992px)">
  <link rel="stylesheet" href="css/bootstrap-grid-1200px.css" media="(min-width:1200px)">

```
2 - Compacted and resized the file pizzeria.jpg

### style-pizza.css
1 - Added code on **_mover_** class

```
.mover {
  ....

  /** added transform function so GPU can be triggered and performance enhanced*/

  transform: translateZ(0);
  -webkit-transform: translateZ(0);
  -moz-transform: translateZ(0);
}
```

2 - Added backface visibility 

```
  /**
   * Backface-visibility property = hidden :  that the back face is not visible, hiding the front face.
   * It improves performance.
  */

  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
```

###main.js

The page pizza.html should run at 60FPS when scrolling and resize the pizzas in less than 5ms.


1 - Changed **_document.addEventListener('DOMContentLoaded')_**

* Reduced the amount of sliding pizzas from 200 to 30 
* Declared elem and movingPizzas outside the loop


```
  var elem; // declared outside the loop
  // declared outside the loop and replaced querySelector by getElementById
  var movingPizzas = document.getElementById('movingPizzas1');
  
  // Generates 30 slilding pizzas to put in the background. There is no need to put 200 as it was.
  for (var i = 0; i < 30; i++) {
    elem = document.createElement('img');
    elem.className = 'mover';
    elem.src = "images/pizza.png";
    elem.style.height = "100px";
    elem.style.width = "73.333px";
    elem.basicLeft = (i % cols) * s;
    elem.style.top = (Math.floor(i / cols) * s) + 'px';
    movingPizzas.appendChild(elem);
  }
...
``` 

2 - Changed the function **_changePizzaSizes_**

```
/** The dx and newwith calculation doesn't need to be inside the for loop.
 *   The loop is only necessary to set the new width for each item
 *   Replaced querySelectorAll for getElementsByClassName
 */
var x = document.getElementsByClassName("randomPizzaContainer");
var dx = determineDx(x[0], size);
var newWidth = (x[0].offsetWidth + dx) + 'px';

// Added the len var
for (var i = 0, len = x.length; i < len; i++) {
  x[i].style.width = newWidth;
}

```

3 - Changed the for-loop that actually creates and appends all of the pizzas when the page loads

```
// This for-loop actually creates and appends all of the pizzas when the page loads

/** The function getElementBYId is now out of the for loop.
*   The for loop now just append the pizzas that were generated.
*/
var pizzasDiv = document.getElementById("randomPizzas");
for (var i = 2; i < 100; i++) {
  pizzasDiv.appendChild(pizzaElementGenerator(i));
}

```

4 - Changed function **_UpdatePositions_**
```
/** The phase calculation was modified and the querySelectorAll was
 *   replaced by getElementByClassName.
 *   phase var was declared outside the loop
 */

var items = document.getElementsByClassName("mover");
var factor = document.body.scrollTop / 1250;
var phase = 0;

// Added var len
for (var i = 0, len = items.length; i < len; i++) {
  phase = Math.sin(factor+(i % 5));
  items[i].style.left = items[i].basicLeft + 100 * phase + 'px';
}

```

5 - Changed function **_determineDx_**


```
    // Replaced querySelector for getElementById
    var windowWidth = document.getElementById("randomPizzas").offsetWidth;
```

6 - Defined all functions with `'use strict';`

## Project Deployment
GULP was used to deploy the project. I used the info from [Getting Started with gulp](https://markgoodyear.com/2014/01/getting-started-with-gulp/)
All files .js, .html and .css were minified during this process.


##Author
Cassia De Melo

email: cassiac@yahoo.com

##Copyright (C) 2015 Cassia

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see [License](http://www.gnu.org/licenses/).

