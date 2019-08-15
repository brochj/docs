# Preparando ambiente no ubuntu 18.04.3

## Atualizando os pacotes do sistema  
#### 1. Modo Rápido 

  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
#### 2. Modo lento

  - `sudo apt update`
  - `apt list --upgradable`
  - `sudo apt upgrade`



## Instalando o curl  
  - Instalando o `curl` [[ link ]](https://www.cyberciti.biz/faq/howto-install-curl-command-on-debian-linux-using-apt-get/)  
  
  ```bash
  sudo apt install curl -y
  ```
  


## Instalando o Node.js  
#### 1. Instalar a versao LTS   
- Ver o número da versão LTS em [nodejs.org/downloads](https://nodejs.org/en/download/)

#### 2. via package manager  [(instructions)](https://github.com/nodesource/distributions/blob/master/README.md#installation-instructions)
```bash
  curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
  sudo apt-get install -y nodejs
```


## Instalando o Yarn
 
#### 1. Configurando o repositório [[ Link ]](https://yarnpkg.com/lang/en/docs/install/#debian-stable)
```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```
#### 2. Instalando o yarn
  ```bash
  sudo apt update -y && sudo apt install yarn -y
  ```
  - Verificar se esta instalado.
  ```bash
  broch@broch-pc:~$ yarn -v
  #output
  1.17.3
  ```
  
#### 1. Possível erro
  - Surgiu quando fiz a instalação no Deepin, para reproduzir `yarn -v`.
  ```bash
    /usr/share/yarn/lib/cli.js:46083
  let {
      ^
  SyntaxError: Unexpected token {
      at exports.runInThisContext (vm.js:53:16)
      ....
  ```
  
  >Devido ao uso do nome `nodejs` ao invés de `node` em algumas distribuições, existem chances do yarn reclamar que o node não está instalado. Uma solução para isso é adicionar um alias em seu arquivo `.bashrc`, dessa forma: `alias nodejs=node`. Isso irá direcionar o yarn a qualquer que tenha sido a versão do node que você decidiu usar.
  
  
#### 1. **SOLUÇÃO:**  
- Na pasta home/**${user}** `ls -a` abrir/criar o `.bash_aliases` e adicionar a linha `alias nodejs=node`
  
  
## Instalando o GIT
```bash
  sudo apt install git
```
## Visual Studio code
#### Setup on linux [[link]](https://code.visualstudio.com/docs/setup/linux)  
  
```bash
  sudo snap install code --classic
``` 
  
## React Native

#### 1. Instalando o React Native CLI [[Link]](https://facebook.github.io/react-native/docs/getting-started.html#the-react-native-cli-1)
```bash
sudo yarn global react-native-cli
```  
ou
```bash
sudo npm install -g react-native-cli
```  

>`-g` significa que vai instalar de forma **global**  

- Verificando se foi instalado `react-native --version`.
```bash
broch@broch-pc:~$ react-native --version
react-native-cli: 2.0.1  //OK
react-native: n/a - not inside a React Native project directory
```

#### 2. Java Development Kit [[Link]](https://facebook.github.io/react-native/docs/getting-started.html#java-development-kit)

  ```bash
$ sudo add-apt-repository ppa:openjdk-r/ppa
$ sudo apt-get update
$ sudo apt-get install openjdk-8-jdk
  ```  
  >A versão 8 do JDK é obrigatória, não utilize versões mais recentes. 

  > Se aparecer um menu de confirmacao, navegar por ele utilizando TAB e SETAS
  
  
2.1. Verificando instalação com `java -version` ou `javac -version`
  ```bash
broch@broch-pc:~$ java -version
openjdk version "1.8.0_222"
OpenJDK Runtime Environment (build 1.8.0_222-8u222-b10-1ubuntu1~18.04.1-b10)
OpenJDK 64-Bit Server VM (build 25.222-b10, mixed mode)

  ``` 
2.2 Instalando libs gráficas  

Em grande parte das vezes precisamos instalar algumas bibliotecas da versão 32bits do Linux para conseguir emular nosso projeto e para isso vamos utilizar o seguinte comando:

`sudo apt-get install gcc-multilib lib32z1 lib32stdc++6`

## Instalando o android SDK  

Baseado no tutorial da [Rockseat](https://docs.rocketseat.dev/ambiente-react-native/android/linux#configurando-sdk-do-android-no-linux)


#### 1. Crie uma pasta em um local desejado para instalação da SDK. Ex: `~/softwares/Android/Sdk`

>Anote esse caminho para ser utilizado posteriormente

>Acesse https://developer.android.com/studio/#downloads, na opção "Command line tools only" baixe a SDK referente ao seu sistema operacional. Após feito o Download, extraia o conteúdo do pacote para a pasta criada no passo anterior. 
#### 2. Configurando as variáveis de ambiente

>Com esse endereço precisamos configurar algumas variáveis ambiente em nosso sistema, procure pelo primeiro dos seguintes arquivos existentes no seu sistema: `~/.bash_profile`, `~/.profile`, `~/.zshrc` ou `~/.bashrc`.

>Se nenhum desses arquivos existir, crie o ~/.bash_profile. Caso esteja utilizando uma pasta diferente para a SDK do Android, altere acima.

```bash
nano $HOME/.zshrc
```
Dentro do arquivo dicione essas três linhas no arquivo (de preferência no início)
```bash
export ANDROID_HOME=$HOME/softwares/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools

```  

Verificando se deu certo com `echo $PATH`
```bash
    broch@broch-pc:~$ echo $PATH
    (...)oracle/db/bin
    :/home/broch/Android/Sdk/emulator
    :/home/broch/Android/Sdk/tools
    :/home/broch/Android/Sdk/tools/bin
    :/home/broch/Android/Sdk/platform-tools
```
Se aparecer esses caminhos está OK.


2.1 No terminal 
```bash
source $HOME/.zshrc
```
2.2 Aceitando as licenses do sdk

```bash
~/softwares/Android/Sdk/tools/bin/sdkmanager --licenses
```
```bash
~/softwares/Android/Sdk/tools/bin/sdkmanager "platform-tools" "platforms;android-27" "build-tools;27.0.3"
```

####  Verificando se instalou SDK corretamente com o comando `adb`
```bash
broch@broch-pc:~$ adb

Android Debug Bridge version 1.0.41
Version 29.0.2-5738569
Installed as /home/broch/softwares/Android/Sdk/platform-tools/adb
```


  
 ## Script final

```bash

    #!/bin/bash
echo Atualizando repositórios..
if ! apt update
then
    echo "Não foi possível atualizar os repositórios. Verifique seu arquivo /etc/apt/sources.list"
    exit 1
fi
echo "Atualização feita com sucesso"


echo "Atualizando pacotes"
if ! apt upgrade -y
then
    echo "Não foi possível atualizar pacotes."
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"


echo "Atualizando pacotes já instalados"
if ! apt dist-upgrade -y
then
    echo "Não foi possível atualizar pacotes."
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if ! apt install curl -y
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando Yarn
if ! curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg
then
    echo "Não foi possível instalar o pacote yarn"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando Yarn
if ! sudo apt-key add
then
    echo "Não foi possível instalar o pacote yarn"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando Yarn
if ! sudo tee /etc/apt/sources.list.d/yarn.list
then
    echo "Não foi possível instalar o pacote yarn"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

echo "Atualizando pacotes"
if ! apt update -y
then
    echo "Não foi possível atualizar pacotes."
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if ! apt install yarn -y
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if ! apt install git
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if ! snap install code --classic
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if ! yarn global react-native-cli
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if ! add-apt-repository ppa:linuxuprising/java -y
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if ! apt update -y
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if ! apt install oracle-java12-installer -y
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if ! apt install oracle-java12-set-default -y
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if ! apt update -y
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"

# Instalando curl
if !apt install android-sdk -y
then
    echo "Não foi possível instalar o pacote curl"
    exit 1
fi
echo "Atualização de pacotes feita com sucesso"




 
```


## Conflito de shortcuts do ubuntu com VSCode

[tutorial link](https://unix.stackexchange.com/questions/394143/how-to-disable-gnome-ctrlaltdown-and-ctrlaltup-shortcut/420395#420395)