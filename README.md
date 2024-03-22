# Querido Diário

<p align="center">
  <img src="./docs/imagens/mascote.webp" width="200px" />
</p>

Este repositório é destinado a documentação do processo de evolução de software do projeto de código aberto [Querido Diário](https://queridodiario.ok.org.br/).  
A seguir temos a lista de repositórios utilizados pelo time de desenvolvimento para a evolução deste software:

* [Front-End](https://github.com/Wildemberg-Projects/querido-diario-frontend)
* [Back-End](https://github.com/Wildemberg-Projects/querido-diario-backend)
* [API](https://github.com/Wildemberg-Projects/querido-diario-api)
* [Data Processing](https://github.com/Wildemberg-Projects/querido-diario-data-processing)
* [Raspadores](https://github.com/okfn-brasil/querido-diario)

## Contribuidores

| Foto | Nome | Github | Email |
| :--: | :--: | :----: | :---: |
| <img src="./docs/imagens/arthur-profile.jpg" width="150px" /> | Arthur Ferreira | [ArthurFerreiraRodrigues](https://github.com/ArthurFerreiraRodrigues) | arthur.250402@gmail.com |
| <img src="./docs/imagens/cristian.jpeg" width="150px" />  | Cristian Furtado | [csafurtado](https://github.com/csafurtado) | cristiansafurtado@gmail.com |
| <img src="./docs/imagens/ester.jpg" width="150px" /> | Ester Lino | [esteerlino](https://github.com/esteerlino) | esteerlino@gmail.com |
| <img src="./docs/imagens/pedro.webp" width="150px" /> | Pedro Cabeceira | [pkbceira03](https://github.com/pkbceira03) | cabeceira2003@gmail.com |
| <img src="./docs/imagens/raissa.webp" width="150px" />| Raissa Oliveira | [raissamsoliveira](https://github.com/raissamsoliveira) | raissa.menezesousa@gmail.com |
| <img src="./docs/imagens/will.jpeg" width="150px" /> | Wildemberg Sales | [wildemberg-sales](https://github.com/wildemberg-sales) | wildemberg.sales.junior@gmail.com | 

## Trabalhando com o MkDocs

O MkDocs é utilizado para a documentação interna do grupo sobre o trabalho no projeto Querido Diário. Abaixo estão as instruções para instalação e os prováveis comandos que você pode ter que usar ao trabalhar com MkDocs.

### Instalação

Além do MkDocs, é utilizado um tema baseado no Material Design, o MkDocs Material. Portanto, ele também será necessário ser instalado.

Para instalar o MkDocs e o MkDocs Material, você precisará do Python e do pip. Com esses dois instalados, você pode rodar o seguinte comando:

```bash
pip install mkdocs mkdocs-material
```

### Comandos

- `mkdocs serve` - Inicia o servidor de documentação com live-reload.
- `mkdocs build` - Gera a documentação estática.

#### Deploy

Não é necessário realizar o deploy manualmente, pois o deploy é feito automaticamente pelo GitHub Actions. A cada push na branch `master`, o GitHub Actions gera a documentação estática e a publica na branch `gh-pages`. A documentação estática pode ser acessada [aqui](https://residenciaticbrisa.github.io/T2G4-Querido-Diario/).
