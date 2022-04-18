## Scaffold Education - WSL 2

Esse guia tem como objetivo preparar seu ambiente no windows para configurar a plataforma;

Tabela de conteúdos
=================
<!--ts-->
   * [Configurando WSL 2](#-configurando-wsl-2)
   * [Configurando Docker](#-configurando-docker)
   * [Configurando VSCode (opcional)](#-configurando-vscode)
   * [Configurando Terminal (opcional)](#-configurando-terminal)
   * [Turbinando seu Terminal](#-turbinando-seu-terminal)
   * [Configurando Node, Npm, Nvm e Yarn](#-configurando-node/npm/nvm/yarn) 
   * [Configurando SSH Keys](#-configurando-ssh-keys)
<!--te-->

## 💻 Configurando WSL 2
1. Abra o `Windows PowerShell` com `permissão de admin` e execute os comandos abaixo
  ```
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
  ```

2. Reinicie seu computador para aplicar as atualizações

3. Faça o download e instale o kernel do linux [**clicando aqui**](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

4. Abra o `Windows PowerShell` com `permissão de admin` e execute os comandos abaixo
  ```
    wsl --set-default-version 2
  ```

5. Instalando uma distro do Linux
  - Entre na loja do windows (`Microsoft Store`)
  - Realize o login com sua conta Microsoft
  - Pesquise por Linux e escolha uma versão (versão utilizada para esse guia 18.04 LTS)
  - Após instalar clique abrir e um terminal sera disponibilizado
  - Crie um usuário e senha (anotar para não perder, pode ser o mesmo do windows)

6. Se não encontrou nenhum problema até aqui, parabéns você conseguiu instalar uma distribuição linux com sucesso.

## 💻 Configurando Docker
1. Faça o download e instale Docker Desktop [**clicando aqui**](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)

2. Abra o Docker Desktop e clique na engrenagem localizado no topo
3. Clique em `Resources` localizado no menu do lado esquerdo
4. Clique em `WSL Integration` e depois habilite a distro Ubuntu;
5. Clique no botão `Apply and Restart` e pronto docker configurado!


## 💻 Configurando VSCode
1. Faça o download e instale o VSCode [**clicando aqui**](https://code.visualstudio.com/docs/?dv=win)
2. Instale o plugin `Remote - WSL`

## 💻 Configurando Terminal
1. Entre na loja do windows (`Microsoft Store`)
2. Pesquise por `Terminal` e realize o download
3. Abra seu novo terminal e clique na setinha localizada no topo e depois clique em `configurações`
4. Clique em `Abrir o arquivo JSON` selecione o VSCode ou outro editor de sua escolha
5. Localize a chave `profiles` dentro dela vai encontrar o profile do `Ubuntu`
  - Adicione uma nova linha dentro do profile Ubuntu
  ```
  "startingDirectory": "//wsl$/Ubuntu-18.04/home/seu-nome-de-usuario"
  ```
  - Copie o contéudo da chave `guid` do profile do Ubuntu
6. Localize a chave `defaultProfile` e coloque como valor dela o `guid` copiado na etapa anterior.
7. Salve o arquivo e reinicie seu Terminal.

## 💻 Turbinando seu Terminal
1. Abra seu `Terminal` e execute os comandos abaixo
```
sudo apt install zsh
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

code .zshrc
```

2. Procure no arquivo aberto por `plugins=(git)` e troque por `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)`
3. Salve o arquivo e reinicie seu Terminal.

## 💻 Configurando node/npm/nvm/yarn
1. Abra seu `Terminal` e execute os comandos abaixo
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
code .zshrc
```

2. Desça até o final do arquivo aberto na etapa anterior e cole o comando abaixo
```
export NVM_DIR="$HOME/.nvm"
      [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
      [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

3. Salve o arquivo e reinicie seu Terminal.
4. Para instalar a versão mais estável do node rode o comando abaixo
```
nvm install --lts
```

5. Para instalar o gerenciador de pacotes Yarn rode o comando abaixo
```
npm install --global yarn
```

## 💻 Configurando SSH Keys
1. Abra seu `Terminal` e execute os comandos abaixo (troque para o e-mail da sua conta do gitlab)
```
ssh-keygen -t rsa -C you@email.account
code ~/.ssh/id_rsa.pub
```

2. Copie todo o contéudo desse arquivo.
3. Acesse o [**gitlab**](https://gitlab.com/)
4. Clique em sua foto de `perfil` e depois em `preferences`
5. No menu do lado esquerdo clique na opção `ssh keys`
6. Cole o contéudo copiado na area de `key`
7. Clique no botão `add Key`.
8. Volte para o terminal e rode os comandos abaixo (trocando pelo seu nome/email)

```
  git config --global user.name "Seu nome"
  git config --global user.email "Seu email scaffold"  
```
  
