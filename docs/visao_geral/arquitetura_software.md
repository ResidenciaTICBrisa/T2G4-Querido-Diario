# **Arquitetura do Querido Diário**

A arquitetura do **Querido Diário** é um reflexo das decisões técnicas que conectam duas pontas: o conjunto de soluções necessárias para enfrentar os obstáculos impostos pela disponibilização de diários oficiais e o interesse pela abertura destes dados. Assim, podemos resumir o fluxo do projeto para cada um dos tipos de diário oficial às etapas abaixo e compreendê-los mais detalhadamente a seguir: 

- **Coletar:** obter arquivos de diários oficiais na fonte, os sites publicadores
- **Processar:** aplicar tratamentos sobre os arquivos originais obtidos
- **Disponibilizar:** permitir acesso e pesquisa nos conteúdos armazenados

Sendo assim, o processo de extração de texto possui o seguinte fluxo: 

1. Spiders coletam os arquivos e metadados, que são salvos no portgresql e o arquivo no Sistema de Arquivos. 
2. Diariamente um job do data processing busca no postgresql quais os arquivos que ainda não foram processados - existe uma flag na base para isso.
3. O job baixa o arquivo original.
4. O job manda o arquvo original para o Apache Tika e obtem o texto puro.
5. O job grava um arquivo txt no Sistema de Arquivos com o texto puro junto ao arquivo original.
6. O job grava no index do motor de busca (opensearch) um novo registro contendo os metadados, o texto do documento e url de acesso tanto do arquivo original quanto do arquivo .txt.
7. O job marca o registro do diario processado no postgresql como "feito".

Uma vez que os registros estão no OpenSearch, a API consegue buscar por eles. Assim, a API traduz a requisição que ele recebe em um query no Opensearch e retorna o resultado para o usuário. 

### **Jornada do Dado**

____________________________________________________________________________________________________________
<img src="./imagens/fluxo_dados2.png"/>

____________________________________________________________________________________________________________

