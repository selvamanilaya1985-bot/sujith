<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Frontend Demo</title>

    <!-- CSS inside same file -->
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f2f2f2;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .card {
            background: white;
            padding: 20px;
            width: 300px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            text-align: center;
        }

        button {
            padding: 10px 15px;
            border: none;
            background: #007bff;
            color: white;
            border-radius: 5px;
            cursor: pointer;
        }

        button:hover {
            background: #0056b3;
        }

        #message {
            margin-top: 15px;
            color: green;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <!-- HTML -->
    <div class="card">
        <h2>Frontend Demo</h2>
        <p>Button click panna message change aagum</p>
        <button onclick="showMessage()">Click Me</button>
        <div id="message"></div>
    </div>

    <!-- JavaScript inside same file -->
    <script>
        function showMessage() {
            document.getElementById("message").innerText =
                "Hello! HTML + CSS + JS working perfectly 🚀";
        }
    </script>

</body>
</html>
