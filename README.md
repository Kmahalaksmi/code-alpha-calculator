<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
        }

        .calculator {
            width: 300px;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
            background-color: #fff;
        }

        .display {
            width: 100%;
            height: 50px;
            margin-bottom: 20px;
            background-color: #222;
            color: #fff;
            text-align: right;
            padding: 10px;
            font-size: 24px;
            border-radius: 5px;
            box-sizing: border-box;
            overflow: hidden;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            grid-gap: 10px;
        }

        .button {
            height: 50px;
            font-size: 18px;
            background-color: #e0e0e0;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .button:hover {
            background-color: #ccc;
        }

        .button:active {
            background-color: #bbb;
        }

        .button.operation {
            background-color: #f9a825;
            color: #fff;
        }

        .button.operation:hover {
            background-color: #f57f17;
        }

        .button.operation:active {
            background-color: #ef6c00;
        }

        .button.equal {
            grid-column: span 2;
            background-color: #43a047;
            color: #fff;
        }

        .button.equal:hover {
            background-color: #388e3c;
        }

        .button.equal:active {
            background-color: #2e7d32;
        }

        .button.clear {
            grid-column: span 2;
            background-color: #e53935;
            color: #fff;
        }

        .button.clear:hover {
            background-color: #d32f2f;
        }

        .button.clear:active {
            background-color: #c62828;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div id="display" class="display">0</div>
        <div class="buttons">
            <button class="button clear" onclick="clearDisplay()">C</button>
            <button class="button operation" onclick="chooseOperation('/')">/</button>
            <button class="button operation" onclick="chooseOperation('*')">*</button>
            <button class="button operation" onclick="chooseOperation('-')">-</button>

            <button class="button" onclick="appendNumber('7')">7</button>
            <button class="button" onclick="appendNumber('8')">8</button>
            <button class="button" onclick="appendNumber('9')">9</button>
            <button class="button operation" onclick="chooseOperation('+')">+</button>

            <button class="button" onclick="appendNumber('4')">4</button>
            <button class="button" onclick="appendNumber('5')">5</button>
            <button class="button" onclick="appendNumber('6')">6</button>

            <button class="button" onclick="appendNumber('1')">1</button>
            <button class="button" onclick="appendNumber('2')">2</button>
            <button class="button" onclick="appendNumber('3')">3</button>
            <button class="button equal" onclick="calculate()">=</button>

            <button class="button" onclick="appendNumber('0')">0</button>
            <button class="button" onclick="appendDecimal()">.</button>
        </div>
    </div>

    <script>
        let currentOperand = '';
        let previousOperand = '';
        let operation = undefined;

        function appendNumber(number) {
            if (number === '0' && currentOperand === '0') return;
            if (currentOperand.includes('.') && number === '.') return;
            currentOperand = currentOperand.toString() + number.toString();
            updateDisplay();
        }

        function appendDecimal() {
            if (currentOperand.includes('.')) return;
            currentOperand = currentOperand.toString() + '.';
            updateDisplay();
        }

        function chooseOperation(op) {
            if (currentOperand === '') return;
            if (previousOperand !== '') {
                calculate();
            }
            operation = op;
            previousOperand = currentOperand;
            currentOperand = '';
            updateDisplay();
        }

        function calculate() {
            let result;
            const prev = parseFloat(previousOperand);
            const current = parseFloat(currentOperand);
            if (isNaN(prev) || isNaN(current)) return;
            switch (operation) {
                case '+':
                    result = prev + current;
                    break;
                case '-':
                    result = prev - current;
                    break;
                case '*':
                    result = prev * current;
                    break;
                case '/':
                    result = prev / current;
                    break;
                default:
                    return;
            }
            currentOperand = result;
            operation = undefined;
            previousOperand = '';
            updateDisplay();
        }

        function clearDisplay() {
            currentOperand = '';
            previousOperand = '';
            operation = undefined;
            updateDisplay();
        }

        function updateDisplay() {
            const display = document.getElementById('display');
            if (operation) {
                display.innerText = `${previousOperand} ${operation} ${currentOperand}`;
            } else {
                display.innerText = currentOperand || '0';
            }
        }
    </script>
</body>
</html>
# code-alpha-calculator
