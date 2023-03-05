# Introdução ao GIT

#### GIT é um sistema de versionamento de código distribuído, cujo criador se chama Linus Torvalds
#### Os sistemas que utlizamos no dia a dia possuem uma interface gráfica, mais conhecida como GUI (Graphic User Interface), porém o git utiliza o que chamamos de CLI(Command Line Interface), ou seja, a forma de interagir com o git é através de linhas de comando.

## Tópicos fundamentais sobre GIT
### 1) SHA1 - Secure Hash Algorithm
####    É um algoritmo de encriptação desenvolvido pela NSA (Agência de segurança dos Estados Unidos) responsável por pegar o arquivo e embaralhar as informações de forma muito específica, essa encriptação gera um conjunto de caracteres indentificadores de 40 dígitos com combinação única. Em poucas palavras, é uma forma curta e segura de representar um arquivo.

### 2) Objetos fundamentais
####    BLOBS: Contém metadados do arquivo
##### 1. \0 
##### 2. Tipo do objeto
##### 3. Tamanho do arquivo
##### 4. Tamanho da string

####    TRES: Armazenam e apontam para diferentes tipos de Blobs
##### 1. \0 
##### 2. Nome do arquivo
##### 3. Sha1
##### 4. Blob
##### 5. Tamanho
###### Podem apontar para blobs ou para outras tres


####    COMMITS: Armazena todos os objetos e aponta para uma árvore e o último commit realizado antes dele.
##### 1. Tree
##### 2. Commit parente
##### 3. autor
##### 4. mensagem
##### 5. sha1
##### 6. Tamanho
##### 7. Timestamp

<p align="center">
  <img src="https://github.com/IasmimFGodoy/dio-desafio-github-primeiro-repositorio/blob/main/Introdu%C3%A7%C3%A3o%20ao%20Git%20e%20ao%20GitHub/assets/ArvoreCommits.png?raw=true">
</p>

### 3) Por que o Git é um sistema distribuído e seguro?
#### Porque para alterar o hash da versão final é necessário alterar desde  primeiro commit, mesmo que isso fosse possível, cada máquina além do servidor teria uma cópia da versão original.

## Chave SSH
#### A chave SSH é uma forma de estabelecer uma conexão segura e encriptada entre duas máquinas:
##### A sua máquina e o servidor do github.
<p align="center">
  <img src="https://github.com/IasmimFGodoy/dio-desafio-github-primeiro-repositorio/blob/main/Introdu%C3%A7%C3%A3o%20ao%20Git%20e%20ao%20GitHub/assets/Chave%20ssh.png?raw=true">
</p>

#### Passo 1: entrar no perfil do github e configurar a chave pública
##### Perfil -> settings -> SSH and GPG Keys
<p align="center">
  <img src="https://github.com/IasmimFGodoy/dio-desafio-github-primeiro-repositorio/blob/main/Introdu%C3%A7%C3%A3o%20ao%20Git%20e%20ao%20GitHub/assets/gerando%20chaves%20ssh.PNG?raw=true">
</p>

##### Title: colocar o titulo que desejar, geralmente se utiliza o nome da máquina do usuário
##### Key type: você pode escolher entre AUTHENTICATION KEY ou SIGNING KEY
###### AUTHENTICATION KEY: você entra com suas credenciais exclusivas que provam quem você declara ser e podem ser utilizadas para acessar repositórios.
###### SIGNING KEY: você entra com suas credenciais exclusivas que provam quem você declara ser e podem ser utilizadas para assinar commits.
1.  Abrir o git bash e digitar:    ssh_keygen -t ed_25519 -C [seuemailgithub]
2. você precisará entrar com sua senha
3. confirme sua senha
##### A saída do comando digitado deverá ser inserida no campo Key 
##### Este processo irá criar dentro de C/users/[user]/.ssh o arquivo com a chave publica e outro arquivo com a chave privada.

#### Passo 2: digitar no git bash:
##### cat id_ed25519.pub 
###### o código gerado é a chave pública
###### se digitar pwd é possível visualizar o caminho completo

### Inicializando o SSH Agent:
#### O SSH Agent é responsável por lidar com as chaves SSH

1. eval $(ssh-agent -s)
###### saída: agent pid 470
###### 470: este número é variável, pois ele dá um start no agent poara rodar em plano de fundo e este número representa o número do processo que está rodando.

2. ssh-add id_ed25519 
###### Passando a chave privada, então será solicitado a senha.
###### Depois de passar a senha correta, o git devolverá como saída o e-mail relacionado com esta chave.

#### Quando o SSH está configurado, clonar um repositório no github não é feito da mesma forma como de costume, pois não basta só utilizar o git clone, pois este utiliza o protocolo https, mas estamos utilizando o ssh.
#### Clonando um repositório utilizando o ssh:
1. Entrar no repositório desejado: 
2. Clicar em <> Code
<p align="cemter">
  <img src="https://github.com/IasmimFGodoy/dio-desafio-github-primeiro-repositorio/blob/main/Introdu%C3%A7%C3%A3o%20ao%20Git%20e%20ao%20GitHub/assets/Clonando%20por%20meio%20de%20ssh%201.png?raw=true">
<p>
3. Copiar o link
<p align="cemter">
  <img src="https://github.com/IasmimFGodoy/dio-desafio-github-primeiro-repositorio/blob/main/Introdu%C3%A7%C3%A3o%20ao%20Git%20e%20ao%20GitHub/assets/Clonando%20por%20meio%20de%20ssh%202.png?raw=true">
<p>
4. Ir no terminal e caminhar com cd até a pasta que deseja baixar o projeto e digitar o seguinte comando

#####   git clone git@github.com:usuario/repositorio.git
##### digitar YES
##### Entrar com sua senha
##### Repositório clonado.

