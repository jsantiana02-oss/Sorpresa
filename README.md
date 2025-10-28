<!DOCTYPE hmlt>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BIENVENIDOS A NUESTRO FUTURO</title>
    <!-- Carga de Tailwind CSS para un diseño moderno y responsive --><script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Configuraciones generales para simular un ambiente de juego RPG */
        @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Inter:wght@400;700&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0d1117; /* Fondo oscuro */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 1rem;
        }

        /* Estilo para simular la fuente de juego en títulos */
        .rpg-title {
            font-family: 'Press Start 2P', cursive;
            text-shadow: 2px 2px #5a00a0;
        }

        /* Estilo para los botones de acción principal */
        .btn-primary {
            transition: all 0.2s;
            box-shadow: 0 4px #005691;
        }
        .btn-primary:hover {
            box-shadow: 0 2px #005691;
            transform: translateY(2px);
        }

        /* Estilo para las opciones de 'clase' */
        .class-option {
            transition: all 0.2s;
            cursor: pointer;
            border: 2px solid #5a00a0;
            box-shadow: 0 4px #9333ea;
        }
        .class-option:hover {
            background-color: #3b0764;
            transform: scale(1.02);
        }
        
        /* Animación de los Brillos (NUEVO) */
        @keyframes shimmer {
            0% { transform: translateY(-100%); opacity: 1; }
            100% { transform: translateY(100%); opacity: 0; }
        }

        .shimmer-effect {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
            z-index: 10; 
        }

        .shimmer-star {
            position: absolute;
            color: #fff9c4; /* Tono de brillo/estrella */
            font-size: 10px;
            opacity: 0;
            animation: shimmer 5s linear infinite;
        }

        /* Contenedor de la imagen de tulipanes */
        .tulip-container {
            width: 100%;
            max-width: 250px; /* Tamaño máximo para el ramo */
            height: auto;
            border-radius: 12px;
            overflow: visible; /* Asegura que los brillos no se corten */
            position: relative;
            margin: 0 auto;
            display: flex; 
            align-items: center;
            justify-content: center;
            /* Se añade un tamaño mínimo para que el placeholder se vea si la imagen no carga */
            min-height: 250px; 
        }

        .tulip-container img {
            width: 100%;
            height: auto;
            display: block;
            position: relative; 
            z-index: 5; /* La imagen debe estar debajo de los brillos */
            /* Efecto 3D de levantamiento (opcional, para simular la "flotación" del corazón) */
            animation: float 3s ease-in-out infinite; 
        }
        /* Fallback de error: si la URL de la imagen es incorrecta, se muestra un mensaje */
        .tulip-container img:not([src]):before {
            content: "Error: Falta URL de la imagen";
            color: white;
            background-color: #ef4444;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            height: 250px;
            font-size: 12px;
        }

        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0px); }
        }

    </style>
