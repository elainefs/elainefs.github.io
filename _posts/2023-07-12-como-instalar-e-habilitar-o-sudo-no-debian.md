---
title: Como instalar e habilitar o sudo no Debian
description: Aprenda como instalar e habilitar o sudo no Debian.
date: 2023-07-12 07:50:00 -0300
categories: [tutorial, linux]
tags: [debian, sudo]
---

## O que é o sudo?

O `sudo` é uma forma abreviada para se referir a _“**s**ubstitute **u**ser **do**”_ (fazer substituição do usuário) ou _“**s**uper **u**ser **do**”_ (fazer como super usuário). É um comando que permite que usuários comuns executem, temporariamente, ações dentro do sistema operacional com os privilégios de um usuário administrador. Ele se difere do comando `su`, pois com este você estará realmente logando no sistema como super usuário.

A principal vantagem em usar o `sudo` está em não permitir que um usuário comum acabe executando comandos que possam quebrar o sistema, pois é possível definir restrições ao usuário comum, não permitindo que ele execute determinados comandos.

Além disso, ao usar o comando `sudo` a senha a ser usada será a do usuário, enquanto o `su` pede a senha do usuário administrador (root).

Por padrão o [Debian](https://elaineferreira.com.br/instalacao-minima-do-debian-com-gnome-desktop) vem apenas com o root habilitado, se você tentar usar o seguinte comando:

```bash
sudo apt update
```

Retornará o seguinte erro se o sudo ainda não estiver instalado no seu sistema:

```bash
bash: sudo: comando não encontrado
```

Caso o sudo já esteja instalado, mas seu usuário não esteja definido como usuário sudo, retorná o seguinte erro:

```bash
seuusername is not in the sudoers file
```

Para resolver esses problemas você precisa instalar e habilitar o sudo para os usuários.

## Como instalar o sudo no Debian

Para habilitar o uso do sudo você precisa primeiro instalá-lo.

Abra o terminal e faça login como root:

```bash
su -
```

Digite sua senha de usuário root.

É sempre recomendado atualizar o sistema antes de uma nova instalação, rode o seguinte comando:

```bash
apt update && apt upgrade -y
```

Em seguida rode o seguinte comando para instalar o sudo:

```bash
apt install sudo -y
```

## Como adicionar usuários ao grupo sudo

Existem algumas formas de definir que um usuário passe a ter privilégios de super usuário com o comando sudo, vejamos algumas delas.

### Usando o usermod

Após o sudo ser instalado adicione o usuário ao grupo sudo com o seguinte comando:

```bash
usermod -aG  sudo username
```

Substitua o “username” no final do comando pelo usuário que você quer adicionar ao grupo sudo, por exemplo, se eu quisesse adicionar o usuário “elaine” no grupo sudo o comando ficaria assim:

```bash
usermod -aG sudo elaine
```

Após adicionar o usuário reinicie o sistema para as alterações serem aplicadas.

Para mim essa é a forma mais simples e fácil de adicionar um usuário ao grupo sudo e recomendo usar essa forma se você for iniciante no Linux. As outras formas que mostrarei a seguir exigem alterações de arquivos importantes do sistema, então tome cuidado ao editá-los.

### Alterando o arquivo group

Com o sudo já instalado e **logado como root** abra o arquivo “group” com o seguinte comando:

```bash
nano /etc/group
```

Procure pela linha do grupo sudo e adicione o usuário que você quer permitir que execute comandos usando o sudo após os dois pontos no final da linha, não dê espaços e se já existir um usuário separe os usuários por vírgula, mas sem espaços entre eles.

```bash
sudo:x:27:elaine,outrousuario
```

Salve o arquivo (`CTRL + O`) e feche (`CTRL + X`).

Reinicie o sistema para as alterações serem aplicadas.

### Alterando o arquivo sudoers

Abra o terminal, faça **login como root** e digite o seguinte comando para abrir o arquivo “sudoers”:

```bash
nano /etc/sudoers
```

Abaixo de `%sudo ALL=(ALL:ALL) ALL` digite o seguinte comando

```bash
username ALL=(ALL:ALL) ALL
```

Troque o “username” pelo usuário que você quer permitir que execute comandos usando o sudo.

Salve o arquivo (`CTRL + O`) e feche (`CTRL + X`).

## Conclusão

Agora você já sabe como instalar o sudo e três formas de habilitar o sudo no Debian para os usuários comuns poderem executar comandos, de forma temporária, como administradores.

Espero que esse artigo tenha sido útil para você e se acha que ele pode ser útil para outras pessoas, compartilhe.
