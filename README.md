
<html>
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
</head>
<body>
    <div class="container-fluid">
        <div class="container">
            <div class="row">
                <div class="col-sm-4"></div>
                <div class="col-sm-4">
                    <label>Card Bin</label>
                    <input type="text" class="form-control" id="bintext" maxlength="16" placeholder="Bin No...">
                </div>
                <div class="col-sm-4"></div>
            </div>
            <div class="row">
                <div class="col-sm-4"></div>
                <div class="col-sm-4">
                    <label>Expiration Date</label>
                    <input type="month" class="form-control" id="Expiration">
                </div>
                <div class="col-sm-4"></div>
            </div>
            <div class="row">
                <div class="col-sm-4"></div>
                <div class="col-sm-4">
                    <label>Cvv</label>
                    <input type="text" class="form-control" id="cvv" placeholder="XXX" maxlength="3">
                </div>
                <div class="col-sm-4"></div>
            </div>
            <div class="row">
                <div class="col-sm-4"></div>
                <div class="col-sm-4">
                    <label>Quantity</label>
                    <input type="text" class="form-control" id="quantity" placeholder="123" maxlength="3">
                </div>
                <div class="col-sm-4"></div>
            </div>
            <br>
            <div class="row">
                <div class="col-sm-4"></div>
                <div class="col-sm-4">
                    <button type="button" class="form-control btn btn-success" id="button">Generate</button>
                </div>
                <div class="col-sm-4"></div>
            </div>
            <br>
            <div class="row">
                <div class="col-sm-12">
                    <table class="table table-bordered" id="resultTable">
                        <thead>
                            <tr>
                                <th>Generated Number</th>
                            </tr>
                        </thead>
                        <tbody>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

</body>
</html>
<script>


    $(document).ready(function() {
    $("#button").click(function() {
        var number = $("#bintext").val();
        var expiration = $("#Expiration").val();
        var cvv = $("#cvv").val();
        var quantity = parseInt($("#quantity").val());

        // Clear the existing table
        $("#resultTable tbody").empty();

        // Generate and append the 16-digit numbers with expiration date and CVV to the table
        for (var i = 0; i < quantity; i++) {
            var randomDigits = generateRandomDigits(16 - number.length);
            var generatedNumber = number + randomDigits + "|" + formatExpirationDate(expiration) + "|" + formatCVV(cvv);
            $("#resultTable tbody").append("<tr><td>" + generatedNumber + "</td></tr>");
        }
    });

    // Function to generate random digits
    function generateRandomDigits(length) {
        var result = "";
        for (var i = 0; i < length; i++) {
            result += Math.floor(Math.random() * 10);
        }
        return result;
    }

    // Function to format the expiration date
    function formatExpirationDate(expiration) {
        if (!expiration) {
            // If expiration date is not selected, generate a random date until 2030
            var year = Math.floor(Math.random() * (2031 - new Date().getFullYear())) + new Date().getFullYear();
            var month = Math.floor(Math.random() * 12) + 1;
            if (month < 10) {
                month = "0" + month;
            }
            return month + "|" + year;
        } else {
            // Format the selected expiration date as MM|YY (e.g., 08|25)
            var date = new Date(expiration);
            var month = date.getMonth() + 1;
            if (month < 10) {
                month = "0" + month;
            }
            var year = date.getFullYear().toString().substr(-2);
            return month + "|" + year;
        }
    }

    // Function to format the CVV
    function formatCVV(cvv) {
        if (!cvv) {
            // If CVV is not entered, generate a random CVV between 001 and 999
            return Math.floor(Math.random() * 999 + 1).toString().padStart(3, "0");
        } else {
            // Return the entered CVV
            return cvv;
        }
    }
});

    $("#button").click(function() {
        var number = $("#bintext").val();
        var expiration = $("#Expiration").val();
        var quantity = parseInt($("#quantity").val());

        // Clear the existing table
        $("#resultTable tbody").empty();

        // Generate and append the 16-digit numbers with expiration date to the table
        for (var i = 0; i < quantity; i++) {
            var randomDigits = generateRandomDigits(16 - number.length);
            var generatedNumber = number + randomDigits + "|" + formatExpirationDate(expiration);
            $("#resultTable tbody").append("<tr><td>" + generatedNumber + "</td></tr>");
        }
    });

    // Function to generate random digits
    function generateRandomDigits(length) {
        var result = "";
        for (var i = 0; i < length; i++) {
            result += Math.floor(Math.random() * 16);
        }
        return result;
    }

    // Function to format the expiration date
    function formatExpirationDate(expiration) {
        if (!expiration) {
            // If expiration date is not selected, generate a random date until 2030
            var year = Math.floor(Math.random() * (2031 - new Date().getFullYear())) + new Date().getFullYear();
            var month = Math.floor(Math.random() * 12) + 1;
            if (month < 10) {
                month = "0" + month;
            }
            return month + "|" + year;
        } else {
            // Format the selected expiration date as MM|YYYY
            var date = new Date(expiration);
            var month = date.getMonth() + 1;
            if (month < 10) {
                month = "0" + month;
            }
            var year = date.getFullYear().toString().substr(-2);
            return month + "|" + year;
        }
    }




</script>