</head>
<body class="text-white">

    <script>
        // Variables de estado
        let currentScreen = 1;
        const screens = {
            1: 'screen-welcome',
            2: 'screen-prepare',
            3: 'screen-proposal',
            4: 'screen-result',
            5: 'screen-animation' 
        };
        
        // Función para generar y animar los brillos (estrellas)
        function createShimmerEffect() {
            const shimmerLayer = document.getElementById('shimmer-layer');
            if (!shimmerLayer) return;

            const starCount = 20; // Número de brillos
            shimmerLayer.innerHTML = ''; // Limpiar brillos anteriores
            
            for (let i = 0; i < starCount; i++) {
                const star = document.createElement('span');
                star.className = 'shimmer-star';
                star.textContent = '✧'; // Un carácter de estrella o brillo
                
                // Posición inicial aleatoria
                star.style.left = `${Math.random() * 100}%`;
                
                // Retraso y duración de animación aleatorios para un efecto natural
                star.style.animationDelay = `${Math.random() * 5}s`;
                star.style.animationDuration = `${4 + Math.random() * 2}s`;
                
                shimmerLayer.appendChild(star);
            }
        }
        
        // Función para cambiar de pantalla
        function changeScreen(targetScreen) {
            // Oculta la pantalla actual
            document.getElementById(screens[currentScreen]).classList.add('hidden');
        
            // Muestra la nueva pantalla
            document.getElementById(screens[targetScreen]).classList.remove('hidden');
            
            // Si vamos a la pantalla de animación (5), iniciamos los brillos
            if (targetScreen === 5) {
                createShimmerEffect();
            }

            // Actualiza el estado
            currentScreen = targetScreen;
        }

        // Función para manejar la selección de clase (la declaración)
        function selectClass(choice) {
            const resultTitle = document.getElementById('result-title');
            const resultMessage = document.getElementById('result-message');
            const confessionText = document.getElementById('confession-text');
            const resultButton = document.getElementById('result-button');
            
            // Deshabilita las opciones para que no pueda cambiar de opinión
            document.getElementById('option-yes').onclick = null;
            document.getElementById('option-no').onclick = null;
            
            if (choice === 'yes') {
                resultTitle.textContent = "¡MISIÓN ACEPTADA!";
                resultTitle.classList.remove('text-[#8b5cf6]');
                resultTitle.classList.add('text-[#facc15]');
                resultMessage.innerHTML = "¡Felicidades, has desbloqueado la ruta de la relación! Nuestro futuro comienza ahora. Prepárate para la mejor aventura.";
                
                // Configuración para el mensaje personal y el botón de Continuar
                confessionText.innerHTML = "Eres la chica con la que quiero estar en mi destino y compartir mi futuro. Eres mi trébol, tan difícil de encontrar pero qué afortunado fui al encontrarte. Te quiero mucho <3. <br><br> Att: <br> gggjjose";
                confessionText.classList.remove('hidden');
                
                // Cambia el botón a "Continuar" y lo dirige a la animación (Pantalla 5)
                resultButton.textContent = "Continuar";
                resultButton.classList.remove('bg-[#dc2626]');
                resultButton.classList.add('bg-[#10b981]');
                resultButton.onclick = () => changeScreen(5);

            } else {
                resultTitle.textContent = "FIN DE LA MISIÓN";
                resultTitle.classList.remove('text-[#8b5cf6]');
                resultTitle.classList.add('text-[#dc2626]');
                resultMessage.textContent = "Entendido. Gracias por tu honestidad. La amistad sigue siendo una gran clase de aventura. Siempre serás mi compañera favorita.";
                confessionText.classList.add('hidden');
                
                // Mantiene el botón como "Terminar Sesión" y recarga la página
                resultButton.textContent = "Terminar Sesión";
                resultButton.classList.remove('bg-[#10b981]');
                resultButton.classList.add('bg-[#dc2626]');
                resultButton.onclick = () => location.reload();
            }
            
            // Muestra la pantalla de resultado (Pantalla 4)
            changeScreen(4);
        }
        
        // Inicializa la primera pantalla al cargar
        document.addEventListener('DOMContentLoaded', () => {
             // Asegura que solo la pantalla inicial es visible
             document.getElementById('screen-welcome').classList.remove('hidden');
        });

    </script>

    <!-- Contenedor Principal de la App, centrado y con ancho fijo (como un móvil) --><div id="game-container" class="w-full max-w-sm md:max-w-md bg-[#161b22] border-4 border-[#30363d] rounded-xl p-6 shadow-2xl">
        
        <!-- Contenido de cada pantalla (se mostrará uno a la vez) --><!-- PANTALLA 1: Bienvenida --><div id="screen-welcome" class="text-center">
            <h1 class="rpg-title text-2xl mb-4 text-[#8b5cf6]">Destiny</h1>
            <p class="text-sm mb-8 text-gray-400">Una nueva aventura te espera. ¿Estás lista para comenzar?</p>
            <button onclick="changeScreen(2)" class="btn-primary w-full bg-[#007acc] text-white py-3 rounded-lg text-lg font-bold uppercase tracking-wider mt-6">
                Iniciar Partida
            </button>
        </div>

        <!-- PANTALLA 2: Preparación (Opcional, para crear expectativa) --><div id="screen-prepare" class="hidden text-center">
            <div class="bg-gray-800 p-4 rounded-lg mb-6">
                <p class="text-lg text-yellow-400 mb-2">Aviso del Sistema:</p>
                <p class="text-gray-300 text-sm">El destino de esta misión es crucial. Por favor, lee las opciones con atención, tu elección es permanente.</p>
            </div>
            <h2 class="rpg-title text-xl mb-6 text-[#10b981]">Welcome to my future</h2>
            <button onclick="changeScreen(3)" class="btn-primary w-full bg-[#10b981] text-gray-900 py-3 rounded-lg text-lg font-bold uppercase tracking-wider mt-6">
                Continuar
            </button>
        </div>

        <!-- PANTALLA 3: Declaración (Seleccionar Clase) --><div id="screen-proposal" class="hidden">
            <h2 class="rpg-title text-xl text-center mb-8 text-white">Selección de Clase</h2>
            
            <p class="text-center text-lg mb-8 text-gray-300">
                Para empezar la partida, debes elegir tu rol de compañera. <br>
                <span class="text-yellow-400 font-bold">La pregunta es simple:</span>
            </p>

            <!-- La Opción de SÍ (Destacada) --><div id="option-yes" onclick="selectClass('yes')" class="class-option bg-[#2d0a4c] p-4 mb-4 rounded-xl flex items-center justify-between">
                <div>
                    <p class="text-xl font-bold text-[#facc15] mb-1">Clase: Acepto</p>
                    <p class="text-sm text-gray-300">Compañera de vida - Nivel 1</p>
                </div>
                <span class="text-3xl">❤️</span>
            </div>

            <!-- El Texto de la Pregunta al Centro --><div class="text-center my-6">
                <p class="text-2xl font-extrabold text-[#f97316] uppercase">¿Quieres ser mi novia?</p>
            </div>


            <!-- La Opción de NO (Menos destacada, pero presente) --><div id="option-no" onclick="selectClass('no')" class="class-option bg-[#1f2937] p-4 rounded-xl flex items-center justify-between">
                <div>
                    <p class="text-xl font-bold text-[#ef4444] mb-1">Clase: No, Gracias</p>
                    <p class="text-sm text-gray-400">Amiga Noble - Nivel 1</p>
                </div>
                <span class="text-3xl">🤝</span>
            </div>
            
        </div>
        
        <!-- PANTALLA 4: Resultado (Mensaje final) --><div id="screen-result" class="hidden text-center">
            <h2 id="result-title" class="rpg-title text-xl mb-4 text-[#8b5cf6]"></h2>
            <p id="result-message" class="text-lg mb-8 text-gray-300"></p>
            <div id="confession-text" class="mt-8 bg-gray-800 p-4 rounded-lg text-sm italic text-gray-400 hidden">
                 <!-- Aquí se puede poner un mensaje de amor personal o un poema corto --></div>
            <!-- Botón ahora llama a changeScreen(5) si acepta, o termina si rechaza --><button id="result-button" onclick="location.reload()" class="btn-primary w-full bg-[#dc2626] text-white py-3 rounded-lg text-lg font-bold uppercase tracking-wider mt-6">
                Terminar Sesión
            </button>
        </div>
        
        <!-- PANTALLA 5: Animación Final (Tulipanes y Brillos) --><div id="screen-animation" class="hidden text-center flex flex-col items-center justify-center min-h-[300px]">
            <h2 class="rpg-title text-xl mb-8 text-[#facc15]">¡Nuestra Aventura ha Comenzado!</h2>
            
            <!-- Contenedor para los tulipanes con el efecto de brillo --><div class="tulip-container mb-10">
                <!-- 
                    *** URL PERMANENTE APLICADA ***
                    Esta URL es la que me has proporcionado y ahora debería mostrar el ramo retro.
                --><img src="https://i.postimg.cc/VdWpZJrt/tulips-retro.png" alt="Ramo de Tulipanes Retro">
                
                <!-- Capa de brillo con estrellas animadas (se generan por JS) --><div id="shimmer-layer" class="shimmer-effect"></div>
            </div>
            
            <p class="text-gray-300 text-lg mb-8">¡Ahora empieza nuestro juego de verdad!</p>
            <button onclick="location.reload()" class="btn-primary w-full bg-[#34d399] text-gray-900 py-3 rounded-lg text-lg font-bold uppercase tracking-wider">
                AQUI EMPIEZA TU NUEVA HISTORIA
            </button>
        </div>
        
        <!-- Mensaje Modal de Alerta (Reemplazo de alert()) --><div id="modal" class="fixed inset-0 bg-black bg-opacity-75 hidden flex justify-center items-center p-4 z-50">
            <div class="bg-[#161b22] p-6 rounded-lg border-2 border-[#f97316] w-full max-w-xs text-center shadow-lg">
                <h3 id="modal-title" class="text-xl font-bold text-[#f97316] mb-3"></h3>
                <p id="modal-message" class="text-gray-300 mb-4"></p>
                <button onclick="document.getElementById('modal').classList.add('hidden')" class="bg-gray-600 text-white px-4 py-2 rounded">Cerrar</button>
            </div>
        </div>
        
    </div>
</body>
</html>
