---
pandoc-render-cmd: pandoc -s index.md --template stamon-template.html -o index.html
css: 'https://cdn.jsdelivr.net/npm/water.css@2/out/dark.min.css'
extra-css: './src/stamonica.css'
lang: 'pt-BR'
title: 'Associação de Moradores do Parque Santa Mônica'
subtitle: 'São Carlos - SP'
logo: './src/logo.png'
favicon: './favicon.ico'
footer: True
morad-page: True
leaflet: True
---

## Comunicados e orientações{#comunicados}

<!--<details style="margin-bottom: 1em;" open=""> <summary class="summary-closed">Comunicados anteriores</summary>-->
Comunicados:
  <ul style="margin-bottom: 1.5em;">
  <li><a href="./media/comunicados2022/comunicado20220110.pdf">Janeiro/2022 -- Projetos e ações realizados em 2021 e futuras</a></li>
  <li><a href="./media/comunicados2022/comunicado-acoes2021.pdf">10/Janeiro/2022 -- Reajuste na contribuição mensal</a></li>
  <li><a href="./media/comunicados2022/comunicado20220201.pdf">01/Fevereiro/2022 -- Ações iniciadas em 2022</a></li>
  </ul>
<!--</details>-->

Orientações (clique no item para detalhar):
<details> <summary class="summary-closed">Como se associar</summary>
<p>Para se associar, basta preencher a ficha (<a href="./associacao-de-moradores.html#associe-se" target="_blank">clique aqui</a>) e aguardar o contato da Associação.</p>
</details>

<details> <summary class="summary-closed">Para comunicar necessidade de manutenção, como poste da rua com luz queimada, mato da praça alto, ou outros</summary>
<p>Por favor preencha a ficha: [clique aqui](#avisar-ocorrencias).</p>
</details>

<details> <summary class="summary-closed">Sugestões de segurança</summary>
<ul>
  <li> Realize manutenção preventiva em sua cerca elétrica;</li>
  <li> Chame o vigia para auxiliá-lo na entrada e saida da residência;</li>
  <li> Caso veja uma atitude suspeita, comunique o vigilante e a polícia.</li>
</ul>
</details>

<details> <summary class="summary-closed">Descarte de podas de jardinagem</summary>
<ul>
  <li> Podas pequenas podem ser ensacadas e colocadas junto ao lixo residencial;</li>
  <li> Podas maiores devem ser destinadas aos ecopontos da cidade (veja mais detalhes [clicando aqui](http://www.saocarlos.sp.gov.br/index.php/servicos-publicos/170833-relacao-ecopontos-saocarlos.html){rel="noopener noreferrer nofollow" target="_blank"});</li>
  <li> Oriente os jardineiros à, **por favor, não jogar nada nos bosques**, pois a decomposição natural não é rápida o suficiente, podendo provocar a proliferação de insetos que retornarão às casas e elevar o risco de queimadas, colocando em risco a saúde dos moradores e transeuntes.</li>
</ul>
</details>

[↥ _Retornar ao menu_](#logo)


## Previsão do tempo{#tempo}

<figure style="text-align: center; overflow:hidden;">
  <img class="previsao" src="https://s0.cptec.inpe.br/grafico/Modelos/WRF/GHT/meteogramas/PPN/4774.png" alt="Previsão do tempo temporariamente fora do ar">
</figure>

[Clique aqui](https://www.ipmetradar.com.br/2animRadar.php){rel="noopener noreferrer nofollow" target="_blank"} para ver a chuva em tempo real (Fonte: IPMET/UNESP)

[↥ _Retornar ao menu_](#logo)


## Reportar ocorrências{#avisar-ocorrencias}
_Por favor, use o formulário abaixo para reportar ocorrências, como lixeiras do bosque cheias, árvore em risco de queda, entre outros. Selecione a opção no menu "Encontrei" e indique o local no campo de texto. Em seguida pressione o botão de enviar._

<form action="https://formspree.io/f/mjvlrrwn" method="POST" id="ocorrencias" target="_blank">
<label>Encontrei:
<select name="ocorrencia" id="ocorrencia" required="required">
 <option value="null">Clique aqui para selecionar o tipo</option>
 <option value="lixeira">Lixeira cheia</option>
 <option value="mato">Mata dos bosques ou praça muito grande</option>
 <option value="arvore">Árvore em risco de queda</option>
 <option value="patrimonio">Patrimônio (lixeira, banco, etc) danificado</option>
 <option value="site">Problema no site</option>
 <option value="outros">Outros (por favor, informe nas observações)</option>
</select></label>
<label>Observações:
    <textarea type="text" name="message" id="message" rows="2" placeholder="Por favor indique a localização e outras informações que julgar pertinentes..." required="required"></textarea>
</label>
 <button type="submit" style="margin-right: auto; margin-top: 0.5em; display: block;">> Enviar <</button>
</form>

[↥ _Retornar ao menu_](#logo)


## Mapa interativo{#mapa}

<div id="map"></div>
<script>
    var reciclagem = L.layerGroup();

    var mbAttr = '<a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> + <a href="https://www.mapbox.com/">Mapbox</a>';
	var mbUrl = 'https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw';

	var streets = L.tileLayer(mbUrl, {id: 'mapbox/streets-v11', tileSize: 512, zoomOffset: -1, attribution: mbAttr});
	var navigation = L.tileLayer(mbUrl, {id: 'mapbox/navigation-day-v1', tileSize: 512, zoomOffset: -1, attribution: mbAttr});

    var map = L.map('map', {
		center: [-22.013138, -47.905626],
		zoom: 15,
		layers: [streets, reciclagem]
	});

    var baseLayers = {
		'Ruas': streets,
		'Trânsito': navigation,
	};

	var overlays = {
		'Reciclagem': reciclagem,
	};

	var layerControl = L.control.layers(baseLayers, overlays,{collapsed:false}).addTo(map);

	var marker = L.marker([-22.015438, -47.906544]).addTo(map)
		.bindPopup('Ponto de coleta de pilhas, esponjas e óleo de cozinha<br>Esquina da Rua Alexandre Fleming com Av. Dr. Paulo Pinheiro Werneck<br>(<a href="geo:0,0?q=R.+Alexandre+Fleming,+1+-+Parque+Santa+Monica,+São+Carlos+-+SP,+13561-232">Clique aqui para ver no GPS</a>)').addTo(reciclagem).openPopup()

<!--	function onMapClick(e) {-->
<!--		popup-->
<!--			.setLatLng(e.latlng)-->
<!--			.setContent('You clicked the map at ' + e.latlng.toString())-->
<!--			.openOn(map);-->
<!--	}-->
<!--	map.on('click', onMapClick);-->

</script>

[↥ Retornar ao menu](#logo)




