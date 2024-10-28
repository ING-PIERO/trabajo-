# html 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Precios de Alquiler</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-iYQeCzEYFbKjA/T2uDLTpkwGzCiq6soy8tYaI1GyVh/UjpbCx/TYkiZhlZB6+fzT" crossorigin="anonymous">
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <div class="container">
        <div class="row">
            <div class="col-12 col-md-8 offset-md-2">
                <div class="card mt-5 shadow">
                    <div class="card-body text-center">
                        <h4 class="card-title">Red Neuronal Pisos de Alquiler Valencia</h4>
                    </div>
                </div>

                <div class="card mt-2 shadow">
                    <div class="card-body">
                        <form id="form">
                            <div class="mb-3">
                                <label for="m2">M²</label>
                                <input type="number" class="form-control" id="m2" required>
                            </div>

                            <div class="mb-3">
                                <label for="hab">Nº de habitaciones</label>
                                <input type="number" class="form-control" id="hab" required>
                            </div>

                            <div class="mb-3">
                                <label for="planta">Nº de planta</label>
                                <input type="number" class="form-control" id="planta" required>
                            </div>

                            <div class="mb-3">
                                <label for="ascensor">Ascensor</label>
                                <select id="ascensor" class="form-select" required>
                                    <option disabled selected>Elige una opción...</option>
                                    <option value="0">No</option>
                                    <option value="1">Sí</option>
                                </select>
                            </div>

                            <div class="mb-3">
                                <label for="ext">Exterior</label>
                                <select id="ext" class="form-select" required>
                                    <option disabled selected>Elige una opción...</option>
                                    <option value="0">No</option>
                                    <option value="1">Sí</option>
                                </select>
                            </div>

                            <div class="mb-3">
                                <label for="est">Estado</label>
                                <select id="est" class="form-select" required>
                                    <option disabled selected>Elige una opción...</option>
                                    <option value="0">No rehabilitado</option>
                                    <option value="1">Rehabilitado</option>
                                    <option value="2">Nuevo</option>
                                </select>
                            </div>

                            <div class="mb-3">
                                <label for="cent">Céntrico</label>
                                <select id="cent" class="form-select" required>
                                    <option disabled selected>Elige una opción...</option>
                                    <option value="0">No</option>
                                    <option value="1">Sí</option>
                                </select>
                            </div>

                            <div class="d-flex justify-content-between align-items-center">
                                <button class="btn btn-primary" type="button" id="btn">Calcular precio</button>
                                <h5 id="resultado" class="result-container"></h5>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@2.0.0/dist/tf.min.js"></script>

    <script>
        var modelo = null;

        (async () => {
            console.log("Cargando el modelo...");
            modelo = await tf.loadLayersModel("model.json");
            console.log("Modelo cargado!");
        })();

        const btn = document.getElementById("btn");
        const resultadoEl = document.getElementById("resultado");

        btn.onclick = () => {
            var m2 = parseInt(document.getElementById('m2').value);
            var hab = parseInt(document.getElementById('hab').value);
            var planta = parseInt(document.getElementById('planta').value);
            var ascensor = parseInt(document.getElementById('ascensor').value);
            var ext = parseInt(document.getElementById('ext').value);
            var est = parseInt(document.getElementById('est').value);
            var cent = parseInt(document.getElementById('cent').value);

            if (modelo != null) {
                var tensor = tf.tensor2d([[0, m2, hab, planta, ascensor, ext, est, cent]]);
                var prediccion = modelo.predict(tensor).dataSync();
                prediccion = Math.round(prediccion[0] * 100) / 100; // Redondear a dos decimales
                resultadoEl.innerHTML = "Precio: " + prediccion + " €/mes";
            } else {
                resultadoEl.innerHTML = "Intenta de nuevo en un rato...";
            }
        }
    </script>

</body>
</html>

css 
body {
    font-family: 'Orbitron', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-image: url('th.jpeg'); 
    background-size: cover; 
    background-position: center; 
    background-repeat: no-repeat; 
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center; 
    align-items: center;
    height: 100vh; 
}

