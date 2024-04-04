# **Visão Geral do Produto**

## **Descrição do Produto**

### **O que é um diário oficial?**

O **diário oficial** é uma publicação feita pelas esferas da administração pública brasileira, seja federal, estadual ou municipal e dos poderes executivo, legislativo e judiciário, que serve para tornar oficial para a população as ações tomadas pelos poderes. Apesar de públicos, esses documentos são disponibilizados por vias difíceis de serem acompanhadas. 

### **O que é o Querido Diário?**

O **Querido Diário** é o projeto que enfrenta esse deserto de dados, oferecendo uma ferramenta que amplia o acesso à informação sobre a administração pública brasileira em sua mais local instância - os municípios -, através da abertura e centralização de diários oficiais eletrônicos. Não é uma empreitada fácil, sobretudo por existirem 5570 municípios no país e grandes discrepâncias quanto à existência e maturidade na disponibilização online de seus dados e informações.

## **Declaração do Problema**

Para este projeto foi proposto o desenvolvimento de rotinas de processamento de dados, criação de pontos de acesso na API e desenvolvimento de interfaces na plataforma web para atender as situações abaixo:

|                           |                                                                      | 
| ------------------------- | -------------------------------------------------------------------- |
|   **Como Jornalista**     | Conseguir realizar o download dos resultados da busca realizada na plataforma web do Querido Diário para sistematizar o processo de apuração de reportagens |
|  **Como Pesquisador(a)**  | Conseguir realizar o download dos textos completos dos diários oficiais, para realizar meus próprios recortes e processamentos de forma transversal |

<br>
<br>

Desta declaração, foram especificados quatro principais dores e pontos de melhoria apontados para o projeto:

| |
| ---- |
| 1. Funcionalidade de download de resultados de busca no [“Querido Diário”](https://queridodiario.ok.org.br/) e [“Querido Diário: Tecnologias na Educação”](https://queridodiario.ok.org.br/educacao) desenvolvida na interface da plataforma web; |
| 2. Desenvolvimento de rotina de agregação e compactação de arquivos de diários (em seu formato textual) em recortes geográficos e cronológicos (unidade federativa, município, ano, mês e dia) para disponibilização em sistema de arquivos em nuvem para download; |
| 3. Ponto de acesso na API do [Querido Diário](https://queridodiario.ok.org.br/api/docs) para listagem de URLs de arquivos de diários agregados e compactados disponíveis para download pelos recortes geográficos e cronológicos desejados; |
| 4. Página na plataforma web do projeto para download de diários oficiais em formato agregado e compactado pelos recortes geográficos e cronológicos desejados. |

## Histórico de Versão

| Versão |    Data    |                 Descrição                 |                                         Responsáveis                                         |                     Revisor                     |
| :----: | :--------: | :---------------------------------------: | :------------------------------------------------------------------------------------------: | :---------------------------------------------: |
|  1.0   | 25/03/2024 |     Criação da página sobre "Visão Geral do Produto"     |    [Raissa Oliveira](https://github.com/raissamsoliveira)            |    [Ester Lino](https://github.com/esteerlino)    |
|  1.1  | 04/04/2024 |     Adicionando tópicos do produto e colocamos as funcionalidades    | Pedro Cabecera e Cristian |    Ester e Raissa   |