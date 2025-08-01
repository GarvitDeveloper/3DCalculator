# 3D Calculator

A sleek, interactive 3D calculator built with HTML, CSS, and JavaScript featuring a modern glass-morphism design with realistic button animations and shadows.

## 🚀 Features

- **3D Visual Design**: Realistic button shadows and depth effects
- **Responsive Layout**: Grid-based button layout that adapts to different screen sizes
- **Interactive Animations**: Button press animations with visual feedback
- **Full Calculator Functionality**: Supports all basic arithmetic operations
- **Glass-morphism UI**: Modern translucent design elements
- **Keyboard-friendly**: Click-based input system

## 📁 Project Structure

```
3DCalculator/
├── index.html          # Main HTML structure and JavaScript logic
├── style.css          # CSS styling and 3D effects
└── README.md          # Project documentation
```

## 🛠️ Installation & Setup

1. **Clone or download** the project files
2. **Open `index.html`** in any modern web browser
3. **No additional dependencies** required - runs entirely in the browser

```bash
# Simple setup
git clone <repository-url>
cd 3DCalculator
open index.html  # macOS
# or
start index.html  # Windows
# or
xdg-open index.html  # Linux
```

## 🎯 Usage

### Basic Operations

1. **Numbers**: Click number buttons (0-9) to input values
2. **Operations**: Use +, -, *, / for arithmetic operations
3. **Decimal**: Click "." for decimal numbers
4. **Double Zero**: Click "00" for quick double zero input
5. **Calculate**: Click "=" to evaluate the expression
6. **Clear**: Click "Clear" to reset the display

### Example Calculations

```
Input: 15 + 25 * 2
Result: 65

Input: 100 / 4 - 10
Result: 15

Input: 12.5 + 7.5
Result: 20
```

## 🏗️ Architecture

### HTML Structure

The calculator uses a semantic HTML structure:

```html
<div class="calculator">
    <div class="buttons">
        <h2 id="value"></h2>     <!-- Display -->
        <span>Button</span>       <!-- Calculator buttons -->
    </div>
</div>
```

### CSS Architecture

The styling follows a component-based approach:
- **Base styles**: Reset and typography
- **Layout**: Flexbox and CSS Grid
- **Components**: Calculator container and buttons
- **Effects**: 3D shadows and animations

### JavaScript Logic

Event-driven architecture with:
- **DOM selection**: Query selectors for elements
- **Event handling**: Click listeners for all buttons
- **State management**: Display value updates
- **Calculation**: JavaScript `eval()` for expression evaluation

## 📚 API Documentation

### JavaScript Functions and Variables

#### Core Variables

```javascript
let buttons = document.querySelector('.buttons');
```
- **Purpose**: Selects the main button container
- **Type**: HTMLElement
- **Usage**: Parent container for all calculator buttons

```javascript
let btn = buttons.querySelectorAll('span');
```
- **Purpose**: Selects all button elements
- **Type**: NodeList
- **Usage**: Array-like collection of all calculator buttons

```javascript
let value = document.getElementById('value');
```
- **Purpose**: Selects the display element
- **Type**: HTMLElement
- **Usage**: Shows current input and calculation results

#### Event Handler Function

```javascript
btn[i].addEventListener('click', function(){
    if (this.innerHTML == "="){
        value.innerHTML = eval(value.innerHTML);
    } else {
        if(this.innerHTML == 'Clear') {
            value.innerHTML = '';
        } else {
            value.innerHTML += this.innerHTML;
        }
    }
})
```

**Function**: Anonymous click handler
- **Parameters**: `this` (clicked button element)
- **Behavior**:
  - If "=" button: Evaluates the expression using `eval()`
  - If "Clear" button: Resets the display to empty
  - Otherwise: Appends button value to display

**Usage Example**:
```javascript
// The function automatically handles:
// - Number input: "5" → display shows "5"
// - Operation: "+" → display shows "5+"
// - Calculation: "=" → display shows result
```

## 🎨 CSS Component Documentation

