<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Reserva de Bicicletas</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen">
    <div class="bg-white p-8 rounded-lg shadow-lg w-full max-w-lg">
        <h1 class="text-2xl font-bold mb-6 text-center">Reserva tu Bicicleta</h1>
        <form id="booking-form" class="space-y-4">
            <!-- Datos Personales -->
            <div>
                <label for="name" class="block text-sm font-medium">Nombre Completo</label>
                <input type="text" id="name" name="name" required class="w-full mt-1 p-2 border rounded-lg">
            </div>
            <div>
                <label for="email" class="block text-sm font-medium">Correo Electrónico</label>
                <input type="email" id="email" name="email" required class="w-full mt-1 p-2 border rounded-lg">
            </div>
            <div>
                <label for="phone" class="block text-sm font-medium">Teléfono</label>
                <input type="tel" id="phone" name="phone" required class="w-full mt-1 p-2 border rounded-lg">
            </div>

            <!-- Marca de Bici -->
            <div>
                <label for="brand" class="block text-sm font-medium">Marca de Bicicleta</label>
                <select id="brand" name="brand" required class="w-full mt-1 p-2 border rounded-lg">
                    <option value="">Selecciona una marca</option>
                    <option value="Trek">Trek</option>
                    <option value="Specialized">Specialized</option>
                    <option value="Giant">Giant</option>
                    <option value="Cannondale">Cannondale</option>
                </select>
            </div>

            <!-- Talla de Bici -->
            <div>
                <label for="size" class="block text-sm font-medium">Talla de Bicicleta</label>
                <select id="size" name="size" required class="w-full mt-1 p-2 border rounded-lg">
                    <option value="">Selecciona una talla</option>
                    <option value="S">S</option>
                    <option value="M">M</option>
                    <option value="L">L</option>
                    <option value="XL">XL</option>
                </select>
            </div>

            <!-- Fecha y Hora -->
            <div>
                <label for="date" class="block text-sm font-medium">Fecha</label>
                <input type="date" id="date" name="date" required class="w-full mt-1 p-2 border rounded-lg">
            </div>
            <div>
                <label for="time" class="block text-sm font-medium">Hora</label>
                <input type="time" id="time" name="time" required class="w-full mt-1 p-2 border rounded-lg">
            </div>

            <!-- Botón de Enviar -->
            <button type="submit" class="w-full bg-blue-500 text-white py-2 px-4 rounded-lg hover:bg-blue-600">Reservar</button>
        </form>
    </div>

    <script>
        // Límite de reservas por marca
        const bookingLimits = {
            Trek: 10,
            Specialized: 10,
            Giant: 10,
            Cannondale: 10
        };

        // Contador de reservas por marca
        const bookings = {
            Trek: 0,
            Specialized: 0,
            Giant: 0,
            Cannondale: 0
        };

        document.getElementById('booking-form').addEventListener('submit', function(e) {
            e.preventDefault();

            const formData = new FormData(e.target);
            const data = Object.fromEntries(formData);

            // Verificar el límite de reservas
            if (bookings[data.brand] >= bookingLimits[data.brand]) {
                alert(`Lo sentimos, no hay más cupos disponibles para la marca ${data.brand}.`);
                return;
            }

            // Incrementar contador de reservas
            bookings[data.brand] += 1;

            console.log('Reserva realizada:', data);
            alert(`Reserva realizada con éxito para la marca ${data.brand}. Cupos restantes: ${bookingLimits[data.brand] - bookings[data.brand]}`);
        });
    </script>
</body>
</html>
