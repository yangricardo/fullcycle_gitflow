# Fullcycle Notas: Padrões e Técnicas Avançadas com Git e GitHub

## 1. Instalação GIT

Ubuntu: `sudo apt-get install git`
Fedora: `sudo dnf install git`

### Customização ZSH / Ohmyzsh

Adicione a variavel `plugin` no arquivo `.zshrc` o elemento git

## 2. Gitflow

### Instalação

Ubuntu: `sudo apt-get install git-flow`
Fedora: `sudo dnf install gitflow`

- Criar repositorio git: `git init`
- Habilitar git flow no repositorio: `git flow init`
  > [Mais informações sobre configuração do git flow](https://www.atlassian.com/br/git/tutorials/comparing-workflows/gitflow-workflow)

### Uso do GitFlow

O GitFlow é um plugin ao Git que facilita no fluxo de trabalho com o git, a partir de um fluxo de trabalho bastante opinativo.

### Feature

Para iniciar uma nova feature: `git flow feature start <feature_name>`. O comando irá criar um branch seguindo o padrão `feature/<feature_name>`, conforme o especificado.

Após a execução dos commits referentes a feature, execute `git flow feature finish <feature_name>`. Isso irá realizar o merge com o branch `develop`

### Release

Execute o comando `git release start <version_id>` para consolidar o branch `develop` no master. Após os commits de ajustes serem consolidados, execute `git release finish <version_id>`. Isso irá realizar o merge do branch `develop` no `main` e gerar o merge do branch `main` com o `develop`

## 3. GPG Keys e Assinatura de Commits

- `gpg --list-secret-key --keyid-form LONG`: lista chaves gpg do ambiente
- `gpg --full-generate-key`: gera uma nova chave gpg
  - adicione o nome e email configurado para o git e utilize rsa de 4096 bits
- `gpg --edit-key <GPG_KEY_ID>`: abre terminal de edição da chave gpg
  - `adduid`: similar ao processo de criação de chave gpg, permite associar a chave novos emails associados
  - `uid <#>`: `<#>` é o identificador do uid, permite selecionar para operações
  - `trust`: permite definir o nivel de confiança sobre um uid / email
  - `save`: conclui operações no terminal uid
- `gpg --armor --export <GPG_KEY_ID>`: exporta o formato pem da chave gpg para ser registrada no GitHUB / GitLab e similares
- `gpgconf --launch gpg-agent`: permite que o ambiente não solicite a senha da chave gpg a cada assinatura de commit
- adicionar `export GPG_TTY=$(tty)` ao final do `.zshrc` ou arquivo de profile de ambiente similar

## 4. Pull Requests (PR) e Code Review

### [Protegendo Branches](https://docs.github.com/pt/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/managing-a-branch-protection-rule)
