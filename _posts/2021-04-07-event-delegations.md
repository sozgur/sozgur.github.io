---
layout: single
title: "Event Delegation"
date: 2021-04-07 15:05:00 -0700
categories:
    - Javascript
tags:
    - Javascript
    - row
    - column
---

<p> Event delegation is a technique by which you delegate a parent element as a listener in order to avoid to add multiple child elements.</p>

<p> Every event listener that you create uses memory in the browser.
So with using event delegation, you save memory and simplify initialization. </p>

<p> <em>Let's see in example:</em></p>

<!-- ![Three Equal Columns](/assets/images/columns.png) -->

<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
* {
  box-sizing: border-box;
}

.column {
float: left;
width: 30%;
padding: 10px;
height: 200px;
}

.row:after {
content: "";
display: table;
clear: both;
}
</style>

</head>
<body>

<h2>Three Equal Columns</h2>

<div class="row">
  <div class="column" style="background-color:#bab;">
    <h3>Column 1</h3>
    <p>Some text..</p>
  </div>
  <div class="column" style="background-color:#bca;">
    <h3>Column 2</h3>
    <p>Some text..</p>
  </div>
  <div class="column" style="background-color:#acc;">
    <h3>Column 3</h3>
    <p>Some text..</p>
  </div>
</div>

</body>

<script type="text/javascript">
    const row = document.querySelector('.row');

    const randomInt = (max, min) => Math.floor(Math.random() * (max - min + 1) + min);
    const randomColor = () => `rgb(${randomInt(0, 255)}, ${randomInt(0, 255)}, ${randomInt(0, 255)})`;

    row.addEventListener('click', function(e) {
        const clicked = e.target.closest('.column');
        if (!clicked) return;
        clicked.style.backgroundColor = randomColor();
    });
</script>
</html>

<br>
<p><em>The HTML code is as below: </em></p>

{% highlight html %}

<h2>Three Equal Columns</h2>

<div class="row">
    <div class="column" style="background-color:#bab;">
        <h3>Column 1</h3>
        <p>Some text..</p>
    </div>
    <div class="column" style="background-color:#bca;">
        <h3>Column 2</h3>
        <p>Some text..</p>
    </div>
    <div class="column" style="background-color:#acc;">
        <h3>Column 3</h3>
        <p>Some text..</p>
    </div>
</div>
{% endhighlight %}

The row has 3 columns, but it could be more than 3.

The column background color will be changed randomly by event delegation instead of assingn an `click` handler to each column (can be many).

<p><em>The JavaScript code is as below:</em></p>

```javascript
const row = document.querySelector(".row");

const randomInt = (max, min) =>
    Math.floor(Math.random() * (max - min + 1) + min);
const randomColor = () =>
    `rgb(${randomInt(0, 255)}, ${randomInt(0, 255)}, ${randomInt(0, 255)})`;

row.addEventListener("click", function (e) {
    //to get the clicked closest column element
    const clicked = e.target.closest(".column");

    // Guard clause
    if (!clicked) return;

    // change column background color randomly
    clicked.style.backgroundColor = randomColor();
});
```

It doesn't matter how many columns are in the row. `column` can be added or removed dynamically at any time and the code will still work.

<small>
References: 
<small> - [three equal columns] </small>
<small> - [event delegation] </small>
<small>

[three equal columns]: https://www.w3schools.com/howto/tryit.asp?filename=tryhow_css_three_columns
[event delegation]: https://javascript.info/event-delegation
