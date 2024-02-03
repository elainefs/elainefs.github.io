---
title: Como instalar e configurar o XAMPP no Debian
description: Aprenda a como instalar o gerenciador de servidor XAMPP no Linux.
date: 2023-08-03 12:11:19 -0300
categories: [tutorial, linux]
tags: [debian, xampp, servidor]
---

## O que é o XAMPP?

O XAMPP é um gerenciador de servidor gratuito, de código aberto, fácil de instalar e que permite executar o Apache, MariaDB, PHP e Perl a partir de uma única instalação. Anteriormente o XAMPP usava o MySQL, mas desde a versão 5.5.30 passou a usar o MariaDB como gerenciador de banco de dados, no entanto, os comandos são os mesmos para ambos.

O XAMPP existe há mais de 10 anos e é mantido pela Apache Friends, um projeto sem fins lucrativos. Além disso, ele é multiplataforma, está disponível para os principais sistemas operacionais, Windows, Linux e MacOS.

No próprio site do XAMPP eles não recomendam o seu uso para ambientes de produção, apenas para ambientes de desenvolvimento. No momento em que escrevo esse artigo estou aprendendo MySQL e se você está aprendendo a usar as tecnologias oferecidas por ele, sem dúvida você economizará bastante tempo por não precisar instalar cada um dos recursos separadamente.

Vou mostrar como instalar e configurar o XAMPP no Debian, mas esse tutorial pode ser usado para instalar o XAMPP em qualquer outra distribuição baseada nele.

## Como instalar o XAMPP no Debian

