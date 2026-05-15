# Curso de Docker — Resumo

## 1. Introdução

**Objetivo:** pegar uma aplicação que está na máquina local e subir para um provedor cloud, entendendo o que são **containers** e **imagens**.

Docker roda nos sistemas operacionais Windows, Mac e Linux.

Docker é uma **plataforma criada para construir, rodar e transferir aplicações** do ambiente de teste/desenvolvimento para o ambiente em produção.

> **Construir, rodar e transferir.**

### Por que Docker?

Os problemas acontecem porque, quando passamos do local para o servidor, podemos ter vários problemas:
- Configuração do ambiente local diferente da configuração do servidor remoto
- Diferença na versão de tecnologias (Node, PHP, etc.)
- Quantidade de arquivos

O **container** é onde eu coloco a minha aplicação para transferir para o servidor web. Dentro do container ficam todos os arquivos da aplicação e a versão necessária das dependências.

---

## 2. Container vs VM

### Virtualização (VM)

Virtualização é quando eu tenho um **Hypervisor** rodando em cima do meu hardware. Dentro do hypervisor eu consigo colocar outro SO (Windows, Mac, Linux). Cada hypervisor tem suas características (quantidade de RAM, HD), limitado ao que temos no PC, e em cada hypervisor eu instalo o environment (ambiente) para rodar minha aplicação.

**Exemplos de hypervisors:**
- VMware Workstation / VMware ESXi
- Windows Virtual PC / Microsoft Hyper-V
- Xen
- KVM

**Limitação:** se o meu hardware tem 32GB de RAM e eu criar 4 VMs, vou ter que dividir — cada VM ficará com 8GB.

### Container

Utilizamos os containers em cima do Linux **sem a necessidade de criar uma VM** para cada ambiente. Posso ter um container de cada SO que eu precisar. Em cima do meu hardware sempre vai ter um sistema Linux rodando, então se eu tiver 32GB de RAM, o Docker distribui esses 32GB entre os containers, e cada container roda de forma isolada.

> **Containers = inicialização mais fácil e rápida que VMs + muito menos consumo de recursos.**

---

## 3. O Docker — Como Funciona

Para colocar nossa aplicação (back, front, banco) dentro do Docker, criamos um arquivo **Dockerfile** dentro da aplicação. Esse arquivo contém parâmetros para que a imagem possa ser criada — ele é o responsável por criar a imagem.

### O que tem dentro de uma imagem
- Um pedaço do OS
- Ambiente (ex: Node)
- Arquivos
- Bibliotecas
- Variáveis

> **Imagem = cópia perfeita do que está rodando no meu sistema, com todas as dependências necessárias.**

A partir desse momento, está tudo pronto para pegar a imagem e colocar dentro do container, que será transferido entre outros containers até chegar na produção.

### Docker Hub

Se eu tenho a aplicação rodando localmente dentro de um container, para essa imagem chegar até o servidor ela passa pelo **registry (Docker Hub)** — semelhante ao GitHub. Eu mando a imagem para o Docker Hub e de lá envio para produção. Caso eu perca a imagem local, ela continua disponível no Docker Hub. É uma forma de **versionamento do Docker**.

### Comandos iniciais

```bash
# Criar uma imagem (precisa de um Dockerfile)
docker build -t alias

# Listar imagens
docker images

# Rodar o Docker pelo terminal
docker run alias

# Ver containers rodando
docker ps

# Ver todos os containers (rodando ou não)
docker ps -A
```

---

## 4. Linux Básico

### Tabela Windows × Linux

| Nº | Windows | Linux | Descrição |
|---|---|---|---|
| 1 | dir | ls -l | Directory listing |
| 2 | ren | mv | Rename a file |
| 3 | copy | cp | Copying a file |
| 4 | move | mv | Moving a file |
| 5 | cls | clear | Clear Screen |
| 6 | del | rm | Delete file |
| 7 | fc | diff | Compare contents of files |
| 8 | find | grep | Search for a string in a file |
| 9 | command /? | man command | Display the manual/help details |
| 10 | chdir | pwd | Returns your current directory location |
| 11 | time | date | Displays the time |
| 12 | cd | cd | Change the current directory |
| 13 | md | mkdir | Create a new directory/folder |
| 14 | echo | echo | Print something on the screen |
| 15 | edit | vim (depende do editor) | Write into files |
| 16 | exit | exit | Leave the terminal/command window |
| 17 | format | mke2fs ou mformat | Format a drive/partition |
| 18 | free | mem | Display free space |
| 19 | rmdir | rm -rf / rmdir | Delete a directory |
| 20 | taskkill | kill | Kill a task |
| 21 | tasklist | ps x | List running tasks |
| 22 | set var=value | export var=value | Set environment variables |
| 23 | attrib | chown / chmod | Change file permissions |
| 24 | tracert | traceroute | Print the route packets trace |
| 25 | at | cron | Daemon to execute scheduled commands |
| 26 | type | cat | Print contents of a file |
| 27 | ping | ping | Send ICMP ECHO_REQUEST |
| 28 | nslookup | nslookup | Query DNS interactively |
| 29 | chdisk | du -s | For disk usage |
| 30 | tree | ls -R | List directory recursively |

