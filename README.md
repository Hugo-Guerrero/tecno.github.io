<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Google Play Store - Descargar App</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background-color: #f0f2f5;
        }
        
        /* Utilidades */
        .hide-scrollbar::-webkit-scrollbar { display: none; }
        .hide-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        .text-play-green { color: #01875f; }
        .bg-play-green { background-color: #01875f; }
        
        /* Contenedor Móvil */
        .mobile-container {
            max-width: 480px;
            margin: 0 auto;
            background-color: white;
            min-height: 100vh;
            position: relative;
            box-shadow: 0 0 20px rgba(0,0,0,0.1);
            overflow: hidden; 
        }

        /* Animación de carga circular */
        @keyframes spin { to { transform: rotate(360deg); } }
        .loading-spinner {
            border: 3px solid #e5e7eb;
            border-top: 3px solid #01875f;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
        }

        /* Animación de transición entre vistas */
        .view-section {
            transition: transform 0.3s ease-in-out, opacity 0.3s;
            width: 100%;
            position: absolute;
            top: 0;
            left: 0;
            min-height: 100vh;
            background: white;
            z-index: 10;
        }
        
        .view-hidden-right { transform: translateX(100%); opacity: 0; pointer-events: none; }
        .view-hidden-left { transform: translateX(-100%); opacity: 0; pointer-events: none; }
        .view-active { transform: translateX(0); opacity: 1; pointer-events: auto; position: relative; }

        /* Barra de progreso de descarga */
        .progress-bar-container {
            width: 100%;
            height: 4px;
            background-color: #e0e0e0;
            position: absolute;
            top: 0;
            left: 0;
            display: none;
        }
        .progress-bar-fill {
            height: 100%;
            background-color: #01875f;
            width: 0%;
            transition: width 0.2s;
        }
    </style>
</head>
<body>

    <div class="mobile-container">
        
        <!-- ================= VISTA 1: HOME ================= -->
        <div id="home-view" class="view-section view-active pb-20">
            <!-- Header Home -->
            <div class="sticky top-0 z-40 bg-white pt-3 pb-2 px-4 shadow-sm">
                <div class="flex items-center bg-gray-100 rounded-full px-4 py-3 shadow-sm border border-gray-200 cursor-pointer">
                    <i class="fa-solid fa-bars text-gray-600 text-lg"></i>
                    <input type="text" placeholder="Buscar apps y juegos" class="bg-transparent border-none outline-none ml-4 flex-grow text-gray-700 text-sm">
                    <div class="w-7 h-7 rounded-full bg-purple-600 flex items-center justify-center text-white font-bold text-xs ml-2">A</div>
                </div>
                <!-- Tabs -->
                <div class="flex mt-3 space-x-6 overflow-x-auto hide-scrollbar border-b border-gray-100">
                    <button class="whitespace-nowrap pb-2 px-1 border-b-2 border-[#01875f] text-[#01875f] font-medium text-sm">Para ti</button>
                    <button class="whitespace-nowrap pb-2 px-1 text-gray-500 font-medium text-sm">Más populares</button>
                    <button class="whitespace-nowrap pb-2 px-1 text-gray-500 font-medium text-sm">Infantiles</button>
                </div>
            </div>

            <!-- Contenido Home -->
            <div class="overflow-y-auto">
                <!-- App Destacada (Lleva al detalle) -->
                <div class="p-4 border-b border-gray-100 cursor-pointer" onclick="goToAppDetail()">
                    <div class="relative rounded-xl overflow-hidden shadow-lg h-48 bg-gray-800 group">
                        <div class="absolute inset-0 flex items-center justify-center bg-gradient-to-r from-green-800 to-teal-900">
                            <i class="fa-brands fa-android text-7xl text-white opacity-20 group-hover:scale-110 transition duration-500"></i>
                        </div>
                        <div class="absolute bottom-0 left-0 p-4 bg-gradient-to-t from-black/90 via-black/50 to-transparent w-full">
                            <h2 class="text-white font-bold text-xl mb-1">Mi Súper Aplicación</h2>
                            <div class="flex items-center text-gray-300 text-xs mb-2">
                                <span>Herramientas</span> • <span class="flex items-center ml-1"><i class="fa-solid fa-star text-[10px] mr-1"></i> 5.0</span>
                            </div>
                            <div class="flex space-x-2">
                                <span class="bg-[#01875f] text-white px-6 py-1.5 rounded-md font-medium text-sm shadow-md">Ver detalles</span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Lista de Apps Sugeridas -->
                <div class="pt-2 px-5 pb-4">
                    <h3 class="font-medium text-lg text-gray-900 mb-3">Sugerencias para ti</h3>
                    <div class="flex overflow-x-auto hide-scrollbar space-x-4 pb-2">
                        <!-- App 1 -->
                        <div class="flex flex-col w-24 flex-shrink-0" onclick="goToAppDetail()">
                            <div class="w-24 h-24 rounded-2xl bg-gray-100 mb-2 overflow-hidden relative shadow-sm">
                                <i class="fa-brands fa-android text-4xl text-green-600 absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2"></i>
                            </div>
                            <span class="text-xs text-gray-900 font-medium truncate">App Debug</span>
                            <span class="text-xs text-gray-500">45 MB</span>
                        </div>
                         <!-- App 2 -->
                         <div class="flex flex-col w-24 flex-shrink-0">
                            <div class="w-24 h-24 rounded-2xl bg-blue-50 mb-2 flex items-center justify-center shadow-sm">
                                <i class="fa-solid fa-cube text-3xl text-blue-400"></i>
                            </div>
                            <span class="text-xs text-gray-900 font-medium truncate">Tools Pro</span>
                            <span class="text-xs text-gray-500">12 MB</span>
                        </div>
                        <!-- App 3 -->
                        <div class="flex flex-col w-24 flex-shrink-0">
                            <div class="w-24 h-24 rounded-2xl bg-orange-50 mb-2 flex items-center justify-center shadow-sm">
                                <i class="fa-solid fa-music text-3xl text-orange-400"></i>
                            </div>
                            <span class="text-xs text-gray-900 font-medium truncate">Music Player</span>
                            <span class="text-xs text-gray-500">28 MB</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Navbar Inferior -->
            <div class="fixed bottom-0 max-w-[480px] w-full bg-white border-t border-gray-200 flex justify-around items-center h-16 z-50">
                <button class="flex flex-col items-center justify-center w-full h-full text-[#01875f]">
                    <i class="fa-solid fa-gamepad text-xl mb-1"></i>
                    <span class="text-[10px] font-medium">Juegos</span>
                </button>
                <button class="flex flex-col items-center justify-center w-full h-full text-gray-400">
                    <i class="fa-solid fa-layer-group text-xl mb-1"></i>
                    <span class="text-[10px] font-medium">Apps</span>
                </button>
                <button class="flex flex-col items-center justify-center w-full h-full text-gray-400">
                    <i class="fa-solid fa-book text-xl mb-1"></i>
                    <span class="text-[10px] font-medium">Libros</span>
                </button>
            </div>
        </div>

        <!-- ================= VISTA 2: DETALLE APP (LANDING) ================= -->
        <div id="detail-view" class="view-section view-hidden-right overflow-y-auto pb-10">
            <!-- Header Detalle -->
            <div class="sticky top-0 bg-white z-40 flex items-center px-4 py-3 shadow-sm">
                <button onclick="goBack()" class="mr-4 text-gray-700 p-1">
                    <i class="fa-solid fa-arrow-left text-xl"></i>
                </button>
                <div class="flex-grow"></div>
                <i class="fa-solid fa-magnifying-glass text-gray-600 text-lg mr-5"></i>
                <i class="fa-solid fa-ellipsis-vertical text-gray-600 text-lg"></i>
                
                <!-- Barra de progreso oculta -->
                <div id="download-progress" class="progress-bar-container">
                    <div id="progress-fill" class="progress-bar-fill"></div>
                </div>
            </div>

            <!-- Info Principal -->
            <div class="px-5 py-4">
                <div class="flex mb-6">
                    <div class="w-20 h-20 rounded-xl bg-gray-900 flex items-center justify-center flex-shrink-0 shadow-md">
                        <!-- ICONO DE LA APP -->
                        <i class="fa-brands fa-android text-4xl text-green-400"></i>
                    </div>
                    <div class="ml-5 flex flex-col justify-center">
                        <h1 class="text-xl font-bold text-gray-900 leading-tight mb-1">App Debug - Versión Beta</h1>
                        <a href="#" class="text-[#01875f] font-medium text-sm mb-1">Developer Inc.</a>
                        <span class="text-xs text-gray-500">Contiene anuncios • Compras en la app</span>
                    </div>
                </div>

                <!-- Estadísticas -->
                <div class="flex justify-between items-center mb-6 px-2 border-r border-gray-100">
                    <div class="flex flex-col items-center flex-1 border-r border-gray-200">
                        <div class="flex items-center font-bold text-gray-800 text-sm">
                            4.5 <i class="fa-solid fa-star text-[10px] ml-1"></i>
                        </div>
                        <span class="text-[10px] text-gray-500 mt-1">1K reseñas</span>
                    </div>
                    <div class="flex flex-col items-center flex-1 border-r border-gray-200">
                        <div class="flex items-center font-bold text-gray-800 text-sm">
                            15 MB
                        </div>
                        <span class="text-[10px] text-gray-500 mt-1">Tamaño</span>
                    </div>
                    <div class="flex flex-col items-center flex-1">
                        <div class="flex items-center font-bold text-gray-800 text-sm">
                            10K+
                        </div>
                        <span class="text-[10px] text-gray-500 mt-1">Descargas</span>
                    </div>
                </div>

                <!-- Botón Instalar -->
                <div class="w-full mb-6">
                    <button id="install-btn" onclick="startDownload()" class="w-full bg-[#01875f] active:bg-[#016e4d] text-white font-medium py-2.5 rounded-lg shadow-sm transition-all flex justify-center items-center">
                        Instalar
                    </button>
                    <!-- Enlace oculto para la descarga real -->
                    <a id="download-link" href="aplicacion/tecno.apk" download class="hidden">

                    </a>
                </div>

                <!-- Carrusel de Screenshots -->
                <div class="flex overflow-x-auto hide-scrollbar space-x-3 mb-6">
                    <!-- Screenshot 1 -->
                    <div class="w-28 h-48 bg-gray-200 rounded-lg flex-shrink-0 flex items-center justify-center border border-gray-300">
                        <i class="fa-solid fa-image text-gray-400 text-2xl"></i>
                    </div>
                    <!-- Screenshot 2 -->
                    <div class="w-28 h-48 bg-gray-200 rounded-lg flex-shrink-0 flex items-center justify-center border border-gray-300">
                        <i class="fa-solid fa-image text-gray-400 text-2xl"></i>
                    </div>
                    <!-- Screenshot 3 -->
                    <div class="w-28 h-48 bg-gray-200 rounded-lg flex-shrink-0 flex items-center justify-center border border-gray-300">
                        <i class="fa-solid fa-image text-gray-400 text-2xl"></i>
                    </div>
                </div>

                <!-- Acerca de -->
                <div class="mb-6">
                    <div class="flex justify-between items-center mb-2">
                        <h3 class="font-bold text-gray-900 text-base">Sobre esta app</h3>
                        <i class="fa-solid fa-arrow-right text-gray-500 text-sm"></i>
                    </div>
                    <p class="text-sm text-gray-600 leading-relaxed">
                        Esta es una versión de prueba (Debug) de nuestra aplicación. Descárgala para probar las últimas funcionalidades, correcciones de errores y mejoras de rendimiento antes del lanzamiento oficial.
                    </p>
                </div>

                <!-- Tags -->
                <div class="flex flex-wrap gap-2 mb-6">
                    <span class="px-3 py-1 rounded-full border border-gray-300 text-xs font-medium text-gray-600">Herramientas</span>
                    <span class="px-3 py-1 rounded-full border border-gray-300 text-xs font-medium text-gray-600">Productividad</span>
                    <span class="px-3 py-1 rounded-full border border-gray-300 text-xs font-medium text-gray-600">Beta</span>
                </div>

                 <!-- Calificaciones y opiniones -->
                 <div>
                    <h3 class="font-bold text-gray-900 text-base mb-4">Calificaciones y opiniones</h3>
                    
                    <!-- Review 1 -->
                    <div class="mb-4">
                        <div class="flex items-center mb-1">
                            <div class="w-8 h-8 rounded-full bg-purple-500 text-white flex items-center justify-center text-xs font-bold mr-3">M</div>
                            <span class="text-sm font-medium">María González</span>
                        </div>
                        <div class="flex items-center mb-1">
                            <i class="fa-solid fa-star text-xs text-[#01875f]"></i>
                            <i class="fa-solid fa-star text-xs text-[#01875f]"></i>
                            <i class="fa-solid fa-star text-xs text-[#01875f]"></i>
                            <i class="fa-solid fa-star text-xs text-[#01875f]"></i>
                            <i class="fa-solid fa-star text-xs text-[#01875f]"></i>
                            <span class="text-xs text-gray-400 ml-2">14/02/24</span>
                        </div>
                        <p class="text-xs text-gray-600">¡Funciona excelente! La descarga fue rápida y la instalación muy sencilla.</p>
                    </div>
                 </div>

            </div>
        </div>

    </div>

    <script>
        const homeView = document.getElementById('home-view');
        const detailView = document.getElementById('detail-view');

        // Navegación: Ir al detalle
        function goToAppDetail() {
            homeView.classList.remove('view-active');
            homeView.classList.add('view-hidden-left');
            
            detailView.classList.remove('view-hidden-right');
            detailView.classList.add('view-active');
            
            // Scroll al top
            window.scrollTo(0,0);
        }

        // Navegación: Volver atrás
        function goBack() {
            detailView.classList.remove('view-active');
            detailView.classList.add('view-hidden-right');
            
            homeView.classList.remove('view-hidden-left');
            homeView.classList.add('view-active');
        }

        // Lógica de Descarga Simulada + Real
        function startDownload() {
            const btn = document.getElementById('install-btn');
            const progressContainer = document.getElementById('download-progress');
            const progressFill = document.getElementById('progress-fill');
            const link = document.getElementById('download-link');
            
            // Evitar múltiples clics
            if (btn.disabled) return;

            // 1. Estado "Pendiente"
            btn.disabled = true;
            btn.innerHTML = '<span class="text-gray-500">Pendiente...</span>';
            btn.classList.remove('bg-[#01875f]', 'text-white');
            btn.classList.add('bg-gray-100', 'border', 'border-gray-200');

            // 2. Simulación de descarga (Barra de progreso)
            progressContainer.style.display = 'block';
            
            let width = 0;
            const interval = setInterval(() => {
                if (width >= 100) {
                    clearInterval(interval);
                    finishDownload();
                } else {
                    width += Math.random() * 5; // Velocidad aleatoria
                    progressFill.style.width = width + '%';
                    
                    // Mostrar porcentaje en botón
                    if(width < 90) {
                        btn.innerHTML = <span class="text-xs text-[#01875f] font-bold">${Math.round(width)}% de 15 MB</span>;
                    } else {
                        btn.innerHTML = <span class="text-xs text-[#01875f] font-bold">Instalando...</span>;
                    }
                }
            }, 100);

            function finishDownload() {
                // 3. Descarga completada
                progressContainer.style.display = 'none';
                
                // Cambiar botón a "Abrir"
                btn.innerHTML = 'Abrir';
                btn.classList.remove('bg-gray-100', 'text-[#01875f]', 'border', 'border-gray-200');
                btn.classList.add('bg-[#01875f]', 'text-white', 'shadow-md');
                btn.disabled = false;
                
                // Cambiar la función del botón para que ahora "abra" la app (o recargue)
                btn.onclick = function() {
                    alert("Abriendo la aplicación...");
                };

                // 4. TRIGGER DE LA DESCARGA REAL
                // Esto intenta descargar el archivo 'app-debug.apk' si existe
                try {
                    link.click();
                    showToast("Descarga iniciada: app-debug.apk");
                } catch (e) {
                    console.error("Error al descargar", e);
                }
            }
        }

        function showToast(msg) {
            const toast = document.createElement('div');
            toast.className = 'fixed bottom-10 left-1/2 transform -translate-x-1/2 bg-gray-800 text-white px-4 py-2 rounded-full text-xs shadow-lg z-50 transition-opacity duration-500';
            toast.innerText = msg;
            document.body.appendChild(toast);
            setTimeout(() => {
                toast.style.opacity = '0';
                setTimeout(() => toast.remove(), 500);
            }, 3000);
        }
    </script>
</body>
</html>
