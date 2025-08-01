# API Reference - 3D Calculator

This document provides detailed technical documentation for all public APIs, functions, CSS classes, and DOM elements used in the 3D Calculator project.

## Table of Contents

- [JavaScript API](#javascript-api)
- [DOM Elements API](#dom-elements-api)
- [CSS Classes API](#css-classes-api)
- [Event Handlers](#event-handlers)
- [Calculation Engine](#calculation-engine)

---

## JavaScript API

### Variables

#### `buttons`
```javascript
let buttons = document.querySelector('.buttons');
```

**Type**: `HTMLElement`  
**Description**: References the main container element that holds all calculator buttons and the display.  
**Scope**: Global  
**Usage**: Used as a parent selector for finding child button elements.

**Example**:
```javascript
// Access the buttons container
console.log(buttons.className); // "buttons"
console.log(buttons.children.length); // Number of child elements
```

---

#### `btn`
```javascript
let btn = buttons.querySelectorAll('span');
```

**Type**: `NodeList`  
**Description**: Collection of all button elements (span tags) within the calculator.  
**Scope**: Global  
**Length**: Variable (depends on calculator layout)

**Properties**:
- `length`: Number of buttons in the calculator
- `[index]`: Access individual button elements

**Methods**:
- `forEach()`: Iterate through all buttons
- `item(index)`: Get button at specific index

**Example**:
```javascript
// Access all buttons
console.log(btn.length); // Total number of buttons

// Access individual button
console.log(btn[0].innerHTML); // Content of first button

// Iterate through buttons
btn.forEach((button, index) => {
    console.log(`Button ${index}: ${button.innerHTML}`);
});
```

---

#### `value`
```javascript
let value = document.getElementById('value');
```

**Type**: `HTMLElement` (h2)  
**Description**: The calculator display element that shows current input and results.  
**Scope**: Global  
**ID**: `value`

**Properties**:
- `innerHTML`: Current display content
- `textContent`: Plain text content
- `style`: CSS styling properties

**Example**:
```javascript
// Set display value
value.innerHTML = "123.45";

// Get current display
let currentValue = value.innerHTML;

// Clear display
value.innerHTML = "";

// Style the display
value.style.color = "red";
```

---

### Functions

#### Anonymous Click Handler
```javascript
function(event) {
    if (this.innerHTML == "="){
        value.innerHTML = eval(value.innerHTML);
    } else {
        if(this.innerHTML == 'Clear') {
            value.innerHTML = '';
        } else {
            value.innerHTML += this.innerHTML;
        }
    }
}
```

**Type**: Anonymous Function  
**Context**: Event listener attached to each button  
**Parameters**: 
- `event` (implicit): Click event object
- `this`: Reference to the clicked button element

**Behavior**:
1. **Equals Operation** (`=`): Evaluates the current expression
2. **Clear Operation** (`Clear`): Resets the display
3. **Default Operation**: Appends button value to display

**Example Usage**:
```javascript
// This function is automatically called when any button is clicked
// Manual invocation example:
let mockButton = { innerHTML: "5" };
let handler = function() {
    // ... function body
};
handler.call(mockButton); // Simulates clicking button "5"
```

---

### Initialization Loop
```javascript
for(let i = 0; i < btn.length; i++) {
    btn[i].addEventListener('click', handler);
}
```

**Purpose**: Attaches click event listeners to all calculator buttons  
**Scope**: Immediate execution  
**Parameters**:
- `i`: Loop counter (0 to btn.length-1)

**Process**:
1. Iterates through all button elements
2. Adds click event listener to each button
3. Associates the anonymous handler function

---

## DOM Elements API

### Main Container

#### `.calculator`
**Element**: `<div class="calculator">`  
**Purpose**: Root container for the entire calculator interface  
**Children**: `.buttons` container

**Properties**:
```javascript
// Access via JavaScript
let calculator = document.querySelector('.calculator');

// Properties
calculator.clientWidth;  // Width in pixels
calculator.clientHeight; // Height in pixels
calculator.children;     // Child elements
```

---

#### `.buttons`
**Element**: `<div class="buttons">`  
**Purpose**: Container for calculator display and all buttons  
**Parent**: `.calculator`  
**Layout**: CSS Grid

**Children**:
- `#value` (display)
- Multiple `<span>` elements (buttons)

---

### Display Element

#### `#value`
**Element**: `<h2 id="value">`  
**Purpose**: Shows current input and calculation results  
**Type**: Display/Output element

**API Methods**:
```javascript
// Get reference
let display = document.getElementById('value');

// Content manipulation
display.innerHTML = "0";        // Set content
display.innerHTML += "5";       // Append content
let content = display.innerHTML; // Get content

// Styling
display.style.fontSize = "2em";
display.style.color = "#fff";
```

---

### Button Elements

#### Number Buttons
**Elements**: `<span>0</span>`, `<span>1</span>`, ... `<span>9</span>`  
**Purpose**: Input numeric values  
**Count**: 10 buttons (0-9)

#### Operation Buttons
**Elements**: `<span>+</span>`, `<span>-</span>`, `<span>*</span>`, `<span>/</span>`  
**Purpose**: Mathematical operations  
**Count**: 4 buttons

#### Special Buttons
- `<span>.</span>` - Decimal point
- `<span>00</span>` - Double zero input
- `<span id="clear">Clear</span>` - Reset display
- `<span id="equal">=</span>` - Calculate result

**API Access**:
```javascript
// Access specific buttons
let clearBtn = document.getElementById('clear');
let equalBtn = document.getElementById('equal');
let plusBtn = document.getElementById('plus');

// Access by content
let numberButtons = Array.from(btn).filter(b => /^\d$/.test(b.innerHTML));
let operatorButtons = Array.from(btn).filter(b => /^[+\-*/]$/.test(b.innerHTML));
```

---

## CSS Classes API

### Layout Classes

#### `.calculator`
```css
.calculator {
    position: relative;
    width: 300px;
}
```

**Purpose**: Main calculator container styling  
**Properties**:
- `width`: Fixed 300px width
- `position`: Relative positioning context

**Customization**:
```css
/* Resize calculator */
.calculator {
    width: 400px; /* Larger calculator */
}

/* Responsive calculator */
.calculator {
    width: min(400px, 90vw); /* Responsive width */
}
```

---

#### `.calculator .buttons`
```css
.calculator .buttons {
    position: relative;
    display: grid;
}
```

**Purpose**: Button container with grid layout  
**Properties**:
- `display: grid` - CSS Grid layout
- Automatic grid sizing based on content

**Grid Configuration**:
```css
/* Explicit grid setup */
.calculator .buttons {
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 6px;
}
```

---

### Component Classes

#### `#value` (Display)
```css
.calculator .buttons #value {
    grid-column: span 4;
    height: 100px;
    background: #a7af7c;
    /* ... additional properties */
}
```

**Purpose**: Calculator display styling  
**Key Properties**:
- `grid-column: span 4` - Spans full width
- `height: 100px` - Fixed height
- `text-align: right` - Right-aligned text
- `overflow: hidden` - Prevents text overflow

**Customization Examples**:
```css
/* Dark theme display */
#value {
    background: #2d2d2d;
    color: #00ff00;
}

/* Larger display */
#value {
    height: 120px;
    font-size: 2em;
}
```

---

#### `.calculator .buttons span` (Buttons)
```css
.calculator .buttons span {
    padding: 10px;
    margin: 6px;
    background: linear-gradient(#555353, #363535);
    /* ... additional properties */
}
```

**Purpose**: Individual button styling  
**Key Properties**:
- `padding: 10px` - Internal spacing
- `margin: 6px` - Button separation
- `cursor: pointer` - Indicates clickable
- `user-select: none` - Prevents text selection

**States**:
```css
/* Hover state */
.calculator .buttons span:hover {
    background: linear-gradient(#666, #444);
}

/* Active state */
.calculator .buttons span:active {
    box-shadow: inset 0 2px 2px rgba(0,0,0,0.35);
}
```

---

### Special Button Classes

#### `#clear` (Clear Button)
```css
.calculator .buttons span#clear {
    grid-column: span 2;
    background: #f44336;
    color: #fff;
}
```

**Purpose**: Clear/Reset button styling  
**Properties**:
- `grid-column: span 2` - Double width
- `background: #f44336` - Red background
- `color: #fff` - White text

---

#### `#plus` (Plus Button)
```css
.calculator .buttons span#plus {
    grid-row: span 2;
    background: #31a935;
    color: #fff;
}
```

**Purpose**: Addition button styling  
**Properties**:
- `grid-row: span 2` - Double height
- `background: #31a935` - Green background
- `color: #fff` - White text

---

#### `#equal` (Equals Button)
```css
.calculator .buttons span#equal {
    background: #2196f3;
    color: #fff;
}
```

**Purpose**: Calculate/Equals button styling  
**Properties**:
- `background: #2196f3` - Blue background
- `color: #fff` - White text

---

## Event Handlers

### Click Event Handler

#### Event Registration
```javascript
btn[i].addEventListener('click', function(){...});
```

**Event Type**: `click`  
**Target**: All calculator buttons (`span` elements)  
**Bubbling**: Default (bubbles up)

#### Event Flow
1. **Capture Phase**: Event travels down to target
2. **Target Phase**: Event reaches the clicked button
3. **Bubble Phase**: Event bubbles up through DOM

#### Handler Logic
```javascript
function handleButtonClick(event) {
    let buttonText = this.innerHTML;
    
    switch(buttonText) {
        case "=":
            // Evaluate expression
            value.innerHTML = eval(value.innerHTML);
            break;
            
        case "Clear":
            // Reset display
            value.innerHTML = '';
            break;
            
        default:
            // Append to display
            value.innerHTML += buttonText;
            break;
    }
}
```

**Parameters**:
- `this`: Reference to clicked button element
- `event`: Click event object (unused but available)

---

### Custom Event Handling

#### Adding New Handlers
```javascript
// Add custom event handler
btn.forEach(button => {
    button.addEventListener('mousedown', function() {
        this.style.transform = 'scale(0.95)';
    });
    
    button.addEventListener('mouseup', function() {
        this.style.transform = 'scale(1)';
    });
});
```

#### Keyboard Support
```javascript
// Add keyboard support
document.addEventListener('keydown', function(event) {
    let key = event.key;
    
    // Find matching button
    let matchingButton = Array.from(btn).find(b => 
        b.innerHTML === key || 
        (key === 'Enter' && b.innerHTML === '=') ||
        (key === 'Escape' && b.innerHTML === 'Clear')
    );
    
    if (matchingButton) {
        matchingButton.click();
    }
});
```

---

## Calculation Engine

### Expression Evaluation

#### Core Function
```javascript
eval(value.innerHTML)
```

**Purpose**: Evaluates mathematical expressions  
**Input**: String representation of mathematical expression  
**Output**: Calculated result or error

**Supported Operations**:
- Addition: `+`
- Subtraction: `-`
- Multiplication: `*`
- Division: `/`
- Parentheses: `(` `)`
- Decimal numbers: `12.34`

#### Security Considerations
```javascript
// Safer evaluation (example implementation)
function safeEval(expression) {
    // Remove non-mathematical characters
    let sanitized = expression.replace(/[^0-9+\-*/.() ]/g, '');
    
    try {
        return eval(sanitized);
    } catch (error) {
        return "Error";
    }
}
```

### Error Handling

#### Division by Zero
```javascript
// Result: Infinity
value.innerHTML = "5/0"; // Display shows "5/0"
// After clicking "=":
value.innerHTML; // "Infinity"
```

#### Invalid Expressions
```javascript
// Result: Error or unexpected behavior
value.innerHTML = "5++3"; // Invalid syntax
value.innerHTML = "5+"; // Incomplete expression
```

#### Recommended Error Handling
```javascript
function calculateResult() {
    try {
        let result = eval(value.innerHTML);
        
        if (!isFinite(result)) {
            value.innerHTML = "Error";
        } else {
            value.innerHTML = result;
        }
    } catch (error) {
        value.innerHTML = "Error";
    }
}
```

---

## Browser Compatibility

### JavaScript Features
- `document.querySelector()`: IE8+
- `addEventListener()`: IE9+
- `querySelectorAll()`: IE8+
- `eval()`: All browsers

### CSS Features
- CSS Grid: IE10+ (with prefix)
- Box Shadow: IE9+
- Linear Gradient: IE10+
- Transform: IE9+

### Recommended Polyfills
```html
<!-- For older browsers -->
<script src="https://polyfill.io/v3/polyfill.min.js?features=default"></script>
```

---

## Performance Considerations

### DOM Queries
```javascript
// Good: Cache selectors
let buttons = document.querySelector('.buttons');
let btn = buttons.querySelectorAll('span');

// Avoid: Repeated queries
// document.querySelector('.buttons') // Don't repeat
```

### Event Delegation
```javascript
// Alternative: Event delegation (more efficient for many buttons)
document.querySelector('.buttons').addEventListener('click', function(event) {
    if (event.target.tagName === 'SPAN') {
        // Handle button click
        handleButtonClick.call(event.target, event);
    }
});
```

### Memory Management
```javascript
// Remove event listeners when not needed
function cleanup() {
    btn.forEach(button => {
        button.removeEventListener('click', handleButtonClick);
    });
}
```

---

This API reference provides comprehensive documentation for all public interfaces in the 3D Calculator project. For implementation examples and usage patterns, refer to the main README.md file.