# Component Documentation - 3D Calculator

This document provides detailed documentation for all UI components used in the 3D Calculator project, including their structure, styling, behavior, and usage examples.

## Table of Contents

- [Component Architecture](#component-architecture)
- [Calculator Container](#calculator-container)
- [Display Component](#display-component)
- [Button Components](#button-components)
- [Layout System](#layout-system)
- [Styling Guide](#styling-guide)
- [Component Examples](#component-examples)

---

## Component Architecture

The 3D Calculator follows a hierarchical component structure:

```
Calculator
├── ButtonsContainer
    ├── Display
    ├── NumberButtons (0-9)
    ├── OperatorButtons (+, -, *, /)
    ├── SpecialButtons (., 00)
    ├── ClearButton
    └── EqualsButton
```

### Design Principles

1. **Single Responsibility**: Each component has one primary function
2. **Reusability**: Common button styling with specific overrides
3. **Accessibility**: Semantic HTML and keyboard support
4. **Visual Hierarchy**: Clear distinction between different button types
5. **Responsive Design**: Adapts to different screen sizes

---

## Calculator Container

### Overview
The root container component that wraps the entire calculator interface.

### HTML Structure
```html
<div class="calculator">
    <!-- All calculator content -->
</div>
```

### Component Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `width` | CSS Length | `300px` | Fixed width of calculator |
| `position` | CSS Position | `relative` | Positioning context |

### CSS Specification
```css
.calculator {
    position: relative;
    width: 300px;
}
```

### Usage Examples

#### Basic Implementation
```html
<div class="calculator">
    <div class="buttons">
        <!-- Calculator content -->
    </div>
</div>
```

#### Responsive Implementation
```css
.calculator {
    width: min(300px, 90vw);
    max-width: 400px;
}
```

#### Themed Implementation
```css
.calculator.dark-theme {
    filter: brightness(0.8);
}

.calculator.large {
    width: 400px;
    transform: scale(1.2);
}
```

### API Methods

```javascript
// Get calculator instance
const calculator = document.querySelector('.calculator');

// Resize calculator
function resizeCalculator(width) {
    calculator.style.width = width + 'px';
}

// Toggle themes
function toggleTheme(theme) {
    calculator.className = `calculator ${theme}`;
}
```

---

## Display Component

### Overview
The display component shows current input values and calculation results.

### HTML Structure
```html
<h2 id="value"></h2>
```

### Component Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `grid-column` | CSS Grid | `span 4` | Spans full calculator width |
| `height` | CSS Length | `100px` | Fixed display height |
| `background` | CSS Color | `#a7af7c` | Display background color |
| `text-align` | CSS Alignment | `right` | Right-aligned text |

### CSS Specification
```css
.calculator .buttons #value {
    position: relative;
    left: 8px;
    margin-bottom: 12px;
    grid-column: span 4;
    height: 100px;
    line-height: 100px;
    padding: 0 20px;
    border-radius: 10px;
    background: #a7af7c;
    text-align: right;
    font-size: 1.5em;
    color: #3a3c2e;
    overflow: hidden;
    box-shadow: inset 0 6px 1px 0 rgba(0,0,0,0.35), 
                0 5px 5px rgba(0,0,0,0.5), 
                0 15px 25px rgba(0,0,0,0.35);
    user-select: none;
    width: calc(100% - 16px);
}
```

### Behavioral Features

#### Text Display
- **Right-aligned**: Numbers appear from right to left
- **Overflow handling**: Long numbers are hidden with `overflow: hidden`
- **Line height**: Vertically centers text in display area

#### Visual Effects
- **Inset shadow**: Creates recessed appearance
- **Rounded corners**: Modern, polished look
- **Gradient reflection**: Simulates glass surface

### Usage Examples

#### Basic Display Updates
```javascript
const display = document.getElementById('value');

// Set display value
display.innerHTML = "123.45";

// Append to display
display.innerHTML += "6";

// Clear display
display.innerHTML = "";

// Format large numbers
function formatNumber(num) {
    return num.toLocaleString();
}
display.innerHTML = formatNumber(1234567);
```

#### Display Animations
```css
/* Fade in new values */
#value {
    transition: opacity 0.2s ease;
}

#value.updating {
    opacity: 0.7;
}
```

```javascript
// Animate display updates
function animateDisplayUpdate(newValue) {
    display.classList.add('updating');
    setTimeout(() => {
        display.innerHTML = newValue;
        display.classList.remove('updating');
    }, 100);
}
```

#### Error Display
```javascript
function showError(message = "Error") {
    display.innerHTML = message;
    display.style.color = "#ff4444";
    
    setTimeout(() => {
        display.style.color = "#3a3c2e";
    }, 2000);
}
```

### Customization Options

#### Theme Variations
```css
/* Dark theme display */
.calculator.dark #value {
    background: #2d2d2d;
    color: #00ff00;
    box-shadow: inset 0 6px 1px 0 rgba(255,255,255,0.1);
}

/* High contrast display */
.calculator.high-contrast #value {
    background: #000;
    color: #fff;
    border: 2px solid #fff;
}

/* Retro display */
.calculator.retro #value {
    background: #000;
    color: #00ff00;
    font-family: 'Courier New', monospace;
    text-shadow: 0 0 10px #00ff00;
}
```

---

## Button Components

### Overview
Interactive button components for calculator input and operations.

### Base Button Structure
```html
<span>Button Text</span>
```

### Component Hierarchy

#### Number Buttons
```html
<span>0</span>
<span>1</span>
<span>2</span>
<!-- ... -->
<span>9</span>
```

#### Operator Buttons
```html
<span>+</span>
<span>-</span>
<span>*</span>
<span>/</span>
```

#### Special Buttons
```html
<span>.</span>      <!-- Decimal point -->
<span>00</span>     <!-- Double zero -->
```

#### Action Buttons
```html
<span id="clear">Clear</span>
<span id="equal">=</span>
<span id="plus">+</span>
```

### Base Button Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `padding` | CSS Length | `10px` | Internal button spacing |
| `margin` | CSS Length | `6px` | Space between buttons |
| `min-width` | CSS Length | `40px` | Minimum button width |
| `font-size` | CSS Length | `1.1em` | Button text size |
| `cursor` | CSS Cursor | `pointer` | Indicates clickable |

### Base CSS Specification
```css
.calculator .buttons span {
    position: relative;
    padding: 10px;
    margin: 6px;
    min-width: 40px;
    font-size: 1.1em;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #999;
    border: 2px solid #222;
    border-radius: 6px;
    background: linear-gradient(#555353, #363535);
    box-shadow: inset 0 6px 1px 0 rgba(0,0,0,0.35), 
                0 5px 5px rgba(0,0,0,0.5), 
                0 15px 25px rgba(0,0,0,0.35);
    cursor: pointer;
    user-select: none;
}
```

### Button States

#### Normal State
- Raised appearance with gradient background
- Subtle border and shadow effects
- Gray text color

#### Hover State (Custom Implementation)
```css
.calculator .buttons span:hover {
    background: linear-gradient(#666, #444);
    color: #ccc;
}
```

#### Active State
```css
.calculator .buttons span:active {
    box-shadow: inset 0 2px 2px rgba(0,0,0,0.35),
                inset 0 5px 15px rgba(0,0,0,0.5),
                inset 0 15px 25px rgba(0,0,0,0.35);
    color: #fff;
    text-shadow: 0 0 5px #219cf3,
                 0 0 8px #219cf3;
}
```

### Special Button Variants

#### Clear Button
```css
.calculator .buttons span#clear {
    grid-column: span 2;  /* Double width */
    background: #f44336;  /* Red background */
    color: #fff;         /* White text */
}
```

**Properties:**
- **Width**: Spans 2 grid columns
- **Color**: Red background with white text
- **Function**: Resets calculator display

#### Plus Button
```css
.calculator .buttons span#plus {
    grid-row: span 2;    /* Double height */
    background: #31a935; /* Green background */
    color: #fff;        /* White text */
}
```

**Properties:**
- **Height**: Spans 2 grid rows
- **Color**: Green background with white text
- **Function**: Addition operation

#### Equals Button
```css
.calculator .buttons span#equal {
    background: #2196f3; /* Blue background */
    color: #fff;        /* White text */
}
```

**Properties:**
- **Color**: Blue background with white text
- **Function**: Calculates and displays result

### Button Event Handling

#### Click Events
```javascript
// Attach click listeners to all buttons
btn.forEach((button, index) => {
    button.addEventListener('click', function() {
        handleButtonClick.call(this);
    });
});

function handleButtonClick() {
    const buttonValue = this.innerHTML;
    const display = document.getElementById('value');
    
    switch(buttonValue) {
        case '=':
            calculateResult();
            break;
        case 'Clear':
            clearDisplay();
            break;
        default:
            appendToDisplay(buttonValue);
            break;
    }
}
```

#### Visual Feedback
```javascript
// Add press animation
function addPressAnimation(button) {
    button.addEventListener('mousedown', function() {
        this.style.transform = 'scale(0.95)';
    });
    
    button.addEventListener('mouseup', function() {
        this.style.transform = 'scale(1)';
    });
}

// Apply to all buttons
btn.forEach(addPressAnimation);
```

### Button Customization

#### Custom Button Types
```javascript
// Create specialized button
function createCustomButton(text, className, handler) {
    const button = document.createElement('span');
    button.innerHTML = text;
    button.className = className;
    button.addEventListener('click', handler);
    return button;
}

// Add memory buttons
const memoryAdd = createCustomButton('M+', 'memory-button', handleMemoryAdd);
const memoryRecall = createCustomButton('MR', 'memory-button', handleMemoryRecall);
```

#### Button Styling Variations
```css
/* Scientific calculator buttons */
.calculator .buttons .scientific {
    background: linear-gradient(#4a4a4a, #2a2a2a);
    color: #fff;
    font-size: 0.9em;
}

/* Function buttons */
.calculator .buttons .function {
    background: linear-gradient(#667db6, #0082c8);
    color: #fff;
    font-weight: bold;
}

/* Number buttons highlight */
.calculator .buttons .number:hover {
    background: linear-gradient(#777, #555);
}
```

---

## Layout System

### Grid Layout
The calculator uses CSS Grid for button arrangement:

```css
.calculator .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 0; /* Handled by button margins */
}
```

### Grid Areas

#### Standard Layout
```
┌─────────────────────┐
│      Display        │  grid-column: span 4
├─────┬─────┬─────────┤
│Clear│  /  │    *    │
├─────┼─────┼─────┬───┤
│  7  │  8  │  9  │   │
├─────┼─────┼─────┤ + │  grid-row: span 2
│  4  │  5  │  6  │   │
├─────┼─────┼─────┼───┤
│  1  │  2  │  3  │   │
├─────┼─────┼─────┤ = │
│  0  │ 00  │  .  │   │
└─────┴─────┴─────┴───┘
```

#### Grid Implementation
```css
/* Display spans full width */
#value {
    grid-column: span 4;
}

/* Clear button spans 2 columns */
#clear {
    grid-column: span 2;
}

/* Plus button spans 2 rows */
#plus {
    grid-row: span 2;
}
```

### Responsive Considerations

#### Mobile Layout
```css
@media (max-width: 480px) {
    .calculator {
        width: 90vw;
        max-width: 350px;
    }
    
    .calculator .buttons span {
        padding: 15px;
        font-size: 1.2em;
    }
}
```

#### Tablet Layout
```css
@media (min-width: 768px) {
    .calculator {
        width: 400px;
    }
    
    .calculator .buttons span {
        padding: 12px;
        font-size: 1.3em;
    }
}
```

---

## Styling Guide

### Color Palette

#### Base Colors
```css
:root {
    --display-bg: #a7af7c;
    --display-text: #3a3c2e;
    --button-bg-start: #555353;
    --button-bg-end: #363535;
    --button-text: #999;
    --button-border: #222;
    --clear-bg: #f44336;
    --plus-bg: #31a935;
    --equal-bg: #2196f3;
    --body-bg: #333;
}
```

#### Usage
```css
.calculator .buttons #value {
    background: var(--display-bg);
    color: var(--display-text);
}

.calculator .buttons span {
    background: linear-gradient(var(--button-bg-start), var(--button-bg-end));
    color: var(--button-text);
    border: 2px solid var(--button-border);
}
```

### Shadow System

#### Display Shadows
```css
/* Inset shadow for recessed appearance */
.display-inset {
    box-shadow: inset 0 6px 1px 0 rgba(0,0,0,0.35),
                0 5px 5px rgba(0,0,0,0.5),
                0 15px 25px rgba(0,0,0,0.35);
}
```

#### Button Shadows
```css
/* Raised button appearance */
.button-raised {
    box-shadow: inset 0 6px 1px 0 rgba(0,0,0,0.35),
                0 5px 5px rgba(0,0,0,0.5),
                0 15px 25px rgba(0,0,0,0.35);
}

/* Pressed button appearance */
.button-pressed {
    box-shadow: inset 0 2px 2px rgba(0,0,0,0.35),
                inset 0 5px 15px rgba(0,0,0,0.5),
                inset 0 15px 25px rgba(0,0,0,0.35);
}
```

### Typography

#### Font Settings
```css
* {
    font-family: monospace;
}

#value {
    font-size: 1.5em;
    line-height: 100px;
}

.calculator .buttons span {
    font-size: 1.1em;
}
```

### Animation Guidelines

#### Transition Properties
```css
.calculator .buttons span {
    transition: all 0.2s ease;
}

#value {
    transition: color 0.3s ease;
}
```

#### Hover Effects
```css
.calculator .buttons span:hover {
    transform: translateY(-2px);
    box-shadow: inset 0 6px 1px 0 rgba(0,0,0,0.35),
                0 8px 8px rgba(0,0,0,0.5),
                0 20px 30px rgba(0,0,0,0.35);
}
```

---

## Component Examples

### Complete Calculator Implementation
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>3D Calculator - Components Demo</title>
    <link rel="stylesheet" href="calculator-components.css">
</head>
<body>
    <div class="calculator">
        <div class="buttons">
            <!-- Display Component -->
            <h2 id="value" class="display-component"></h2>
            
            <!-- Clear Button Component -->
            <span id="clear" class="button-component clear-button">Clear</span>
            
            <!-- Operator Button Components -->
            <span class="button-component operator-button">/</span>
            <span class="button-component operator-button">*</span>
            
            <!-- Number Button Components -->
            <span class="button-component number-button">7</span>
            <span class="button-component number-button">8</span>
            <span class="button-component number-button">9</span>
            
            <!-- Plus Button Component (Special) -->
            <span id="plus" class="button-component plus-button">+</span>
            
            <!-- More Number Button Components -->
            <span class="button-component number-button">4</span>
            <span class="button-component number-button">5</span>
            <span class="button-component number-button">6</span>
            
            <span class="button-component number-button">1</span>
            <span class="button-component number-button">2</span>
            <span class="button-component number-button">3</span>
            
            <!-- Special Button Components -->
            <span class="button-component number-button">0</span>
            <span class="button-component special-button">00</span>
            <span class="button-component special-button">.</span>
            
            <!-- Equals Button Component -->
            <span id="equal" class="button-component equals-button">=</span>
        </div>
    </div>
    
    <script src="calculator-components.js"></script>
</body>
</html>
```

### Component-Based JavaScript
```javascript
// Calculator Component System
class CalculatorComponent {
    constructor(element) {
        this.element = element;
        this.display = element.querySelector('#value');
        this.buttons = element.querySelectorAll('.button-component');
        this.init();
    }
    
    init() {
        this.attachEventListeners();
        this.reset();
    }
    
    attachEventListeners() {
        this.buttons.forEach(button => {
            button.addEventListener('click', (e) => {
                this.handleButtonClick(e.target);
            });
        });
    }
    
    handleButtonClick(button) {
        const value = button.innerHTML;
        
        if (button.classList.contains('number-button') || 
            button.classList.contains('operator-button') ||
            button.classList.contains('special-button')) {
            this.appendToDisplay(value);
        } else if (button.classList.contains('equals-button')) {
            this.calculate();
        } else if (button.classList.contains('clear-button')) {
            this.clear();
        }
    }
    
    appendToDisplay(value) {
        this.display.innerHTML += value;
    }
    
    calculate() {
        try {
            const result = eval(this.display.innerHTML);
            this.display.innerHTML = result;
        } catch (error) {
            this.display.innerHTML = 'Error';
        }
    }
    
    clear() {
        this.display.innerHTML = '';
    }
    
    reset() {
        this.display.innerHTML = '';
    }
}

// Initialize calculator
document.addEventListener('DOMContentLoaded', () => {
    const calculator = new CalculatorComponent(
        document.querySelector('.calculator')
    );
});
```

### Advanced Component Features

#### Button Factory
```javascript
class ButtonFactory {
    static create(type, text, id = null) {
        const button = document.createElement('span');
        button.innerHTML = text;
        button.className = `button-component ${type}-button`;
        
        if (id) {
            button.id = id;
        }
        
        return button;
    }
    
    static createNumber(number) {
        return this.create('number', number.toString());
    }
    
    static createOperator(operator) {
        return this.create('operator', operator);
    }
    
    static createSpecial(text, id) {
        return this.create('special', text, id);
    }
}

// Usage
const button7 = ButtonFactory.createNumber(7);
const plusButton = ButtonFactory.createOperator('+');
const clearButton = ButtonFactory.createSpecial('Clear', 'clear');
```

#### Component Theme System
```javascript
class ThemeManager {
    static themes = {
        default: {
            displayBg: '#a7af7c',
            buttonBg: 'linear-gradient(#555353, #363535)',
            textColor: '#999'
        },
        dark: {
            displayBg: '#2d2d2d',
            buttonBg: 'linear-gradient(#333, #111)',
            textColor: '#ccc'
        },
        neon: {
            displayBg: '#000',
            buttonBg: 'linear-gradient(#001122, #000)',
            textColor: '#00ffff'
        }
    };
    
    static applyTheme(calculatorElement, themeName) {
        const theme = this.themes[themeName];
        const display = calculatorElement.querySelector('#value');
        const buttons = calculatorElement.querySelectorAll('.button-component');
        
        display.style.background = theme.displayBg;
        buttons.forEach(button => {
            button.style.background = theme.buttonBg;
            button.style.color = theme.textColor;
        });
    }
}

// Usage
ThemeManager.applyTheme(calculatorElement, 'dark');
```

---

This component documentation provides a comprehensive guide to understanding, implementing, and customizing all UI components in the 3D Calculator project. Each component is designed to be modular, reusable, and easily customizable for different themes and layouts.