.container {
    width: 100%; /* Ajuste adaptable para diferentes tamaños de pantalla */
    max-width: 600px; /* Ancho máximo para evitar que crezca demasiado en pantallas grandes */
    padding: 40px; /* Espaciado optimizado */
    background-color: rgba(255, 255, 255, 0); /* Fondo invisible */
    border-radius: 15px; /* Bordes redondeados */
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.4); /* Sombra mejorada para mayor profundidad */
    text-align: center;
    backdrop-filter: blur(15px); /* Efecto de desenfoque más marcado */
    border: 1px solid rgba(255, 255, 255, 0.3); /* Borde suave */
    animation: pulse 1.5s infinite;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    transition: transform 0.3s ease, box-shadow 0.3s ease; /* Transición suave */
}

.container:hover {
    transform: scale(1.02); /* Efecto de agrandamiento sutil en hover */
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.5); /* Sombra más intensa en hover */
}

.inner-box {
    background-color: rgba(103, 206, 77, 0.5); 
    border-radius: 10px; 
    padding: 20px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); 
    margin-top: 20px; 
    width: 100%;
}

@keyframes pulse {
    0% {
        box-shadow: 0 0 5px rgba(125, 231, 76, 0.8);
    }
    50% {
        box-shadow: 0 0 50px rgba(125, 231, 76, 0.8);
    }
    100% {
        box-shadow: 0 0 5px  rgba(125, 231, 76, 0.8);
    }
}

h4 {
    color: rgba(12, 161, 172, 0.9); 
    font-size: 2em; 
    text-align: center; 
    margin-top: 20px; 
    margin-bottom: 20px; 
    padding: 10px 0; 
    font-weight: 700;
    text-shadow: 0 0 5px rgba(0, 123, 255, 0.8); 
}

form {
    margin-top: 30px; 
}

form label {
    font-weight: 600;
    color: rgba(68, 68, 68, 0.8); 
    display: block;
    margin-bottom: 8px;
    text-align: left;
    font-size: 1.1em;
}

form input[type="text"],
form input[type="number"],
form select {
    width: calc(100% - 16px); 
    padding: 16px; 
    margin-bottom: 20px; 
    border: 1px solid rgba(187, 187, 187, 0.8); 
    border-radius: 5px; 
    font-size: 1.2em; 
    background-color: rgba(255, 255, 255, 0.8); 
    transition: border-color 0.3s ease, box-shadow 0.3s ease; 
}

form input[type="text"]:focus,
form input[type="number"]:focus,
form select:focus {
    border-color: rgba(0, 123, 255, 0.8); 
    outline: none; 
    box-shadow: 0 0 10px rgba(0, 123, 255, 0.8); 
}

form button {
    width: 100%;
    background-color: rgba(0, 123, 255, 0.8); 
    color: rgba(255, 255, 255, 0.9); 
    border: none;
    padding: 20px 0; 
    font-size: 1.2em; 
    border-radius: 5px; 
    cursor: pointer;
    transition: background-color 0.3s ease, box-shadow 0.3s ease; 
    margin-top: 20px; 
    font-weight: 600;
}

form button:hover {
    background-color: rgba(0, 86, 179, 0.8); 
    box-shadow: 0 0 10px rgba(0, 86, 179, 0.8); 
}

a {
    color: rgba(0, 123, 255, 0.8); 
    text-decoration: none;
    transition: color 0.3s ease;
    font-weight: 600;
}

a:hover {
    color: rgba(0, 86, 179, 0.8); 
}

/* Estilos generales para los globos flotantes */
.float-icon {
    position: fixed;
    right: 20px;
    width: 60px; 
    height: 60px; 
    display: flex; 
    justify-content: center; 
    align-items: center; 
    border-radius: 50%; 
    box-shadow: 0 2px 15px rgba(0, 0, 0, 0.3); 
    z-index: 1000; 
    transition: transform 0.3s ease, box-shadow 0.3s ease; 
}

.float-icon img {
    width: 35px; 
    height: 35px; 
}

/* Efecto de hover para los globos flotantes */
.float-icon:hover {
    transform: scale(1.1); 
    box-shadow: 0 4px 25px rgba(0, 0, 0, 0.4); 
}

/* Específico para WhatsApp */
.float-icon.whatsapp {
    bottom: 20px;
    background-color: #25d366; 
}

/* Específico para Facebook */
.float-icon.facebook {
    bottom: 90px; 
    background-color: #4267B2; 
}
