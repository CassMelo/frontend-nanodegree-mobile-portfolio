#Website Performance Optimization portfolio project

With this challenge, I was supposed to :
- Identify and perform optimizations on index.html to achieve a PageSpeed score of 90 for Mobile and Desktop
- Make pizza.html run at 60FPS when scrolling and resize the pizzas in less than 5ms.


##Pizza page

###Updates on pizza.html

1- Resized pizzeria.jpg: the file went from 2,26 Mb to 131k.


2- Separated  bootstrap-grid.css acording with the media query used.

   ```
  <link rel="stylesheet" href="css/bootstrap-grid.css">
  <link rel="stylesheet" href="css/bootstrap-grid-768px.css" media="(min-width:786px)">
  <link rel="stylesheet" href="css/bootstrap-grid-992px.css" media="(min-width:992px)">
  <link rel="stylesheet" href="css/bootstrap-grid-1200px.css" media="(min-width:1200px)">
   ```

###Updates on main.js



1-Reduced the amount of sliding pizzas from 200 to 30 

```
document.addEventListener('DOMContentLoaded', function() {
  // Generates 30 slilding pizzas to put in the background. There is no need to put 200 as it was.
  for (var i = 0; i < 30; i++) {
```

2-Changed the function changePizzaSizes

```
  /** The dx and newwith calculation doesn't need to be inside the for loop.
    *   The loop is only necessary to set the new width for each item
    */
    var x = document.querySelectorAll(".randomPizzaContainer");
    var dx = determineDx(x[0], size);
    var newWidth = (x[0].offsetWidth + dx) + 'px';


    for (var i = 0; i < x.length; i++) {
      x[i].style.width = newWidth;
    }
  }

```

3-Changed the for-loop that actually creates and appends all of the pizzas when the page loads

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

4-Changed Function UpdatePositions
```
   /** The phase calculation was modified and the querySelectorAll was
  *   replaced by getElementByClassName.
  */

  var items = document.getElementsByClassName("mover");
  var factor = document.body.scrollTop / 1250;
  for (var i = 0; i < items.length; i++) {
    var phase = Math.sin(factor+(i % 5));
    items[i].style.left = items[i].basicLeft + 100 * phase + 'px';
  }
```