### Distros mais famosas do Linux
- Ubuntu
- Debian
- CentOS
- Fedora
- Alpine

### Baixar e rodar um Ubuntu no Docker

```bash
# Baixar a imagem do Ubuntu
docker pull ubuntu

# Rodar e depois parar (modo interativo)
docker run -it ubuntu
```

### Comandos Linux essenciais

```bash
# Ver usuário atual
whoami

# Enviar algo para a tela
echo alguma coisa

# Saber qual diretório você se encontra
echo $0

# Últimos comandos executados
history
```

### Gerenciamento de pacotes (apt)

Pacotes no Linux são como os aplicativos do Windows. Sempre que pegamos um Linux, primeiro fazemos update dos pacotes.

```bash
# Listar pacotes (advanced package tool)
apt list

# Atualizar pacotes
apt update

# Instalar um pacote (ex: editor de texto nano)
apt install nano

# Criar um arquivo .txt com o nano
nano teste.txt

# Remover um pacote
apt remove nano
```

### Sistema de arquivos do Linux

No **Windows** tudo começa em:
```
C:\
   arquivos e programas
   windows
   documentos
```

No **Linux** começamos a partir do **root (`/`)**:
- `/bin` — comandos binários (como `ls`)
- `/dev` — arquivos de device
- `/etc` (extended tool chest) — arquivos pertencentes ao root
- `/home` — diretório dos usuários

### Navegação e listagem

```bash
# Lista tudo do diretório
ls

# Um item por linha
ls -1

# Informações detalhadas (permissões etc.)
ls -l

# Conteúdo de outro diretório sem entrar nele
ls /etc

# Onde estou? (print working directory)
pwd

# Mudar de diretório (change directory)
cd nome_do_diretorio

# Ir para a home
cd ~
```

> **Dica:** a tecla **TAB** faz autocomplete.

### Criar, mover, remover

```bash
# Criar diretório
mkdir nome_diretorio

# Renomear ou mover
mv flavio flaviorodrigo

# Criar arquivos (um ou vários)
touch flavio.txt
touch flavio.txt flavio2.txt

# Remover arquivo
rm flavio.txt

# Remover tudo que começa com "hi"
rm hi*

# Remover diretório
rm -r flavioRodrigo
```

### Visualizar conteúdo de arquivos

```bash
# Conteúdo inteiro
cat etc/debconf.conf

# Conteúdo paginado
more /etc/denconf.conf
```

### Redirecionamento

- **Input:** teclado envia informações ao Linux
- **Output:** tela mostra o resultado

Eu posso mudar o destino do output para um arquivo:

```bash
# Joga conteúdo de flavio.txt em teste.txt
cat flavio.txt > teste.txt

# Coloca texto direto em um arquivo
echo hi docker > docker.txt
```

### Busca (grep) — global regular expression print

```bash
# Procurar "hello" nos arquivos indicados
grep hello docker.txt flavio.txt

# Procurar em todos os arquivos do diretório (recursivo, case-insensitive)
grep -i -r hello .
```

### Find

`find` encontra arquivos e diretórios — mostra inclusive arquivos ocultos (assim como `ls -a`).

```bash
# Somente arquivos
find -type f

# Somente diretórios
find -type d

# Por nome específico
find -type f -name "docker.txt"

# Por padrão (tudo que começa com "an")
find -type f -name "an*"
```

### Chaining (executar múltiplos comandos)

```bash
# Executa sempre, mesmo se um falhar
mkdir teste ; cd teste ; echo ok

# Para se algum comando falhar
mkdir teste && cd teste && echo ok
```

### Gerenciamento de processos

```bash
# Listar processos rodando
ps

# Executar em background (ex: sleep)
sleep 5 &

# Matar processo pelo PID
kill 118
```

### Gerenciando usuários

