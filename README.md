Okay, aquí tienes el código HTML completo con CSS y JavaScript, incluyendo la lista de los 40 productos y todas las funcionalidades especificadas en los prompts anteriores.

Este es un archivo `.html` autocontenido. Puedes copiar todo el contenido y guardarlo como un archivo `index.html` (o cualquier otro nombre con extensión `.html`) y abrirlo directamente en tu navegador web.

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Encuesta de Preferencia de Productos</title>
    <link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ctext y='.9em' font-size='90'%3E📊%3C/text%3E%3C/svg%3E">
    <style>
        /* Importa una fuente moderna de Google Fonts */
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap');

        /* Variables CSS para colores y estilos consistentes */
        :root {
            --primary-color: #6a11cb; /* Morado profundo */
            --secondary-color: #2575fc; /* Azul brillante */
            --text-color: #333; /* Gris oscuro para texto */
            --bg-light: #f8f9fa; /* Fondo muy claro */
            --bg-dark: #e9ecef; /* Fondo ligeramente oscuro */
            --shadow-light: rgba(0, 0, 0, 0.1); /* Sombra ligera */
            --border-radius: 12px; /* Bordes redondeados */
            --success-bg: #d4edda;
            --success-text: #155724;
            --info-bg: #ffe0b2;
            --info-text: #e65100;
            --error-bg: #f8d7da;
            --error-text: #721c24;
        }

        /* Estilos generales del cuerpo */
        body {
            font-family: 'Poppins', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
            color: var(--text-color);
            line-height: 1.6;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        /* Contenedor principal de la aplicación */
        .container {
            background-color: #ffffff;
            border-radius: var(--border-radius);
            box-shadow: 0 15px 40px var(--shadow-light);
            padding: 3rem;
            margin: 2rem;
            max-width: 960px; /* Ancho máximo para el contenido */
            width: 100%;
            box-sizing: border-box;
            transform: translateY(0);
            transition: transform 0.3s ease-out;
        }

        /* Encabezado de la aplicación */
        header {
            text-align: center;
            margin-bottom: 2.5rem;
        }

        header h1 {
            color: var(--primary-color);
            font-size: 2.8rem;
            margin-bottom: 0.7rem;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.05);
        }

        header p {
            color: #666;
            font-size: 1.15rem;
            max-width: 600px;
            margin: 0 auto;
        }

        /* Títulos de sección */
        .section-title {
            font-size: 2rem;
            color: var(--secondary-color);
            margin-bottom: 2rem;
            border-bottom: 3px solid var(--secondary-color);
            padding-bottom: 0.8rem;
            text-align: center;
            position: relative;
        }
        .section-title::after {
            content: '';
            display: block;
            width: 60px;
            height: 4px;
            background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
            position: absolute;
            bottom: -2px;
            left: 50%;
            transform: translateX(-50%);
            border-radius: 2px;
        }


        /* Listado de productos */
        .product-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 1.2rem;
            margin-bottom: 2.5rem;
        }

        .product-item {
            background-color: var(--bg-light);
            padding: 1.2rem;
            border-radius: var(--border-radius);
            border: 1px solid #e0e0e0;
            display: flex;
            align-items: flex-start; /* Alinea los ítems arriba */
            cursor: pointer;
            transition: all 0.2s ease-in-out;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        }

        .product-item:hover {
            border-color: var(--secondary-color);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
            transform: translateY(-4px);
        }

        .product-item input[type="checkbox"] {
            margin-right: 1rem;
            margin-top: 2px; /* Ajuste fino para la alineación */
            transform: scale(1.3);
            accent-color: var(--primary-color);
            min-width: 20px; /* Asegura un tamaño mínimo para el checkbox */
            min-height: 20px;
        }
        .product-item input[type="checkbox"]:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .product-item label {
            flex-grow: 1;
            cursor: pointer;
            font-weight: 500;
            color: var(--text-color);
            font-size: 1.05rem;
            line-height: 1.4;
        }

        /* Estilo para la opción "Otro" (Ítem 41) */
        #item41-container {
            background-color: var(--bg-dark);
            padding: 2rem;
            border-radius: var(--border-radius);
            margin-top: 2rem;
            border: 1px solid #ccc;
            box-shadow: 0 4px 15px rgba(0,0,0,0.07);
            transition: all 0.3s ease-in-out;
        }

        #item41-container.disabled {
            opacity: 0.6;
            pointer-events: none;
            background-color: #f0f0f0;
        }
        #item41-container.disabled label, #item41-container.disabled input {
            cursor: not-allowed;
        }


        #item41-container input[type="checkbox"] {
            margin-right: 0.8rem;
            transform: scale(1.3);
            accent-color: var(--primary-color);
        }

        #item41-container label[for="item41-checkbox"] {
            font-weight: 600;
            font-size: 1.1rem;
            display: inline-block;
            margin-bottom: 1rem;
            color: var(--primary-color);
        }

        #item41-input {
            width: calc(100% - 20px);
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 8px;
            margin-top: 0.8rem;
            box-sizing: border-box;
            font-size: 1rem;
            transition: border-color 0.2s ease-in-out;
        }
        #item41-input:focus {
            outline: none;
            border-color: var(--secondary-color);
            box-shadow: 0 0 0 3px rgba(37, 117, 252, 0.2);
        }

        /* Botón de envío */
        .vote-button {
            display: block;
            width: 100%;
            padding: 1.2rem 2.5rem;
            background: linear-gradient(45deg, var(--primary-color) 0%, var(--secondary-color) 100%);
            color: white;
            border: none;
            border-radius: var(--border-radius);
            font-size: 1.3rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 8px 25px rgba(0,0,0,0.2);
            margin-top: 3rem;
            letter-spacing: 0.5px;
        }

        .vote-button:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.3);
            filter: brightness(1.1);
        }
        .vote-button:active {
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        .vote-button:disabled {
            opacity: 0.7;
            cursor: not-allowed;
            background: linear-gradient(45deg, #a0a0a0, #b0b0b0);
            box-shadow: none;
            transform: none;
        }

        /* Mensajes de información/error */
        .info-message, .error-message, .success-message {
            padding: 1rem;
            border-radius: 8px;
            margin-bottom: 1.5rem;
            text-align: center;
            font-weight: 500;
            display: none; /* Oculto por defecto */
            font-size: 0.95rem;
            border: 1px solid transparent;
        }
        .info-message {
            background-color: var(--info-bg);
            color: var(--info-text);
            border-color: darken(var(--info-bg), 10%);
        }
        .error-message {
            background-color: var(--error-bg);
            color: var(--error-text);
            border-color: darken(var(--error-bg), 10%);
        }
        .success-message {
            background-color: var(--success-bg);
            color: var(--success-text);
            border-color: darken(var(--success-bg), 10%);
        }

        /* Sección de Resultados */
        #results-section {
            display: none; /* Oculta por defecto */
            animation: fadeIn 0.8s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .results-summary {
            background-color: var(--bg-dark);
            padding: 2rem;
            border-radius: var(--border-radius);
            text-align: center;
            margin-bottom: 2.5rem;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
        }

        .results-summary h3 {
            color: var(--primary-color);
            margin-bottom: 1rem;
            font-size: 1.8rem;
        }
        .results-summary p {
            color: #555;
            font-size: 1.05rem;
        }

        /* Lista de resultados individuales */
        .results-list .result-item {
            display: flex;
            flex-direction: column;
            margin-bottom: 1.2rem;
            background-color: var(--bg-light);
            padding: 1.2rem;
            border-radius: var(--border-radius);
            border: 1px solid #e0e0e0;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            transition: all 0.2s ease-in-out;
        }
        .results-list .result-item:hover {
            border-color: var(--primary-color);
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }

        .result-item-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.8rem;
            flex-wrap: wrap; /* Permite que los elementos se ajusten en móviles */
        }

        .result-item-name {
            font-weight: 600;
            flex-grow: 1;
            margin-right: 1.5rem;
            font-size: 1.1rem;
            color: var(--text-color);
        }

        .result-item-votes {
            font-size: 0.95rem;
            color: #555;
            white-space: nowrap;
            font-weight: 500;
        }

        .progress-bar-container {
            width: 100%;
            background-color: #eee;
            border-radius: 8px;
            overflow: hidden;
            height: 25px;
            position: relative;
            box-shadow: inset 0 1px 3px rgba(0,0,0,0.1);
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--secondary-color), var(--primary-color));
            width: 0%; /* Establecido por JS */
            border-radius: 8px;
            transition: width 0.7s ease-out; /* Animación más suave */
            display: flex;
            align-items: center;
            justify-content: flex-end;
            padding-right: 8px;
            box-sizing: border-box;
            position: relative; /* Para el porcentaje si se va fuera */
        }

        .progress-percentage {
            color: white;
            font-weight: 700;
            font-size: 0.85rem;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.4);
            white-space: nowrap;
            overflow: hidden; /* Oculta si el texto es muy largo */
        }
        .progress-bar[style*="width: 0%"] .progress-percentage {
            color: var(--text-color); /* Color para 0% */
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            text-shadow: none;
        }
        /* Asegura que el porcentaje esté visible si la barra es muy pequeña */
        .progress-bar:not([style*="width: 0%"]) .progress-percentage {
            position: absolute;
            right: 8px;
            color: white;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.4);
        }
        .progress-bar[style*="width: 0%"] .progress-percentage {
            color: var(--text-color); /* Color para 0% */
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            text-shadow: none;
        }
        .progress-bar[style*="width: 0%"] {
             background: none; /* No background if 0% */
        }


        /* Secciones de Top y Bottom Products */
        .top-bottom-products {
            display: flex;
            flex-wrap: wrap; /* Permite que los elementos se envuelvan */
            gap: 2.5rem;
            margin-top: 2.5rem;
            margin-bottom: 2.5rem;
            justify-content: center;
        }

        .top-bottom-section {
            flex: 1;
            min-width: 320px;
            max-width: 45%; /* Limita el ancho para que quepan dos en línea */
            background-color: var(--bg-light);
            padding: 2rem;
            border-radius: var(--border-radius);
            box-shadow: 0 5px 15px var(--shadow-light);
        }
        @media (max-width: 768px) {
            .top-bottom-section {
                max-width: 100%; /* Una columna en pantallas pequeñas */
            }
        }


        .top-bottom-section h4 {
            color: var(--primary-color);
            margin-bottom: 1.5rem;
            text-align: center;
            font-size: 1.5rem;
            border-bottom: 1px dashed #e0e0e0;
            padding-bottom: 0.8rem;
        }

        .top-bottom-section ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .top-bottom-section li {
            padding: 0.8rem 0;
            border-bottom: 1px solid #eee;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: 500;
            font-size: 1rem;
            color: #444;
        }

        .top-bottom-section li:last-child {
            border-bottom: none;
        }

        .top-bottom-section li .percentage {
            font-weight: 700;
            color: var(--secondary-color);
            font-size: 1.1rem;
        }


        /* Pie de página */
        footer {
            text-align: center;
            padding: 1.5rem;
            margin-top: 3rem;
            color: white;
            font-size: 0.9rem;
            opacity: 0.9;
        }

        /* Ajustes responsivos */
        @media (max-width: 768px) {
            .container {
                padding: 1.5rem;
                margin: 1rem;
            }

            header h1 {
                font-size: 2.2rem;
            }

            header p {
                font-size: 1rem;
            }

            .section-title {
                font-size: 1.7rem;
            }

            .product-list {
                grid-template-columns: 1fr;
            }

            .product-item {
                padding: 1rem;
            }

            #item41-container {
                padding: 1.5rem;
            }

            .vote-button {
                font-size: 1.1rem;
                padding: 1rem 1.5rem;
            }

            .results-summary {
                padding: 1.5rem;
            }

            .results-summary h3 {
                font-size: 1.5rem;
            }

            .result-item-name {
                font-size: 1rem;
                margin-right: 0.5rem;
            }

            .result-item-votes {
                font-size: 0.85rem;
            }

            .progress-bar-container {
                height: 20px;
            }

            .progress-percentage {
                font-size: 0.75rem;
            }
        }

        @media (max-width: 480px) {
            .container {
                margin: 0.5rem;
                padding: 1rem;
            }
            header h1 {
                font-size: 1.8rem;
            }
            .section-title {
                font-size: 1.4rem;
            }
            .product-item label {
                font-size: 0.95rem;
            }
            .top-bottom-section {
                padding: 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Encuesta de Preferencia de Productos</h1>
            <p>Selecciona tus 40 productos preferidos de la lista. Si deseas sugerir uno nuevo, usa la opción "Ítem 41: Otro".</p>
        </header>

        <main>
            <section id="voting-section">
                <h2 class="section-title">Elige tus Productos</h2>
                <div class="info-message" id="selection-info">Debes seleccionar exactamente 40 productos. Actualmente has seleccionado <span id="selected-count">0</span>.</div>
                <div class="error-message" id="error-message"></div>

                <div class="product-list" id="product-list">
                    </div>

                <div id="item41-container">
                    <input type="checkbox" id="item41-checkbox">
                    <label for="item41-checkbox">Ítem 41: Otro (Sugiere un producto alternativo)</label>
                    <input type="text" id="item41-input" placeholder="Escribe tu sugerencia aquí..." disabled>
                    <div class="info-message" style="display: block; margin-top: 15px; color: var(--info-text); background-color: var(--info-bg);">
                        Si seleccionas el "Ítem 41", este contará como una de tus 40 selecciones. Puedes usarlo para reemplazar uno de los productos de la lista principal.
                    </div>
                </div>

                <button class="vote-button" id="submit-vote">Enviar Voto</button>
            </section>

            <section id="results-section">
                <h2 class="section-title">Resultados de la Encuesta</h2>
                <div class="results-summary">
                    <h3>Total de Votantes Únicos Procesados: <span id="total-voters-count">0</span> de 354</h3>
                    <p>Estos resultados reflejan las preferencias y se actualizan con cada envío de voto.</p>
                </div>

                <div class="top-bottom-products">
                    <div class="top-bottom-section">
                        <h4>Top 5 Productos Más Votados</h4>
                        <ul id="top-products-list">
                            </ul>
                    </div>
                    <div class="top-bottom-section">
                        <h4>Top 5 Productos Menos Votados</h4>
                        <ul id="bottom-products-list">
                            </ul>
                    </div>
                </div>

                <h3 class="section-title" style="margin-top: 2.5rem;">Resultados Detallados por Producto</h3>
                <div class="results-list" id="full-results-list">
                    </div>
            </section>
        </main>
    </div>

    <footer>
        <p>&copy; 2025 Encuesta de Productos. Todos los derechos reservados.</p>
    </footer>

    <script>
        // Lista completa de los 40 productos
        const products = [
            "Extra Virgin Olive Oil (1 L)", "El Almendro Crunchy Almond 7.05 Oz 200",
            "knott Berry farm premium cookies raspber", "Oreo Sandwich Cookies, 30 Pk",
            "Kirkland Signature Spanish Queen Olives", "Paesana Organic Non Pareil Capers 22 oz",
            "Sun-Mail Raisins, 2.25 Lbs, 2-count", "Danish Butter Cookies, 4 Lbs",
            "Member's Mark honey 40 oz 390", "Kirkland signature sliced peaches",
            "Jif Creamy Peanut Butter 1 kilo", "Kraft parmesan grated cheese 24 oz",
            "Nutella Hazelnut Spread 26.5 oz", "HERSHEY'S Chocolate Syrup",
            "Kirkland signature extra fancy mixed nut", "Pringles Potato Crisps Chips, Variety",
            "Nature's eats shelled walnuts 3 Lbs", "Wonderful roasted salted pistachios",
            "Sutter Home California Pink Moscato", "Kirkland Signature Irish cream liqueur",
            "Kirkland Sangria (1.5 L)", "Chardonnay White wine 1.5 L",
            "Betty Crocker HershCey's fudge brownie", "Hershey Assorted Chocolate Miniatures",
            "Smucker Strawberry 4Lbs", "Frasco de Encurtidos",
            "Dulces de lechoza de 500gr C/U", "PAQUETE DE 6 U/N DE PANQUE ONCE ONCE",
            "RON SANTA TERESA LINAJE DE 0,75 Lts", "Panettone: Tan Rico",
            "Buchanan's DeLuxe Aged 12 Years", "Frasco de aceitunas de 21 oz",
            "Harina de maiz amarillo-marca Pan 4 KG", "Paquete de Hojas de Hallacas (50 UND C/)",
            "Pernil con Hueso", "Paquetes de Carne Pulpa Negra de 4Kg C/U",
            "Lomo de cerdo 4Kg.", "QUESO BOLA", "JAMON PLANCHADO", "PECHUGA DE GALLINA 4KG"
        ];

        // Constante para el total de votantes esperados (para cálculo de porcentajes)
        const TOTAL_VOTERS_EXPECTED = 354;

        // Referencias a elementos del DOM
        const productListDiv = document.getElementById('product-list');
        const item41Checkbox = document.getElementById('item41-checkbox');
        const item41Input = document.getElementById('item41-input');
        const item41Container = document.getElementById('item41-container');
        const submitVoteBtn = document.getElementById('submit-vote');
        const votingSection = document.getElementById('voting-section');
        const resultsSection = document.getElementById('results-section');
        const selectedCountSpan = document.getElementById('selected-count');
        const selectionInfo = document.getElementById('selection-info');
        const errorMessage = document.getElementById('error-message');
        const totalVotersCountSpan = document.getElementById('total-voters-count');
        const fullResultsList = document.getElementById('full-results-list');
        const topProductsList = document.getElementById('top-products-list');
        const bottomProductsList = document.getElementById('bottom-products-list');

        // Estado de la aplicación
        let selectedProducts = new Set(); // Almacena los IDs de los productos seleccionados en la sesión actual
        let voteCounts = initializeVoteCounts(); // Objeto para almacenar el conteo de votos por ítem
        let totalUniqueVoters = getInitialTotalVoters(); // Conteo total de votantes únicos que han enviado un voto

        /**
         * Inicializa el conteo de votos de cada producto desde localStorage.
         * Si no hay datos, inicializa en 0.
         */
        function initializeVoteCounts() {
            const storedVotes = JSON.parse(localStorage.getItem('voteCounts')) || {};
            const initialCounts = {};
            products.forEach((_, index) => {
                initialCounts[`item_${index + 1}`] = storedVotes[`item_${index + 1}`] || 0;
            });
            initialCounts['item_41'] = storedVotes['item_41'] || 0; // Para la opción "Otro"
            return initialCounts;
        }

        /**
         * Obtiene el conteo inicial de votantes únicos desde localStorage.
         */
        function getInitialTotalVoters() {
            return parseInt(localStorage.getItem('totalUniqueVoters') || '0');
        }

        /**
         * Guarda el conteo de votos y el total de votantes únicos en localStorage.
         */
        function saveVoteCounts() {
            localStorage.setItem('voteCounts', JSON.stringify(voteCounts));
            localStorage.setItem('totalUniqueVoters', totalUniqueVoters.toString());
        }

        /**
         * Renderiza la lista de productos en la sección de votación.
         */
        function renderProductList() {
            productListDiv.innerHTML = '';
            products.forEach((productName, index) => {
                const itemId = `item_${index + 1}`;
                const productItemDiv = document.createElement('div');
                productItemDiv.classList.add('product-item');
                productItemDiv.innerHTML = `
                    <input type="checkbox" id="${itemId}" value="${productName}">
                    <label for="${itemId}">${index + 1}. ${productName}</label>
                `;
                productListDiv.appendChild(productItemDiv);

                // Agrega el evento de escucha a cada checkbox
                productItemDiv.querySelector('input').addEventListener('change', updateSelection);
            });
        }

        /**
         * Actualiza el conjunto de productos seleccionados cuando un checkbox cambia.
         * También gestiona la lógica de deshabilitar/habilitar checkboxes si ya se han seleccionado 40.
         */
        function updateSelection(event) {
            const checkbox = event.target;
            const itemId = checkbox.id;

            if (checkbox.checked) {
                selectedProducts.add(itemId);
            } else {
                selectedProducts.delete(itemId);
            }

            updateSelectionInfo();
            validateSelectionCount(false); // Validar al instante, pero no mostrar error hasta el submit
        }

        /**
         * Actualiza el contador de productos seleccionados y el estado visual del mensaje de información.
         * Deshabilita/habilita checkboxes si se alcanzan 40 selecciones.
         */
        function updateSelectionInfo() {
            let currentSelections = selectedProducts.size;
            selectedCountSpan.textContent = currentSelections;

            // Actualiza el estilo del mensaje de información/error
            if (currentSelections === 40) {
                selectionInfo.classList.remove('info-message', 'error-message');
                selectionInfo.classList.add('success-message');
                selectionInfo.style.display = 'block';
            } else if (currentSelections > 40) {
                selectionInfo.classList.remove('info-message', 'success-message');
                selectionInfo.classList.add('error-message');
                selectionInfo.style.display = 'block';
            } else {
                selectionInfo.classList.remove('success-message', 'error-message');
                selectionInfo.classList.add('info-message');
                selectionInfo.style.display = 'block';
            }


            // Deshabilita o habilita todos los checkboxes si se llega a 40 selecciones
            const allProductCheckboxes = productListDiv.querySelectorAll('input[type="checkbox"]');
            const item41Checked = item41Checkbox.checked;

            allProductCheckboxes.forEach(cb => {
                // Deshabilita si ya hay 40 seleccionados y este no está marcado
                if (currentSelections >= 40 && !cb.checked) {
                    cb.disabled = true;
                } else {
                    cb.disabled = false;
                }
            });

            // Lógica específica para el Ítem 41
            if (currentSelections >= 40 && !item41Checked) {
                item41Checkbox.disabled = true;
                item41Container.classList.add('disabled');
            } else {
                item41Checkbox.disabled = false;
                // Solo quitar 'disabled' si no está marcado y aún no se llegó a 40 (o si se desmarcó)
                if (!item41Checked) {
                    item41Container.classList.remove('disabled');
                }
            }

            // Si el Ítem 41 está marcado, su input siempre debe estar habilitado
            item41Input.disabled = !item41Checked;
        }


        /**
         * Valida que se hayan seleccionado exactamente 40 productos y la sugerencia del Ítem 41 si aplica.
         * Muestra mensajes de error si la validación falla.
         * @param {boolean} showErrors - Si es true, muestra los mensajes de error en el DOM.
         */
        function validateSelectionCount(showErrors = true) {
            errorMessage.style.display = 'none'; // Oculta errores previos

            if (selectedProducts.size !== 40) {
                if (showErrors) {
                    errorMessage.textContent = `Error: Debes seleccionar exactamente 40 productos. Has seleccionado ${selectedProducts.size}.`;
                    errorMessage.style.display = 'block';
                }
                return false;
            }

            if (item41Checkbox.checked && item41Input.value.trim() === '') {
                if (showErrors) {
                    errorMessage.textContent = 'Error: Si seleccionas "Ítem 41: Otro", debes especificar tu sugerencia.';
                    errorMessage.style.display = 'block';
                }
                return false;
            }
            return true;
        }

        /**
         * Maneja el envío del voto.
         * Valida las selecciones, actualiza los conteos y cambia a la sección de resultados.
         */
        function handleSubmitVote() {
            if (!validateSelectionCount(true)) { // Muestra errores si falla la validación al enviar
                return;
            }

            // Se asume que cada envío es de un votante único para el total de 354
            totalUniqueVoters++;

            // Actualiza el conteo de votos para cada producto seleccionado
            selectedProducts.forEach(itemId => {
                if (itemId === 'item41-checkbox') {
                    voteCounts['item_41']++;
                } else {
                    voteCounts[itemId]++;
                }
            });

            saveVoteCounts(); // Guarda los datos actualizados
            renderResults(); // Renderiza la sección de resultados

            // Cambia la vista y resetea el formulario de votación
            votingSection.style.display = 'none';
            resultsSection.style.display = 'block';
            window.scrollTo({ top: 0, behavior: 'smooth' }); // Desplazarse al inicio de los resultados
            
            // Resetea el formulario para una nueva votación (opcional, para demo)
            resetVotingForm();
        }

        /**
         * Resetea el formulario de votación después de un envío.
         */
        function resetVotingForm() {
            productListDiv.querySelectorAll('input[type="checkbox"]').forEach(cb => {
                cb.checked = false;
                cb.disabled = false; // Habilitar todos los checkboxes de nuevo
            });
            item41Checkbox.checked = false;
            item41Input.value = '';
            item41Input.disabled = true;
            item41Container.classList.remove('disabled'); // Quitar estilo disabled del contenedor
            selectedProducts.clear();
            updateSelectionInfo(); // Actualiza el contador a 0
        }

        /**
         * Renderiza todos los resultados de la encuesta, incluyendo porcentajes, top y bottom.
         */
        function renderResults() {
            totalVotersCountSpan.textContent = totalUniqueVoters;
            fullResultsList.innerHTML = '';
            topProductsList.innerHTML = '';
            bottomProductsList.innerHTML = '';

            const allResults = [];

            // Añadir productos originales a los resultados
            products.forEach((productName, index) => {
                const itemId = `item_${index + 1}`;
                const votes = voteCounts[itemId] || 0;
                // El porcentaje se calcula sobre el total de votantes esperados (354)
                const percentage = TOTAL_VOTERS_EXPECTED > 0 ? ((votes / TOTAL_VOTERS_EXPECTED) * 100) : 0;
                allResults.push({ id: itemId, name: productName, votes: votes, percentage: parseFloat(percentage.toFixed(2)) });
            });

            // Añadir Ítem 41 a los resultados
            const item41Votes = voteCounts['item_41'] || 0;
            const item41Percentage = TOTAL_VOTERS_EXPECTED > 0 ? ((item41Votes / TOTAL_VOTERS_EXPECTED) * 100) : 0;
            allResults.push({ id: 'item_41', name: 'Ítem 41: Sugerencia (Otro Producto)', votes: item41Votes, percentage: parseFloat(item41Percentage.toFixed(2)) });

            // Ordenar todos los resultados para la lista completa (descendente por votos)
            allResults.sort((a, b) => b.votes - a.votes);

            allResults.forEach(item => {
                const resultItemDiv = document.createElement('div');
                resultItemDiv.classList.add('result-item');
                resultItemDiv.innerHTML = `
                    <div class="result-item-header">
                        <span class="result-item-name">${item.name}</span>
                        <span class="result-item-votes">${item.votes} votos (${item.percentage}%)</span>
                    </div>
                    <div class="progress-bar-container">
                        <div class="progress-bar" style="width: ${item.percentage > 100 ? 100 : item.percentage}%;">
                             ${item.percentage > 0 ? `<span class="progress-percentage">${item.percentage}%</span>` : ''}
                        </div>
                         ${item.percentage === 0 ? `<span class="progress-percentage" style="position: absolute; left: 50%; transform: translateX(-50%); color: #666; text-shadow: none;">0.00%</span>` : ''}
                    </div>
                `;
                fullResultsList.appendChild(resultItemDiv);
            });

            // Top 5 productos (ordenados por porcentaje, descendente)
            const sortedByPercentage = [...allResults].sort((a, b) => b.percentage - a.percentage);
            sortedByPercentage.slice(0, 5).forEach(item => {
                const listItem = document.createElement('li');
                listItem.innerHTML = `<span>${item.name}</span> <span class="percentage">${item.percentage}%</span>`;
                topProductsList.appendChild(listItem);
            });

            // Bottom 5 productos (ordenados por porcentaje, ascendente)
            // Se filtran los que tienen 0 votos si hay muchos para mostrar solo los que tienen algún voto si aplica,
            // o los de 0 si todos o la mayoría son 0.
            const sortedByPercentageAsc = [...allResults].sort((a, b) => a.percentage - b.percentage);
            const nonZeroVotes = sortedByPercentageAsc.filter(item => item.votes > 0);

            let bottomFive = [];
            if (nonZeroVotes.length >= 5) {
                bottomFive = nonZeroVotes.slice(0, 5); // Si hay al menos 5 con votos, coge los 5 más bajos con votos
            } else {
                // Si hay menos de 5 con votos, coge todos los que tienen votos y luego completa con los de 0 votos
                bottomFive = sortedByPercentageAsc.slice(0, 5);
            }

            if (bottomFive.length === 0) {
                 bottomProductsList.innerHTML = '<li>No hay votos registrados aún.</li>';
            } else {
                bottomFive.forEach(item => {
                    const listItem = document.createElement('li');
                    listItem.innerHTML = `<span>${item.name}</span> <span class="percentage">${item.percentage}%</span>`;
                    bottomProductsList.appendChild(listItem);
                });
            }
        }

        // --- Event Listeners ---
        item41Checkbox.addEventListener('change', () => {
            item41Input.disabled = !item41Checkbox.checked;
            if (item41Checkbox.checked) {
                selectedProducts.add('item41-checkbox');
                item41Container.classList.remove('disabled');
            } else {
                selectedProducts.delete('item41-checkbox');
                item41Input.value = ''; // Limpiar el input si se desmarca
            }
            updateSelectionInfo();
            validateSelectionCount(false); // Validar sin mostrar error hasta el submit
        });

        submitVoteBtn.addEventListener('click', handleSubmitVote);

        // --- Inicialización al cargar la página ---
        renderProductList(); // Carga la lista de productos en el DOM
        updateSelectionInfo(); // Actualiza el contador inicial (debe ser 0)
        renderResults(); // Renderiza los resultados iniciales (desde localStorage o 0)
    </script>
</body>
</html>
```
