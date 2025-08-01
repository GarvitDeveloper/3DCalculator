# Usage Guide - 3D Calculator

This guide provides practical examples, tutorials, and step-by-step instructions for using, customizing, and extending the 3D Calculator project.

## Table of Contents

- [Quick Start](#quick-start)
- [Basic Usage](#basic-usage)
- [Customization Examples](#customization-examples)
- [Extension Tutorials](#extension-tutorials)
- [Integration Guide](#integration-guide)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)

---

## Quick Start

### 1. Setup and Installation

#### Option A: Direct Download
```bash
# Download the project files
curl -L https://github.com/your-repo/3dcalculator/archive/main.zip -o calculator.zip
unzip calculator.zip
cd 3dcalculator-main
```

#### Option B: Clone Repository
```bash
git clone https://github.com/your-repo/3dcalculator.git
cd 3dcalculator
```

### 2. Running the Calculator

#### Method 1: Direct File Opening
```bash
# Open in default browser
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

#### Method 2: Local Server (Recommended)
```bash
# Using Python 3
python -m http.server 8000

# Using Node.js
npx serve .

# Using PHP
php -S localhost:8000
```

Then visit `http://localhost:8000` in your browser.

### 3. Basic File Structure
```
3DCalculator/
├── index.html          # Main calculator interface
├── style.css          # Styling and 3D effects
├── README.md          # Project documentation
├── API-REFERENCE.md   # Technical API documentation
├── COMPONENTS.md      # Component documentation
└── USAGE-GUIDE.md     # This file
```

---

## Basic Usage

### Calculator Operations

#### Performing Calculations

1. **Simple Arithmetic**
   ```
   Input: 15 + 25
   Action: Click "=" button
   Result: 40
   ```

2. **Complex Expressions**
   ```
   Input: 100 / 4 * 3 - 10
   Action: Click "=" button
   Result: 65
   ```

3. **Decimal Numbers**
   ```
   Input: 12.5 + 7.25
   Action: Click "=" button  
   Result: 19.75
   ```

#### Button Functions

| Button | Function | Example |
|--------|----------|---------|
| `0-9` | Number input | Click `5` → display shows "5" |
| `+` | Addition | `5 + 3 =` → `8` |
| `-` | Subtraction | `10 - 4 =` → `6` |
| `*` | Multiplication | `6 * 7 =` → `42` |
| `/` | Division | `20 / 4 =` → `5` |
| `.` | Decimal point | `3.14` |
| `00` | Double zero | Quick input for hundreds |
| `Clear` | Reset display | Clears all input |
| `=` | Calculate | Evaluates expression |

### Keyboard Shortcuts (If Implemented)

```javascript
// Add this to enable keyboard support
document.addEventListener('keydown', function(event) {
    const key = event.key;
    const keyMap = {
        '0': '0', '1': '1', '2': '2', '3': '3', '4': '4',
        '5': '5', '6': '6', '7': '7', '8': '8', '9': '9',
        '+': '+', '-': '-', '*': '*', '/': '/',
        '.': '.', 'Enter': '=', 'Escape': 'Clear'
    };
    
    if (keyMap[key]) {
        const button = Array.from(btn).find(b => 
            b.innerHTML === keyMap[key] || 
            (key === 'Enter' && b.innerHTML === '=') ||
            (key === 'Escape' && b.innerHTML === 'Clear')
        );
        if (button) button.click();
    }
});
```

---

## Customization Examples

### Theme Customization

#### 1. Dark Theme
```css
/* Add to style.css or create new theme file */
.calculator.dark-theme {
    background: #1a1a1a;
}

.calculator.dark-theme .buttons #value {
    background: #2d2d2d;
    color: #00ff00;
    box-shadow: inset 0 6px 1px 0 rgba(255,255,255,0.1),
                0 5px 5px rgba(0,0,0,0.8),
                0 15px 25px rgba(0,0,0,0.6);
}

.calculator.dark-theme .buttons span {
    background: linear-gradient(#333, #111);
    color: #ccc;
    border-color: #444;
}

.calculator.dark-theme .buttons span:active {
    color: #00ff00;
    text-shadow: 0 0 5px #00ff00;
}
```

**Implementation:**
```html
<div class="calculator dark-theme">
    <!-- calculator content -->
</div>
```

#### 2. Neon Theme
```css
.calculator.neon-theme {
    background: #000;
}

.calculator.neon-theme .buttons #value {
    background: #000;
    color: #00ffff;
    border: 2px solid #00ffff;
    text-shadow: 0 0 10px #00ffff;
    box-shadow: 0 0 20px rgba(0,255,255,0.5);
}

.calculator.neon-theme .buttons span {
    background: linear-gradient(#001122, #000011);
    color: #00ffff;
    border: 1px solid #00ffff;
    box-shadow: 0 0 10px rgba(0,255,255,0.3);
}

.calculator.neon-theme .buttons span:hover {
    box-shadow: 0 0 20px rgba(0,255,255,0.6);
    text-shadow: 0 0 10px #00ffff;
}
```

#### 3. Retro Calculator Theme
```css
.calculator.retro-theme {
    background: #8B4513;
    border: 5px solid #654321;
    border-radius: 15px;
}

.calculator.retro-theme .buttons #value {
    background: #000;
    color: #ff6600;
    font-family: 'Courier New', monospace;
    border: 2px inset #654321;
}

.calculator.retro-theme .buttons span {
    background: linear-gradient(#D2691E, #A0522D);
    color: #fff;
    border: 2px outset #CD853F;
    font-family: 'Arial', sans-serif;
    font-weight: bold;
}
```

### Size Variations

#### 1. Mini Calculator
```css
.calculator.mini {
    width: 200px;
    transform: scale(0.8);
}

.calculator.mini .buttons #value {
    height: 60px;
    line-height: 60px;
    font-size: 1.2em;
}

.calculator.mini .buttons span {
    padding: 6px;
    margin: 3px;
    font-size: 0.9em;
}
```

#### 2. Large Calculator
```css
.calculator.large {
    width: 400px;
    transform: scale(1.2);
}

.calculator.large .buttons #value {
    height: 120px;
    line-height: 120px;
    font-size: 2em;
}

.calculator.large .buttons span {
    padding: 15px;
    margin: 8px;
    font-size: 1.4em;
}
```

### Color Scheme Generator

```javascript
// Dynamic color scheme generator
class ColorSchemeGenerator {
    static generateScheme(baseColor) {
        const schemes = {
            blue: {
                display: '#4a90e2',
                buttons: 'linear-gradient(#5aa3f0, #4a90e2)',
                text: '#2c5aa0',
                special: {
                    clear: '#e74c3c',
                    plus: '#27ae60',
                    equal: '#3498db'
                }
            },
            purple: {
                display: '#9b59b6',
                buttons: 'linear-gradient(#af7ac5, #9b59b6)',
                text: '#6c3483',
                special: {
                    clear: '#e74c3c',
                    plus: '#27ae60',
                    equal: '#8e44ad'
                }
            },
            green: {
                display: '#27ae60',
                buttons: 'linear-gradient(#52c882, #27ae60)',
                text: '#1e8449',
                special: {
                    clear: '#e74c3c',
                    plus: '#2ecc71',
                    equal: '#16a085'
                }
            }
        };
        
        return schemes[baseColor] || schemes.blue;
    }
    
    static applyScheme(calculatorElement, schemeName) {
        const scheme = this.generateScheme(schemeName);
        const display = calculatorElement.querySelector('#value');
        const buttons = calculatorElement.querySelectorAll('span:not([id])');
        const clearBtn = calculatorElement.querySelector('#clear');
        const plusBtn = calculatorElement.querySelector('#plus');
        const equalBtn = calculatorElement.querySelector('#equal');
        
        // Apply display colors
        display.style.background = scheme.display;
        display.style.color = scheme.text;
        
        // Apply button colors
        buttons.forEach(btn => {
            btn.style.background = scheme.buttons;
            btn.style.color = scheme.text;
        });
        
        // Apply special button colors
        if (clearBtn) clearBtn.style.background = scheme.special.clear;
        if (plusBtn) plusBtn.style.background = scheme.special.plus;
        if (equalBtn) equalBtn.style.background = scheme.special.equal;
    }
}

// Usage
ColorSchemeGenerator.applyScheme(
    document.querySelector('.calculator'), 
    'purple'
);
```

---

## Extension Tutorials

### 1. Adding Memory Functions

#### HTML Structure
```html
<!-- Add these buttons to your calculator -->
<span id="memory-clear" class="memory-btn">MC</span>
<span id="memory-recall" class="memory-btn">MR</span>
<span id="memory-add" class="memory-btn">M+</span>
<span id="memory-subtract" class="memory-btn">M-</span>
```

#### CSS Styling
```css
.calculator .buttons .memory-btn {
    background: linear-gradient(#8e44ad, #6c3483);
    color: #fff;
    font-size: 0.9em;
    grid-column: span 1;
}

.calculator .buttons .memory-btn:active {
    background: linear-gradient(#6c3483, #8e44ad);
}
```

#### JavaScript Implementation
```javascript
// Memory functionality
class CalculatorMemory {
    constructor() {
        this.memory = 0;
        this.initMemoryButtons();
    }
    
    initMemoryButtons() {
        const memoryClear = document.getElementById('memory-clear');
        const memoryRecall = document.getElementById('memory-recall');
        const memoryAdd = document.getElementById('memory-add');
        const memorySubtract = document.getElementById('memory-subtract');
        
        if (memoryClear) {
            memoryClear.addEventListener('click', () => this.clear());
        }
        if (memoryRecall) {
            memoryRecall.addEventListener('click', () => this.recall());
        }
        if (memoryAdd) {
            memoryAdd.addEventListener('click', () => this.add());
        }
        if (memorySubtract) {
            memorySubtract.addEventListener('click', () => this.subtract());
        }
    }
    
    clear() {
        this.memory = 0;
        this.showMemoryStatus('Memory Cleared');
    }
    
    recall() {
        const display = document.getElementById('value');
        display.innerHTML = this.memory.toString();
        this.showMemoryStatus(`Recalled: ${this.memory}`);
    }
    
    add() {
        const display = document.getElementById('value');
        const currentValue = parseFloat(display.innerHTML) || 0;
        this.memory += currentValue;
        this.showMemoryStatus(`Memory: ${this.memory}`);
    }
    
    subtract() {
        const display = document.getElementById('value');
        const currentValue = parseFloat(display.innerHTML) || 0;
        this.memory -= currentValue;
        this.showMemoryStatus(`Memory: ${this.memory}`);
    }
    
    showMemoryStatus(message) {
        // Create temporary status display
        const status = document.createElement('div');
        status.className = 'memory-status';
        status.textContent = message;
        status.style.cssText = `
            position: absolute;
            top: -30px;
            left: 0;
            right: 0;
            background: rgba(0,0,0,0.8);
            color: white;
            text-align: center;
            padding: 5px;
            border-radius: 5px;
            font-size: 0.8em;
            z-index: 1000;
        `;
        
        document.querySelector('.calculator').appendChild(status);
        
        setTimeout(() => {
            if (status.parentNode) {
                status.parentNode.removeChild(status);
            }
        }, 2000);
    }
}

// Initialize memory functionality
const calculatorMemory = new CalculatorMemory();
```

### 2. Adding Scientific Functions

#### HTML Structure
```html
<!-- Scientific calculator buttons -->
<span class="scientific-btn" data-function="sin">sin</span>
<span class="scientific-btn" data-function="cos">cos</span>
<span class="scientific-btn" data-function="tan">tan</span>
<span class="scientific-btn" data-function="sqrt">√</span>
<span class="scientific-btn" data-function="pow">x²</span>
<span class="scientific-btn" data-function="log">log</span>
```

#### JavaScript Implementation
```javascript
// Scientific calculator functions
class ScientificCalculator {
    constructor() {
        this.initScientificButtons();
        this.angleMode = 'degrees'; // or 'radians'
    }
    
    initScientificButtons() {
        const scientificBtns = document.querySelectorAll('.scientific-btn');
        scientificBtns.forEach(btn => {
            btn.addEventListener('click', (e) => {
                const func = e.target.getAttribute('data-function');
                this.executeFunction(func);
            });
        });
    }
    
    executeFunction(functionName) {
        const display = document.getElementById('value');
        const currentValue = parseFloat(display.innerHTML) || 0;
        let result;
        
        try {
            switch (functionName) {
                case 'sin':
                    result = Math.sin(this.toRadians(currentValue));
                    break;
                case 'cos':
                    result = Math.cos(this.toRadians(currentValue));
                    break;
                case 'tan':
                    result = Math.tan(this.toRadians(currentValue));
                    break;
                case 'sqrt':
                    result = Math.sqrt(currentValue);
                    break;
                case 'pow':
                    result = Math.pow(currentValue, 2);
                    break;
                case 'log':
                    result = Math.log10(currentValue);
                    break;
                default:
                    result = currentValue;
            }
            
            // Round to prevent floating point precision issues
            result = Math.round(result * 1000000) / 1000000;
            display.innerHTML = result.toString();
            
        } catch (error) {
            display.innerHTML = 'Error';
        }
    }
    
    toRadians(degrees) {
        return this.angleMode === 'degrees' ? degrees * (Math.PI / 180) : degrees;
    }
    
    toggleAngleMode() {
        this.angleMode = this.angleMode === 'degrees' ? 'radians' : 'degrees';
        // Update UI to show current mode
        this.showAngleMode();
    }
    
    showAngleMode() {
        const modeDisplay = document.getElementById('angle-mode') || 
                           this.createAngleModeDisplay();
        modeDisplay.textContent = this.angleMode.toUpperCase();
    }
    
    createAngleModeDisplay() {
        const modeDisplay = document.createElement('div');
        modeDisplay.id = 'angle-mode';
        modeDisplay.style.cssText = `
            position: absolute;
            top: 5px;
            right: 5px;
            background: rgba(0,0,0,0.7);
            color: white;
            padding: 2px 6px;
            border-radius: 3px;
            font-size: 0.7em;
            cursor: pointer;
        `;
        modeDisplay.addEventListener('click', () => this.toggleAngleMode());
        document.querySelector('.calculator').appendChild(modeDisplay);
        return modeDisplay;
    }
}

// Initialize scientific calculator
const scientificCalc = new ScientificCalculator();
```

### 3. Adding History Feature

#### HTML Structure
```html
<!-- Add history panel -->
<div id="history-panel" class="history-panel">
    <div class="history-header">
        <span>History</span>
        <button id="clear-history">Clear</button>
    </div>
    <div class="history-list" id="history-list">
        <!-- History items will be added here -->
    </div>
</div>

<!-- Toggle button -->
<button id="history-toggle" class="history-toggle">History</button>
```

#### CSS Styling
```css
.history-panel {
    position: absolute;
    right: -250px;
    top: 0;
    width: 240px;
    height: 100%;
    background: rgba(0,0,0,0.9);
    color: white;
    transition: right 0.3s ease;
    border-radius: 0 10px 10px 0;
    overflow: hidden;
}

.history-panel.open {
    right: 0;
}

.history-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    background: rgba(255,255,255,0.1);
    border-bottom: 1px solid rgba(255,255,255,0.2);
}

.history-list {
    padding: 10px;
    max-height: calc(100% - 60px);
    overflow-y: auto;
}

.history-item {
    padding: 8px;
    margin: 5px 0;
    background: rgba(255,255,255,0.1);
    border-radius: 5px;
    cursor: pointer;
    transition: background 0.2s ease;
}

.history-item:hover {
    background: rgba(255,255,255,0.2);
}

.history-toggle {
    position: absolute;
    right: 10px;
    top: 10px;
    background: rgba(0,0,0,0.7);
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
}
```

#### JavaScript Implementation
```javascript
// Calculator history feature
class CalculatorHistory {
    constructor() {
        this.history = [];
        this.maxHistory = 50;
        this.initHistoryFeature();
    }
    
    initHistoryFeature() {
        this.createHistoryPanel();
        this.initHistoryToggle();
        this.initClearHistory();
        this.overrideCalculation();
    }
    
    createHistoryPanel() {
        if (!document.getElementById('history-panel')) {
            const historyHTML = `
                <div id="history-panel" class="history-panel">
                    <div class="history-header">
                        <span>History</span>
                        <button id="clear-history">Clear</button>
                    </div>
                    <div class="history-list" id="history-list"></div>
                </div>
                <button id="history-toggle" class="history-toggle">History</button>
            `;
            document.querySelector('.calculator').insertAdjacentHTML('afterend', historyHTML);
        }
    }
    
    initHistoryToggle() {
        const toggleBtn = document.getElementById('history-toggle');
        const panel = document.getElementById('history-panel');
        
        toggleBtn.addEventListener('click', () => {
            panel.classList.toggle('open');
        });
    }
    
    initClearHistory() {
        const clearBtn = document.getElementById('clear-history');
        clearBtn.addEventListener('click', () => {
            this.clearHistory();
        });
    }
    
    overrideCalculation() {
        // Override the original calculation function
        const originalEqualButton = document.getElementById('equal');
        originalEqualButton.addEventListener('click', () => {
            setTimeout(() => this.recordCalculation(), 10);
        });
    }
    
    recordCalculation() {
        const display = document.getElementById('value');
        const expression = display.innerHTML;
        
        // Don't record if it's an error or empty
        if (expression && expression !== 'Error' && !isNaN(parseFloat(expression))) {
            const historyItem = {
                expression: this.lastExpression || expression,
                result: expression,
                timestamp: new Date()
            };
            
            this.addToHistory(historyItem);
        }
    }
    
    addToHistory(item) {
        this.history.unshift(item);
        
        if (this.history.length > this.maxHistory) {
            this.history.pop();
        }
        
        this.updateHistoryDisplay();
    }
    
    updateHistoryDisplay() {
        const historyList = document.getElementById('history-list');
        historyList.innerHTML = '';
        
        this.history.forEach((item, index) => {
            const historyElement = document.createElement('div');
            historyElement.className = 'history-item';
            historyElement.innerHTML = `
                <div class="history-expression">${item.expression || 'Unknown'}</div>
                <div class="history-result">= ${item.result}</div>
                <div class="history-time">${this.formatTime(item.timestamp)}</div>
            `;
            
            historyElement.addEventListener('click', () => {
                document.getElementById('value').innerHTML = item.result;
            });
            
            historyList.appendChild(historyElement);
        });
    }
    
    clearHistory() {
        this.history = [];
        this.updateHistoryDisplay();
    }
    
    formatTime(date) {
        return date.toLocaleTimeString('en-US', {
            hour: '2-digit',
            minute: '2-digit'
        });
    }
}

// Initialize history
const calculatorHistory = new CalculatorHistory();
```

---

## Integration Guide

### 1. Embedding in Existing Website

#### Basic Embedding
```html
<!-- Include in your HTML page -->
<div class="calculator-container">
    <div class="calculator">
        <div class="buttons">
            <!-- Calculator content from index.html -->
        </div>
    </div>
</div>

<!-- Include styles -->
<link rel="stylesheet" href="path/to/calculator/style.css">

<!-- Include script -->
<script src="path/to/calculator/calculator.js"></script>
```

#### React Integration
```jsx
// CalculatorComponent.jsx
import React, { useEffect, useRef } from 'react';
import './calculator.css';

const CalculatorComponent = () => {
    const calculatorRef = useRef(null);
    
    useEffect(() => {
        // Initialize calculator when component mounts
        const initCalculator = () => {
            const buttons = calculatorRef.current.querySelector('.buttons');
            const btn = buttons.querySelectorAll('span');
            const value = calculatorRef.current.querySelector('#value');
            
            btn.forEach((button, i) => {
                button.addEventListener('click', function() {
                    if (this.innerHTML === "=") {
                        value.innerHTML = eval(value.innerHTML);
                    } else if (this.innerHTML === 'Clear') {
                        value.innerHTML = '';
                    } else {
                        value.innerHTML += this.innerHTML;
                    }
                });
            });
        };
        
        initCalculator();
    }, []);
    
    return (
        <div ref={calculatorRef} className="calculator">
            <div className="buttons">
                <h2 id="value"></h2>
                <span id="clear">Clear</span>
                <span>/</span>
                <span>*</span>
                {/* ... other buttons */}
            </div>
        </div>
    );
};

export default CalculatorComponent;
```

#### Vue.js Integration
```vue
<!-- Calculator.vue -->
<template>
    <div class="calculator" ref="calculator">
        <div class="buttons">
            <h2 id="value" ref="display"></h2>
            <span 
                v-for="button in buttons" 
                :key="button.id"
                :id="button.id"
                @click="handleButtonClick"
                v-text="button.text"
            ></span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Calculator',
    data() {
        return {
            buttons: [
                { id: 'clear', text: 'Clear' },
                { id: '', text: '/' },
                { id: '', text: '*' },
                // ... other buttons
            ]
        };
    },
    methods: {
        handleButtonClick(event) {
            const buttonText = event.target.innerHTML;
            const display = this.$refs.display;
            
            if (buttonText === "=") {
                display.innerHTML = eval(display.innerHTML);
            } else if (buttonText === 'Clear') {
                display.innerHTML = '';
            } else {
                display.innerHTML += buttonText;
            }
        }
    }
};
</script>

<style src="./calculator.css"></style>
```

### 2. API for External Control

```javascript
// Calculator API for external control
class CalculatorAPI {
    constructor(calculatorElement) {
        this.calculator = calculatorElement;
        this.display = calculatorElement.querySelector('#value');
        this.buttons = calculatorElement.querySelectorAll('span');
    }
    
    // Public API methods
    setValue(value) {
        this.display.innerHTML = value.toString();
        return this;
    }
    
    getValue() {
        return this.display.innerHTML;
    }
    
    appendValue(value) {
        this.display.innerHTML += value.toString();
        return this;
    }
    
    clear() {
        this.display.innerHTML = '';
        return this;
    }
    
    calculate() {
        try {
            const result = eval(this.display.innerHTML);
            this.display.innerHTML = result;
            return result;
        } catch (error) {
            this.display.innerHTML = 'Error';
            return null;
        }
    }
    
    simulateButtonClick(buttonText) {
        const button = Array.from(this.buttons).find(b => 
            b.innerHTML === buttonText
        );
        if (button) {
            button.click();
        }
        return this;
    }
    
    // Event handling
    onCalculation(callback) {
        const equalButton = this.calculator.querySelector('#equal');
        equalButton.addEventListener('click', () => {
            setTimeout(() => {
                callback(this.getValue());
            }, 10);
        });
        return this;
    }
    
    onClear(callback) {
        const clearButton = this.calculator.querySelector('#clear');
        clearButton.addEventListener('click', callback);
        return this;
    }
    
    onChange(callback) {
        const observer = new MutationObserver(() => {
            callback(this.getValue());
        });
        observer.observe(this.display, { 
            childList: true, 
            subtree: true, 
            characterData: true 
        });
        return this;
    }
}

// Usage example
const calculatorAPI = new CalculatorAPI(document.querySelector('.calculator'));

// Chain operations
calculatorAPI
    .setValue(10)
    .appendValue('+')
    .appendValue(5)
    .calculate();

// Listen for changes
calculatorAPI
    .onChange(value => console.log('Display changed:', value))
    .onCalculation(result => console.log('Calculation result:', result));
```

---

## Troubleshooting

### Common Issues and Solutions

#### 1. Calculator Not Loading
**Problem**: Calculator doesn't appear or function

**Solutions**:
```javascript
// Check if DOM is loaded
document.addEventListener('DOMContentLoaded', function() {
    // Initialize calculator here
});

// Verify element selectors
const buttons = document.querySelector('.buttons');
if (!buttons) {
    console.error('Calculator buttons container not found');
}

// Check for CSS loading
const computed = getComputedStyle(document.querySelector('.calculator'));
if (computed.width === 'auto') {
    console.error('Calculator CSS not loaded properly');
}
```

#### 2. Buttons Not Responding
**Problem**: Button clicks don't register

**Solutions**:
```javascript
// Check if event listeners are attached
btn.forEach((button, index) => {
    if (!button.onclick && !button.addEventListener) {
        console.error(`Button ${index} has no event listener`);
    }
});

// Verify button selection
console.log('Number of buttons found:', btn.length);
if (btn.length === 0) {
    console.error('No buttons found. Check selector: buttons.querySelectorAll("span")');
}

// Test individual button
const testButton = document.querySelector('span');
testButton.addEventListener('click', () => console.log('Button clicked!'));
```

#### 3. Display Issues
**Problem**: Display not updating or showing wrong values

**Solutions**:
```javascript
// Check display element
const display = document.getElementById('value');
if (!display) {
    console.error('Display element not found');
}

// Test display updates
display.innerHTML = 'Test';
console.log('Display content:', display.innerHTML);

// Check for CSS interference
const displayStyles = getComputedStyle(display);
console.log('Display visibility:', displayStyles.visibility);
console.log('Display display:', displayStyles.display);
```

#### 4. CSS Grid Layout Problems
**Problem**: Buttons not arranged properly

**Solutions**:
```css
/* Explicit grid definition */
.calculator .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: auto;
    gap: 6px;
}

/* Browser compatibility */
@supports not (display: grid) {
    .calculator .buttons {
        display: flex;
        flex-wrap: wrap;
    }
    
    .calculator .buttons span {
        flex: 1 0 22%;
    }
}
```

#### 5. Calculation Errors
**Problem**: Wrong calculation results

**Solutions**:
```javascript
// Safe evaluation function
function safeEval(expression) {
    // Remove any non-mathematical characters
    const sanitized = expression.replace(/[^0-9+\-*/.() ]/g, '');
    
    // Check for valid expression
    if (!/^[0-9+\-*/.() ]+$/.test(sanitized)) {
        throw new Error('Invalid expression');
    }
    
    try {
        return Function(`"use strict"; return (${sanitized})`)();
    } catch (error) {
        throw new Error('Calculation error');
    }
}

// Enhanced calculation with error handling
function calculate() {
    const display = document.getElementById('value');
    try {
        const result = safeEval(display.innerHTML);
        
        if (typeof result !== 'number' || !isFinite(result)) {
            throw new Error('Invalid result');
        }
        
        display.innerHTML = result.toString();
    } catch (error) {
        display.innerHTML = 'Error';
        console.error('Calculation error:', error.message);
    }
}
```

### Performance Optimization

#### 1. Event Delegation
```javascript
// Instead of individual listeners, use delegation
document.querySelector('.buttons').addEventListener('click', function(event) {
    if (event.target.tagName === 'SPAN') {
        handleButtonClick(event.target);
    }
});
```

#### 2. Debounced Updates
```javascript
// Debounce rapid calculations
function debounce(func, wait) {
    let timeout;
    return function executedFunction(...args) {
        const later = () => {
            clearTimeout(timeout);
            func(...args);
        };
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
    };
}

const debouncedCalculate = debounce(calculate, 300);
```

---

## Best Practices

### 1. Code Organization

#### Modular Structure
```javascript
// calculator.js - Main calculator logic
class Calculator {
    constructor(element) {
        this.element = element;
        this.display = element.querySelector('#value');
        this.buttons = element.querySelectorAll('span');
        this.init();
    }
    
    init() {
        this.attachEventListeners();
        this.reset();
    }
    
    // ... other methods
}

// extensions/memory.js - Memory functionality
class CalculatorMemory extends Calculator {
    // Memory-specific methods
}

// extensions/scientific.js - Scientific functions
class ScientificCalculator extends Calculator {
    // Scientific calculation methods
}
```

#### Configuration System
```javascript
// config.js - Calculator configuration
const CalculatorConfig = {
    theme: 'default',
    precision: 10,
    maxDisplayLength: 15,
    enableMemory: false,
    enableScientific: false,
    enableHistory: true,
    buttons: {
        layout: 'standard', // or 'scientific'
        customButtons: []
    },
    display: {
        format: 'decimal', // or 'scientific'
        thousandsSeparator: false
    }
};

// Apply configuration
class ConfigurableCalculator extends Calculator {
    constructor(element, config = {}) {
        super(element);
        this.config = { ...CalculatorConfig, ...config };
        this.applyConfig();
    }
    
    applyConfig() {
        if (this.config.enableMemory) {
            this.memory = new CalculatorMemory(this.element);
        }
        // ... other configuration applications
    }
}
```

### 2. Error Handling

#### Comprehensive Error System
```javascript
class CalculatorErrorHandler {
    static errors = {
        DIVISION_BY_ZERO: 'Cannot divide by zero',
        INVALID_EXPRESSION: 'Invalid expression',
        OVERFLOW: 'Number too large',
        UNDERFLOW: 'Number too small'
    };
    
    static handle(error, display) {
        let message = 'Error';
        
        if (error.message.includes('division by zero')) {
            message = this.errors.DIVISION_BY_ZERO;
        } else if (error.message.includes('invalid')) {
            message = this.errors.INVALID_EXPRESSION;
        }
        
        display.innerHTML = message;
        
        // Auto-clear error after 3 seconds
        setTimeout(() => {
            if (display.innerHTML === message) {
                display.innerHTML = '';
            }
        }, 3000);
    }
}
```

### 3. Accessibility

#### ARIA Labels and Keyboard Support
```html
<!-- Accessible calculator structure -->
<div class="calculator" role="application" aria-label="Calculator">
    <div class="buttons" role="grid">
        <h2 id="value" role="textbox" aria-live="polite" aria-label="Calculator display"></h2>
        <button role="gridcell" aria-label="Clear calculator">Clear</button>
        <button role="gridcell" aria-label="Divide">/</button>
        <!-- ... other buttons -->
    </div>
</div>
```

```javascript
// Keyboard accessibility
class AccessibleCalculator extends Calculator {
    constructor(element) {
        super(element);
        this.initAccessibility();
    }
    
    initAccessibility() {
        // Make calculator focusable
        this.element.setAttribute('tabindex', '0');
        
        // Add keyboard navigation
        this.element.addEventListener('keydown', (e) => {
            this.handleKeyboard(e);
        });
        
        // Screen reader announcements
        this.addAriaLiveRegion();
    }
    
    handleKeyboard(event) {
        const keyMap = {
            'Enter': '=',
            'Escape': 'Clear',
            'Backspace': 'backspace',
            'Delete': 'Clear'
        };
        
        const key = keyMap[event.key] || event.key;
        
        if (this.isValidInput(key)) {
            event.preventDefault();
            this.processInput(key);
        }
    }
    
    announceResult(result) {
        const announcer = document.getElementById('calculation-announcer');
        announcer.textContent = `Result: ${result}`;
    }
}
```

### 4. Testing Strategy

#### Unit Tests
```javascript
// tests/calculator.test.js
describe('Calculator', () => {
    let calculator;
    
    beforeEach(() => {
        document.body.innerHTML = `
            <div class="calculator">
                <div class="buttons">
                    <h2 id="value"></h2>
                    <!-- buttons -->
                </div>
            </div>
        `;
        calculator = new Calculator(document.querySelector('.calculator'));
    });
    
    test('should initialize properly', () => {
        expect(calculator.display).toBeTruthy();
        expect(calculator.buttons.length).toBeGreaterThan(0);
    });
    
    test('should perform basic addition', () => {
        calculator.setValue('5');
        calculator.appendValue('+');
        calculator.appendValue('3');
        const result = calculator.calculate();
        expect(result).toBe(8);
    });
    
    test('should handle division by zero', () => {
        calculator.setValue('5/0');
        calculator.calculate();
        expect(calculator.getValue()).toBe('Error');
    });
});
```

#### Integration Tests
```javascript
// tests/integration.test.js
describe('Calculator Integration', () => {
    test('should work with memory functions', () => {
        const calculator = new Calculator(element);
        const memory = new CalculatorMemory(element);
        
        calculator.setValue('10');
        memory.add();
        calculator.setValue('5');
        memory.recall();
        
        expect(calculator.getValue()).toBe('10');
    });
});
```

This comprehensive usage guide provides practical examples and tutorials for effectively using, customizing, and extending the 3D Calculator project. Follow these examples to implement features that best suit your needs.