```bash
# Ver variações do comando
useradd

# Criar usuário com home directory
useradd -m Flavio

# Modificar usuário
usermod

# Remover usuário
userdel

# Verificar usuários criados
cat /etc/passwd

# Logar com o usuário criado dentro de um container
docker ps                               # pega o id do container
docker exec -it -u <nome_usuario> <id_container> bash
```

### Grupos de usuários

Quando criamos um usuário, podemos adicioná-lo a um grupo:
- **Grupo primário:** sempre ele mesmo
- **Grupo secundário:** os que você pode criar

```bash
# Ver grupos do usuário
groups Flavio

# Adicionar / remover / modificar grupos
groupadd
groupdel
groupmod

# Listar todos os grupos
cat /etc/group

# Adicionar usuário a um grupo
usermod -G docker flavio

# Ver grupos do usuário (de novo)
groups flavio
```

### Permissões e arquivos

```bash
ls -l
```

Saída exemplo:
```
-rw-r--r-- 1 root root   10 May 11 17:38 docker.txt
-rw-r--r-- 1 root root   14 May 11 17:34 flavio.txt
-rw-r--r-- 1 root root   14 May 11 17:34 flavio2.txt
drwxr-xr-x 2 root root 4096 May 11 17:51 teste
```

- Começa com `d` → diretório; com `-` → arquivo
- **1º bloco:** permissões do usuário dono (r=read, w=write, x=execute)
- **2º bloco:** permissões do grupo
- **3º bloco:** permissões de "everyone" (todos)

```bash
# Adicionar permissão de execução ao dono
chmod u+x docker.txt
```

---

## 5. Criando Imagens Docker

A **Docker image** contém tudo que é necessário para a aplicação funcionar. Quando converto um app em imagem, estou convertendo todo o sistema operacional para que ele rode em outra máquina.

**Conteúdo da imagem:**
- Cut-down OS (um SO reduzido dentro)
- Libraries
- Arquivos da app
- Variáveis de ambiente

**Containers** — quando temos uma imagem pronta, criamos um container e colocamos a imagem nele para rodar a aplicação:
- Ambiente isolado (como se fosse uma VM)
- Start / Stop (via linha de comando ou Docker Desktop)
- Processo que roda dentro de uma máquina

> **Fluxo:** aplicação pronta → converte para imagem com o Dockerfile → cria container → carrega imagem → roda aplicação.

### Diretivas do Dockerfile

| Diretiva | Função |
|---|---|
| `FROM` | Qual imagem base será carregada (Linux, Ubuntu, Node, Python...) |
| `WORKDIR` | Define o diretório de trabalho |
| `COPY` | Copia todos os arquivos da aplicação para a imagem |
| `ADD` | Adiciona arquivos à imagem (pode ser URL ou arquivo zipado) |
| `RUN` | Roda comandos durante o build |
| `ENV` | Configurações do ambiente |
| `EXPOSE` | Define a porta da aplicação |
| `USER` | Define o usuário para executar a aplicação |
| `CMD` / `ENTRYPOINT` | Roda comandos quando o container inicia |

### Criando a primeira imagem

Na raiz da aplicação, crie um arquivo `Dockerfile` e coloque o caminho da imagem escolhida do Docker Hub:

```dockerfile
FROM node:12-alpine
```

Build da imagem (o `.` significa "pegue tudo do diretório atual"):

```bash
docker build -t <nome_da_imagem> .
```

Rodar a imagem (`sh` = abrir no shell, `-it` = modo interativo):

```bash
docker run -it <nome_da_imagem> sh
```

Para sair do terminal do Docker:
```bash
exit
```

### Variações do COPY

```dockerfile
# Copiar apenas um arquivo específico
COPY yarn.lock

# Copiar dois ou mais arquivos
COPY yarn.lock package.json

# Copiar para um diretório específico
COPY package.json /app

# Copiar todos arquivos de um tipo específico
COPY *.json /app/

# Copiar todos os arquivos da aplicação
COPY . /app/
```

### WORKDIR + COPY

Caso não queira repetir o diretório de destino, use o `WORKDIR`:

```dockerfile
WORKDIR /app
COPY . .
```

> **Resumindo:** `COPY` copia, `WORKDIR` informa qual diretório usar, `ADD` adiciona um arquivo que não está no seu diretório (ou está zipado, ou está em uma URL externa).

### ADD

```dockerfile
# Baixar de uma URL externa
ADD https://microsoft.com/teste.json .

# Arquivo zipado (Docker descompacta automaticamente)
ADD teste.zip .
```

Depois das alterações, faça o build de novo:

```bash
docker build -t app .
```

### RUN

