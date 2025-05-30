<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mapa Interativo das Unidades Prisionais do Espírito Santo</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
    <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
    <style>
        #map { height: 600px; }
        body {
            background-color: #e3f2fd;
            color: #0d47a1;
            font-family: Arial, sans-serif;
            text-align: center;
        }
        h2 {
            color: #0d47a1;
        }
    </style>
</head>
<body>
    <h2>Mapa Interativo das Unidades Prisionais do Espírito Santo</h2>
    <div id="map"></div>
    <script>
        var map = L.map('map').setView([-19.1834, -40.3089], 8);

        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '© OpenStreetMap contributors'
        }).addTo(map);

        var cidades = [
            { nome: "Cariacica", lat: -20.2632, lon: -40.4165, unidades: [{ nome: "Penitenciária Feminina de Cariacica (PFC)", presos: 320 }] },
            { nome: "Cachoeiro de Itapemirim", lat: -20.8462, lon: -41.1198, unidades: [
                { nome: "Penitenciária Regional de Cachoeiro de Itapemirim (PRCI)", presos: 450 },
                { nome: "Centro Prisional Feminino de Cachoeiro de Itapemirim (CPFCI)", presos: 200 },
                { nome: "Centro de Detenção Provisória de Cachoeiro de Itapemirim (CDPCI)", presos: 500 }
            ]},
            { nome: "Vila Velha", lat: -20.3297, lon: -40.2922, unidades: [
                { nome: "Penitenciária Estadual de Vila Velha I (PEVV I)", presos: 700 },
                { nome: "Penitenciária Estadual de Vila Velha II (PEVV II)", presos: 650 },
                { nome: "Penitenciária Estadual de Vila Velha III (PEVV III)", presos: 600 },
                { nome: "Centro de Detenção Provisória de Vila Velha (CDPVV)", presos: 550 }
            ]},
            { nome: "Serra", lat: -20.121, lon: -40.307, unidades: [ { nome: "Centro de Detenção Provisória da Serra (CDPS)", presos: 700 } ] },
            { nome: "Linhares", lat: -19.3946, lon: -40.0643, unidades: [ { nome: "Centro de Detenção Provisória de Linhares (CDPL)", presos: 400 } ] },
            { nome: "São Mateus", lat: -18.7218, lon: -39.8574, unidades: [ { nome: "Centro de Detenção Provisória de São Mateus (CDPSM)", presos: 350 } ] },
            { nome: "Colatina", lat: -19.5399, lon: -40.6304, unidades: [ { nome: "Centro de Detenção Provisória de Colatina (CDPC)", presos: 450 } ] },
            { nome: "Guarapari", lat: -20.6772, lon: -40.5093, unidades: [ { nome: "Centro de Detenção Provisória de Guarapari (CDPG)", presos: 380 } ] },
            { nome: "Marataízes", lat: -21.0437, lon: -40.8381, unidades: [ { nome: "Centro de Detenção Provisória de Marataízes (CDPM)", presos: 300 } ] },
            { nome: "Aracruz", lat: -19.8202, lon: -40.2764, unidades: [ { nome: "Centro de Detenção Provisória de Aracruz (CDPA)", presos: 280 } ] },
            { nome: "São Domingos do Norte", lat: -19.145, lon: -40.628, unidades: [ { nome: "Centro de Detenção Provisória de São Domingos do Norte (CDPSDN)", presos: 330 } ] },
            { nome: "Barra de São Francisco", lat: -18.755, lon: -40.890, unidades: [ { nome: "Centro de Detenção Provisória de Barra de São Francisco (CDPBSF)", presos: 310 } ] },
            { nome: "Viana", lat: -20.3825, lon: -40.4931, unidades: [
                { nome: "Penitenciária Estadual de Viana I (PEV I)", presos: 750 },
                { nome: "Penitenciária Estadual de Viana II (PEV II)", presos: 700 },
                { nome: "Centro de Detenção Provisória de Viana (CDPV)", presos: 600 }
            ] }
        ];

        cidades.forEach(cidade => {
            var totalPresos = cidade.unidades.reduce((sum, unidade) => sum + unidade.presos, 0);
            var popupContent = `<b>${cidade.nome}</b><br>Quantidade de unidades: ${cidade.unidades.length}<br>Total de presos: ${totalPresos}<br><ul>`;
            cidade.unidades.forEach(unidade => {
                popupContent += `<li>${unidade.nome} - ${unidade.presos} presos</li>`;
            });
            popupContent += `</ul>`;
            L.circleMarker([cidade.lat, cidade.lon], {
                radius: 8,
                color: "#0d47a1",
                fillColor: "#2196f3",
                fillOpacity: 0.7
            }).addTo(map)
            .bindPopup(popupContent);
        });
    </script>
</body>
</html>
