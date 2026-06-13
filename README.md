<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Painel AgroSustentável - Monitoramento de Impacto</title>
    
    <style>
        /* --- VARIÁVEIS E CORES --- */
        :root {
            --primary: #2e7d32;       /* Verde Sustentabilidade */
            --secondary: #1565c0;     /* Azul Eficiência/Água */
            --warning: #ef6c00;       /* Laranja Alerta/Solo */
            --bg-dark: #1e293b;       /* Fundo Dark Moderno */
            --bg-card: #334155;       /* Fundo dos Cards */
            --text-light: #f8fafc;    /* Texto Claro */
            --text-muted: #94a3b8;    /* Texto Secundário */
            --accent: #ffb300;        /* Foco de Acessibilidade */
        }

        /* --- CONFIGURAÇÕES GERAIS --- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', system-ui, sans-serif;
            background-color: var(--bg-dark);
            color: var(--text-light);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* --- HEADER --- */
        .dash-header {
            background-color: #0f172a;
            padding: 1.5rem 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid var(--primary);
        }

        .dash-header h1 {
            font-size: 1.5rem;
            color: var(--text-light);
        }

        .dash-header h1 span {
            color: var(--primary);
        }

        .badge-live {
            background-color: var(--primary);
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: bold;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 0.6; }
            50% { opacity: 1; }
            100% { opacity: 0.6; }
        }

        /* --- LAYOUT DO PAINEL (CSS GRID) --- */
        .dash-container {
            flex: 1;
            padding: 2rem 5%;
            max-width: 1400px;
            width: 100%;
            margin: 0 auto;
            
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
        }

        /* --- CARDS DO DASHBOARD --- */
        .dash-card {
            background-color: var(--bg-card);
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            border-top: 4px solid var(--text-muted);
            transition: transform 0.2s;
        }

        .dash-card:hover {
            transform: translateY(-3px);
        }

        /* Customização das bordas por categoria */
        .card-agua { border-top-color: var(--secondary); }
        .card-solo { border-top-color: var(--warning); }
        .card-carbono { border-top-color: var(--primary); }

        .dash-card h2 {
            font-size: 1rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 10px;
        }

        .dash-data {
            font-size: 2.2rem;
            font-weight: bold;
            margin-bottom: 5px;
        }

        .dash-card p {
            font-size: 0.9rem;
            color: var(--text-muted);
        }

        /* --- INTERAÇÃO (BOTÃO DE ATUALIZAÇÃO) --- */
        .control-panel {
            grid-column: 1 / -1;
            display: flex;
            justify-content: flex-end;
            margin-bottom: 10px;
        }

        .btn-update {
            background-color: transparent;
            color: var(--primary);
            border: 2px solid var(--primary);
            padding: 10px 20px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s;
        }

        .btn-update:hover {
            background-color: var(--primary);
            color: var(--text-light);
        }

        .btn-update:focus {
            outline: 3px solid var(--accent);
        }

        /* --- RODAPÉ --- */
        .dash-footer {
            background-color: #0f172a;
            text-align: center;
            padding: 15px;
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-top: 40px;
        }
    </style>
</head>
<body>

    <header class="dash-header">
        <h1>Agro<span>Sustentável</span> | Monitor de Impacto</h1>
        <div class="badge-live" aria-live="polite">DADOS EM TEMPO REAL</div>
    </header>

    <main class="dash-container">
        
        <div class="control-panel">
            <button class="btn-update" id="btn-atualizar">Simular Atualização de Dados</button>
        </div>

        <section class="dash-card card-agua" aria-labelledby="title-agua">
            <h2 id="title-agua">Economia de Água</h2>
            <div class="dash-data" id="dado-agua">38%</div>
            <p>Redução no consumo via irrigação inteligente por gotejamento automatizado.</p>
        </section>

        <section class="dash-card card-solo" aria-labelledby="title-solo">
            <h2 id="title-solo">Uso de Defensivos</h2>
            <div class="dash-data" id="dado-solo">-24%</div>
            <p>Diminuição no uso de químicos devido ao monitoramento por drones e IA.</p>
        </section>

        <section class="dash-card card-carbono" aria-labelledby="title-carbono">
            <h2 id="title-carbono">Área Preservada</h2>
            <div class="dash-data" id="dado-carbono">4.2k ha</div>
            <p>Hectares de mata nativa monitorados e protegidos dentro das propriedades.</p>
        </section>

        <section class="dash-card card-carbono" aria-labelledby="title-carbono-cr">
            <h2 id="title-carbono-cr">Carbono Sequestrado</h2>
            <div class="dash-data" id="dado-carbono-cr">12.5t</div>
            <p>Toneladas de CO₂ retidas no solo através do plantio direto e rotação de culturas.</p>
        </section>

    </main>

    <footer class="dash-footer">
        <p>&copy; 2026 Dashboard AgroSustentável. Desenvolvido por Beatriz Restani | Interface Acessível e Responsiva.</p>
    </footer>

    <script>
        document.addEventListener("DOMContentLoaded", () => {
            const btnAtualizar = document.getElementById("btn-atualizar");
            
            // Elementos dos dados
            const dadoAgua = document.getElementById("dado-agua");
            const dadoSolo = document.getElementById("dado-solo");
            const dadoCarbonoCr = document.getElementById("dado-carbono-cr");

            btnAtualizar.addEventListener("click", () => {
                // Simula novos números vindo de sensores do campo
                const novaAgua = Math.floor(Math.random() * (45 - 30 + 1)) + 30;
                const novoSolo = Math.floor(Math.random() * (-15 - -35 + 1)) + -35;
                const novoCarbono = (Math.random() * (15 - 10) + 10).toFixed(1);

                // Atualiza a tela com os novos valores
                dadoAgua.textContent = `${novaAgua}%`;
                dadoSolo.textContent = `${novoSolo}%`;
                dadoCarbonoCr.textContent = `${novoCarbono}t`;

                // Efeito visual rápido para indicar mudança
                btnAtualizar.innerText = "Dados Atualizados!";
                setTimeout(() => {
                    btnAtualizar.innerText = "Simular Atualização de Dados";
                }, 1500);
            });
        });
    </script>
</body>
</html>
