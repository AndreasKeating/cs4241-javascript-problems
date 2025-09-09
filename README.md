
# ICE 02: JavaScript Exercises

In this activity, you will be completing a series of JavaScript exercises on your own and comparing your answers to those around you. This should help you develop a sense of different ways to go about solving JavaScript problems.

**DO NOT USE AI FOR THIS EXERCISE!!!**

### Instructions

1. Divide yourselves into groups of 3 - 5 students. You are submitting individually and thus do not need to create groups on Canvas.

2. Below are a series of JavaScript problems. Try to solve each one on your own. You may use the web to get more information, although you may not simply look up the answer to the entire problem. Be sure to cite in your code comments any websites you used to help you out. Avoid third-pary frameworks and libraries (Three.js, Canvas, SVG, etc.) .

3. After you complete each problem, check in with your teammates. If you were unable to complete the problem, ask your teammates for help. Your teammates should NOT simply show you the answer. 

4. Once everybody in your team has completed the problem, compare your respective solutions and note any differences in your approaches. In the comments below your problem, briefly note these differences, highlighting anything you found interesting. If everybody on your team had essentially the same solution, note that instead.

5. Once your team has completed all problems, create a *.zip file containing all of your code and submit it on Canvas. Each team member is submitting their own work. Your *.zip file does not have to have a specific name.


**Problem 1**
```js
// Make two objects named Artist
// and Painter. Artist should have
// a function named speak() that
// when called logs "I am an artist"
// to the console. Painter should be
// able to use the Artist's speak function
// (painters are artists, after all) in some
// way, and should also have a function named
// paint() that sets the background color of the
// page to a random color whenever called. 

const Artist  = {
    speak(){
        console.log("I am an artist");
    }
};

const Painter = {
    speak(){
        Artist.speak();
    },
    paint(){

        //const r = Math.floor(Math.random() * 256);
         //const g = Math.floor(Math.random() * 256);
        //const b = Math.floor(Math.random() * 256); 

        const randomColorNum = `#${Math.floor(Math.random() * ((256 * 256 * 256))).toString(16).padStart(6, "0")}`; //Fixed by makig it an actual Hex color
        document.body.style.backgroundColor = randomColorNum;
    }
};
```

**Problem 2**
```js
// create a for loop that creates 20 blocks,
// all on a single row, with a random color for each
// make sure the values for each color channel are different
// (i.e. no gray/black/white blocks)

function randomColor(){

   //const randomColorNum = `#${Math.floor(Math.random() * ((256 * 256 * 256))).toString(16)}`;

    let r, g, b;
    r = Math.floor(Math.random() * 256);
    g = Math.floor(Math.random() * 256);
    b = Math.floor(Math.random() * 256);

    while (g === b && r ===g) { //To make sure I don't generate gray/black/white colors.
        r = Math.floor(Math.random() * 256);
        g = Math.floor(Math.random() * 256);
        b = Math.floor(Math.random() * 256);
    } 

    return ("#" + r.toString(16).padStart(2, "0") + g.toString(16).padStart(2, "0") + b.toString(16).padStart(2, "0"));
    //return randomColorNum;
}

const usedColors = [];
const row = document.getElementById("row");
for (let i = 0; i < 20; i++) {

    const block = document.createElement("div");

    block.style.width = "50px";
    block.style.height = "50px";
    block.style.display = "inline-block"; // (Buttons "spawn" in Single row)

    let repeatedColor = true;
    let color;
    while (repeatedColor) { // Checks for repeat colors
        color = randomColor();
        repeatedColor = false;

        for (let x = 0; x < usedColors.length; x++) {
            if (color === usedColors[x]) {
            repeatedColor = true;

            break;
            }
        }
    }
    
    usedColors.push(color);
    block.style.backgroundColor = color;
    row.appendChild(block);
}

```

**Problem 3**
```js
// create a for input field that does the following 
// whenever the user enters a letter in it:
// 1. Creates a <h1> element containing the letter and appends it to the page
// 2. deletes the inputted letter from the input field so it is blank
<!DOCTYPE html>

<html>
<body>

    <input id  = "letterInput" type = "text" maxlength= "1">

    <script>
        const input = document.getElementById("letterInput");

        input.addEventListener("input", function () {
            const letter = input.value;
            if(letter) {
                const h1 = document.createElement("h1")
                h1.textContent = letter;
                document.body.appendChild(h1);

                input.value = "";
            }
        });
    </script>
</body>
</html>
```

**Problem 4**
```js
// make a button that, when clicked, creates a new
// button, and then deletes the original button. 
// every button that is created should have this same behavior.
// put random text inside of each button so you can be sure 
// that each button is different.
<!DOCTYPE html>

<html>
<body>
  <button id="starter"> Click me </button>

  <script>
    function RandomText (){
      const texts = ["Alpha", "Bravo", "Charlie", "Delta", "Echo"];
      const index = Math.floor(Math.random() * texts.length);
      return texts[index];
    }

    function setupButton(button) {
      button.addEventListener("click", function() {
        const newButton = document.createElement("button");
        newButton.innerHTML = RandomText();
        setupButton(newButton);
        document.body.appendChild(newButton);
        //button.delete();
        button.remove();
      })
    }

    const starter = document.getElementById("starter");
    setupButton(starter);
  </script>
</body>
</html>
```