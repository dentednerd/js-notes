# p5.js
JS library for animations  
Node can't handle visual elements, need to go to browser  
need to create HTML page  
use Bower package manager, installed with npm  
then run `bower init` to get bower.json  
scripts get loaded in order and put into global scope  
2 functions that p5 looks for:
```javascript
function setup () {
    createCanvas(400, 400);
    background(51);
}

function draw () {
    // 30fps
    ellipse(width/2, height/2, 16, 16);
}   // draws a dot in the middle of the background

    ellipse(mouseX, mouseY, 16, 16)
    // draws a dot wherever the mouse is - trail of dots

    if(mouseIsPressed) {
        fill(255);
    } else {
        fill(0);
    }
    // fills the background white when clicked
```