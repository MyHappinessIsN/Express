# Express
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device width, initial scale=1.0">
    <title>Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: white;
        }

        #nameForm {
            margin: 50px;
        }

        input[type="text"] {
            padding: 5px;
            font-size: 16px;
        }

        input[type="submit"] {
            padding: 10px 20px;
            font-size: 18px;
            background-color: #4CAF50;
            color: #fff;
            border: none;
            cursor: pointer;
        }

        input[type="submit"]:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <form id="nameForm">
        <label for="nameInput">Guess my name:</label>
        <input type="text" id="nameInput">
        <input type="submit" value="Submit">
    </form>

    <script>
        document.getElementById("nameForm").addEventListener("submit", function (event) {
            event.preventDefault(); // Prevent the form from submitting

            var name = document.getElementById("nameInput").value;

            if (name.toLowerCase() === "chinmay") {
                alert("You are the only moon that keeps the tides of my ocean-heart at bay.");
                alert("Would you like to go on a date with me...");
            } else if (name.toLowerCase() === "chinmaya"){
                alert("You are the only moon that keeps the tides of my ocean-heart at bay.");
                alert("Would you like to go on a date with me...");
            }else {
                alert("Invalid");
            }
        });
    </script>
</body>
</html>
