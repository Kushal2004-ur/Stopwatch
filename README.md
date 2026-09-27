# ⏱️ Stopwatch

A simple and responsive **Stopwatch Web Application** built using **HTML, CSS, and JavaScript**. The stopwatch allows users to start, stop, and reset a timer while displaying elapsed time in **hours, minutes, seconds, and milliseconds**.

This project was created to practice JavaScript timing functions, DOM manipulation, time calculations, conditional logic, and event-driven programming.

## ✨ Features

- ▶️ Start the stopwatch
- ⏸️ Stop/pause the stopwatch
- 🔄 Reset the stopwatch
- ⏱️ Displays hours, minutes, seconds, and milliseconds
- 🚫 Prevents multiple stopwatch intervals from starting at the same time
- 🎨 Clean and simple user interface
- 🖱️ Interactive button hover effects
- 📱 Responsive viewport configuration

## 🛠️ Technologies Used

- **HTML5** – Creates the stopwatch structure
- **CSS3** – Handles layout, styling, colors, buttons, and hover effects
- **JavaScript** – Implements stopwatch functionality and time calculations

## 📚 JavaScript Concepts Practiced

- Variables with `let` and `const`
- Functions
- `if` conditions
- Boolean values
- `Date.now()`
- `setInterval()`
- `clearInterval()`
- DOM manipulation
- `document.getElementById()`
- `textContent`
- `Math.floor()`
- `String()`
- `padStart()`
- Template literals
- Arithmetic operators
- Modulus `%` operator
- Event handling using HTML `onclick`

## 📁 Project Structure

```text
Stopwatch/
│
├── index.html
├── style.css
├── index.js
└── README.md
```

## ⚙️ How It Works

### 1. HTML Structure

The HTML contains a display area and three buttons:

```html
<div id="display">00:00:00:00</div>

<div id="buttons">
    <button id="startbtn" onclick="start()">Start</button>
    <button id="stopbtn" onclick="stop()">Stop</button>
    <button id="resetbtn" onclick="reset()">Reset</button>
</div>
```

The buttons call their respective JavaScript functions when clicked.

### 2. Initial Variables

```javascript
const display = document.getElementById('display');

let timer = null;
let startTime = 0;
let elapsedTime = 0;
let isRunning = false;
```

| Variable | Purpose |
|---|---|
| `display` | References the stopwatch display element |
| `timer` | Stores the interval ID |
| `startTime` | Stores the time when the stopwatch starts |
| `elapsedTime` | Stores the elapsed time |
| `isRunning` | Tracks whether the stopwatch is running |

## ▶️ Start Function

The `start()` function begins the stopwatch:

```javascript
function start(){
    if(!isRunning){
        startTime = Date.now() - elapsedTime;
        timer = setInterval(update, 10);
        isRunning = true;
    }
}
```

`Date.now() - elapsedTime` allows the stopwatch to continue from where it was stopped instead of starting again from zero.

The `if(!isRunning)` condition also prevents multiple intervals from being created if Start is clicked repeatedly.

## ⏸️ Stop Function

The `stop()` function pauses the stopwatch:

```javascript
function stop(){
    if(isRunning){
        clearInterval(timer);
        elapsedTime = Date.now() - startTime;
        isRunning = false;
    }
}
```

`clearInterval()` stops the repeated execution of `update()`.

The current elapsed time is saved so the stopwatch can continue from the same point when started again.

## 🔄 Reset Function

The `reset()` function returns the stopwatch to its initial state:

```javascript
function reset(){
    clearInterval(timer);
    startTime = 0;
    elapsedTime = 0;
    isRunning = false;
    display.textContent = "00:00:00:00";
}
```

It stops the timer, clears the stored time values, changes the running state to `false`, and resets the display.

## ⏱️ Updating the Stopwatch

The `update()` function calculates the elapsed time:

```javascript
function update(){
    const currentTime = Date.now();
    elapsedTime = currentTime - startTime;
}
```

