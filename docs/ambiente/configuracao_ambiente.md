# Configurando o ambiente

## Introdução
Este documento foi criado pelo Giulio em parceria com a nossa equipe, responsável pela evolução do Querido Diário.

O QD usa podman para sua infra. Para criar um ambiente onde todos os containers dos repos possam se comunicar, vamos começar montando um ambiente que possibilite toda essa integração.

## Repositório do querido-diario-data-processing

0. Instalar o pacote do podman (caso não esteja instalado)

```bash
sudo apt install podman
```

1. Execute  

``` bash
make build
```

2. No Makefile, mude a variável FULL_PROJECT para `true`

3. Para resolver o problema com o Apache Tika (caso seja a primeira instalção do projeto na máquina local), execute os comandos abaixo: 
``` bash
podman image rm --force localhost/okfn-brasil/querido-diario-apache-tika-server 
podman pull ghcr.io/okfn-brasil/querido-diario-apache-tika-server:latest 
make apache-tika-server
```

4. Execute

``` bash
make setup
```
### **Observação**

Ao executar o comando "make setup" pode ser que apareça o erro a seguir:

<img src="./imagens/Erro_porta8000.jpeg"/>
<h5 style="text-align: center; margin: 0 auto">Figura 1: Erro com a porta 8000</h5>

Nesse caso, a alternativa que foi encontrada para solucionar é executar o comando a seguir, o qual irá derrubar porta 8000.

``` bash
sudo kill -9 `sudo lsof -t -i:8000`
```
**Após a execução desse comando, executar novamente o "passo 4".**


#### Agora o pod foi criado, assim como vários recursos como Opensearch, Postgres e Minio. Porém, eles ainda estão vazios. Vamos populá-los.

## Repositório do querido-diario (raspadores)

1. Copie local.env do repo querido-diario para .env 

2. Configure o ambiente de desenvolvimento do repo querido-diario
   
``` bash
python3 -m venv .venv
source .venv/bin/activate
sudo apt-get install pre-commit
pip install --no-deps -r data\_collection/requirements-dev.txt
```

3. No repo querido-diario, abra a pasta "data_collection" e execute um raspador, por exemplo
   
``` bash
scrapy crawl sp_campinas -a start_date=2024-03-01
```

4. Execute no repo querido-diario-data-processing
   
``` bash
make re-run
```

#### Agora temos arquivos, tabelas e índices populados. Podemos habilitar a API.

## Repositório do querido-diario-api

1. Execute 
   
``` bash
make build
``` 

2. Execute 
   
``` bash
make re-run
```

#### Com a API disponível, podemos iniciar o backend local

## Repositório do querido-diario-backend

1. Configure o ambiente de desenvolvimento do repo querido-diario-backend
   
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements-dev.txt
python -m cli setup --pod-name querido-diario --migrate --superuser 
```

2. Faça o cadastro do superuser como pedido.

#### Com o backend disponível, o frontend que usa API e backend locais também pode ser configurado.

## Repositório do querido-diario-frontend

0. Instalar o pacote nvm (gerenciador de versões do node.js) e o yarn (gerenciador de pacotes do node) para instalar as dependências do projeto
```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh
source ~/.bashrc        # para aplicar o script de instalação do nvm ao bash

nvm install v16.2.0
npm install --global yarn
cd <raiz_do_repo_frontend>
yarn
``` 

1. Aplique esse patch no repo querido-diario-frontend

```bash
./src/app/constants.ts 
- export const API = 'https://queridodiario.ok.org.br/api'; 
+ export const API = 'http://localhost:8080';

./src/app/services/gazette/gazette.service.ts 
81 - const url = new URL( `/api/gazettes?${encodedQueryString}${territoryQuery}` ,  `https://queridodiario.ok.org.br` ).toString(); 
81 + const url = new URL( `/gazettes?${encodedQueryString}${territoryQuery}` ,  `http://localhost:8080` ).toString(); 

./src/app/services/utils/index.ts
- export const educationApi = 'https://backend-api.queridodiario.ok.org.br/api/'; 
+ export const educationApi = 'http://localhost:8000/api/'; 
```

2. Execute o ambiente de desenvolvimento de acordo com os passos descritos no README do repositório querido-diario-frontend.

Pronto! Agora o ambiente está todo configurado.

# Usando o ambiente

Algumas maneiras úteis de usar o ambiente de desenvolvimento:

1. Quer acessar o banco postgres para ver registros de diários oficiais, usuários do backend, etc.?<br>
    Execute `make shell-database` no repo querido-diario-data-processing e estará na linha de comando psql.

2. Quer acessar o motor de busca para ver os índices textuais de diários e excertos temáticos?<br>
    Execute `curl -k -u admin:admin -X GET "localhost:9200/\_cat/indices?v&pretty=true`
> Outros endpoints  funcionarão  igualmente  de  acordo  com  a  documentação  do  opensearch.

3. Quer acessar o sistema de arquivos para ver onde foram baixados?<br>
    Acesse  [localhost:9000](http://localhost:9000) com  as  credenciais localizadas  no  envvars do repo  querido-diario- data-processing.

4. Quer baixar mais arquivos de diários e processá-los?<br>
    Execute outro scrapy crawl no repo querido-diario e então execute `make re-run` no querido-diario-data-processing novamente. 

5. No frontend o live reload está habilitado e na API e backend não. Como checar as mudanças?<br>
    Na API, execute make re-run novamente. No backend, execute `python -m cli setup -- pod-name querido-diario`.

6. Como acessar a documentação da API?<br>
    Acesse [localhost:8080/docs](http://localhost:8080). 

7. Como acessar o painel de admin do backend?<br>
    Acesse [localhost:8000/api/admin](http://localhost:8080/api/admin) com as credenciais de superuser criadas anteriormente.

## Histórico de versão

| Versão |    Data    |             Descrição             |                              Responsáveis                               |                        Revisor                         |
| :----: | :--------: | :-------------------------------: | :---------------------------------------------------------------------: | :----------------------------------------------------: |
|  1.0   | 08/04/2024 | Criação da estrutura do documento |               [Ester Lino](https://github.com/esteerlino)               | [Raissa Oliveira](https://github.com/raissamsoliveira) |
|  1.1   | 08/04/2024 |       Revisão para release        | [Arthur Ferreira Rodrigues](https://github.com/ArthurFerreiraRodrigues) |      [Ester Lino](https://github.com/esteerlino)       |
|  1.2   | 23/04/2024 | Atualização do documento e inclusão do erro com a porta 8000 |               [Ester Lino](https://github.com/esteerlino)               | [Raissa Oliveira](https://github.com/raissamsoliveira) |
|  1.3   | 25/05/2024 | Atualização do documento incluindo detalhes do podman, apache tika, ordem dos comandos no raspador e comando para instalar o nvm |               [Cristian Furtado](https://github.com/csafurtado)               | [Ester Lino](https://github.com/esteerlino) |