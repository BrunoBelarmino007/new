Com base nas suas informações (Linux Mint 21.2 "Zara", codinome Ubuntu **`noble`**) e nas instruções oficiais do Docker, o método mais recomendado é **"Install using the `apt` repository"**.

Este método garante que você terá o Docker Engine e o **Docker Compose Plugin** (a versão moderna) instalados corretamente e poderá mantê-los atualizados via `apt`.

-----

## 🚀 Passo a Passo: Instalação Oficial do Docker no Linux Mint

Siga esta sequência de comandos no terminal. Como o seu Mint é baseado no Ubuntu Noble (24.04), usaremos o codinome `noble` para configurar o repositório.

### Etapa 1: Preparação e Remoção de Conflitos

Primeiro, garanta que não há pacotes ou arquivos de configuração antigos que possam causar os erros que você encontrou anteriormente.

```bash
# 1. Tenta remover quaisquer pacotes Docker não oficiais/conflitantes (conforme documentação)
sudo apt remove docker.io docker-compose docker-compose-v2 docker-doc podman-docker containerd runc

# 2. Limpa o diretório de listas de fontes, caso haja arquivos incompletos como 'docker.list.d'
sudo rm -f /etc/apt/sources.list.d/docker.list*

# 3. Remove chaves GPG antigas/conflitantes
sudo rm -f /etc/apt/keyrings/docker.asc /etc/apt/keyrings/docker.gpg
```

-----

### Etapa 2: Configurar o Repositório Oficial do Docker

Vamos adicionar a chave de segurança GPG e configurar o arquivo de fontes para que o `apt` saiba onde baixar os pacotes.

```bash
# 1. Atualiza o sistema e instala utilitários essenciais
sudo apt update
sudo apt install ca-certificates curl gnupg

# 2. Cria o diretório de keyrings (se necessário) e configura permissões
sudo install -m 0755 -d /etc/apt/keyrings

# 3. Baixa a chave GPG oficial do Docker
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# 4. Adiciona o repositório do Docker à lista de fontes. 
# O comando usa 'noble' como CODENAME, conforme identificado no seu sistema.
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  noble stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

-----

### Etapa 3: Instalar Docker e Docker Compose Plugin

Agora você pode atualizar e instalar o software. O pacote `docker-compose-plugin` instala o Docker Compose moderno.

```bash
# 1. Atualiza a lista de pacotes para incluir o novo repositório Docker
sudo apt update

# 2. Instala os pacotes principais do Docker e o Plugin Compose
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

-----

### Etapa 4: Teste e Pós-Instalação (Usar Sem `sudo`)

O Docker já deve estar rodando após a instalação.

```bash
# 1. Verifica se a instalação foi bem-sucedida
sudo docker run hello-world

# 2. Adiciona seu usuário atual ao grupo 'docker' para rodar comandos sem 'sudo'
sudo usermod -aG docker $USER

# 3. ATENÇÃO: Para que a permissão entre em vigor IMEDIATAMENTE, execute este comando.
# Alternativamente, você pode simplesmente fechar e reabrir o terminal ou reiniciar o PC.
newgrp docker

# 4. Teste final (sem 'sudo')
docker run hello-world

# 5. Verifique se o Docker Compose Plugin está funcionando (comando sem traço)
docker compose version
```
