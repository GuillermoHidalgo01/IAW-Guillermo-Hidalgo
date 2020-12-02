# Almacenar datos en la Base de datos:
```powershell
<!DOCTYPE html>
<html>

<head>
	<meta content="text/html; charset=utf-8" http-equiv="Content-Type">
	<title>P001</title>
</head>

<body>
	<?php
	
		$nombre = htmlspecialchars($_GET['nombre']); 
		
		$var = "datos.ini";
		$base = parse_ini_file($var);		
		$php = new PDO($base["baseDeDatos"],$base["usuario"],$base["password"]);
		
		$con = $php->prepare("INSERT INTO encabezados VALUES (default,:tex);");
		$con->bindParam(':tex',$nombre);
		$con->execute();

		//$resultado = $registros[0][1];
	?>
	<h1><?
<h1><?php echo "Valor Introducido" ?></h1>
</body>

</html>
```
# Saber posición GPS y almacenarla en un fichero:
```powershell
<?php 

$long = $_POST['longitude'];
$lat = $_POST['latitude'];


$file = fopen("archivo.txt", "a");
fwrite($file, "longitud" . $long ."|latitud:". $lat);
fclose($file);
?>


<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="https://code.jquery.com/jquery-3.5.1.min.js" integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0=" crossorigin="anonymous"></script>
</head>

<body>
    <script>

		navigator.geolocation.getCurrentPosition((posicion) => {
    		$.post("http://localhost/gpsexamen.php", { latitude : posicion.coords.latitude, longitude : posicion.coords.longitude }, (response) => {
        	console.log(response.results);
   	 	});
	});

    </script>
</body>

</html>
```
