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

<details>

<summary>Código</summary>

   ## Instalação da biblioteca pytelegrambotapi
        # Certifique-se de que a biblioteca está instalada usando o comando: pip install pytelegrambotapi
        #------Bibliotecas------#
        import telebot  # Importa a biblioteca para interação com a API do Telegram
        import pandas as pd  # Importa a biblioteca pandas para manipulação de dados
        #-----------------------#
        
  ## Chave de API para o bot no Telegram
        CHAVE_API = "2068198957:AAE46QIHyUk3AEy5hPcXR-_M0f-duqP_NZg"
        
  ## Leitura de dados de três arquivos CSV
        df = pd.read_csv("docs\df_estadotratado.csv")
        df_vs = pd.read_csv("docs\df_vacinastratado.csv")
        df_reg = pd.read_csv("docs\df_regiao_tratado.csv")
        
  ## Adiciona uma linha "Total" no DataFrame df_vs e calcula a soma de colunas específicas
        df_vs.loc["Total"] = df_vs.sum()
        column_sum = df_vs["Total_imunizados"] = df_vs["doseunica"] + df_vs["segundadose"]
        column_tt = df_vs["Total_imunizados"]
        max_vs = column_tt.max()
        
  ## Identifica a data mais recente no DataFrame df
        date_column = df["datahora"]
        max_value = date_column.max()
        row = df.loc[df["datahora"] == max_value]
        
  ## Tratamento do DataFrame df_regiao
        df_nreg = df_reg.loc[7181]
        df_reg = df_reg.drop(df_reg.columns[[0]], axis=1)
        
  ## Obtém dados mais atualizados sobre a Covid19
        lastDate = row["datahora"].values[0]
        cases = row["casos"].values[0]
        new_cases = row["casos_novos"].values[0]
        deaths = row["obitos"].values[0]
        new_deaths = row["obitos_novos"].values[0]
        population = row["pop"].values[0]
        ocupation_7d = df_nreg["ocupacao_leitos"]
        ocupation = df_nreg["ocupacao_leitos_ultimo_dia"]
        uti = df_nreg["total_covid_uti_ultimo_dia"]
        inter = df_nreg["internacoes_ultimo_dia"]
        inter_7d = df_nreg["internacoes_7d"]
        date_reg = df_nreg["datahora"]
        
   ## Formatação Numérica para melhor legibilidade
        form_cases = (f"{cases:_}")
        form_cases = form_cases.replace("_",".")
        form_ncases = (f"{new_cases:_}")
        form_ncases = form_ncases.replace("_",".")
        form_deaths = (f"{deaths:_}")
        form_deaths = form_deaths.replace("_",".")
        form_ndeaths = (f"{new_deaths:_}")
        form_ndeaths = form_ndeaths.replace("_",".")
        form_pop = (f"{population:_}")
        form_pop = form_pop.replace("_",".")
        form_vs = (f"{max_vs:_}")
        form_vs = form_vs.replace("_",".")
        form_uti = (f"{uti:_}")
        form_uti = form_uti.replace("_",".")
        form_inter = (f"{inter:_}")
        form_inter = form_inter.replace("_",".")
        form_inter7 = (f"{inter_7d:_}")
        form_inter7 = form_inter7.replace("_",".")
        
   ## Inicialização do bot do Telegram
        bot = telebot.TeleBot(CHAVE_API)
        
  ## Função que responde ao comando /drs
        @bot.message_handler(commands=["drs"])
        def drs(mensagem):
            bot.send_message(mensagem.chat.id, f"Dados do dia:  {date_reg}\n  \nOcupação de Leitos:  {ocupation}%\nOcupação de Leitos Ultimos 7 dias:   {ocupation_7d}%\n------------------------------------------------------------------\nLeitos de UTI para a COVID: {form_uti}\n------------------------------------------------------------------\nInternações confirmadas/suspeita: {form_inter}\nInternações nos ultimos 7 dias: {form_inter7}\n------------------------------------------------------------------\nPara ver dados da Covid19: /dados\nPara ver dados sobre a população: /pop\nPara ver sobre o projeto: /sobre. ")
        
   ## Função que responde ao comando /obitos
        @bot.message_handler(commands=["obitos"])
        def obitos(mensagem):
            bot.send_message(mensagem.chat.id, f"Dados do dia:  {lastDate}\n  \nÓbitos Totais:  {form_deaths}\n \nNovos óbitos:  {form_ndeaths}.\n------------------------------------------------------------------\nPara ver dados da Covid19: /dados\nPara ver dados sobre a população: /pop\nPara ver dados do Departamento Regional de Saúde /drs\nPara ver sobre o projeto: /sobre. ")
        
   ## Função que responde ao comando /imunizados
        @bot.message_handler(commands=["imunizados"])
        def imunizados(mensagem):
            bot.send_message(mensagem.chat.id, f"Dados do dia:  {lastDate}\n  \n Atualmente foram imunizadas: {form_vs} pessoas.\n-----------------------------------------------------------------------\n Para ver dados da Covid19: /dados\nPara ver dados sobre a população: /pop\nPara ver dados do Departamento Regional de Saúde /drs\nPara ver sobre o projeto: /sobre.")
        
  ## Função que responde ao comando /casos
        @bot.message_handler(commands=["casos"])
        def casos(mensagem):
            bot.send_message(mensagem.chat.id, f"Dados do dia:  {lastDate}\n  \nCasos Totais:  {form_cases}\n \nNovos casos: {form_ncases}\n---------------------------------------------------------------\nPara ver dados da Covid19: /dados\nPara ver dados sobre a população: /pop\nPara ver dados do Departamento Regional de Saúde /drs\nPara ver sobre o projeto: /sobre.")
        
  ## Função que responde ao comando /pop
        @bot.message_handler(commands=["pop"])
        def casos(mensagem):
            bot.send_message(mensagem.chat.id, f" Atualmente a população do estado de \nSão Paulo é de {form_pop} pessoas.\n-----------------------------------------------------------------------\nPara ver dados da Covid19: /dados\nPara ver dados do Departamento Regional de Saúde /drs\nPara ver sobre o projeto: /sobre.  ")
        
  ## Função que responde ao comando /dados
        @bot.message_handler(commands=["dados"])
        def opcao1(mensagem):
            texto =  f"O que você quer visualizar? (Clique em uma opção)\n-----------------------------------------------------------------------\n /obitos Óbitos\n/imunizados Imunizados\n/casos Casos"
            bot.send_message(mensagem.chat.id, texto)
        
  ## Função que responde ao comando /sobre
        @bot.message_handler(commands=["sobre"])
        def opcao2(mensagem):
            bot.send_message(mensagem.chat.id, f" SPanel é um projeto de estudantes da FATEC SJC que visa informar dados atualizados sobre a Covid19 no estado de São Paulo. Para mais informações entrar em contato via E-mail.\n ------------------------------------------------------------------ \nE-mail (fluffyfatec@gmail.com)\nGitHub (https://github.com/fluffyfatec)\n\nPara ver dados da Covid19: /dados\nPara ver dados sobre a população: /pop \nPara ver dados do Departamento Regional de Saúde /drs\n ------------------------------------------------------------------ \n")
        
  ## Função que sempre retorna True para qualquer mensagem
        def verificar(mensagem):
            return True
        
   ## Função que responde a qualquer mensagem com uma mensagem padrão
        @bot.message_handler(func=verificar)
        def responder(mensagem):
            texto = """Olá, eu sou o Bot do SPanel que te atualiza sobre os resultados da Covid19 no estado de São Paulo.
        
             Escolha uma opção para continuar (clique no item)
            
            /dados Visualizar dados da Covid19
            /drs Visualizar dados do Departamento Regional de Saúde
            /pop População do estado de São Paulo
            /sobre Sobre
            
            Qualquer outra opção não vai funcionar"""
            bot.reply_to(mensagem, texto)
        
  ## Inicia o bot e inicia o loop para responder às mensagens
        print("\n\n\033[32m-------Em execução-------\033[0;0m\n\n")
        bot.polling()


</details>
</details>

## Aprendizados Efetivos

### Python

Este foi o meu primeiro contato com uma linguagem de programação, então aprendi os conceitos básicos como variáveis, funções, tipos de dados, formatação de strings e também tive minha primeira integração com uma API externa, e também tive me primeiro contato com bibliotecas e seus imports.

### Pandas

Neste projeto desenvolvi um Bot com a API do Telegram o qual foi necessario um tratamento e manipulação dos dados a serem repassados ao usuário, aqui aprendi todo o basico de pandas e manipulação dos dados com o mesmo.

### Github

Neste projeto tive também meu primeiro contato com o Github, onde pude aprender os comando básicos como Pull, Commit, Push.
