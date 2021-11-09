# Ambiente de desenvolvimento

## Tema e fonte [VS Code]

### Extensão dracula

`Ctrl + shift + P` `color theme` `dracula`

### Alterando a fonte

#### 1. Baixar o [firacode](https://github.com/tonsky/FiraCode#solution)

#### 2. Extrair e instalar as fontes que ficam na pasta `/ttf`

#### 3. `Ctrl + shift + P` `settings (JSON)`

#### 4. No settings adicionar essas configs

```json
"editor.formatOnSave": true,
"editor.fontFamily": "Fira Code",
"editor.fontLigatures": true,
"editor.rulers": [80,120],
"editor.tabSize": 2,
"editor.renderLineHighlight": "gutter",
"terminal.integrated.fontSize": 14,

"emmet.syntaxProfiles": {
    "javascript": "jsx"
},
"emmet.includeLanguages": {
    "javascript": "javascriptreact"
},
"javascript.updateImportsOnFileMove.enabled": "never",
"breadcrumbs.enabled": true,
"editor.parameterHints.enabled": false,
```

## Plugins [VS Code]

### Adicionar a extensão `vscode-icons`

### Adicionar a extensão `editorconfig`

### Adicionar a extensão `eslint`

### Adicionar a extensão `prettier -code formatter`

#### 1. `Ctrl + shift + P` `settings (JSON)`

#### 2. No settings adicionar essas configs

```json
  "prettier.eslintIntegration": true,
```

### Adicionar a extensão `Rocketseat ReactJS` e `React Native`

## Tema e fonte [Terminal] (linux e mac)

#### 1.Ir nas configs do terminal e trocar a fonte para a firacode-retina con tamanho 14

#### 2. Ir em [dracula theme](https://draculatheme.com/) e buscar por terminal

#### 3. escolher qual está utilizando (terminal.app)

#### 4. Seguir o tuto do dracula, mas basicamente é o `git clone` depois ir nas preferencias do terminal e importar o theme onde foi feito o git clone

## Oh my Zsh [Terminal]

#### 1. Ir para o site [ohmyz.sh](https://ohmyz.sh/)

#### 2. Instalar via `curl`

```bash
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

#### 3. Instalar o tema [Oh My Zsh spaceship](https://github.com/denysdovhan/spaceship-prompt#installing)

> Selecionar o metodo oh-my-zsh e seguir as intrucoes de la

#### 4. Dentro do .zshrc

- Adicionar as linhas

```bash
SPACESHIP_PROMPT_ORDER=(
  user          # Username section
  dir           # Current directory section
  host          # Hostname section
  git           # Git section (git_branch + git_status)
  hg            # Mercurial section (hg_branch  + hg_status)
  exec_time     # Execution time
  line_sep      # Line break
  vi_mode       # Vi-mode indicator
  jobs          # Background jobs indicator
  exit_code     # Exit code section
  char          # Prompt character
)

SPACESHIP_PROMPT_ADD_NEWLINE=false
SPACESHIP_CHAR_SYMBOL="❯"
SPACESHIP_CHAR_SUFFIX=" "
```

## Plugins [Terminal]

#### 1. instalar o [zplugin](https://github.com/zdharma/zplugin#installation)

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/zdharma/zplugin/master/doc/install.sh)"
```

#### 2. Dentro do .zshrc

- Adicionar as linhas abaixo das configs do zplugin

```bash
zplugin light zsh-users/zsh-autpsuggestions
zplugin light zsh-users/zsh-completions
zplugin light zdharma/fast-syntax-highlighting
```

## Extensões Chrome

#### 1. [React developer tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=pt-BR)

#### 2. Opcional [Dracula DevTools Theme](https://chrome.google.com/webstore/detail/dracula-devtools-theme/gdhgkfojgddhijhlnnnbopleoabkeife?hl=pt-BR)

## Ferramentas

#### 1. Baixar instalar o [insomnia](https://insomnia.rest/download/)

```bash
sudo snap install Insomnia
```

#### 2. Baixar e instala o [DevDocs](https://devdocs.egoist.sh/)

#### Nas Configs, selecionar as linguagens javascript, react, reactNative, node v10
