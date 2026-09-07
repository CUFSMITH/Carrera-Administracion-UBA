<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lic. en Administración - Panel Interactivo</title>
    <style>
        :root {
            --primary: #d97736;
            --primary-dark: #b85e23;
            --bg-color: #fdfbf7;
            --card-bg: #ffffff;
            --text-main: #333333;
            --approved-bg: #d1e7dd;
            --approved-text: #0f5132;
            --available-bg: #cfe2ff;
            --available-text: #084298;
            --locked-bg: #e2e3e5;
            --locked-text: #6c757d;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 20px;
            user-select: none;
        }

        header {
            text-align: center;
            margin-bottom: 20px;
        }

        h1 {
            color: var(--primary);
            margin-bottom: 5px;
        }

        /* Barra de progreso */
        .progress-container {
            max-width: 600px;
            margin: 0 auto 20px auto;
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            height: 25px;
            box-shadow: inset 0 1px 3px rgba(0,0,0,0.2);
            position: relative;
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #28a745, #20c997);
            width: 0%;
            transition: width 0.4s ease;
        }

        .progress-text {
            position: absolute;
            width: 100%;
            text-align: center;
            top: 3px;
            font-weight: bold;
            font-size: 0.85rem;
            color: #333;
            text-shadow: 0 0 2px #fff;
        }

        .stats {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }

        .stat-box {
            background: white;
            padding: 8px 15px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
            border-left: 4px solid var(--primary);
            font-size: 0.95rem;
        }

        .legend {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
            font-size: 0.85rem;
        }

        .color-dot {
            width: 15px;
            height: 15px;
            border-radius: 3px;
        }

        .section-title {
            background-color: var(--primary);
            color: white;
            text-align: center;
            padding: 10px;
            border-radius: 6px;
            margin: 30px auto 20px auto;
            max-width: 1200px;
            font-size: 1.1rem;
            letter-spacing: 1px;
        }

        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(170px, 1fr));
            gap: 12px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .materia {
            background-color: var(--card-bg);
            border: 2px solid #ccc;
            border-radius: 8px;
            padding: 10px;
            text-align: center;
            cursor: pointer;
            transition: transform 0.1s ease, box-shadow 0.1s ease;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            min-height: 75px;
            position: relative;
            overflow: hidden;
        }

        .materia:active {
            transform: scale(0.95);
        }

        .materia .codigo {
            font-size: 0.7rem;
            background: #eee;
            padding: 2px 5px;
            border-radius: 4px;
            align-self: center;
            margin-top: 4px;
            color: #666;
        }

        .materia .nombre {
            font-weight: 600;
            font-size: 0.8rem;
            line-height: 1.1;
        }

        /* Estados de las materias */
        .materia.locked {
            background-color: var(--locked-bg);
            color: var(--locked-text);
            border-color: #b0bec5;
            opacity: 0.6;
            cursor: not-allowed;
        }

        .materia.available {
            background-color: var(--available-bg);
            color: var(--available-text);
            border-color: #9ec5fe;
        }

        .materia.available:hover {
            border-color: #0d6efd;
            box-shadow: 0 0 10px rgba(13, 110, 253, 0.4);
        }

        .materia.approved {
            background-color: var(--approved-bg);
            color: var(--approved-text);
            border-color: #badbcc;
            text-decoration: line-through;
        }

        .materia.approved .codigo {
            background: #a3cfbb;
            color: #051b11;
        }

        /* Efecto de disparo del minijuego */
        @keyframes shootEffect {
            0% { background-color: #ff4d4d; transform: scale(1.05); filter: brightness(1.5); }
            50% { background-color: #ffff66; transform: scale(0.95); }
            100% { background-color: var(--approved-bg); transform: scale(1); }
        }

        .materia.shooting {
            animation: shootEffect 0.3s ease;
        }

        /* Mira láser temporal en el impacto */
        .impact-crosshair {
            position: absolute;
            color: red;
            font-weight: bold;
            font-size: 1.5rem;
            pointer-events: none;
            animation: fadeOut 0.4s forwards;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        @keyframes fadeOut {
            0% { opacity: 1; transform: translate(-50%, -50%) scale(0.5); }
            100% { opacity: 0; transform: translate(-50%, -50%) scale(1.5); }
        }

        .notes {
            max-width: 800px;
            margin: 40px auto 20px auto;
            background: #fff3cd;
            border: 1px solid #ffeeba;
            padding: 15px;
            border-radius: 6px;
            font-size: 0.85rem;
            color: #856404;
        }

        .reset-btn {
            display: block;
            margin: 20px auto;
            padding: 8px 16px;
            background-color: #dc3545;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.9rem;
        }

        .reset-btn:hover {
            background-color: #bb2d3b;
        }
    </style>
</head>
<body>

    <header>
        <h1>Licenciatura en Administración</h1>
        <p>¡Dispara a tus materias aprobadas para avanzar en la carrera!</p>
    </header>

    <!-- Barra de Progreso -->
    <div class="progress-container">
        <div class="progress-bar" id="progress-bar"></div>
        <div class="progress-text" id="progress-text">0% Completado</div>
    </div>

    <div class="stats">
        <div class="stat-box">Aprobadas: <span id="count-approved">0</span></div>
        <div class="stat-box">Faltantes: <span id="count-missing">34</span></div>
        <div class="stat-box">Disponibles: <span id="count-available">0</span></div>
    </div>

    <div class="legend">
        <div class="legend-item"><div class="color-dot" style="background: var(--locked-bg); border: 1px solid #999;"></div> Bloqueada</div>
        <div class="legend-item"><div class="color-dot" style="background: var(--available-bg);"></div> ¡Disponible para disparar!</div>
        <div class="legend-item"><div class="color-dot" style="background: var(--approved-bg);"></div> ¡Aprobada!</div>
    </div>

    <!-- PRIMER TRAMO -->
    <div class="section-title">PRIMER TRAMO</div>
    <div class="grid-container" id="tramo-1"></div>

    <!-- SEGUNDO TRAMO -->
    <div class="section-title">SEGUNDO TRAMO</div>
    <div class="grid-container" id="tramo-2"></div>

    <button class="reset-btn" onclick="resetProgress()">Reiniciar Progreso</button>

    <div class="notes">
        <strong>Aclaraciones del plan:</strong>
        <ul>
            <li>Haz clic en las materias disponibles para "dispararles" y marcarlas como aprobadas.</li>
            <li>Si quieres desmarcar una materia aprobada, vuelve a hacerle clic.</li>
        </ul>
    </div>

    <script>
        const materiasData = [
            // Primer Tramo
            { id: 245, nombre: "ÁLGEBRA", tramo: 1, req: [] },
            { id: 241, nombre: "ANÁLISIS MATEMÁTICO 1", tramo: 1, req: [] },
            { id: 242, nombre: "ECONOMÍA", tramo: 1, req: [] },
            { id: 246, nombre: "HISTORIA ECON. Y SOC. GENERAL", tramo: 1, req: [] },
            { id: 252, nombre: "ADMINISTRACIÓN GENERAL", tramo: 1, req: [] },
            { id: 254, nombre: "SOCIOLOGÍA DE LAS ORGANIZACIONES", tramo: 1, req: [] },

            // Segundo Tramo
            { id: 248, nombre: "ESTADÍSTICA 1", tramo: 2, req: [245, 241, 242, 246, 252, 254] },
            { id: 247, nombre: "TEORÍA CONTABLE", tramo: 2, req: [245, 241, 242, 246, 252, 254] },
            { id: 250, nombre: "MICROECONOMÍA 1", tramo: 2, req: [245, 241, 242, 246, 252, 254] },
            { id: 463, nombre: "GESTIÓN DE TEC. DIGITALES", tramo: 2, req: [245, 241, 242, 246, 252, 254] },
            { id: 274, nombre: "SISTEMAS ADMINISTRATIVOS", tramo: 2, req: [245, 241, 242, 246, 252, 254] },
            { id: 462, nombre: "DERECHO EMPRESARIAL", tramo: 2, req: [245, 241, 242, 246, 252, 254] },

            { id: 276, nombre: "CÁLCULO FINANCIERO", tramo: 2, req: [248, 247, 241, 245] },
            { id: 464, nombre: "GESTIÓN DE COSTOS", tramo: 2, req: [247, 250] },
            { id: 278, nombre: "MACROECON. Y POLÍTICA ECON.", tramo: 2, req: [250, 242] },
            { id: 467, nombre: "GESTIÓN DEL TALENTO", tramo: 2, req: [252] },
            { id: 466, nombre: "ADMINISTRACIÓN DE OPERACIONES", tramo: 2, req: [252, 248] },
            
            { id: 465, nombre: "MÉTODO PREDICTIVOS P/ LA GESTIÓN", tramo: 2, req: [276, 248] },
            { id: 468, nombre: "ADMINISTRACIÓN TRIBUTARIA", tramo: 2, req: [278, 247] },
            { id: 279, nombre: "ADMINISTRACIÓN FINANCIERA", tramo: 2, req: [247, 276] },
            { id: 469, nombre: "MARKETING", tramo: 2, req: [466, 250] },

            { id: 470, nombre: "CIENCIAS DE LA DECISIÓN", tramo: 2, req: [465] },
            { id: 471, nombre: "PLANEAMIENTO ESTRATÉGICO", tramo: 2, req: [279] },

            { id: 472, nombre: "DIRECCIÓN", tramo: 2, req: [471, 469] },
            { id: 473, nombre: "PRÁCTICA PROFESIONAL", tramo: 2, req: [] },
            
            { id: 901, nombre: "OPTATIVA I (ORIENTADA)", tramo: 2, req: [] },
            { id: 902, nombre: "OPTATIVA II (ORIENTADA)", tramo: 2, req: [] },
            { id: 903, nombre: "OPTATIVA III (COMPETENCIA)", tramo: 2, req: [] }
        ];

        let approvedIds = JSON.parse(localStorage.getItem('admin_approved')) || [];

        function render() {
            const container1 = document.getElementById('tramo-1');
            const container2 = document.getElementById('tramo-2');
            container1.innerHTML = '';
            container2.innerHTML = '';

            let approvedCount = 0;
            let availableCount = 0;
            const totalMaterias = materiasData.length;
            const primerTramoCompleto = [245, 241, 242, 246, 252, 254].every(id => approvedIds.includes(id));

            materiasData.forEach(mat => {
                const isApproved = approvedIds.includes(mat.id);
                let isAvailable = false;

                if (isApproved) {
                    approvedCount++;
                } else {
                    if (mat.id === 473) {
                        isAvailable = approvedIds.length >= (totalMaterias - 5);
                    } else if (mat.tramo === 2 && mat.req.length === 6 && mat.req.includes(252)) {
                        isAvailable = primerTramoCompleto;
                    } else if (mat.req.length === 0) {
                        isAvailable = true;
                    } else {
                        isAvailable = mat.req.every(reqId => approvedIds.includes(reqId));
                    }

                    if (isAvailable) availableCount++;
                }

                const div = document.createElement('div');
                div.className = 'materia';
                if (isApproved) div.classList.add('approved');
                else if (isAvailable) div.classList.add('available');
                else div.classList.add('locked');

                div.innerHTML = `
                    <div class="nombre">${mat.nombre}</div>
                    <div class="codigo">${mat.id}</div>
                `;

                // Evento de disparo / clic
                div.onclick = (e) => {
                    // Si está bloqueada, sacude un poco o no hace nada
                    if (!isApproved && !isAvailable) {
                        return;
                    }

                    if (!isApproved) {
                        // Disparar efecto visual
                        div.classList.add('shooting');
                        const crosshair = document.createElement('div');
                        crosshair.className = 'impact-crosshair';
                        crosshair.innerHTML = '🎯';
                        div.appendChild(crosshair);

                        setTimeout(() => {
                            div.classList.remove('shooting');
                        }, 300);
                    }

                    toggleApprove(mat.id);
                };

                if (mat.tramo === 1) {
                    container1.appendChild(div);
                } else {
                    container2.appendChild(div);
                }
            });

            // Actualizar estadísticas y barra de progreso
            const missingCount = totalMaterias - approvedCount;
            const percentage = Math.round((approvedCount / totalMaterias) * 100);

            document.getElementById('count-approved').innerText = approvedCount;
            document.getElementById('count-missing').innerText = missingCount;
            document.getElementById('count-available').innerText = availableCount;

            const progressBar = document.getElementById('progress-bar');
            progressBar.style.width = percentage + '%';
            document.getElementById('progress-text').innerText = percentage + '% Completado (' + approvedCount + '/' + totalMaterias + ')';

            localStorage.setItem('admin_approved', JSON.stringify(approvedIds));
        }

        function toggleApprove(id) {
            if (approvedIds.includes(id)) {
                approvedIds = approvedIds.filter(item => item !== id);
            } else {
                approvedIds.push(id);
            }
            render();
        }

        function resetProgress() {
            if (confirm('¿Estás seguro de reiniciar todo tu progreso?')) {
                approvedIds = [];
                render();
            }
        }

        render();
    </script>
</body>
</html>