Para instalar o XAMPP é preciso baixar a versão do programa referente ao seu sistema operacional. Acesse o site da [Apache Friends](https://www.apachefriends.org/pt_br/index.html) e selecione a opção “XAMPP para Linux”. O download irá iniciar automaticamente.

![Tela inicial do site da Apache Friends](assets/img/posts/instalar-xampp-linux/tela-inicial-do-site-da-Apache-Friends.webp)

### Torna o instalador do XAMPP executável

Após a conclusão do download, é preciso tornar o instalador do XAMPP executável.

Abra o terminal e acesse a pasta onde você salvou o arquivo e rode um dos seguintes comandos:

```bash
sudo chmod 755 xampp-linux-*-installer.run
```

ou

```bash
sudo chmod +x xampp-linux-*-installer.run
```

### Instalar o XAMPP

Para instalar o XAMPP rode o seguinte comando no terminal:

```bash
sudo ./xampp-linux-*-installer.run
```

O painel de instalação irá iniciar, clique em Next

![Painel de instalação do XAMPP](assets/img/posts/instalar-xampp-linux/painel-de-instalacao-do-XAMPP.webp)

A próxima janela permite que você selecione os componentes que você deseja instalar. Deixe todas as opções marcadas.

![Selecionar componentes de instalação](assets/img/posts/instalar-xampp-linux/selecionar-componentes-de-instalacao.webp)

Na janela seguinte, o programa mostrará onde será feita a instalação do programa. Por padrão ela é feita na pasta **/opt/lampp**

![Diretório de instalação do XAMPP](assets/img/posts/instalar-xampp-linux/diretorio-de-instalacao-do-XAMPP.webp)

Na tela seguinte será mostrado que o programa está pronto para ser instalado. Clique em Next.

![Confirmar instalação do XAMPP](assets/img/posts/instalar-xampp-linux/confirmar-instalacao-do-XAMPP.webp)

A instalação irá iniciar e é só esperar o programa terminar de ser instalado.

![Instalação do XAMPP no Linux](assets/img/posts/instalar-xampp-linux/instalacao-do-XAMPP.webp)

Quando a janela abaixo aparecer, marque a caixa
Launch XAMPP para iniciar o painel de controle do XAMPP e clique em Finish.

![Instalação do XAMPP finalizada](assets/img/posts/instalar-xampp-linux/instalacao-do-XAMPP-finalizada.webp)

Se tudo correu como o esperado você verá a tela abaixo, ela possui três abas, a aba Welcome, a aba Manage Servers e a aba Application Log.

![Painel de Controle do XAMPP](assets/img/posts/instalar-xampp-linux/painel-de-controle-do-XAMPP.webp)

A aba Manage Servers é onde você poderá iniciar, parar, reiniciar e configurar os serviços.

![Painel de Controle do XAMPP aba Manager Servers](assets/img/posts/instalar-xampp-linux/painel-de-controle-manager-do-XAMP.webp)

Selecione o serviço e clique em **Start** para iniciar um serviço específico ou em **Start All** para iniciar todos de uma vez.

Para verificar se tudo está funcionando corretamente, com os serviços ativos, digite a seguinte url no seu navegador:

[http://localhost/dashboard/](http://localhost/dashboard/)

A seguinte tela irá aparecer para você. A partir dela você terá acesso a diversos serviços oferecidos pelo XAMPP, incluindo o phpMyAdmin para a criação e manipulação de banco de dados.

![Localhost com XAMPP em execução](assets/img/posts/instalar-xampp-linux/localhost-com-XAMPP-em-execucao.webp)

## Como iniciar o XAMPP

Por padrão o XAMPP não fica no menu de aplicativos, para iniciar os serviços você pode seguir dois caminhos, direto pelo painel de controle com uma interface gráfica, a mesma mostrada anteriormente, ou usando comandos via terminal para cada serviço.

### Gerenciar serviços pelo painel de controle do XAMPP

Para iniciar o painel de controle do XAMPP e poder gerenciar os serviços a partir de uma interface gráfica, rode o seguinte comando:

```bash
sudo /opt/lampp/manager-linux-x64.run
```

O painel de controle abrirá e você poderá iniciar, parar ou reiniciar os serviços.

Talvez seja um pouco chato fica digitando esse comando no terminal toda vez que quiser iniciar o XAMPP. Há duas alternativas para resolver esse problema: **criar um ícone para o menu de aplicativos** ou **um alias para o terminal**.

### Gerenciar serviços do XAMPP pelo terminal

Para **iniciar todos os serviços** do XAMPP de uma vez, rode o seguinte comando:

```bash
sudo /opt/lampp/lampp start
```

Para **parar todos os serviços** do XAMPP de uma vez, rode o seguinte comando:

```bash
sudo /opt/lampp/lampp stop
```

Para **iniciar apenas o Apache**, rode o seguinte comando:

```bash
sudo /opt/lampp/lampp startapache
```

Para **parar apenas o Apache**, rode o seguinte comando:

```bash
sudo /opt/lampp/lampp stopapache
```

Para **iniciar apenas o FTP ProFTPD**, rode o seguinte comando:

```bash
sudo /opt/lampp/lampp startftp
```

Para **parar apenas o FTP ProFTPD**, rode o seguinte comando:

```bash
sudo /opt/lampp/lampp stopftp
```

Para **iniciar apenas o MySQL**, rode o seguinte comando:

```bash
sudo /opt/lampp/lampp startmysql
```

Para **parar apenas o MySQL**, rode o seguinte comando:

```bash
sudo /opt/lampp/lampp stopmysql
```

Às vezes ao rodar os comandos para iniciar os serviços individualmente aparece um erro no terminal dizendo que o comando não foi encontrado, mas ao acessar o `http://localhost/dashboard/` os serviços estarão ativos normalmente.
{: .bubble-note}

## Configurar as variáveis de ambiente

Para usar os serviços oferecidos pelo XAMPP você precisa configurar as variáveis de ambiente.

Se você rodar o comando mysql para tentar manipular bancos de dados pelo terminal, retornará o erro de comando não encontrado, mesmo que você tenha iniciado o MySQL.

![MySQL Comando não encontrado](assets/img/posts/instalar-xampp-linux/mysql-comando-nao-encontrado-XAMPP.webp)

Se você tentar verificar, por exemplo, as versões dos serviços pelo terminal, obterá o mesmo erro.

![Comando não encontrado para versões dos serviços](assets/img/posts/instalar-xampp-linux/comando-nao-encontrado-XAMPP.webp)

Para resolver esse problema e poder usar os serviços é preciso adicionar a pasta bin do XAMPP ao arquivo `.bashrc`

Para isso, abra o terminal e rode o seguinte comando:

```bash
sudo nano .bashrc
```

No final do arquivo que abrirá adicione a seguinte linha:

```bash
export PATH=/opt/lampp/bin:$PATH
```

Salve o arquivo com as modificações e para elas serem aplicadas rode o seguinte comando:

```bash
source .bashrc
```

Após isso já será possível usar todos os serviços do XAMPP

![Versões dos serviços oferecidos pelo XAMPP](assets/img/posts/instalar-xampp-linux/XAMPP-versoes-servicos.webp)

Para acessar o MySQL é preciso estar logado como root e por padrão a senha do root é vazia.
{: .bubble-note}

## Liberar acesso à pasta htdocs

Para criar seus projetos usando o XAMPP você deve criar as pastas dos seus projetos dentro da pasta htdocs, no entanto, por padrão essa pasta não é habilitada para que os usuários comuns do sistema criem pastas dentro dela.

![Pasta htdosc bloqueada](assets/img/posts/instalar-xampp-linux/htdocs-bloqueada.webp)

Para liberar o acesso rode o seguinte comando no terminal:

```bash
sudo chmod 777 -R /opt/lampp/htdocs
```

A partir de agora você já pode criar suas pastas e arquivos normalmente.

![Pasta htdos liberada](assets/img/posts/instalar-xampp-linux/htdocs-desbloqueada.webp)

## Conclusão

A partir de agora você já pode usar todos os serviços oferecidos pelo XAMPP. Espero que esse artigo tenha sido útil para você e se acha que ele pode ser útil para outras pessoas, compartilhe.