`RUN` serve para instalar dependências da aplicação / rodar comandos no terminal durante o build:

```dockerfile
# Instalando o python 2 dentro da nossa distro
RUN apk add --no-cache python2 g++ make
```

Para executar:
```bash
docker build -t app .
```

### ENV (environment)

Usado quando o código do Dockerfile precisa falar com uma API ou backend:

```dockerfile
ENV AAPI_URL=http://api.flaviorodrigo.com/
```

Isso coloca esse path dentro do Linux e sempre que precisar buscar algo referente a essa API, ele vai buscar nesse environment.

### EXPOSE

Informa em qual porta a aplicação vai trabalhar:

```dockerfile
EXPOSE 3000
```

### CMD vs RUN

Quando você monta o container, garanta que ele vai rodar a aplicação. A partir da imagem que você cria, ele automaticamente cria o container, e se não rodar no modo interativo (`-it`) ele vai parar. Por isso usamos `CMD` para ele executar.

- **`RUN`** → executado durante a criação da imagem
- **`CMD`** → executado quando a aplicação inicia (imagem já criada)

```dockerfile
CMD ["node", "src/index.js"]
```

### USER

Para criar usuários que vão usar aquele container/aplicação use `USER`. Sem isso, será usado o usuário **root**, o que **não é uma boa prática**. Recomenda-se colocar os usuários no topo do Dockerfile.

Primeiro cria o grupo, depois adiciona o usuário no grupo (igual no Linux):

```dockerfile
RUN addgroup dev && adduser -S -G dev andre
USER andre
```

### Rodando o container e mapeando porta

Para a aplicação funcionar, ela precisa usar a mesma porta do host (Mac/PC), então além do `EXPOSE` no Dockerfile, precisamos rodar o Docker com o mapeamento:

```bash
docker run -dp 3000:3000
```

- **`-d`** = rodar em background
- **`-p`** = porta

### Otimizando performance com cache

Pedimos para o Docker copiar o `package.json` (onde ficam as dependências) **antes** de copiar o resto da aplicação. Assim, se não houve alteração nas dependências, ele usa o **cache** da última instalação.

```dockerfile
FROM node:12-alpine
WORKDIR /app
COPY package.json .                       # Copia o arquivo de dependências; sem alteração, reusa cache
RUN apk add --no-cache python2 g++ make
RUN yarn install --production
COPY . .
CMD ["node", "src/index.js"]
EXPOSE 3000
```

### Tags (versionamento da imagem)

```bash
# Build com tag
docker build -t app:v1.0.0 .

# Remover imagem
docker image remove app:v1.0.0

# Renomear / adicionar nova tag
docker image tag app:latest app:v1.0.0
```

### Compartilhando a imagem (Docker Hub)

```bash
# 1. Build da imagem
docker build -t app:v1 .

# 2. Lista as imagens (pega o ID da sua)
docker images

# 3. Adiciona a tag no formato usuario/repositorio:tag
docker image tag dfd5f062fae8 flaviorsr/app:v1

# 4. Login no Docker Hub
docker login

# 5. Push para o Docker Hub
docker push flaviorsr/app:v1
```

> **Convenção:** `usuario/repositorio:tag`. Sempre cria tags para evitar mandar imagens repetidas.

Quando você altera algo na imagem, é importante buildar uma nova versão com nova tag. Ao fazer o push, o Docker manda **somente as alterações** — mais rápido que a primeira vez.

### Compartilhando a imagem via arquivo (.tar)

```bash
# Ver imagens
docker images

# Ajuda do save
docker image save --help

# Salvar imagem em arquivo .tar
docker image save -o <nome_arquivo.tar> <nome_da_imagem>

# Carregar imagem de um .tar
docker image load -i <nome_do_zip>
```

Ao carregar, a imagem vai aparecer junto com as outras.

---

## 6. Containers

```bash
# Iniciar container
docker run <nome_da_imagem>

# Iniciar em background
docker run -d <nome_da_aplicacao>

# Ver containers rodando
docker ps
```

O `-d` deixa o container rodando em **background**, liberando o terminal.

Cada container ganha um nome automático do Docker — mas você pode passar o seu:

```bash
docker run -d --name <nome_do_container> <nome_da_imagem>
```

### Start / Stop

```bash
docker stop <nome_do_container>
docker start <nome_do_container>
```

> **Diferença:** `docker run` cria + roda; `docker start` apenas roda um já criado.

### Logs

