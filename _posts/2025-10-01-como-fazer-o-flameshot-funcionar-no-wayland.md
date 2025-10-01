---
title: Como fazer o Flameshot funcionar no Wayland
description: Aprenda com fazer o Flameshot funcionar no Wayland
date: 2025-10-01 16:28:29 -0300
category: [Dica, Linux]
tags: [flameshot, gnome, tools]
---

O [Flameshot](https://flameshot.org/){:target="_blank"} é um software livre, de código aberto e multiplataforma para tirar capturas de telas, seu diferencial é a quantidade de recursos que a ferramenta oferece.

Recentemente atualizei meu computador para o Debian 13. Nessa versão, o Debian vem por padrão com o Wayland habilitado, no entanto, o Wayland, diferente do Xorg, possui algumas medidas de segurança que acaba dificultando a captura de tela.

A forma que encontrei para executar a aplicação no Wayland foi criando um script bash e definindo um atalho de teclado, nesse arquivo de configuração é definida uma variável de ambiente necessária para executar a aplicação.

## Arquivo de Configuração

Para que o Flameshot execute corretamente, abra o terminal e execute os seguintes comandos.

Para manter os arquivos organizados, criei uma pasta específica para armazenar o script:

```bash
mkdir ~/.local/bin/
```

Crie o arquivo de configuração dentro da da nova pasta:

```bash
touch ~/.local/bin/flameshot-wayland.sh
```

Abra o arquivo de configuração:

```bash
nano ~/.local/bin/flameshot-wayland.sh
```

Adicione o seguinte código no arquivo:

```bash
#!/bin/bash

# Variável para o Flameshot usar o backend Wayand (Qt Platform Abstraction)
export QT_QPA_PLATFORM=wayland

# Executa o Flameshot no modo GUI
flameshot gui
```

Torne o arquivo executável:

```bash
chmod +x ~/.local/bin/flameshot-wayland.sh
```

## Configuração do Atalho de Teclado

Após tornar o arquivo executável, abra as configurações do sistema e e procure pelos atalhos personalizados para teclado.

Nos atalhos de teclado adicione o atalho e o caminho completo para o arquivo:

Atalho: `Ctrl+Alt+F`

Comando: `/home/seunome/.local/bin/flameshot-wayland.sh`

O atalho de teclado pode ser a combinação de teclas que você desejar. 

No comando é importante passar o caminho completo até o arquivo, abreviações como `~/.local/bin/flameshot-wayland.sh` podem não funcionar.
