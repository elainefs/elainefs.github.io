---
title: Como corrigir erro de rede cabeada com ponto de interrogação no Linux
description: Aprenda como corrigir o erro de rede cabeada não gerenciável e com ponto de interrogação no Linux.
date: 2023-07-19 07:50:00 -0300
categories: [dica, linux]
tags: [linux, redes]
---

Após realizar a [Instalação mínima do Debian](https://elaineferreira.com.br/instalacao-minima-do-debian-com-gnome-desktop) notei um problema relacionado a rede cabeada. O applet da tray da rede cabeada ficava com um ponto de interrogação, e nas configurações não aparecia a opção de gerenciar as redes cabeadas.

![Configurações do Gnome sem painel de redes](assets/img/posts/rede-cabeada-nao-gerenciavel-com-interrogacao/erro-rede-cabeada-nao-gerenciavel-e-com-icone-de-interrogacao.webp)

No Debian, o Gerenciador de Redes ([NetworkManager](<https://wiki.debian.org/pt_BR/NetworkManager#:~:text=ifupdown%5D%20managed%3Dfalse-,Habilitando%20o%20Gerenciamento%20de%20Interface,Gerenciador%20de%20Redes%20(NetworkManager)%3A>)) não gerencia nenhuma interface definida em `/etc/network/interfaces` desde o Debian 6.0 "Squeeze", mas isso é bem fácil de resolver.

## Configurar arquivo NetworkManager.conf

Para resolver esse problema é bem fácil, abra o arquivo de configurações do Network Manager com o seguinte comando:

```bash
sudo nano /etc/NetworkManager/NetworkManager.conf
```

O arquivo que abrirá terá um conteúdo semelhante a esse:

```
[main]
plugins = ifupdown,keyfile

[ifupdown]
managed = false;
```

Em `managed=false`, troque para `managed=true`, como abaixo:

```
[main]
plugins=ifupdown,keyfile

[ifupdown]
managed=true
```

Após isso salve (`CTRL + O`) e feche (`CTRL + X`) o aquivo.

Após a alteração é necessário reiniciar o NetworkManager, rode o seguinte comando:

```bash
sudo service NetworkManager restart
```

Automaticamente suas redes começaram a aparecer no gerenciador de redes e o ícone com ponto de interrogação da tray mudará para ícone padrão de redes cabeadas.

![Configurações do Gnome sem painel de redes](assets/img/posts/rede-cabeada-nao-gerenciavel-com-interrogacao/correcao-erro-rede-cabeada-nao-gerenciavel-e-icone-de-interrogacao.webp)

Caso o sistema não aplique as mudanças imediatamente, reinicie o sistema.

## Conclusão

Deu para notar que não é um bicho de sete cabeças resolver esse problema, mas confesso que demorei a achar a solução, então quis compartilhar :). Espero que seja útil para você.
