Com base no sistema operacional que você está usando (Linux Mint 21.2 "Zara", baseado no Ubuntu **`noble`**) e sabendo que você já está usando o terminal, a maneira mais fácil e recomendada de instalar o Visual Studio Code (VS Code) é usando o repositório oficial do Visual Studio Code.

Aqui está o passo a passo completo, via terminal:

-----

## 💻 Instalação do Visual Studio Code

O VS Code disponibiliza um repositório APT próprio, o que garante que você sempre receberá as atualizações através do comando `sudo apt update` e `sudo apt upgrade`.

### Etapa 1: Instalar Dependências e a Chave GPG

Precisamos instalar algumas dependências e adicionar a chave de segurança (GPG key) do Microsoft VS Code ao seu sistema:

```bash
# 1. Atualiza a lista de pacotes
sudo apt update

# 2. Instala pacotes necessários para usar repositórios via HTTPS
sudo apt install apt-transport-https wget -y

# 3. Baixa e adiciona a chave GPG pública da Microsoft.
# Esta chave garante que os pacotes que você baixar são autênticos.
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
```

### Etapa 2: Adicionar o Repositório do VS Code

Agora, você adiciona o repositório oficial do VS Code à sua lista de fontes de software:

```bash
# Adiciona o repositório do VS Code (compatível com sistemas baseados em Debian/Ubuntu)
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
```

### Etapa 3: Instalar o Visual Studio Code

Com o repositório configurado, você pode atualizar a lista de pacotes e instalar o VS Code:

```bash
# 1. Atualiza a lista de pacotes para incluir o novo repositório
sudo apt update

# 2. Instala o Visual Studio Code
sudo apt install code
```

-----

## ✅ Como Iniciar o VS Code

Após a instalação, você pode iniciar o Visual Studio Code de duas maneiras:

1.  **Pelo Terminal:** Basta digitar o comando:
    ```bash
    code
    ```
2.  **Pelo Menu Gráfico:** Procure por "Visual Studio Code" no menu de aplicativos do Linux Mint.

Pronto\! Seu VS Code está instalado e pronto para usar.