`Date.now()` returns the current time in milliseconds.

The difference between the current time and the start time gives the total elapsed time.

## 🧮 Converting Milliseconds

The elapsed milliseconds are converted into hours, minutes, seconds, and milliseconds:

```javascript
let hours = Math.floor(elapsedTime / (1000 * 60 * 60));
let minutes = Math.floor(elapsedTime / (1000 * 60) % 60);
let seconds = Math.floor(elapsedTime / 1000 % 60);
let milliseconds = Math.floor(elapsedTime % 1000 / 10);
```

### Time conversions

```text
1 second      = 1,000 milliseconds
1 minute      = 60,000 milliseconds
1 hour        = 3,600,000 milliseconds
```

The milliseconds are divided by `10` so the display shows hundredths of a second.

## 🔢 Adding Leading Zeros

The project uses `padStart()` to maintain a consistent two-digit format:

```javascript
hours = String(hours).padStart(2,"0");
minutes = String(minutes).padStart(2,"0");
seconds = String(seconds).padStart(2,"0");
milliseconds = String(milliseconds).padStart(2,"0");
```

For example:

```text
1 → 01
5 → 05
9 → 09
```

So the display becomes:

```text
01:05:09:03
```

instead of:

```text
1:5:9:3
```

## 🖥️ Updating the Display

A template literal creates the final stopwatch value:

```javascript
display.textContent = `${hours}:${minutes}:${seconds}:${milliseconds}`;
```

The value is then inserted into the HTML element with the ID `display`.

## 🔁 How `setInterval()` Works

The stopwatch uses:

```javascript
timer = setInterval(update, 10);
```

The `update()` function runs approximately every **10 milliseconds** while the stopwatch is running.

When the stopwatch is stopped:

```javascript
clearInterval(timer);
```

stops the interval.

## 🎨 CSS Highlights

Flexbox is used to center the stopwatch:

```css
body {
    margin: 0px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
```

The main container uses a rounded border and centered layout:

```css
#container {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 30px;
    border: 5px solid;
    border-radius: 50px;
    background-color: white;
}
```

The timer display uses a large monospace font:

```css
#display {
    font-size: 5rem;
    font-family: monospace;
    font-weight: bold;
}
```

The buttons use different colors:

- **Start** → Green
- **Stop** → Red
- **Reset** → Blue

Hover effects make the buttons interactive.

## ▶️ How to Run

### Method 1: Open Directly

1. Download or clone the repository.
2. Open the project folder.
3. Open `index.html` in your browser.

### Method 2: Using VS Code Live Server

1. Open the project in **Visual Studio Code**.
2. Install the **Live Server** extension.
3. Right-click `index.html`.
4. Select **Open with Live Server**.
5. The stopwatch will open in your browser.

## 📤 Upload to GitHub

Create a new repository on GitHub and run:

```bash
git init
git add .
git commit -m "Add stopwatch project"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

Replace `YOUR-USERNAME` and `YOUR-REPOSITORY` with your GitHub username and repository name.

## 🔮 Future Improvements

- Add **Lap** functionality
- Store and display lap times
- Add a Pause/Resume button
- Add keyboard controls
- Add dark/light theme
- Improve mobile responsiveness
- Add sound notifications
- Add countdown timer functionality
- Add a lap history table
- Add animation effects to the timer

## 🎯 Learning Outcome

The main working flow of the project is:

```text
User clicks Start
        ↓
start() runs
        ↓
setInterval() calls update()
        ↓
Date.now() calculates elapsed time
        ↓
Milliseconds are converted
        ↓
padStart() formats the values
        ↓
textContent updates the display
        ↓
User clicks Stop
        ↓
clearInterval() pauses the stopwatch
```

## 👨‍💻 Author

**Kushal Raj U R**

B.E. – Information Science and Engineering

---

⭐ If you found this project useful, consider giving the repository a star!
