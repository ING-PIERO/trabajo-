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


# css

