---
title: Como fazer a instalação mínima do Debian com Gnome Desktop
description: Aprenda a fazer a instalação minima do gnome no Debian sem o excesso de aplicações desnecessárias.
date: 2023-06-20 16:47:10 -0300
categories: [tutorial, linux]
tags: [debian, gnome]
---

O [Projeto Debian](https://www.debian.org/), lançado por Ian Murdock em agosto de 1993, cresceu e se consolidou por meio de uma comunidade mundial de desenvolvedores voluntários muito bem organizada.

O Debian tem como objetivo principal fornecer um sistema operacional estável e confiável. Além disso, é conhecido por sua ênfase na liberdade de software e no suporte a uma ampla variedade de dispositivos, como desktops, laptops, servidores, sistemas embarcados e diversas arquiteturas de hardware.

A estabilidade do Debian é o que mais atrai os usuários, eu, sem dúvida, estou inclusa nesse grupo.

No entanto, se você utiliza o Debian fora de um servidor e precisa de uma interface gráfica, uma coisa notável é a quantidade um tanto quanto exagerada de programas que vem instalados com os ambientes desktops, muitos desses programas você nunca nem se que utilizará.

Dos ambientes desktops que já utilizei o Gnome foi o que melhor me atendeu e o que me permite ser mais produtiva, mas o excesso de programas sempre me incomodou. O Gnome também é conhecido por não ser um ambiente desktop muito leve, então o objetivo aqui é instalar somente o necessário e tentar deixar ele o mais enxuto e performático possível.

## Requisitos mínimos para instalação do sistema operacional Debian

| Tipo de Instalação | RAM (mínimo) | RAM (recomendado) | Disco Rígido |
| :----------------: | :----------: | :---------------: | :----------: |
|    Sem Desktop     |    256MB     |       512MB       |     2GB      |
|    Com Desktop     |     1GB      |        2GB        |     10GB     |

Requisitos para instalação do Debian
{: .caption-table}

Os valores presente na tabela acima foram retirados do [site oficial do Debian](https://www.debian.org/releases/stable/arm64/ch03s04.pt.html). Os valores mínimos assumem que a swap estará ativa, além disso, para a instalação **Com Desktop**, essas especificações não são recomendadas para os ambientes Gnome e KDE Plasma, pois consomem muitos recursos, você pode até conseguir rodá-los, mas com certeza apresentará alguns travamentos, principalmente devido à pouca memória RAM.

Como o objetivo desse tutorial é justamente fazer a instalação do ambiente desktop Gnome, e para que você possa usufruir de fato dele, eu recomendo o mínimo de 4GB RAM, pois usei por muito tempo uma máquina limitada a essa quantidade de memória e ela rodava bem, para coisas básicas do dia a dia, o Debian com Gnome com essa instalação mínima.

## Criação da mídia de instalação

Para instalar o Debian na sua máquina, você pode gravar a imagem ISO do sistema em um CD/DVD, um método raramente utilizado atualmente, ou pode gravar a mídia de instalação em um pendrive. Recomendo usar o pendrive por ser mais usual e prático e ter diversos tutoriais na internet ensinando a fazer dessa forma. O pendrive deve ter no mínimo 4GB de armazenamento, porém recomendo um de 8GB para evitar problemas de espaço na hora da gravação da ISO, lembre-se de fazer backup dos dados contidos no pendrive, eles serão apagados ao gravar a imagem ISO.

Para criar um pendrive bootável primeiro precisamos da imagem ISO do Debian, acesse o [site oficial do Debian](https://www.debian.org/distrib/), no site você encontrará algumas opções e encontrará uma explicação para que cada uma dessas opções servem. Baixe uma pequena imagem de instalação, você deve baixar de acordo com a arquitetura do seu processador, 64bits ou 32bits.

![Página de download do Debian](assets/img/posts/debian-minimal/debian-obter-iso.webp)

Após baixar a imagem ISO é preciso usar um programa para criar o pendrive bootável, exitem várias opções como o Rufus que funciona apenas em Windows, ou o UNetbootin, Ventoy e Balena Etcher, que são multiplataformas.

Fique a vontade para escolher um desses, ou outro de sua preferência, em uma pesquisa rápida no Google você encontra diversos tutoriais ensinando a criar o pendrive bootável a partir do seu sistema operacional atual através dessas ferramentas.

Nesse tutorial vou usar o UNetbootin, por ser multiplataforma e o processo ser igual em todos os sistemas operacionais a partir do qual você estiver criando seu pendrive bootável com Debian.

Entre no site do [UNetbootin](https://unetbootin.github.io/), selecione o seu sistema operacional atual, instale o programa e abra ele.

![Site de download do UNetbootin](assets/img/posts/debian-minimal/unetbootin-00.webp)

Ao executar o programa você verá a seguinte tela:

![UNetbootin Tela Inicial](assets/img/posts/debian-minimal/unetbootin-01.webp)

Para criar o pendrive bootável a partir da imagem ISO que você baixou do site do Debian, com o seu pendrive já espetado na máquina, selecione a opção "Imagem de disco", em seguida clique nos 3 três pontinhos ao lado do espaço em branco e selecione a imagem ISO que você baixou do site, em “Tipo” deixe selecionado “Unidade USB”, e o mais importante, em “Unidade” selecione o pendrive que você vai utilizar para criar o pendrive bootável, feito todos esses passos, clique em “OK”.

![Tela Inicial UNetbootin com passo a passo de configuração](assets/img/posts/debian-minimal/unetbootin.webp)

O programa vai iniciar o processo de criação do seu pendrive bootável, após finalizado, clique em “Sair” e pronto, seu pendrive bootável com Debian está criado.

## Preparando o seu computador para a instalação

Para fazer a instalação é preciso fazer algumas configurações na BIOS da sua máquina, ligue a máquina e pressione a tecla para acessar a BIOS, as teclas para acessar a BIOS podem ser: F2, F10, F11, F12, ESC, BackSpace, Delete, uma combinação delas ou outra dependo do fabricante da sua placa-mãe.

Normalmente ao iniciar o computador aparece uma mensagem informando qual a tecla que deve ser pressionada para acessar a BIOS.
{: .bubble-tip}

Dependendo do fabricante da sua placa-mãe as opções que eu vou apresentar abaixo podem ser definidas com outros nomes, mas provavelmente será possível deduzir do que se trata, então procure as opções correspondentes dentro da sua BIOS para fazer as seguintes configurações.

### Configure a máquina para Boot em modo UEFI e desabilite o Secure Boot

Procure pela opção “Boot Mode Selection” e selecione o modo "UEFI" ou "UEFI and Legacy", se estiver disponível.

O “secure boot” permite que apenas firmwares criptograficamente assinados com chaves específicas sejam carregados e executados, bloqueando qualquer inicialização potencialmente maliciosa. Por padrão, a única chave aceita no sistema UEFI com “secure boot” ativado é a chave da Microsoft para ativação do Windows. Por isso, será preciso desabilitar o “secure boot” para seguir com a instalação do Debian.

![Desabilitar o secure boot](assets/img/posts/debian-minimal/secure-boot-disabled.webp)

Em algumas BIOS, a opção de desabilitar o “secure boot” se torna visível apenas ao definir uma senha para o administrador da BIOS. Então, caso não esteja aparecendo a opção de “secure boot” na sua BIOS, defina a senha de administrador, salve as configurações, reinicie o sistema, entre novamente na BIOS e procure novamente pela opção do “secure boot” para desativá-la.

![Definir senha para administrador da BIOS](assets/img/posts/debian-minimal/set-adm-password.webp)

### Defina a ordem de prioridade do Boot

Ao entrar na BIOS procure também pela opção “Boot Priority Order” e defina o seu pendrive de instalação como a primeira opção, assim ao reiniciar o sistema para a instalação, a BIOS identificará automaticamente ele para iniciar o processo de instalação, mas lembre-se de entrar novamente na BIOS após finalizar a instalação e mudar a ordem de Boot para o seu HD/SSD onde foi instalado o sistema.

![Definição de Boot Priority e USB Boot](assets/img/posts/debian-minimal/boot-priority.webp)

Algumas BIOS permitem acessar um menu de seleção de Boot ao iniciar a máquina, normalmente para acessar esse menu usa-se a tecla F11, F12 ou F8. Você pode testar se essa opção está disponível na sua BIOS, assim não será necessário fazer a mudança de prioridade de Boot acima, espete o seu pendrive de instalação na máquina, ligue ele e comece a apertar a tecla correspondente a sua placa-mãe até o menu aparecer e selecione o pendrive bootável pelo qual você quer fazer a instalação.

![Menu de seleção de Boot](assets/img/posts/debian-minimal/boot-menu.webp)

### Habilite o Boot pelo Pendrive

Procure pelas opções “External Device Boot” ou “USB Boot” e as ative para que seu pendrive bootável seja reconhecido.

### Habilite o AHCI

Procure pela opção “Sata Mode” ou “Configure SATA as” e mude para AHCI, principalmente se você for fazer a instalação do seu sistema em um SSD.

### Salve suas alterações

Na aba “Exit” do menu, selecione a opção “Exit Saving Changes” para salvar suas alterações e sair da BIOS, o seu computador irá reiniciar e, se o seu pendrive bootável estiver conectado, ele irá ser reconhecido e a tela de instalação do Linux Debian aparecerá.

Lembre-se que dependendo do modelo da sua placa-mãe, algumas opções podem não estar disponíveis ou podem ter nomes diferentes dos citados. Caso você realmente não encontre alguma opção, tente mudar todas as que consegui e tente realizar o processo de instalação.
{: .bubble-note}

## Instalação do Debian Mínimo

Assim que o seu pendrive bootável estiver criado e sua BIOS da máquina configurada, podemos seguir para a instalação do Debian.

Antes de prosseguir é importante ressaltar que a instalação mínima do Debian deixa de lado algumas configurações de uma instalação padrão, então tenha em mente que ao fazer essa instalação, você precisará instalar programa por programa e pode precisar configurar algumas coisas por conta própria futuramente. Sugiro fazer essa instalação primeiro em uma máquina virtual ou de teste, testar se essa instalação satisfaz as suas necessidade e só então fazer em uma máquina real. Nesse tutorial tentarei deixar o sistema o mais funcional possível.
{: .bubble-warning}

Para seguir com a instalação conecte seu computador via cabo de rede, erros podem ocorrer porque algum firmware pode não estar incluso na mídia de instalação e sua placa de Wi-Fi pode não ser reconhecida. Já aconteceu de a minha placa Wi-Fi ser reconhecida, eu conseguir me conectar, finalizar a instalação básica, mas no momento da instalação do ambiente desktop e dos aplicativos essenciais o Wi-Fi não funcionar.

Por precaução conecte sua máquina via cabo desde o início da instalação.
{: .bubble-warning}

Desligue o computador, espete o pendrive bootável na máquia e a ligue novamente. Caso você tenha mudado a ordem de boot para o seu pendrive ele iniciará automaticamente no menu de instalação do Debian, caso contrário pressione repetidamente a tecla para entrar no menu de boot e selecione o seu pendrive.

Se você usou o UNetbootin para criar seu pendrivre bootável pode ser que apareça uma mensagem dizendo que alguns usuários já relataram erros ao usá-lo para fazer a instalação do Debian, acredito que esse problema está relacionado a usar a opção “Distribuição” para criar o pendrivre bootável, e não “Imagem de disco”, como foi demonstrado aqui. Mesmo que essa mensagem apareça, tente seguir com a instalação, caso você realmente não consiga finalizar a instalação, tente outro programa de criação de pendrivre bootável e realize o processo de instalação novamente a partir dos passos a seguir.
{: .bubble-warning}

### Passo 1: Selecione a primeira opção, “Graphical Install”

![](assets/img/posts/debian-minimal/001-debian-installer.webp)

### Passo 2: Selecione o idioma do instalador

![](assets/img/posts/debian-minimal/002-idioma-instalador.webp)

### Passo 3: Selecione sua localidade

![](assets/img/posts/debian-minimal/003-localidade.webp)

### Passo 4: Selecione o idioma do seu teclado

![](assets/img/posts/debian-minimal/004-teclado.webp)

### Passo 5: Defina o nome da sua máquina

![](assets/img/posts/debian-minimal/005-nome-maquina.webp)

### Passo 6: Defina o nome do seu domínio

Para redes domésticas normalmente não é necessário

![](assets/img/posts/debian-minimal/006-nome-dominio.webp)

### Passo 7: Defina a senha de usuário root

Recomenda-se sempre usar uma senha forte, e ao definir uma senha nesse momento, sempre que quiser fazer alterações no sistema, com privilégios de usuário administrador, você deve usar o comando `su`. Caso queria usar o `sudo`, você deverá configurá-lo.

![](assets/img/posts/debian-minimal/007-senha-root.webp)

### Passo 8: Defina um nome do usuário comum

Esse é o nome que aparece quando você vai logar no sistema.

![](assets/img/posts/debian-minimal/008-nome-conta.webp)

### Passo 9: Defina o nome de usuário para a sua conta

Deve iniciar sempre com letra minúscula

![](assets/img/posts/debian-minimal/009-nome-usuario.webp)

### Passo 10: Defina a senha para o seu usuário comum

Essa é a senha que você usará para entrar no sistema. Se você definiu uma senha para root, essa senha de usuário deve ser, por segurança, diferente dela.

![](assets/img/posts/debian-minimal/010-senha-usuario.webp)

### Passo 11: Escolha o Estado onde você está para configurar seu fuso horário

![](assets/img/posts/debian-minimal/011-definir-fuso-horario.webp)

### Passo 12: Particionamento do disco

Você pode fazer vários tipos de particionamento dependo da sua necessidade. Aqui usarei um particionamento simples, fácil de fazer e voltado para um usuário comum, mas caso você use ou queira usar outro tipo de particionamento, pode fazer ele normalmente.

#### Selecione a primeira opção “Assistido - usar o disco inteiro”

![](assets/img/posts/debian-minimal/012-particionamento-01.webp)

#### Em seguida selecione o seu disco

![](assets/img/posts/debian-minimal/012-particionamento-02.webp)

#### Selecione a segunda opção “Partição /home separada”.

![](assets/img/posts/debian-minimal/012-particionamento-03.webp)

#### Visão geral de como ficará particionado o disco

Selecione “Finalizar o particionamento e escrever as mudanças no disco” e clique “Continuar”

![](assets/img/posts/debian-minimal/012-particionamento-04.webp)

#### Confirme o particionamento, clique em “Sim”

![](assets/img/posts/debian-minimal/012-particionamento-05.webp)

### Passo 13: Instalação do sistema básico

Ele iniciará o processo de instalação do sistema básico, dependo da sua internet esse processo pode demorar um pouco.

![](assets/img/posts/debian-minimal/013-instalacao-sistema-basico.webp)

### Passo 14: Ele pedirá para você ler mídias adicionais caso queira, clique em “Não”

![](assets/img/posts/debian-minimal/014-midias-adicionais.webp)

### Passo 15: Escolha o país do espelho dos repositórios

![](assets/img/posts/debian-minimal/015-pais-gerenciador-pacotes.webp)

### Passo 16: Selecione o espelho do repositório

Em seguida ele mostrar os espelhos disponíveis no país que você selecionou, o padrão é o “deb.debian.org”, quanto mais perto de você o espelho estiver localizado, melhor, caso dentre as opções você identifique um mais perto de você, escolha ele, caso contrario, deixe o padrão.

![](assets/img/posts/debian-minimal/016-repositorios-pacotes.webp)

### Passo 17: Defina seu proxy, caso precise usar algum

![](assets/img/posts/debian-minimal/017-proxy.webp)

### Passo 18: Configure o popularity-contest

Ele perguntará se você quer enviar informações anônimas sobre o seu sistema para que eles saibam quais os pacotes mais utilizados pelos usuários, essa escolha fica a seu critério.

![](assets/img/posts/debian-minimal/018-popularity-contest.webp)

### Passo 19: Instalação do ambiente de área de trabalho

Agora chegamos na parte mais importante da proposta desse tutorial, a instalação mínima do Debian. Você já instalou o sistema básico do sistema, agora deve escolher o ambiente de área de trabalho que você quer utilizar, existe a opção de instalar o Gnome, como você pode ver, mas se você usar essa opção virá junto todas as coisas desnecessárias que a gente está tentando evitar aqui.

Então desmarque todas as opções

![](assets/img/posts/debian-minimal/019-desktop.webp)

Após desmarcar tudo clique em “Continuar”.

![](assets/img/posts/debian-minimal/019-desktop-empty.webp)

### Passo 20: Instale o GRUB, clique em “sim”

![](assets/img/posts/debian-minimal/020-grub.webp)

Selecione o seu disco

![](assets/img/posts/debian-minimal/020-grub-disc.webp)

Após isso, sua instalação está concluída.

![](assets/img/posts/debian-minimal/021-instalacao-concluida.webp)

É hora de entrar no seu novo sistema. Clique em continuar, mas lembre-se de remover seu pendrive bootável e caso você tenha mudado a ordem de Boot na BIOS é hora de mudar a ordem novamente e colocar o seu HD/SSD onde foi instalado o sistema como primeira opção.

## Instalação do ambiente desktop Gnome e aplicativos essenciais

Ao reiniciar o seu sistema você cairá nessa tela.

![Terminal de login do Debian](assets/img/posts/debian-minimal/022-login-minimal.webp)

Digite o seu nome de usuário definido no Passo 9 e clique “Enter”, ele pedirá a sua senha definida no Passo 10, se você é novo no mundo Linux saiba que as senhas não são exibidas no terminal ao digitá-las, tenha certeza que digitou certo e clique “Enter”.

Agora você está logado no sistema como usuário comum.

![Terminal de login do Debian mostrando informações do sistema](assets/img/posts/debian-minimal/023-login-sistema-minimal.webp)

Para os próximos passos você deve logar como root, dessa forma rode o seguinte comando

```bash
su -
```

E em seguida sua senha de root definida no Passo 7.

![](assets/img/posts/debian-minimal/024-login-root-minimal.webp)

A primeira coisa que você deve fazer é atualizar o seu sistema, rode o seguinte comando:

```bash
apt update && apt upgrade -y
```

Após atualizado, vamos à instalação do Gnome Mínimo.

Os comandos a seguir são para fazer uma instalação mínima, com os programas essenciais para você utilizar o sistema, mas é claro que dependo das suas necessidades você pode precisar de outros programas, os quais você poderá instalar posteriormente, inclusive, nesse momento, você pode adicionar alguns programas que não estão nessa lista, ou até mesmo remover alguns se você sabe que não vai precisar ou usa outros programas no lugar desses que deixo aqui como recomendação.

Rode o seguinte comando no terminal:

```bash
apt install --no-install-recommends gnome-session xserver-xorg tilix gedit nautilus gnome-tweaks gnome-control-center gnome-calculator network-manager gnome-software pulseaudio gnome-bluetooth pulseaudio-module-bluetooth gdm3 firefox-esr shotwell cheese vlc gnome-sushi
```

Para colar no terminal do Linux use `CTRL+SHIFT+V`
{: .bubble-tip}

Será listado todos os pacotes a serem instalados no seu sistema e, sim, são muitos e você deve estar se perguntando se isso realmente é uma instalação mínima. Acredite, é!

![](assets/img/posts/debian-minimal/025-instalacao-pacotes-essenciais.webp)

Clique “Enter” para instalar todos esses pacotes. Esse processo de instalação pode demorar um pouco dependendo da sua internet.

Quando tudo estiver finalizado você precisa reiniciar o sistema, rode o seguinte comando:

```bash
systemctl reboot
```

Ao reiniciar você entrará na tela de login e você já pode começar a desfrutar do seu novo Debian.

![](assets/img/posts/debian-minimal/026-login-gnome.webp)

## Configuração do sistema pós-instalação

Para as próximas instalações certifique-se de estar logado como root.

### Instalação de Drivers

A partir do Debian 12 os drivers proprietários passaram a ser incluídos direto na mídia de instalação, mas caso sua placa de Wi-Fi, do Bluetooth ou outra não seja reconhecida automaticamente, conecte sua máquina via cabo de Ethernet e realize os passos a seguir.

Você precisa verificar se a sua `sources.list` está configurada para o repositório `non-free-firmware`

No terminal rode o seguinte comando:

```bash
nano /etc/apt/sources.list
```

Adicione `non-free-firmware` depois de `main`, caso não esteja.

Sua `sources.list` deve ficar assim:

```bash
deb http://deb.debian.org/debian/ bookworm main non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm main non-free-firmware

deb http://security.debian.org/debian-security bookworm-security main non-free-firmware
deb-src http://security.debian.org/debian-security bookworm-security main non-free-firmware

deb http://deb.debian.org/debian/ bookworm-updates main non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm-updates main non-free-firmware
```

Salve o arquivo com `CTRL+O`, e feche com `CTRL+X`.

Depois atualize a lista de repositórios com o seguinte comando:

```bash
apt update && apt upgrade -y
```

Para fazer a sua máquina reconhecer o máximo de drivers possíveis de uma só vez rode o seguinte comando:

```bash
apt install firmware-linux firmware-linux-free firmware-linux-nonfree -y
```

Assim que a instalação tiver concluída reinicie o sistema para as alterações serem aplicadas.

### Instalação de thumbnail para vídeos e imagens

Ao instalar o gerenciador de arquivos Nautilus no modo de instalação mínima é comum o erro de não aparecer as miniaturas das imagens e vídeos, ficando dessa forma:

![](assets/img/posts/debian-minimal/027-thumbnail.webp)

Para resolver esse problema, log novamente como root e instale os seguintes pacotes:

```bash
apt install ffmpegthumbnailer libgdk-pixbuf2.0-bin -y
```

### Habilitar leitura de arquivos NTFS

O NTFS é um sistema de arquivos do Windows, pendrives e HD externos usam esse tipo de sistema de arquivo porque assim podem ser reconhecidos em qualquer sistema operacional.

No Linux para ativar o suporte a esse sistema de arquivos basta rodar o seguinte comando:

```bash
apt install ntfs-3g -y
```

### Dicas adicionais

Talvez seja útil para você essas configurações adicionais:

[Como instalar e habilitar o sudo no Debian](https://elaineferreira.com.br/como-instalar-e-habilitar-o-sudo-no-debian/)

[Como corrigir erro de rede cabeada com ponto de interrogação no Linux](https://elaineferreira.com.br/corrigir-erro-de-rede-cabeada-com-ponto-de-interrogacao-no-linux)

## Conclusão

Agora você já tem o seu sistema Debian o mais completo e funcional possível, sem programas que você não usará, ocupando menos espaço e talvez até menos memória RAM.

Veja essa comparação do antes e depois da instalação padrão e da instalação mínima.

![](assets/img/posts/debian-minimal/031-programas-padrao.webp)

![](assets/img/posts/debian-minimal/030-programas-minimal.webp)

Espero que esse tutorial tenha sido útil para você e se acha que pode ser útil para outras pessoas, compartilhe.
