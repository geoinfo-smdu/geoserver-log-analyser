# Analisador de logs do GeoServer

Conjunto de scripts e notebooks para analisar logs do GeoServer

## Motivação

Recebemos frequentemente logs dos Servidores de GeoServer e precisamos fazer analises quantitativas e qualitativas para tomarmos decisões sobre planejamento de infraestrutura e novas camadas.

## Arquivos de log Recebidos

Recebemos os arquivos de log separados por servidor e por dia. Eles contem linhas como a linha de exemplo a seguir:

`127.0.0.1 - - [11/Nov/2019:06:43:37 -0200] "GET /geoserver/geoportal/wms?hc=XXXXXXX-XXXXXXXX-XXXXXXX&LAYERS=geoportal:v_logradouro_segmento&FORMAT=image/png&TRANSPARENT=TRUE&STYLES=line.Logradouro.CamadaLabel&SERVICE=WMS&VERSION=1.1.1&REQUEST=GetMap&SRS=EPSG:31983&BBOX=342223.77784638,7393166.1781994,342707.61784638,7393549.6381994&WIDTH=1728&HEIGHT=1369 HTTP/1.1" 200 198686 0.641 641 610`

## Método

Inicialmente vamos usar o Pandas para tablular todos os logs e podermo então gerar as análises. Simplesmente extraindo as linhas para um DataFrame, e posteriormente fazer as análises. Os campos que já temos possibilidade de definir são os seguintes:

* Data/hora
* URL
* Status da resposta HTTP
* Tamanho da resposta
* Tempo da resposta

Através da [extração de parâmetros da URL](https://stackoverflow.com/questions/33288420/extracting-url-parameters-into-pandas-dataframe) ainda temos os seguintes campos relevantes entre muitos outros parâmetros possíveis:

* ID de usuário único
* Layer
* Formato
* Serviço
* Bounding Box (Informação geográfica)
* Tamanho/Resolução de tela