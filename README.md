<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Consulta de Cédula Profesional</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }
        .container {
            background-color: #fff;
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            max-width: 600px;
            width: 100%;
            text-align: center;
        }
        h1 {
            color: #333;
            margin-bottom: 25px;
        }
        .input-group {
            margin-bottom: 15px;
            text-align: left;
        }
        .input-group label {
            display: block;
            margin-bottom: 5px;
            color: #555;
            font-weight: bold;
        }
        .input-group input {
            width: 95%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            width: 100%;
            padding: 12px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 18px;
            cursor: pointer;
            transition: background-color 0.3s ease;
            margin-top: 20px;
        }
        button:hover {
            background-color: #0056b3;
        }
        #resultados {
            margin-top: 30px;
            text-align: left;
            border-top: 1px solid #eee;
            padding-top: 20px;
        }
        .info {
            color: #555;
            font-style: italic;
        }
        .registro-card {
            border: 1px solid #ddd;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
            background-color: #f9f9f9;
        }
        .registro-card h3 {
            margin-top: 0;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Consulta de Cédula Profesional</h1>
    <p class="info">Puedes dejar campos vacíos para ampliar tu búsqueda.</p>
    <div class="input-group">
        <label for="nombreInput">Nombre(s):</label>
        <input type="text" id="nombreInput" placeholder="Ej. Juan">
    </div>
    <div class="input-group">
        <label for="paternoInput">Apellido Paterno:</label>
        <input type="text" id="paternoInput" placeholder="Ej. Pérez">
    </div>
    <div class="input-group">
        <label for="maternoInput">Apellido Materno:</label>
        <input type="text" id="maternoInput" placeholder="Ej. García">
    </div>
    
    <button onclick="buscarCedula()">Buscar Cédula</button>
    
    <div id="resultados">
        </div>
</div>

<script>
function buscarCedula() {
    // 1. Obtener los valores y convertirlos a mayúsculas para una búsqueda insensible
    const nombre = document.getElementById('nombreInput').value.trim().toUpperCase();
    const paterno = document.getElementById('paternoInput').value.trim().toUpperCase();
    const materno = document.getElementById('maternoInput').value.trim().toUpperCase();
    const resultadosDiv = document.getElementById('resultados');

    // Limpiar resultados anteriores
    resultadosDiv.innerHTML = '';

    // 2. Base de datos de ejemplo (¡esto debería ser un API o una base de datos real!)
    const registros = [
        { nombre: "JUAN", paterno: "PEREZ", materno: "GARCIA", cedula: "12345678", profesion: "Ingeniero Civil", institucion: "Universidad Nacional Autónoma de México (UNAM)" },
        { nombre: "MARIA", paterno: "LOPEZ", materno: "HERNANDEZ", cedula: "87654321", profesion: "Médico Cirujano", institucion: "Instituto Politécnico Nacional (IPN)" },
        { nombre: "CARLOS", paterno: "SANCHEZ", materno: "RUIZ", cedula: "98765432", profesion: "Licenciado en Derecho", institucion: "Universidad de Guadalajara (UdG)" },
        { nombre: "JOSÉ", paterno: "JUÁREZ", materno: "RAMÍREZ", cedula: "55554444", profesion: "Arquitecto", institucion: "Universidad Iberoamericana" },
        { nombre: "PEDRO", paterno: "PEREZ", materno: "GUTIÉRREZ", cedula: "11223344", profesion: "Ingeniero en Sistemas", institucion: "Tecnológico de Monterrey" },
        { nombre: "ANA", paterno: "GARCIA", materno: "PEREZ", cedula: "99887766", profesion: "Licenciada en Pedagogía", institucion: "Benemérita Escuela Nacional de Maestros" }
    ];

    // 3. Filtrar todos los registros que coincidan con la búsqueda
    const resultados = registros.filter(registro => {
        // Creamos una cadena de texto para buscar en ella
        const textoBusqueda = `${registro.nombre} ${registro.paterno} ${registro.materno}`;
        
        // Verificamos si los campos del formulario están en el registro
        const coincideNombre = nombre ? textoBusqueda.includes(nombre) : true;
        const coincidePaterno = paterno ? textoBusqueda.includes(paterno) : true;
        const coincideMaterno = materno ? textoBusqueda.includes(materno) : true;

        // El registro coincide si al menos uno de los campos ingresados coincide
        return coincideNombre || coincidePaterno || coincideMaterno;
    });

    // 4. Mostrar los resultados encontrados
    if (resultados.length > 0) {
        let htmlResultados = `<h3>${resultados.length} registro(s) encontrado(s):</h3>`;
        resultados.forEach(registro => {
            htmlResultados += `
                <div class="registro-card">
                    <h3>${registro.nombre} ${registro.paterno} ${registro.materno}</h3>
                    <p><strong>Cédula:</strong> ${registro.cedula}</p>
                    <p><strong>Profesión:</strong> ${registro.profesion}</p>
                    <p><strong>Institución:</strong> ${registro.institucion}</p>
                </div>
            `;
        });
        resultadosDiv.innerHTML = htmlResultados;
    } else {
        resultadosDiv.innerHTML = `<p class="info">No se encontraron registros que coincidan con la búsqueda.</p>`;
    }
}
</script>

</body>
</html>
