---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-03"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:aside: .aside}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Tutorial Introdução
{: #getting_started}

* {: download} Parabéns, você implementou um aplicativo de amostra Hello World no {{site.data.keyword.Bluemix}}!  Para iniciar, siga este guia passo a passo. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Fazer download de código de amostra)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Fazer download de código do aplicativo" />faça download do código de amostra</a> e explore você mesmo.

Seguindo este tutorial de introdução, você configurará um ambiente de desenvolvimento, implementará um app localmente e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados ao seu app.

Em todos esses docs, as referências à CLI do Cloud Foundry agora foram atualizadas para a CLI do {{site.data.keyword.Bluemix_notm}}! A CLI do {{site.data.keyword.Bluemix_notm}} tem os mesmos comandos conhecidos do Cloud Foundry, mas com uma melhor integração com as contas do {{site.data.keyword.Bluemix_notm}} e outros serviços. Saiba mais sobre como começar a usar a CLI do {{site.data.keyword.Bluemix_notm}} neste tutorial.
{: tip}

## Antes de Começar
{: #prereqs}

Você precisará do seguinte:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [Ruby ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ruby-lang.org/en/downloads/){: new_window}
* [rbenv ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/rbenv/rbenv#installation){: new_window}

## Etapa 1: clonar o aplicativo de amostra
{: #clone}

Primeiro, clone o repositório e mude o diretório no qual o app de amostra está localizado.

  ```
git clone https://github.com/IBM-Cloud/get-iniciado-ruby
  ```
  {: codeblock}

  ```
cd get-started-ruby
  ```
  {: codeblock}


## Etapa 2: executar o app localmente (opcional)
{: #run_locally}

1. Execute o app localmente executando os comandos a seguir.

  ```
rbenv install 2.3.0
  ```
  {: codeblock}

  ```
rbenv local 2.3.0
  ```
  {: codeblock}

  ```
gem install bundler
  ```
  {: codeblock}

  ```
bundle install
  ```
  {: codeblock}

  ```
rails server
  ```
  {: codeblock}

1. Visualize o seu app na URL a seguir: http://localhost:3000

## Etapa 3: preparar o app para implementação
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_notm}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-ruby`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedRuby` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
applications:
  - name: GetStartedRuby
    random-route: true
    memory: 128M
  ```
  {: codeblock}

  Nesse arquivo manifest.yml, **`random-route: true`** gera uma rota aleatória para seu app para evitar que sua rota colida com outras.  Se você optar por isso, será possível substituir **`random-route: true`** por **`host: myChosenHostName`**, fornecendo um nome de host de sua preferência.
{: tip}

## Etapa 4: implementar o app
{: #deploy}

É possível usar a CLI do {{site.data.keyword.Bluemix_short}} para implementar apps.

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_short}} e selecione um terminal de API.

  ```
ibmcloud login
  ```
  {: codeblock}

  Se você tiver um ID do usuário federado, em vez disso, use o comando a seguir para efetuar login com o seu ID de conexão única. Veja [Efetuando login com um ID federado](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) para saber mais.

  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Tenha como destino uma organização e um espaço do Cloud Foundry:

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Se você não tiver uma organização nem uma configuração de espaço, veja [Incluindo organizações e espaços](https://console.bluemix.net/docs/account/orgs_spaces.html).
  {: tip}

1. No diretório *get-started-node*, envie seu app por push para o {{site.data.keyword.Bluemix_short}}.

  ```
ibmcloud cf push
  ```
  {: codeblock}

  Isso pode levar um minuto. Se houver um erro no processo de implementação, será possível usar o comando `ibmcloud cf logs <Your-App-Name> --recent` para solucionar problemas.

Quando a implementação for concluída, você deverá ver uma mensagem indicando que o app está em execução.  Visualize o app na URL listada na saída do comando push.  Também é possível emitir o comando a seguir para visualizar o status de seus apps e ver a URL.

  ```
Ibmcloud cf apps
  ```
  {: codeblock}

## Etapa 5: incluir um banco de dados
{: #add_database}

Em seguida, incluiremos um banco de dados do {{site.data.keyword.cloudant_short_notm}} nesse aplicativo e configuraremos o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione **Criar recurso**.
2. Escolha a seção **Dados e análise de dados**, selecione o **{{site.data.keyword.cloudant_short_notm}}** e crie o seu serviço.
3. Acesse a visualização **Conexões**, selecione seu aplicativo e, em seguida, **Criar conexão**.
4. Selecione **Remontar** quando solicitado. O {{site.data.keyword.Bluemix_short}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_short}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte.
{: tip}

## Etapa 6: usar o banco de dados
{: #use_database}
Vamos agora atualizar seu código local para apontar para esse banco de dados. Nós criaremos um arquivo .env que armazenará as
credenciais para os serviços que o aplicativo usará. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente VCAP_SERVICES.

1. Crie um arquivo chamado `.env` no diretório `get-started-ruby` com o conteúdo a seguir:

  ```
CLOUDANT_URL=
  ```
  {: codeblock}

2. Em seu navegador, acesse o painel do {{site.data.keyword.Bluemix_notm}} e selecione **_seu app_ > Conexões**. Clique no ícone do menu do {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) e selecione **Visualizar credenciais**.

3. Copie e cole apenas a `URL` das credenciais no campo `CLOUDANT_URL` do arquivo `.env` e salve as mudanças.  O resultado será algo como:

  ```
CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```
   {: codeblock}

4. Execute seu aplicativo localmente.

  ```
rails server
  ```
  {: codeblock}

  Visualize seu app em: http://localhost:3000. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados.  Visualize o app {{site.data.keyword.Bluemix_notm}} na URL listada na saída do comando push acima.  Os nomes que você incluir de qualquer um dos apps deverão aparecer em ambos quando os navegadores forem atualizados.


Se você não precisar de seu app em tempo real, pare-o para que você não incorra em nenhum encargo inesperado.
{: tip}

## Próximas Etapas

* [Tutorials (Tutoriais)](/docs/tutorials/index.html)
* [Amostras ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
