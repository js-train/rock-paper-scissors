# Rock Paper Scissors

## Setup a default HTML page

Create a file named `rpc.html` and add the standard HTML5 template:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  
</body>
</html>
```

## Setup User Selection Buttons

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <button>Rock</button>
  <button>Paper</button>
  <button>Scissors</button>
</body>
</html>
```

Next wire up an even handler function to each button. Optionally add some CSS to style the buttons. 

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Rock Paper Scissors</title>

  <!-- CSS - cascading style sheet -->
  <style>
    /* Use a CSS selector, then style rules */
    button {
      font-size: 40px;
      margin: 20px;
      padding: 10px;
      color: #7bc6ef;
      background-color: Transparent;
    }

  </style>

</head>
<body>

  <button onclick='onClicked("rock")'>Rock</button>
  <button onclick="onClicked('paper')">Paper</button>
  <button onclick="onClicked('scissors')">Scissors</button>

  <script>
    function onClicked(choice) {
      console.log("Player chose " + choice)
    }

  </script>

</body>
</html>

```

Checkpoint: clicking buttons should produce the expected output in the console


## Display the users choice on the screen

Add a `div` tag below the buttons which we will use to display the users choice. 

```html
  <button onclick='onClicked("rock")'>Rock</button>
  <button onclick="onClicked('paper')">Paper</button>
  <button onclick="onClicked('scissors')">Scissors</button>

  <div id="player-choice"></div>

```

Add the necessary Javascript needed in order to show this choice on the screen


```javascript
    function onClicked(choice) {
      console.log("Player chose " + choice)
      document.getElementById("player-choice").innerText = "The player chose " + choice
    }
```

## Hard code and display the users choice on the screen


Add another `div` which we will use to show the computers choice

```html
  <button onclick='onClicked("rock")'>Rock</button>
  <button onclick="onClicked('paper')">Paper</button>
  <button onclick="onClicked('scissors')">Scissors</button>

  <div id="player-choice"></div>
  <div id="computer-choice"></div>

```

Add the javascript to show a hard coded (static) computer choice of `rock`

```javascript
    function onClicked(choice) {
      console.log("Player chose " + choice)
      document.getElementById("player-choice").innerText = "The player chose " + choice

      const computerChoice = "rock"
      document.getElementById("computer-choice").innerText = "The computer chose " + computerChoice
    }
```

## If Statements 

Next we will use `if` statements. To understand these please read at least one of the following:

- https://www.w3schools.com/js/js_if_else.asp
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else
- https://www.geeksforgeeks.org/else-statement-javascript/


To implement this game we also need to know about logical operators. 

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators


hint:

```javascript

 if(playerMove === "rock" && computerMove === "paper") {
   console.log('player wins!')
 }

```


*If* these pages don't make sense, please ask for a bit of help.

## Add some partial game logic

First we add another `div` to show the result of the game

```html
  <button onclick='onClicked("rock")'>Rock</button>
  <button onclick="onClicked('paper')">Paper</button>
  <button onclick="onClicked('scissors')">Scissors</button>

  <div id="player-choice"></div>
  <div id="computer-choice"></div>
  <div id="game-result"></div>

```


Now in JavaScript we will add an `if` statement to implement the first bit of logic needed for the game. 

This is basic logic, which assumes the computer will always choose rock.


```javascript
    function onClicked(choice) {
      console.log("Player chose " + choice)
      document.getElementById("player-choice").innerText = "The player chose " + choice

      const computerChoice = "rock"
      document.getElementById("computer-choice").innerText = "The computer chose " + computerChoice

      if(choice === "rock") {
        document.getElementById("game-result").innerText = "It is a draw"
      } else if (choice === "paper") {
        document.getElementById("game-result").innerText = "You win!"
      } else {
        document.getElementById("game-result").innerText = "You loose :("
      }

    }
```

## Make the computer 'smarter'

### Random numbers 

The game would more be interesting if the computer made random choices, and not just rock. To do this we can make use of the random function built into JavaScript. This will produce a random number. We can then convert this to a random computer choice of rock, paper, or scissors.


##### TL;DR

We can use `Math.floor(Math.random() * 3)` to produce a random number of either 0, 1, or 2.

```javascript
const random = Math.floor(Math.random() * 3)
```

##### The explanation

To get a random number between from 0 to 1 we use `Math.random()`. This is inclusive of 0 but exclusive of 1. Try using `Math.random()` in the browsers console:

```
Math.random()
0.5646268108402965
Math.random()
0.7914220853289831
Math.random()
0.8838623687628653
Math.random()
0.9748423688421486
```

In this example, we want to get a random number from 0 to 3 (not including 3).

Multiplying `Math.random()` by 3 should produce results similar to:

```
Math.random() * 3
0.22772836579111422
Math.random() * 3
0.2450863107467307
Math.random() * 3
1.941311637616254
Math.random() * 3
0.27820652937094525
Math.random() * 3
2.9245514067166507
Math.random() * 3
0.6183681050203105
```

We can use `Math.floor` to remove the decimals e.g.

```
rnd = Math.random() * 3
1.7457885831489917
Math.floor(rnd)
1
```

To do this in one line we can use `Math.floor(Math.random() * 3)`:
```
Math.floor(Math.random() * 3)
1
Math.floor(Math.random() * 3)
1
Math.floor(Math.random() * 3)
0
Math.floor(Math.random() * 3)
2
Math.floor(Math.random() * 3)
0
Math.floor(Math.random() * 3)
0
```

Therefore we can use `Math.floor(Math.random() * 3)` to produce a random number of either 0, 1, or 2.

```javascript
const random = Math.floor(Math.random() * 3)
```

### Random computer choice

Using the code above, produce a random number from 0 to 3 (exclusive of 3). Using `if\else` statements convert that random number into a players choice of rock, paper or scissors.

## Complete the game (simples)

Now you have enough information, knowledge, skill, and self perseverance to finish the rock paper scissors game - good luck :)