### Layout Components

#### `.calculator`
```css
.calculator {
    position: relative;
    width: 300px;
}
```
- **Purpose**: Main calculator container
- **Properties**: Fixed width responsive container
- **Usage**: Wraps the entire calculator interface

#### `.calculator .buttons`
```css
.calculator .buttons {
    position: relative;
    display: grid;
}
```
- **Purpose**: Button grid container
- **Layout**: CSS Grid for button arrangement
- **Usage**: Contains all calculator buttons and display

### Visual Components

#### `#value` (Display)
```css
.calculator .buttons #value {
    grid-column: span 4;
    height: 100px;
    background: #a7af7c;
    /* ... additional styling */
}
```
- **Purpose**: Calculator display screen
- **Features**:
  - Spans 4 grid columns
  - Right-aligned text
  - 3D inset shadow effect
  - Overflow hidden for long numbers

#### `.calculator .buttons span` (Buttons)
```css
.calculator .buttons span {
    padding: 10px;
    margin: 6px;
    background: linear-gradient(#555353, #363535);
    /* ... additional styling */
}
```
- **Purpose**: Individual calculator buttons
- **Features**:
  - 3D raised appearance
  - Gradient background
  - Hover and active states
  - Box shadow effects

### Special Button Classes

#### `#clear` (Clear Button)
```css
.calculator .buttons span#clear {
    grid-column: span 2;
    background: #f44336;
    color: #fff;
}
```
- **Purpose**: Reset calculator display
- **Features**: Red background, spans 2 columns

#### `#plus` (Plus Button)
```css
.calculator .buttons span#plus {
    grid-row: span 2;
    background: #31a935;
    color: #fff;
}
```
- **Purpose**: Addition operation
- **Features**: Green background, spans 2 rows

#### `#equal` (Equals Button)
```css
.calculator .buttons span#equal {
    background: #2196f3;
    color: #fff;
}
```
- **Purpose**: Calculate result
- **Features**: Blue background, standard size

### Animation Classes

#### `:active` State
```css
.calculator .buttons span:active {
    box-shadow: inset 0 2px 2px rgba(0,0,0,0.35);
    color: #fff;
    text-shadow: 0 0 5px #219cf3;
}
```
- **Purpose**: Button press animation
- **Effect**: Inset shadow simulating button press
- **Visual**: Blue glow text effect

## 🔧 Customization Guide

### Changing Colors

1. **Display Background**: Modify `.calculator .buttons #value` background
2. **Button Colors**: Update `.calculator .buttons span` background gradients
3. **Special Buttons**: Change individual button ID selectors

### Modifying Layout

1. **Calculator Size**: Adjust `.calculator` width
2. **Button Grid**: Modify CSS Grid properties in `.buttons`
3. **Button Spacing**: Change margin/padding in button styles

### Adding New Features

1. **Memory Functions**: Add new button elements and event handlers
2. **Scientific Operations**: Extend the button grid and calculation logic
3. **History**: Add display area and storage functionality

## 🧪 Testing

### Manual Testing Checklist

- [ ] All number buttons (0-9) input correctly
- [ ] Basic operations (+, -, *, /) work
- [ ] Decimal point functions properly
- [ ] Clear button resets display
- [ ] Equals button calculates results
- [ ] Visual feedback on button press
- [ ] Responsive design on different screen sizes

### Edge Cases

- **Division by zero**: Results in `Infinity`
- **Invalid expressions**: May cause JavaScript errors
- **Very long numbers**: Display overflow is hidden
- **Consecutive operations**: Each operation appends to display

## 🎭 Browser Compatibility

- **Chrome**: ✅ Full support
- **Firefox**: ✅ Full support  
- **Safari**: ✅ Full support
- **Edge**: ✅ Full support
- **IE11**: ⚠️ Limited CSS Grid support

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📧 Support

For support, questions, or feature requests, please open an issue in the repository.

---

**Made with ❤️ using HTML, CSS, and JavaScript**