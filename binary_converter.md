<html>
    <head>
        <title>
            Nl binary converter
        </title>
        <script>
            function dTob(){
                //alert('hello');
                var decimalInput = document.getElementById('decimalInput').value;
                var binaryOutput = Number(decimalInput).toString(2);
                alert(binaryOutput);
            }
        </script>
    </head>
    <body>
        <div style="background-color: orange; ">
        <p>this is my binary converter</p>
        <input id="decimalInput" type="number" />
        <button onclick="dTob();">convert</button>
        </div>
    </body>
</html>
