<h1 align="center"> Projeto 1: 2º Semestre de 2021 </h1>

<div align="center"> Projeto Integrador - 1° Semestre | Fatec Prof. Jessen Vidal - 2021 | Cliente parceiro: Professor Fabiano Sabha </div>
<br>
<div align="center"><img align="center" src="https://github.com/fluffyfatec/SPanel/blob/main/Sprint_2/assets/logospanel3.png" width="60%" height="55%"></div>

<div align="center">
<br>

[Repositório](https://github.com/fluffyfatec/SPanel)
</div>

## Visão do Projeto

Com o intuito de melhorar e facilitar o acesso aos números da COVID-19 disponibilizados pelo Estado de São Paulo, o SPanel foi desenvolvido para que o usuário tenha acesso aos dados de forma simples e intuitiva. 

## Tecnologias adotadas na solução
<details>
<summary>Front-End</summary>

* [HTML5](https://www.w3schools.com/css/)
* [CSS3](https://www.w3schools.com/css/)

</details>

<details>
<summary>Back-End</summary>

* [Python](https://www.python.org/)

</details>

## Contribuições pessoais

<details>
<summary>Bot</summary>

### Leitura e Manipulação dos dados
Utilizei a biblioteca "Pandas" para ler e manipular os dados fornecidos pelo back-end, realiza algumas operações de manipulação de dados, como a soma de colunas específicas no DataFrame e a identificação da data mais recente no DataFrame.
Foi feita a formatação de números de casos, óbitos, população, para facilitar a leitura e apresentação no bot do Telegram.

### API do Telegram

Utilizei a biblioteca "pytelegrambotapi" para criar um bot do Telegram e definir comandos para diferentes funcionalidades.

* /drs: Apresenta dados do Departamento Regional de Saúde, incluindo ocupação de leitos, leitos de UTI, internações, etc.
* /obitos: Apresenta dados sobre óbitos, incluindo óbitos totais e novos óbitos.
* /imunizados: Apresenta dados sobre pessoas imunizadas.
* /casos: Apresenta dados sobre casos totais e novos casos.
* /pop: Apresenta a população do estado de São Paulo.
* /dados: Solicita ao usuário que escolha o que visualizar entre óbitos, imunizados e casos.
* /sobre: Fornece informações sobre o projeto SPanel, incluindo contatos e links.

</details>

## Aprendizados Efetivos

### Python

Este foi o meu primeiro contato com uma linguagem de programação, então aprendi os conceitos básicos como variáveis, funções, tipos de dados, formatação de strings e também tive minha primeira integração com uma API externa, e também tive me primeiro contato com bibliotecas e seus imports.

### Pandas

Neste projeto desenvolvi um Bot com a API do Telegram o qual foi necessario um tratamento e manipulação dos dados a serem repassados ao usuário, aqui aprendi todo o basico de pandas e manipulação dos dados com o mesmo.

### Github

Neste projeto tive também meu primeiro contato com o Github, onde pude aprender os comando básicos como Pull, Commit, Push.
