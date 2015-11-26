#Website Performance Optimization portfolio project

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


##Optimizations made on main.js

The page pizza.html should run at 60FPS when scrolling and resize the pizzas in less than 5ms.


1 - Reduced the amount of sliding pizzas from 200 to 30 

```
document.addEventListener('DOMContentLoaded', function() {
/** Generates 30 slilding pizzas to put in the background. There is no need to put 
 * 200 as it was.
 */
for (var i = 0; i < 30; i++) {
  ...
}
```

2 - Changed the function **_changePizzaSizes_**

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
*/

var items = document.getElementsByClassName("mover");
var factor = document.body.scrollTop / 1250;
for (var i = 0; i < items.length; i++) {
  var phase = Math.sin(factor+(i % 5));
  items[i].style.left = items[i].basicLeft + 100 * phase + 'px';
}
```
