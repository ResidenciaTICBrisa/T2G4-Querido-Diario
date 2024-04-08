# **Arquitetura do Querido Diário**

A arquitetura do **Querido Diário** é um reflexo das decisões técnicas que conectam duas pontas: o conjunto de soluções necessárias para enfrentar os obstáculos impostos pela disponibilização de diários oficiais e o interesse pela abertura destes dados. Assim, podemos resumir o fluxo do projeto para cada um dos tipos de diário oficial às etapas abaixo e compreendê-los mais detalhadamente a seguir: 

- **Coletar:** obter arquivos de diários oficiais na fonte, os sites publicadores
- **Processar:** aplicar tratamentos sobre os arquivos originais obtidos
- **Disponibilizar:** permitir acesso e pesquisa nos conteúdos armazenados

Sendo assim, o processo de extração de texto possui o seguinte fluxo: 

1. Spiders coletam os arquivos e metadados, que são salvos no PostgreSQL e o arquivo no Sistema de Arquivos. 
2. Diariamente, um job do data processing busca no PostgreSQL quais os arquivos que ainda não foram processados - existe uma flag na base para isso.
3. O job baixa o arquivo original.
4. O job manda o arqiuvo original para o Apache Tika e obtém o texto puro.
5. O job grava um arquivo txt no Sistema de Arquivos com o texto puro junto ao arquivo original.
6. O job grava, no index do motor de busca (opensearch), um novo registro contendo os metadados, o texto do documento e url de acesso tanto do arquivo original quanto do arquivo .txt.
7. O job marca o registro do diário processado no PostgreSQL como "feito".

Uma vez que os registros estão no OpenSearch, a API consegue buscar por eles. Assim, a API traduz a requisição que ele recebe em um query no Opensearch e retorna o resultado para o usuário. 

## **Jornada do Dado**

O processo de deduzir a **Jornada do Dado** envolve entender e mapear como os dados se movem e são processados em um sistema ou aplicação, desde sua origem até seu destino final, o que geralmente envolve identificar todas as etapas pelas quais os dados passam, as transformações que sofrem e as interações com diferentes componentes do sistema ao longo do caminho.

Esta jornada pode incluir várias etapas, como coleta, processamento, armazenamento, análise, visualização e distribuição. O objetivo é compreender como os dados são criados ou capturados, como são manipulados e transformados ao longo do tempo e como são usados para fornecer valor ou insights para os usuários finais. Ao deduzir a jornada do dado, os profissionais podem identificar possíveis pontos de falha, gargalos de desempenho, oportunidades de otimização e requisitos de segurança. Isso ajuda a garantir que os dados sejam gerenciados de forma eficiente, confiável e segura em todo o ciclo de vida da informação.

Sendo assim, a Jornada do Dado dentro do projeto do Querido Diário está representada na imagem abaixo: 
____________________________________________________________________________________________________________
<img src="./imagens/fluxo_dados2.png"/>
<h5 style="text-align: center; margin: 0 auto">Figura 1: Arquitetura do projeto Querido Diário</h5>

____________________________________________________________________________________________________________


### **Jornada do Dado na funcionalidade F1**

<p>A funcionalidade 1 trabalha a área do front-end, onde será necessário manipular dados que aparecem na página após o resultado de uma pesquisa, seja ela a página do Querido Diário Geral ou do Querido Diário Educação, transformando-os em arquivos .csv para download. A figura abaixo descreve melhor dentro da arquitetura geral do projeto a área de influência da funcionalidade.</p>
<p>Para esta funcionalidade também foi criado um <a href="https://www.figma.com/file/PTRrSgLiz6DOlkYwA3Tt6Q/Prot%C3%B3tipo-para-a-p%C3%A1gina-%22Tecnologia-na-Educa%C3%A7%C3%A3o%22?type=design&node-id=0%3A1&mode=design&t=86esN6klke9ftwbL-1">protótipo no Figma</a> para a visualização da página, com a participação do cliente.</p>


<img src="./imagens/Fluxo-Us1-Us2.png"/>
<h5 style="text-align: center; margin: 0 auto">Figura 2: Fluxo de dados da funcionalidade 1</h5>



<!-- 

### **Jornada do Dado na fucionalidade F2**

inserir o fluxo de dados da funcionalidade F@

-->


## Histórico de Versão

| Versão |    Data    |                                 Descrição                                 |                                             Responsáveis                                             |                         Revisor                         |
| :----: | :--------: | :-----------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------: | :-----------------------------------------------------: |
|  1.0   | 25/03/2024 |             Criação da página "Arquitetura do Querido Diário"             |                        [Raissa Oliveira](https://github.com/raissamsoliveira)                        |       [Ester Lino](https://github.com/esteerlino)       |
|  1.1   | 04/04/2024 |  Adicionando o fluxo de dados da funcionalidade F1 e legenda das figuras  | [Cristian Furtado](https://github.com/csafurtado) e [Pedro Cabeceira](https://github.com/pkbceira03) | [Wildemberg Sales](https://github.com/wildemberg-sales) |
|  1.2   | 05/04/2024 | Adiciona informação e link sobre o protótipo do Figma da funcionalidade 1 |                          [Cristian Furtado](https://github.com/csafurtado)                           | [Raissa Oliveira](https://github.com/raissamsoliveira)  |
|  1.3   | 08/04/2024 |                              Revisão textual                              |                    [Arthur Ferreira](https://github.com/ArthurFerreiraRodrigues)                     |                                                         |