```bash
docker logs <id_container>        # Logs do container
docker logs -f <id_container>     # Follow (acompanhar em tempo real)
docker logs -n <id_container>     # Últimas N linhas
docker logs -t <id_container>     # Com timestamps
```

### Mapeamento de portas

```bash
docker run -d -p <porta_host>:<porta_container> --name <nome_container> <nome_imagem>
```

- **Porta do Host (esquerda — ex: 80):** porta na sua máquina física que será aberta para o mundo externo. Ao acessar `http://localhost:80`, você se conecta ao container.
- **Porta do Container (direita — ex: 3000):** porta interna onde a aplicação está rodando e escutando.

Exemplo:
```bash
docker run -d -p 80:3000 --name banana app:v2
```

### Executar comandos dentro do container

```bash
# Listar arquivos dentro do container sem entrar nele
docker exec <nome_do_container> ls

# Entrar no terminal do container
docker exec -it <nome_do_container> sh
```

### Remover containers

```bash
# Remover (container precisa estar parado)
docker rm <nome_do_container>

# Forçar exclusão de container rodando
docker rm -f <nome_do_container>

# Listar todos os containers (rodando ou não)
docker ps -a
```

---

## 7. Volumes

Volume é quando eu **crio um backup do container** — sempre que eu criar um novo container, ele vai vir com os arquivos que eu tinha. **O volume é persistente.**

```bash
# Criar um volume
docker volume create <nome_do_volume>

# Inspecionar o volume
docker volume inspect <nome_do_volume>

# Criar container associado a um volume
docker run -d -p <porta_host>:<porta_container> --name <nome_container> -v <nome_volume>:<diretorio_no_linux> <nome_imagem>

# Entrar no terminal do container
docker exec -it <nome_do_container> sh

# Remover o container (o volume continua existindo)
docker rm -f <nome_do_container>
```

> Como o container tinha um volume, ele **não perde os arquivos**. Importante sempre fazer esse backup.

### Copiar arquivos entre máquina e container

```bash
# Do container para a máquina local (o "." significa "para cá")
docker cp <container>:<diretorio/arquivo> .
docker cp kiwi2:/app/teste.txt .

# Da máquina local para o container
docker cp <arquivo_local> <container>:<diretorio_do_container>
docker cp copia.txt kiwi2:/app
```

---

## 8. Docker Compose

O **Docker Compose** é quando a gente separa a aplicação em **containers diferentes** — por exemplo: front, back e banco de dados, cada um com seu container dedicado.

O Docker Compose precisa estar instalado. Se você tem o **Docker Desktop**, o plugin do Compose já vem incluso.

### docker-compose.yml

É o arquivo que **orquestra tudo** dentro do Docker. Dentro dele eu configuro o que vai subir no front, no back e no database. Ele passa instruções sobre os containers que vão subir.

- A extensão `.yml` vem da linguagem **YAML**.
- O Docker Compose usa YAML para escrever as configurações.
- É sempre lido **de cima para baixo**.
- Usa indentação (igual ao Python).

### Comandos do Compose

```bash
# Build + subir containers
docker compose up --build

# Subir containers (imagens já criadas)
docker compose up

# Subir em background
docker-compose up -d

# Parar e remover containers
docker compose down
```

> **Recomendado:** usar `--build` junto com `-d` para deixar o terminal ativo.

`docker compose down` encerra a aplicação — para os containers e **os remove completamente**.

---

## 9. Rede do Docker

Para saber o IP de cada container:

```bash
docker exec -it -u root <id_container> sh
```

Dentro do terminal Linux do container, use:

```bash
ifconfig
```

O IP aparece em `addr:`.

**Exemplo de mapeamento em uma stack com Compose:**
- Front: `172.18.0.4`
- Back: `172.18.0.3`
- DB: `172.18.0.2`

Para verificar a conectividade entre containers, dentro do container use:

```bash
ping <nome_do_container>
```

Isso funciona porque o **Docker cria uma rede virtual própria**, com **servidor DNS próprio** e **DNS resolver** que mapeia o hostname do container ao endereço IP.

### Logs do Compose

```bash
docker compose logs
```

> Os logs vêm **sempre separados por sessão (serviço)**.

---

## Anexo — Glossário rápido

- **Imagem:** snapshot/cópia da aplicação com OS + libs + arquivos + variáveis.
- **Container:** instância em execução de uma imagem; ambiente isolado.
- **Dockerfile:** receita para construir uma imagem.
- **Docker Hub:** registry público para armazenar/compartilhar imagens.
- **Volume:** mecanismo de persistência de dados entre execuções.
- **Compose:** orquestrador de múltiplos containers via YAML.
