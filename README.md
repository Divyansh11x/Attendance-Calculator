<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Attendance Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 0;
            background-color: #f4f4f9;
            color: #333;
        }
        .container {
            max-width: 400px;
            margin: 0 auto;
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            font-size: 1.5em;
            margin-bottom: 20px;
        }
        input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        .output {
            margin-top: 20px;
            padding: 10px;
            border-radius: 5px;
            background: #e9ecef;
            font-weight: bold;
        }
        .tips {
            margin-top: 20px;
            padding: 10px;
            border-radius: 5px;
            background: #f8d7da;
            color: #721c24;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Attendance Calculator</h1>
        <label for="totalClasses">Total Classes:</label>
        <input type="number" id="totalClasses" placeholder="Enter total number of classes">

        <label for="classesPresent">Total Present:</label>
        <input type="number" id="classesPresent" placeholder="Enter number of classes attended">

        <button onclick="calculateAttendance()">Calculate Attendance</button>

        <div id="result" class="output"></div>
        <div id="tips" class="tips"></div>
    </div>

    <script>
        function calculateAttendance() {
            const totalClasses = parseInt(document.getElementById('totalClasses').value);
            const classesPresent = parseInt(document.getElementById('classesPresent').value);

            if (isNaN(totalClasses) || isNaN(classesPresent) || totalClasses <= 0 || classesPresent < 0) {
                document.getElementById('result').textContent = "Please enter valid numbers.";
                document.getElementById('tips').textContent = "";
                return;
            }

            if (classesPresent > totalClasses) {
                document.getElementById('result').textContent = "Classes attended cannot exceed total classes.";
                document.getElementById('tips').textContent = "";
                return;
            }

            const percentage = ((classesPresent / totalClasses) * 100).toFixed(2);
            const cutPerLeave = (100 / totalClasses).toFixed(2);
            document.getElementById('result').textContent = `Your attendance percentage is ${percentage}%.\nOne leave will reduce your percentage by ${cutPerLeave}%.`;

            if (percentage < 75) {
                const requiredAttendance = Math.ceil((0.75 * totalClasses - classesPresent) / (1 - 0.75));
                document.getElementById('tips').textContent = 
                    `You need to attend the next ${requiredAttendance} classes without missing any to reach 75%.`;
            } else {
                document.getElementById('tips').textContent = "Great! You are maintaining more than 75% attendance.";
            }
        }
    </script>
</body>
</html>

<!-- README.md -->
<!--
# Attendance Calculator

A simple tool to calculate attendance percentage and understand the impact of missed classes.

## Features
- Calculates attendance percentage.
- Shows the effect of one leave on your attendance.
- Provides actionable tips to maintain 75% attendance.

## Usage
1. Clone the repository:
   ```bash
   git clone <repository_url>
   ```
2. Open `index.html` in a web browser.
3. Enter the total number of classes and the number of classes attended.
4. View the attendance percentage and suggestions.

## Contributing
Feel free to contribute by forking this repository and creating pull requests.

## License
MIT License.
-->
