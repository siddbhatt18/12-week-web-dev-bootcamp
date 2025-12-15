# Week 2: JavaScript Essentials - Daily Structured Plan

## **Day 8 (Week 2, Day 1): JavaScript Fundamentals**
*Understanding the language basics*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Study: How JavaScript works in the browser
  - Script loading (async vs defer)
  - JavaScript engine basics
  - Console and debugging basics
- [ ] Learn: Variables and Data Types
  - let, const, var (and why var is problematic)
  - Primitive types: string, number, boolean, null, undefined, symbol
  - Type coercion and checking (typeof)
- [ ] Understand: Operators
  - Arithmetic (+, -, *, /, %, **)
  - Assignment (=, +=, -=, etc.)
  - Comparison (==, ===, !=, !==, >, <)
  - Logical (&&, ||, !)

**Resources:**
- MDN: [JavaScript First Steps](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps)
- JavaScript.info: [Fundamentals](https://javascript.info/first-steps)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: JavaScript Playground**
```javascript
// Create an interactive console program
1. variables-practice.js
   - Create variables of each type
   - Practice type conversion
   - Demonstrate type coercion

2. calculator.js
   - Basic arithmetic operations
   - Store results in variables
   - Chain operations

3. comparison-lab.js
   - Compare different data types
   - Truthy/falsy values
   - Logical operator combinations

4. user-info.js
   - Prompt for user input
   - Store in appropriate variables
   - Display formatted output
```

**Exercises:**
```javascript
// Complete these challenges:
// 1. Temperature Converter
let celsius = 25;
let fahrenheit = // your code here
let kelvin = // your code here

// 2. Age Calculator
let birthYear = 1995;
let currentYear = 2024;
let age = // your code here
let monthsLived = // your code here
let daysLived = // your code here (approximate)

// 3. Shopping Cart
let itemPrice = 29.99;
let quantity = 3;
let taxRate = 0.08;
let subtotal = // your code here
let tax = // your code here
let total = // your code here

// 4. String Manipulation
let firstName = "John";
let lastName = "Doe";
let fullName = // combine them
let initials = // extract initials
let email = // create email from name
```

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Run all scripts in browser console
- [ ] Document type coercion gotchas you discovered
- [ ] Create a reference sheet for operators
- [ ] Commit: "Add JavaScript fundamentals practice"

**Checklist for Day 1:**
- [ ] Understand difference between let and const
- [ ] Can convert between data types
- [ ] Know == vs === difference
- [ ] Created 10+ working JavaScript snippets

---

## **Day 9 (Week 2, Day 2): Control Flow & Functions**
*Making decisions and organizing code*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Study: Conditional Statements
  - if, else if, else
  - Ternary operator
  - switch statements
- [ ] Learn: Loops
  - for loop
  - while and do-while
  - break and continue
- [ ] Master: Functions
  - Function declaration vs expression
  - Parameters and arguments
  - Return values
  - Scope (global vs local)

**Resources:**
- MDN: [Control Flow](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
- JavaScript.info: [Functions](https://javascript.info/function-basics)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Decision Making Programs**
```javascript
// Build these programs:

1. grade-calculator.js
// Function that takes score, returns letter grade
function calculateGrade(score) {
    // A: 90-100, B: 80-89, C: 70-79, D: 60-69, F: <60
    // Add + and - modifiers (93+ is A+, 87-89 is B+, etc.)
}

2. password-validator.js
// Check password strength
function validatePassword(password) {
    // Check length (min 8)
    // Check for uppercase
    // Check for lowercase
    // Check for numbers
    // Check for special characters
    // Return strength: "weak", "medium", "strong"
}

3. game-menu.js
// Simple text adventure game starter
function gameMenu() {
    // Display options
    // Get user choice
    // Execute different paths based on choice
    // Use switch statement
}

4. pattern-printer.js
// Use loops to create patterns
function printTriangle(height) {
    // Print:
    // *
    // **
    // ***
    // ****
}

function printPyramid(height) {
    // Print:
    //    *
    //   ***
    //  *****
    // *******
}
```

**Loop Challenges:**
```javascript
// 1. FizzBuzz (classic)
// Print 1-100, but:
// - "Fizz" for multiples of 3
// - "Buzz" for multiples of 5
// - "FizzBuzz" for multiples of both

// 2. Prime Number Checker
function isPrime(num) {
    // Return true if prime, false otherwise
}

// 3. Fibonacci Sequence
function fibonacci(n) {
    // Return first n Fibonacci numbers
}

// 4. Multiplication Table
function multiplicationTable(num, limit) {
    // Print table up to limit
}
```

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Refactor code to use different loop types
- [ ] Test edge cases (negative numbers, zero, large numbers)
- [ ] Create function library for reuse
- [ ] Commit: "Add control flow and function exercises"

**Checklist for Day 2:**
- [ ] Can write all three loop types
- [ ] Understand function scope
- [ ] Used both if/else and switch statements
- [ ] Created 10+ custom functions

---

## **Day 10 (Week 2, Day 3): Arrays & Array Methods**
*Working with collections of data*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Study: Array Basics
  - Creating arrays (literal and constructor)
  - Accessing elements (indexing)
  - Array.length and properties
  - Multi-dimensional arrays
- [ ] Learn: Array Methods
  - Mutating: push, pop, shift, unshift, splice, sort, reverse
  - Non-mutating: concat, slice, indexOf, includes
  - Iteration: forEach, map, filter, reduce, find
- [ ] Understand: Arrays vs Objects (when to use which)

**Resources:**
- MDN: [Array Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- JavaScript.info: [Arrays](https://javascript.info/array)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Data Processing Suite**
```javascript
// 1. student-gradebook.js
const students = [
    { name: "Alice", grades: [90, 85, 92] },
    { name: "Bob", grades: [75, 80, 85] },
    { name: "Charlie", grades: [95, 95, 95] }
];

// Functions to build:
function calculateAverage(grades) { }
function getClassAverage(students) { }
function getTopStudent(students) { }
function getFailingStudents(students) { } // avg < 70

// 2. inventory-manager.js
let inventory = [
    { id: 1, name: "Laptop", price: 999, quantity: 5 },
    { id: 2, name: "Mouse", price: 25, quantity: 50 },
    { id: 3, name: "Keyboard", price: 75, quantity: 30 }
];

// Functions to build:
function addProduct(product) { }
function removeProduct(id) { }
function updateQuantity(id, newQuantity) { }
function getTotalValue() { }
function getLowStock(threshold) { }

// 3. todo-list-engine.js
let todos = [];

function addTodo(task, priority) { }
function completeTodo(id) { }
function deleteTodo(id) { }
function getPriorityTodos() { }
function sortByPriority() { }
function searchTodos(keyword) { }
```

**Array Method Challenges:**
```javascript
// 1. Data Transformation
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
// Create: squares, evens, sum, product

// 2. String Manipulation
const words = ["hello", "world", "javascript", "is", "awesome"];
// Create: capitalizedWords, longWords (>5 chars), acronym

// 3. Complex Filtering
const people = [
    { name: "Alice", age: 25, city: "NYC" },
    { name: "Bob", age: 30, city: "LA" },
    { name: "Charlie", age: 35, city: "NYC" }
];
// Get: NYC residents, people over 30, names only

// 4. Array Statistics
function arrayStats(numbers) {
    return {
        min: // find minimum
        max: // find maximum
        sum: // calculate sum
        average: // calculate average
        median: // find median
    }
}
```

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Chain multiple array methods
- [ ] Compare performance of different approaches
- [ ] Create utility functions library
- [ ] Commit: "Add array manipulation exercises"

**Checklist for Day 3:**
- [ ] Can use all basic array methods
- [ ] Understand map vs forEach
- [ ] Comfortable with filter and reduce
- [ ] Solved 10+ array problems

---

## **Day 11 (Week 2, Day 4): Objects & JSON**
*Complex data structures and APIs*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Study: Object Basics
  - Object literals and properties
  - Dot notation vs bracket notation
  - Methods (functions in objects)
  - this keyword basics
- [ ] Learn: Object Operations
  - Adding/updating/deleting properties
  - Object.keys(), Object.values(), Object.entries()
  - Spread operator with objects
  - Object destructuring
- [ ] Understand: JSON
  - JSON.stringify() and JSON.parse()
  - Working with API responses
  - LocalStorage with JSON

**Resources:**
- MDN: [Working with Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
- JavaScript.info: [Objects](https://javascript.info/object)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Object-Oriented Systems**
```javascript
// 1. user-profile-system.js
const userProfile = {
    username: "",
    email: "",
    profile: {
        firstName: "",
        lastName: "",
        age: 0,
        address: {
            street: "",
            city: "",
            country: ""
        }
    },
    settings: {
        theme: "light",
        notifications: true,
        privacy: "public"
    },
    
    // Methods
    updateProfile(updates) { },
    changePassword(oldPass, newPass) { },
    toggleTheme() { },
    getFullName() { },
    getAge() { }
};

// 2. shopping-cart-object.js
const shoppingCart = {
    items: [],
    
    addItem(product, quantity) { },
    removeItem(productId) { },
    updateQuantity(productId, newQuantity) { },
    getTotal() { },
    applyDiscount(percentage) { },
    checkout() { },
    saveCart() { }, // to localStorage
    loadCart() { }  // from localStorage
};

// 3. library-system.js
const library = {
    books: [
        { id: 1, title: "1984", author: "Orwell", available: true },
        { id: 2, title: "Brave New World", author: "Huxley", available: true }
    ],
    members: [],
    
    addBook(book) { },
    removeBook(id) { },
    findBooksByAuthor(author) { },
    borrowBook(bookId, memberId) { },
    returnBook(bookId) { },
    getAvailableBooks() { },
    getMemberHistory(memberId) { }
};
```

**Object Manipulation Challenges:**
```javascript
// 1. Deep Clone Function
function deepClone(obj) {
    // Create a deep copy of nested object
}

// 2. Object Comparison
function compareObjects(obj1, obj2) {
    // Return true if objects are equal
}

// 3. Merge Objects
function mergeObjects(...objects) {
    // Merge multiple objects, later values override
}

// 4. Object to Query String
function objectToQueryString(obj) {
    // Convert {name: "John", age: 30} to "?name=John&age=30"
}

// 5. Nested Property Access
function getNestedProperty(obj, path) {
    // getNestedProperty(user, "profile.address.city")
}
```

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Test all object methods
- [ ] Practice JSON conversions
- [ ] Save/load data from localStorage
- [ ] Commit: "Add object and JSON exercises"

**Checklist for Day 4:**
- [ ] Understand reference vs value types
- [ ] Can manipulate nested objects
- [ ] Comfortable with this keyword
- [ ] Created 5+ complex objects with methods

---

## **Day 12 (Week 2, Day 5): DOM Manipulation**
*Making web pages interactive*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Study: The Document Object Model
  - What is the DOM?
  - DOM tree structure
  - Node types and relationships
- [ ] Learn: Selecting Elements
  - getElementById, getElementsByClassName, getElementsByTagName
  - querySelector and querySelectorAll
  - Parent, child, and sibling traversal
- [ ] Understand: Modifying the DOM
  - innerHTML vs textContent
  - setAttribute and getAttribute
  - classList methods
  - Creating and removing elements

**Resources:**
- MDN: [Introduction to the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)
- JavaScript.info: [Document](https://javascript.info/document)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Interactive Web Components**
```html
<!-- Create these interactive elements -->

<!-- 1. dynamic-navbar.html -->
<nav id="navbar">
    <!-- JavaScript will:
    - Add/remove 'scrolled' class on scroll
    - Highlight active section
    - Toggle mobile menu
    -->
</nav>

<!-- 2. tab-switcher.html -->
<div class="tab-container">
    <div class="tab-buttons">
        <button data-tab="1">Tab 1</button>
        <button data-tab="2">Tab 2</button>
        <button data-tab="3">Tab 3</button>
    </div>
    <div class="tab-content">
        <!-- Show/hide content based on active tab -->
    </div>
</div>

<!-- 3. accordion.html -->
<div class="accordion">
    <div class="accordion-item">
        <h3>Question 1</h3>
        <div class="content">Answer...</div>
    </div>
    <!-- Expand/collapse on click -->
</div>

<!-- 4. modal-popup.html -->
<button id="open-modal">Open Modal</button>
<div class="modal" id="modal">
    <!-- Create, show, hide, close modal -->
</div>
```

**DOM Manipulation Exercises:**
```javascript
// 1. Color Theme Switcher
function createThemeSwitcher() {
    // Add buttons to switch between themes
    // Save preference to localStorage
    // Apply theme on page load
}

// 2. Dynamic List Manager
function createListManager() {
    // Add items with input field
    // Delete items on click
    // Edit items inline
    // Mark items as complete
    // Filter: all/active/completed
}

// 3. Image Gallery
function createGallery(images) {
    // Display thumbnails
    // Click to show full size
    // Previous/next navigation
    // Keyboard support (arrows)
}

// 4. Form Validator
function createFormValidator() {
    // Real-time validation
    // Show error messages
    // Disable submit until valid
    // Custom validation rules
}

// 5. Live Search
function createLiveSearch(data) {
    // Search as user types
    // Highlight matching text
    // Show/hide results
    // Handle no results
}
```

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Test in different browsers
- [ ] Check for memory leaks (removed event listeners)
- [ ] Optimize DOM operations (batch updates)
- [ ] Commit: "Add DOM manipulation features"

**Checklist for Day 5:**
- [ ] Can select any element multiple ways
- [ ] Understand DOM traversal
- [ ] Created/removed elements dynamically
- [ ] Modified styles and classes via JavaScript

---

## **Day 13 (Week 2, Day 6): Events & Event Handling**
*Responding to user interactions*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Study: Event Basics
  - Event types (click, submit, keydown, etc.)
  - Event listeners vs inline handlers
  - Event object and properties
  - removeEventListener
- [ ] Learn: Event Flow
  - Event bubbling
  - Event capturing
  - stopPropagation and preventDefault
  - Event delegation
- [ ] Understand: Common Events
  - Mouse events
  - Keyboard events
  - Form events
  - Window events (scroll, resize, load)

**Resources:**
- MDN: [Introduction to Events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)
- JavaScript.info: [Events](https://javascript.info/events)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Event-Driven Applications**
```javascript
// 1. interactive-form.js
const form = document.querySelector('#signup-form');

// Add these features:
// - Real-time validation on blur
// - Password strength meter
// - Confirm password match
// - Show/hide password toggle
// - Progress indicator
// - Submit with AJAX (prevent page reload)

// 2. drag-drop-interface.js
// Create draggable elements
// - Make items draggable
// - Define drop zones
// - Visual feedback during drag
// - Reorder items
// - Save new order

// 3. keyboard-shortcuts.js
// Implement keyboard controls:
// - Ctrl+S: Save
// - Ctrl+Z: Undo
// - Escape: Close modal
// - Arrow keys: Navigate
// - Enter: Submit
// - Custom combos

// 4. infinite-scroll.js
// Load content as user scrolls:
// - Detect when near bottom
// - Fetch new content
// - Append to page
// - Show loading indicator
// - Handle end of content
```

**Event Handling Challenges:**
```javascript
// 1. Custom Context Menu
function createContextMenu() {
    // Right-click to show custom menu
    // Position at cursor
    // Handle menu item clicks
    // Close when clicking outside
}

// 2. Drawing Canvas
function createDrawingApp() {
    // Mouse down: start drawing
    // Mouse move: draw line
    // Mouse up: stop drawing
    // Touch support
    // Color and size options
}

// 3. Keyboard Game
function createSnakeGame() {
    // Arrow keys control movement
    // Spacebar to pause
    // Collision detection
    // Score tracking
}

// 4. Gesture Recognition
function addSwipeSupport() {
    // Detect swipe direction
    // Swipe to delete
    // Pull to refresh
    // Pinch to zoom
}

// 5. Double-Click Editor
function makeEditable() {
    // Double-click text to edit
    // Enter to save
    // Escape to cancel
    // Click outside to save
}
```

**Event Delegation Project:**
```javascript
// Todo List with Event Delegation
const todoList = {
    init() {
        // Single event listener on container
        // Handle all clicks (add, delete, complete)
        // Efficient for dynamic items
    },
    
    handleClick(e) {
        // Identify what was clicked
        // Perform appropriate action
    }
};
```

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Test all event handlers
- [ ] Check for event listener cleanup
- [ ] Verify mobile/touch support
- [ ] Commit: "Add event handling systems"

**Checklist for Day 6:**
- [ ] Understand event bubbling/capturing
- [ ] Can use event delegation
- [ ] Handled 10+ different event types
- [ ] Created complex interactive features

---

## **Day 14 (Week 2, Day 7): Calculator Project & Integration**
*Build a fully-featured calculator*

### 🌅 Morning Session (9:00 - 10:30)
**Project Planning (90 min)**
- [ ] Design calculator UI mockup
- [ ] Plan features and operations
- [ ] Set up project structure:
  ```
  calculator/
  ├── index.html
  ├── css/
  │   └── styles.css
  ├── js/
  │   ├── calculator.js
  │   ├── history.js
  │   └── themes.js
  └── README.md
  ```
- [ ] Create feature checklist

**Calculator Requirements:**
```javascript
// Core Features:
1. Basic Operations (+, -, ×, ÷)
2. Decimal numbers
3. Clear (C) and Clear Entry (CE)
4. Backspace/Delete
5. Equals and chaining operations
6. Keyboard support

// Advanced Features:
1. History log (stored in localStorage)
2. Memory functions (M+, M-, MR, MC)
3. Scientific mode (sin, cos, tan, log, sqrt, power)
4. Percentage calculations
5. Positive/negative toggle
6. Theme switcher (light/dark/custom)
```

### ☀️ Extended Build Session (10:30 - 4:30)
**Build Complete Calculator**

**HTML Structure:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Calculator</title>
    <link rel="stylesheet" href="css/styles.css">
</head>
<body>
    <div class="calculator-container">
        <!-- Theme Toggle -->
        <div class="theme-switcher">
            <button data-theme="light">☀️</button>
            <button data-theme="dark">🌙</button>
            <button data-theme="neon">💫</button>
        </div>
        
        <!-- Calculator -->
        <div class="calculator">
            <!-- Display -->
            <div class="display">
                <div class="history-display"></div>
                <div class="current-display">0</div>
            </div>
            
            <!-- Mode Toggle -->
            <div class="mode-toggle">
                <button id="basic-mode">Basic</button>
                <button id="scientific-mode">Scientific</button>
            </div>
            
            <!-- Memory Buttons -->
            <div class="memory-buttons">
                <button class="mem-btn" data-action="MC">MC</button>
                <button class="mem-btn" data-action="MR">MR</button>
                <button class="mem-btn" data-action="M+">M+</button>
                <button class="mem-btn" data-action="M-">M-</button>
            </div>
            
            <!-- Main Buttons -->
            <div class="buttons-grid">
                <!-- Generate with JavaScript -->
            </div>
        </div>
        
        <!-- History Panel -->
        <div class="history-panel">
            <h3>History</h3>
            <div class="history-list"></div>
            <button class="clear-history">Clear History</button>
        </div>
    </div>
    
    <script src="js/calculator.js"></script>
    <script src="js/history.js"></script>
    <script src="js/themes.js"></script>
</body>
</html>
```

**Core JavaScript Implementation:**
```javascript
// calculator.js
class Calculator {
    constructor() {
        this.currentValue = '0';
        this.previousValue = '';
        this.operation = null;
        this.shouldResetScreen = false;
        this.memory = 0;
        this.init();
    }
    
    init() {
        this.setupDisplay();
        this.setupButtons();
        this.setupKeyboard();
        this.loadFromStorage();
    }
    
    // Number input
    appendNumber(number) {
        if (this.currentValue === '0' || this.shouldResetScreen) {
            this.currentValue = '';
            this.shouldResetScreen = false;
        }
        
        // Handle decimal
        if (number === '.' && this.currentValue.includes('.')) return;
        
        this.currentValue += number;
        this.updateDisplay();
    }
    
    // Operations
    setOperation(op) {
        if (this.operation !== null) {
            this.calculate();
        }
        
        this.previousValue = this.currentValue;
        this.operation = op;
        this.shouldResetScreen = true;
        this.updateHistory();
    }
    
    // Calculate result
    calculate() {
        let result;
        const prev = parseFloat(this.previousValue);
        const current = parseFloat(this.currentValue);
        
        if (isNaN(prev) || isNaN(current)) return;
        
        switch(this.operation) {
            case '+': result = prev + current; break;
            case '-': result = prev - current; break;
            case '×': result = prev * current; break;
            case '÷': result = prev / current; break;
            case '^': result = Math.pow(prev, current); break;
            default: return;
        }
        
        this.currentValue = result.toString();
        this.operation = null;
        this.previousValue = '';
        this.addToHistory();
    }
    
    // Scientific functions
    scientificOperation(func) {
        const current = parseFloat(this.currentValue);
        let result;
        
        switch(func) {
            case 'sin': result = Math.sin(current); break;
            case 'cos': result = Math.cos(current); break;
            case 'tan': result = Math.tan(current); break;
            case 'log': result = Math.log10(current); break;
            case 'ln': result = Math.log(current); break;
            case 'sqrt': result = Math.sqrt(current); break;
            case 'x²': result = Math.pow(current, 2); break;
            case 'x³': result = Math.pow(current, 3); break;
            case '1/x': result = 1 / current; break;
            case '!': result = this.factorial(current); break;
        }
        
        this.currentValue = result.toString();
        this.updateDisplay();
    }
    
    // Memory operations
    memoryOperation(op) {
        const current = parseFloat(this.currentValue);
        
        switch(op) {
            case 'MC': this.memory = 0; break;
            case 'MR': this.currentValue = this.memory.toString(); break;
            case 'M+': this.memory += current; break;
            case 'M-': this.memory -= current; break;
        }
        
        this.updateMemoryIndicator();
        this.saveToStorage();
    }
    
    // Clear functions
    clear() {
        this.currentValue = '0';
        this.previousValue = '';
        this.operation = null;
        this.updateDisplay();
    }
    
    clearEntry() {
        this.currentValue = '0';
        this.updateDisplay();
    }
    
    backspace() {
        if (this.currentValue.length > 1) {
            this.currentValue = this.currentValue.slice(0, -1);
        } else {
            this.currentValue = '0';
        }
        this.updateDisplay();
    }
    
    // Keyboard support
    setupKeyboard() {
        document.addEventListener('keydown', (e) => {
            // Numbers
            if (e.key >= '0' && e.key <= '9') {
                this.appendNumber(e.key);
            }
            // Operations
            else if (e.key === '+' || e.key === '-') {
                this.setOperation(e.key);
            }
            else if (e.key === '*') {
                this.setOperation('×');
            }
            else if (e.key === '/') {
                e.preventDefault();
                this.setOperation('÷');
            }
            // Special keys
            else if (e.key === 'Enter' || e.key === '=') {
                this.calculate();
            }
            else if (e.key === 'Escape') {
                this.clear();
            }
            else if (e.key === 'Backspace') {
                this.backspace();
            }
            else if (e.key === '.') {
                this.appendNumber('.');
            }
        });
    }
}

// history.js
class HistoryManager {
    constructor(calculator) {
        this.calculator = calculator;
        this.history = [];
        this.maxItems = 50;
        this.load();
    }
    
    add(expression, result) {
        const entry = {
            expression,
            result,
            timestamp: new Date().toISOString()
        };
        
        this.history.unshift(entry);
        if (this.history.length > this.maxItems) {
            this.history.pop();
        }
        
        this.save();
        this.render();
    }
    
    clear() {
        this.history = [];
        this.save();
        this.render();
    }
    
    save() {
        localStorage.setItem('calculatorHistory', JSON.stringify(this.history));
    }
    
    load() {
        const saved = localStorage.getItem('calculatorHistory');
        if (saved) {
            this.history = JSON.parse(saved);
        }
    }
}

// themes.js
class ThemeManager {
    constructor() {
        this.themes = {
            light: {
                '--bg-primary': '#ffffff',
                '--bg-secondary': '#f0f0f0',
                '--text-primary': '#333333',
                '--btn-primary': '#4CAF50',
                '--btn-operator': '#ff9800'
            },
            dark: {
                '--bg-primary': '#1a1a1a',
                '--bg-secondary': '#2d2d2d',
                '--text-primary': '#ffffff',
                '--btn-primary': '#4CAF50',
                '--btn-operator': '#ff9800'
            },
            neon: {
                '--bg-primary': '#0a0a0a',
                '--bg-secondary': '#1a0a2a',
                '--text-primary': '#00ffff',
                '--btn-primary': '#ff00ff',
                '--btn-operator': '#ffff00'
            }
        };
        
        this.init();
    }
    
    init() {
        this.loadTheme();
        this.setupSwitcher();
    }
    
    setTheme(themeName) {
        const theme = this.themes[themeName];
        if (!theme) return;
        
        Object.entries(theme).forEach(([property, value]) => {
            document.documentElement.style.setProperty(property, value);
        });
        
        localStorage.setItem('calculatorTheme', themeName);
    }
}
```

**CSS Styling (Advanced):**
```css
/* Modern, responsive calculator design */
.calculator {
    background: var(--bg-primary);
    border-radius: 20px;
    padding: 20px;
    box-shadow: 0 10px 40px rgba(0,0,0,0.2);
    max-width: 400px;
    margin: 20px auto;
}

.display {
    background: var(--bg-secondary);
    padding: 20px;
    margin-bottom: 20px;
    border-radius: 10px;
    text-align: right;
    min-height: 80px;
}

.current-display {
    font-size: 2.5em;
    color: var(--text-primary);
    word-wrap: break-word;
    overflow-wrap: break-word;
}

.buttons-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}

button {
    padding: 20px;
    font-size: 1.2em;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    transition: all 0.3s ease;
}

button:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
}

button:active {
    transform: translateY(0);
}

/* Animations */
@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.05); }
    100% { transform: scale(1); }
}

.calculate-animation {
    animation: pulse 0.3s ease;
}
```

### 🌙 Evening: Testing & Deployment (4:30 - 6:00)
- [ ] Test all operations thoroughly
- [ ] Verify keyboard shortcuts work
- [ ] Test edge cases (division by zero, overflow)
- [ ] Check localStorage persistence
- [ ] Test on mobile devices
- [ ] Deploy to GitHub Pages
- [ ] Create comprehensive README

**Testing Checklist:**
```javascript
// Test cases to verify:
1. Basic arithmetic: 2 + 2 = 4
2. Decimal operations: 0.1 + 0.2 = 0.3 (handle floating point)
3. Chain operations: 5 + 3 × 2 = 16 (order of operations)
4. Division by zero: Show error
5. Very large numbers: Scientific notation
6. Negative numbers: -5 + 3 = -2
7. Percentage: 50 × 20% = 10
8. Memory operations persist
9. History saves correctly
10. Theme preference saves
```

---

## 📊 Week 2 Success Metrics

By the end of Week 2, you should be able to:

### Knowledge Check ✅
- [ ] Write JavaScript without syntax errors
- [ ] Explain scope and hoisting
- [ ] Understand event propagation
- [ ] Debug using browser DevTools
- [ ] Manipulate any aspect of a webpage

### Skills Acquired 💪
- [ ] Created 20+ JavaScript functions
- [ ] Used 15+ different array methods
- [ ] Handled 10+ event types
- [ ] Manipulated DOM in 10+ ways
- [ ] Built a complex interactive application

### Portfolio Pieces 🎨
1. JavaScript utilities library
2. Interactive DOM components collection
3. Fully-featured calculator (deployed)

### Code Statistics 📈
- [ ] Wrote 1000+ lines of JavaScript
- [ ] Created 50+ functions
- [ ] Solved 30+ programming challenges
- [ ] Fixed 20+ bugs independently

---

## 💡 Week 2 Tips for Success

### Daily Habits
1. **Console is your friend** - Test everything in console first
2. **Break problems down** - Solve in small pieces
3. **Read error messages** - They usually tell you exactly what's wrong
4. **Use debugger** - Step through code line by line
5. **Comment your code** - Explain the "why", not the "what"

### Common Pitfalls to Avoid
- **Don't forget semicolons** (even though they're optional)
- **Watch for type coercion** - Use === instead of ==
- **Careful with this keyword** - It changes based on context
- **Avoid global variables** - Use function scope
- **Remove event listeners** - Prevent memory leaks

### Debugging Techniques
```javascript
// 1. Console methods
console.log('Basic output');
console.table(arrayOrObject);
console.time('timer'); // ... console.timeEnd('timer');
console.group('Group name'); // ... console.groupEnd();

// 2. Debugger
debugger; // Pauses execution here

// 3. Try-catch for error handling
try {
    // Code that might fail
} catch (error) {
    console.error('Error:', error.message);
}
```

### Resources for Stuck Moments
- **MDN Web Docs** - The ultimate reference
- **JavaScript.info** - Modern tutorial
- **Stack Overflow** - Search before asking
- **CodePen** - Test ideas quickly
- **JSFiddle** - Share problematic code

---

## 🚀 Week 3 Preview

Next week you'll dive into:
- **ES6+ Features** - Modern JavaScript syntax
- **Asynchronous JavaScript** - Promises, async/await
- **API Integration** - Fetch data from external sources
- **Build Tools** - NPM, bundlers, and modern workflow

Your JavaScript foundation is now solid. The calculator project proves you can build real, functional applications. Keep practicing, and remember: the best way to learn JavaScript is to write JavaScript every day! 💪
