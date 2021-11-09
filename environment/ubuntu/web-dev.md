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

- Instalando o `curl` [[link]](https://www.cyberciti.biz/faq/howto-install-curl-command-on-debian-linux-using-apt-get/)

```bash
sudo apt install curl -y
```

## Instalando o Node.js

#### 1. Instalar a versao LTS

- Ver o número da versão LTS em [nodejs.org/downloads](https://nodejs.org/en/download/)

#### 2. via package manager [(instructions)](https://github.com/nodesource/distributions/blob/master/README.md#installation-instructions)

```bash
  curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
  sudo apt-get install -y nodejs
```

## Instalando o Yarn

#### 1. Configurando o repositório [[Link]](https://yarnpkg.com/lang/en/docs/install/#debian-stable)

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

> Devido ao uso do nome `nodejs` ao invés de `node` em algumas distribuições, existem chances do yarn reclamar que o node não está instalado. Uma solução para isso é adicionar um alias em seu arquivo `.bashrc`, dessa forma: `alias nodejs=node`. Isso irá direcionar o yarn a qualquer que tenha sido a versão do node que você decidiu usar.

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

> `-g` significa que vai instalar de forma **global**

- Verificando se foi instalado `react-native --version`.

```bash
broch@broch-pc:~$ react-native --version
react-native-cli: 2.0.1  //OK
react-native: n/a - not inside a React Native project directory
```

#### 2. Java Development Kit [[Link]](https://facebook.github.io/react-native/docs/getting-started.html#java-development-kit)

2.1. Adiciona repositório

```bash
    sudo add-apt-repository ppa:linuxuprising/java -y
```

2.2. Atualiza os repositórios

```bash
    sudo apt update
```

2.3. Instala o java12

```bash
    sudo apt install oracle-java12-installer -y
```

> Se aparecer um menu de confirmacao, navegar por ele utilizando TAB e SETAS

2.4. Verificando instalação com `javac --version`

```bash
    broch@broch-pc:~$ javac --version
    javac 12.0.2
```

2.5. Setando a variável de ambiente

```bash
    sudo apt install oracle-java12-set-default
```

## Instalando o android SDK

> Uns 500 MB, demora um pouco mais..

```bash
  sudo apt update && sudo apt install android-sdk -y
```

#### Verificando se instalou corretamente com o comando `adb`

```bash
  broch@broch-pc:~$ adb
  Android Debug Bridge version 1.0.39
  Version 1:8.1.0+r23-5~18.04
  Installed as /usr/lib/android-sdk/platform-tools/adb
```

#### Configurando as variáveis de ambiente

```bash
nano $HOME/.bash_profile
```

1.  Dentro do arquivo adicionar e salvar

```bash
  export ANDROID_HOME=$HOME/Android/Sdk
  export PATH=$PATH:$ANDROID_HOME/emulator
  export PATH=$PATH:$ANDROID_HOME/tools
  export PATH=$PATH:$ANDROID_HOME/tools/bin
  export PATH=$PATH:$ANDROID_HOME/platform-tools
```

3. No terminal

```bash
source $HOME/.bash_profile
```

4. Verificando se deu certo com `echo $PATH`

```bash
    broch@broch-pc:~$ echo $PATH
    (...)oracle/db/bin
    :/home/broch/Android/Sdk/emulator
    :/home/broch/Android/Sdk/tools
    :/home/broch/Android/Sdk/tools/bin
    :/home/broch/Android/Sdk/platform-tools
```

5. Se aparecer esses caminhos está OK.

## Script final

### Em desenvolvimento

```bash
#!/bin/bash
#Atualizando
sudo apt update;
sudo apt upgrade -y;
#Instalando o curl
sudo apt install curl -y;
# Instalando o Yarn
sudo curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg;
sudo apt-key add;
sudo tee /etc/apt/sources.list.d/yarn.list;
sudo apt update -y;
sudo apt install yarn -y;
# instalando o GIT
sudo apt install git;
# instalando o VS code
sudo snap install code --classic;
# instalando o React-native-cli
sudo yarn global react-native-cli;
# Instalando Java Development Kit
sudo add-apt-repository ppa:linuxuprising/java -y;
sudo apt update -y;
sudo apt install oracle-java12-installer -y;
sudo apt install oracle-java12-set-default -y;
# Instalando o Android SDK
sudo apt update -y;
sudo apt install android-sdk -y;

```

### Em desenvolvimento

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
