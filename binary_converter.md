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
            function dToH(){
                //alert('hello');
                var decimalInput = document.getElementById('decimalInput').value;
                var hexOutput = Number(decimalInput).toString(16);
                alert(hexOutput);
            }
        </script>
    </head>
    <body>
        <div style="background-color: orange; ">
        <p>this is my binary and hexidecimal converter</p>
        <input id="decimalInput" type="number" />
        <button onclick="dTob();">convert to binary</button>
        <button onclick="dToh();">convert to hexidecimal</button>
        </div>
    </body>
</html>
