---
title:  "Javascript: Best Practices"
date: 2017-10-30
author: Ajay Upreti
categories:
- blog
tags:
- frontend
---


In this blog, I’ll share a set of Javascript best practices.

## 1. Use var keyword when assigning a variable’s value for the first time.
Assignment to an undeclared variable automatically results in a global variable being created. Avoid global variables.

## 2. use === instead of ==
Always use === and !== operators because they are reliable. Using their similars == and != may lead to unpredictable results.
```
<script type="text/javascript">
//AVOID
false == '0' //true
//BETTER
false === '0' //false
</script>
```
## 3. Avoid Global variables
Global variables are visible in every scope. They can be changed by any part of your program at any time. Avoiding global variables in early stage will save you a lot of problems when your code base grows up.
```
<script type="text/javascript">
//AVOID
var x = 5; //it's global
window.y = 2; //it's global
//it's global
function multiply(x, y) {
    return x * y;
}
//BETTER
(function () {
    var x = 5, y = 2;
    function multiply(x, y) {
        return x * y;
    }
})();
</script>
```

## 4. Use Semicolons for line termination
The use of semi-colons for line termination is a good practice. You won’t be warned if you forget it because in most cases it will be inserted by the JavaScript parser.

## 5. Create a Self-calling Function

This is often called a Self-Invoked Anonymous Function or Immediately Invoked Function Expression (IIFE). It is a function that executes automatically when you create it, and has the following form:
```
(function(){
    // some private code that will be executed automatically
})();  
(function(a,b){
    var result = a+b;
    return result;
})(10,20)
```

## 6. Avoid Increment(++) and Decrement(--) Operators

Due possible security vulnerabilities you should avoid increment and decrement operators.
```
<script type="text/javascript">
//AVOID
for (var i = 0; i < 10; i++)
//BETTER
for (var i = 0; i < 10; i += 1)
</script>
```

## 7. Stop Touching the DOM
Accessing the DOM is memory expensive and may slow down your javascript program. So it's always better to cache the references to DOM elements.
```
<script type="text/javascript">
//AVOID
document.getElementById("test").style.display = 'block';
document.getElementById("test").className = 'my-class';
document.getElementById("test").innerHTML = 'Hello World';
//BETTER
var el = document.getElementById("test");
el.style.display = 'block';
el.className = 'my-class';
el.innerHTML = 'Hello World';
</script>
```

## 8. String Concatination
You can concatenate strings in many ways, but most efficient is Array.join()
```
<script type="text/javascript">
var store = {'lemon': 'yellow', 'cherry': 'red'};
//AVOID
var str = "Lemons are " + store.lemon + ", tomatos are" + store.cherry;
//BETTER
var str = ["Lemons are ", store.lemon, ", tomatos are", store.cherry].join("");
</script>
```


## 9. Use a switch/case statement instead of a series of if/else

Using switch/case is faster when there are more than 2 cases, and it is more elegant (better-organized code). Avoid using it when you have more than 10 cases.

## 10. Use switch/case statement with numeric ranges

Using a switch/case statement with numeric ranges is possible with this trick.
```
function getCategory(age) {  
    var category = "";  
    switch (true) {  
        case isNaN(age):  
            category = "not an age";  
            break;  
        case (age >= 50):  
            category = "Old";  
            break;  
        case (age <= 20):  
            category = "Baby";  
            break;  
        default:  
            category = "Young";  
            break;  
    };  
    return category;  
}  
getCategory(5);  // will return "Baby"
```

## 11. Pass functions, not strings, to setTimeout() and setInterval()
If you pass a string into setTimeout() or setInterval(), the string will be evaluated the same way as with eval, which is slow.
```
//AVOID
setInterval('doSomethingPeriodically()', 1000);   
Edit Message

setTimeout('doSomethingAfterFiveSeconds()', 5000);

//BETTER
setInterval(doSomethingPeriodically, 1000);  
setTimeout(doSomethingAfterFiveSeconds, 5000);
````


## 12. Avoid Multiple "var" Statements
Declare var only once. You can place your var statements everywhere in your program, but it's more readable if you put them at the top of your functions or block scope. Don't forget to declare your variables and functions before using them.


## 13. The Proper way For iterate over objects

Before using an object property you should check if it exists. So you need to use the hasOwnProperty method.
```
<script type="text/javascript">
var store = {'lemon': 8, 'banana': 12, 'orange': 3};
//WRONG
for (var x in store) {
    console.log(x, store[x]);
}
//BETTER
for (var x in store) {
    if (store.hasOwnProperty(x)) {
        console.log(x, store[x]);
    }
}
</script>
```

## 14. Optimize Loops
Instead of reading the length of an array at every iteration, you should get it only once.
```
<script type="text/javascript">
var haystack = [1,10,13,7,29,0,4,21];
//AVOID
for (var i = 0; i < haystack.length; i += 1) {
    console.log(haystack[i]);
}
//BETTER
for (var i = 0, iCnt = haystack.length; i < iCnt; i += 1) {
    console.log(haystack[i]);
}
</script>
```

## CONCLUSION
There are great free tools that can help you to validate, analyze and improve your javascript code. Check out one of the best [JSLint](http://www.jslint.com/) and [JSHint](http://jshint.com/). 
