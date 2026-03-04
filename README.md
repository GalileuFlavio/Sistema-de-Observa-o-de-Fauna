# Sistema-de-Observa-o-de-Fauna
Sistema de Observação de Fauna (Wildlife Observation System)

<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🌿 Wildlife Observation Tracker</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #e8f5e9 0%, #c8e6c9 100%);
            min-height: 100vh;
            color: #2d5016;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            padding: 40px 20px;
            background: linear-gradient(135deg, #43a047 0%, #2e7d32 100%);
            color: white;
            border-radius: 20px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .subtitle {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .card {
            background: white;
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.08);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border: 2px solid #e8f5e9;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.15);
        }

        .card-header {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
            font-size: 1.3em;
            font-weight: bold;
            color: #2d5016;
        }

        .card-icon {
            font-size: 2em;
            margin-right: 15px;
        }

        .observation-form {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        input, select, textarea {
            padding: 12px;
            border: 2px solid #c8e6c9;
            border-radius: 10px;
            font-size: 1em;
            transition: border-color 0.3s;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #43a047;
        }

        button {
            background: linear-gradient(135deg, #43a047 0%, #2e7d32 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 10px;
            font-size: 1.1em;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            font-weight: bold;
        }

        button:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 20px rgba(67, 160, 71, 0.4);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }

        .stat-item {
            background: #f1f8e9;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            border: 2px solid #dcedc8;
        }

        .stat-number {
            font-size: 2.5em;
            font-weight: bold;
            color: #43a047;
            display: block;
        }

        .stat-label {
            color: #689f38;
            font-size: 0.9em;
            margin-top: 5px;
        }

        .observation-list {
            max-height: 300px;
            overflow-y: auto;
        }

        .observation-item {
            background: #f1f8e9;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 10px;
            border-left: 4px solid #43a047;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .observation-info h4 {
            color: #2d5016;
            margin-bottom: 5px;
        }

        .observation-info p {
            color: #689f38;
            font-size: 0.9em;
        }

        .badge {
            background: #43a047;
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.8em;
            font-weight: bold;
        }

        .map-container {
            height: 300px;
            background: #e8f5e9;
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .map-placeholder {
            text-align: center;
            color: #689f38;
        }

        .animal-icon {
            position: absolute;
            font-size: 2em;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .animal-icon:hover {
            transform: scale(1.5);
        }

        footer {
            text-align: center;
            padding: 30px;
            color: #689f38;
            font-size: 0.9em;
        }

        .github-link {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            background: #333;
            color: white;
            padding: 12px 25px;
            border-radius: 25px;
            text-decoration: none;
            margin-top: 15px;
            transition: transform 0.3s;
        }

        .github-link:hover {
            transform: scale(1.05);
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }

        .floating {
            animation: float 3s ease-in-out infinite;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🌿 Wildlife Observation Tracker</h1>
            <p class="subtitle">Registre e monitore a fauna local de forma divertida! 🦉🦊🦌</p>
        </header>

        <div class="grid">
            <!-- Formulário de Observação -->
            <div class="card">
                <div class="card-header">
                    <span class="card-icon floating">📝</span>
                    <span>Nova Observação</span>
                </div>
                <form class="observation-form" id="observationForm">
                    <select id="species" required>
                        <option value="">Selecione a espécie 🦅</option>
                        <option value="Coruja">🦉 Coruja</option>
                        <option value="Raposa">🦊 Raposa</option>
                        <option value="Veado">🦌 Veado</option>
                        <option value="Urubu">🦅 Urubu</option>
                        <option value="Urso">🐻 Urso</option>
                        <option value="Lobo">🐺 Lobo</option>
                    </select>
                    <input type="text" id="location" placeholder="📍 Localização" required>
                    <input type="datetime-local" id="datetime" required>
                    <textarea id="notes" rows="3" placeholder="📝 Observações adicionais..."></textarea>
                    <button type="submit">✨ Registrar Observação</button>
                </form>
            </div>

            <!-- Estatísticas -->
            <div class="card">
                <div class="card-header">
                    <span class="card-icon">📊</span>
                    <span>Estatísticas</span>
                </div>
                <div class="stats-grid">
                    <div class="stat-item">
                        <span class="stat-number" id="totalObs">0</span>
                        <span class="stat-label">Total Observações</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-number" id="totalSpecies">0</span>
                        <span class="stat-label">Espécies Únicas</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-number" id="thisWeek">0</span>
                        <span class="stat-label">Esta Semana</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-number" id="rareCount">0</span>
                        <span class="stat-label">Avistamentos Raros</span>
                    </div>
                </div>
            </div>

            <!-- Mapa de Observações -->
            <div class="card">
                <div class="card-header">
                    <span class="card-icon">🗺️</span>
                    <span>Mapa de Observações</span>
                </div>
                <div class="map-container" id="mapContainer">
                    <div class="map-placeholder">
                        <p style="font-size: 3em;">🗺️</p>
                        <p>Mapa Interativo</p>
                    </div>
                </div>
            </div>

            <!-- Lista de Observações -->
            <div class="card">
                <div class="card-header">
                    <span class="card-icon">📋</span>
                    <span>Observações Recentes</span>
                </div>
                <div class="observation-list" id="observationList">
                    <p style="text-align: center; color: #999; padding: 20px;">
                        Nenhuma observação registrada ainda 🌱
                    </p>
                </div>
            </div>
        </div>

        <footer>
            <p>🌿 Projeto de Conservação da Fauna | Desenvolvido com 💚</p>
            <a href="#" class="github-link">
                <span>⭐</span>
                <span>Ver no GitHub</span>
            </a>
        </footer>
    </div>

    <script>
        // Dados iniciais
        let observations = JSON.parse(localStorage.getItem('observations')) || [];
        
        const rareSpecies = ['Urso', 'Lobo'];
        
        // Elementos DOM
        const form = document.getElementById('observationForm');
        const observationList = document.getElementById('observationList');
        const mapContainer = document.getElementById('mapContainer');
        
        // Atualizar estatísticas
        function updateStats() {
            document.getElementById('totalObs').textContent = observations.length;
            
            const uniqueSpecies = [...new Set(observations.map(o => o.species))];
            document.getElementById('totalSpecies').textContent = uniqueSpecies.length;
            
            const oneWeekAgo = new Date();
            oneWeekAgo.setDate(oneWeekAgo.getDate() - 7);
            const thisWeek = observations.filter(o => new Date(o.datetime) > oneWeekAgo);
            document.getElementById('thisWeek').textContent = thisWeek.length;
            
            const rare = observations.filter(o => rareSpecies.includes(o.species));
            document.getElementById('rareCount').textContent = rare.length;
        }
        
        // Renderizar lista
        function renderObservations() {
            if (observations.length === 0) {
                observationList.innerHTML = '<p style="text-align: center; color: #999; padding: 20px;">Nenhuma observação registrada ainda 🌱</p>';
                return;
            }
            
            observationList.innerHTML = observations
                .sort((a, b) => new Date(b.datetime) - new Date(a.datetime))
                .slice(0, 10)
                .map(obs => `
                    <div class="observation-item">
                        <div class="observation-info">
                            <h4>${getEmoji(obs.species)} ${obs.species}</h4>
                            <p>📍 ${obs.location} | 🕐 ${new Date(obs.datetime).toLocaleString('pt-BR')}</p>
                            ${obs.notes ? `<p style="margin-top: 5px; font-style: italic;">"${obs.notes}"</p>` : ''}
                        </div>
                        ${rareSpecies.includes(obs.species) ? '<span class="badge">⭐ RARO</span>' : ''}
                    </div>
                `).join('');
        }
        
        // Emoji helper
        function getEmoji(species) {
            const emojis = {
                'Coruja': '🦉',
                'Raposa': '🦊',
                'Veado': '🦌',
                'Urubu': '🦅',
                'Urso': '🐻',
                'Lobo': '🐺'
            };
            return emojis[species] || '🐾';
        }
        
        // Atualizar mapa
        function updateMap() {
            mapContainer.innerHTML = '';
            
            // Fundo do mapa
            const mapBg = document.createElement('div');
            mapBg.style.cssText = 'position: absolute; top: 0; left: 0; right: 0; bottom: 0; background: linear-gradient(135deg, #c8e6c9 0%, #a5d6a7 100%);';
            mapContainer.appendChild(mapBg);
            
            // Adicionar ícones de animais aleatórios
            observations.forEach((obs, index) => {
                const icon = document.createElement('div');
                icon.className = 'animal-icon';
                icon.textContent = getEmoji(obs.species);
                icon.style.left = Math.random() * 80 + 10 + '%';
                icon.style.top = Math.random() * 80 + 10 + '%';
                icon.title = `${obs.species} em ${obs.location}`;
                mapContainer.appendChild(icon);
            });
            
            if (observations.length === 0) {
                mapContainer.innerHTML = `
                    <div class="map-placeholder">
                        <p style="font-size: 3em;">🗺️</p>
                        <p>Mapa Interativo</p>
                    </div>
                `;
            }
        }
        
        // Submit form
        form.addEventListener('submit', (e) => {
            e.preventDefault();
            
            const newObservation = {
                id: Date.now(),
                species: document.getElementById('species').value,
                location: document.getElementById('location').value,
                datetime: document.getElementById('datetime').value,
                notes: document.getElementById('notes').value
            };
            
            observations.push(newObservation);
            localStorage.setItem('observations', JSON.stringify(observations));
            
            // Reset form
            form.reset();
            
            // Atualizar UI
            updateStats();
            renderObservations();
            updateMap();
            
            // Animação de sucesso
            alert(`🎉 ${newObservation.species} registrado com sucesso!`);
        });
        
        // Inicializar
        updateStats();
        renderObservations();
        updateMap();
    </script>
</body>
</html>
