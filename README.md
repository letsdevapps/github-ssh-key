### O que é uma chave SSH?

Uma chave SSH é uma maneira segura de se identificar e se conectar com outros servidores, sem precisar digitar uma senha toda vez. No caso do GitHub, você usa a chave SSH para autenticar sua máquina quando você faz operações de git (como `git push`, `git pull`, etc.) sem precisar ficar colocando sua senha.
---

### Passo 1: Verificar se já existe uma chave SSH

Antes de criar uma chave nova, vamos ver se você já tem uma. Abra o terminal e digite esse comando:

```bash
ls -al ~/.ssh
```

Esse comando vai listar os arquivos dentro da pasta `.ssh` no seu computador. Se você já tiver chaves SSH, vai ver algo como `id_rsa` e `id_rsa.pub` (ou algo parecido). Se aparecer, tudo bem, você pode usar essas chaves. Se não aparecer nada, vamos criar uma nova chave!

---

### Passo 2: Criar uma nova chave SSH

Agora, vamos criar uma chave SSH nova. No terminal, digite o seguinte comando:

```bash
ssh-keygen -t rsa -b 4096 -C "seu-email@exemplo.com"
```

Aqui está o que acontece:

* `-t rsa` diz ao terminal para usar o tipo de chave RSA (o mais comum).
* `-b 4096` significa que a chave terá 4096 bits de segurança (quanto maior o número, mais segura é a chave).
* `-C "seu-email@exemplo.com"` é um comentário que ajuda a identificar a chave (normalmente, você coloca seu email do GitHub aqui).

Depois de digitar isso, o terminal vai pedir para você escolher onde salvar a chave. A maioria das pessoas deixa o padrão, que é o caminho:

```
/home/usuário/.ssh/id_rsa   (Linux ou macOS)
C:\Users\usuário\.ssh\id_rsa (Windows)
```

Aí você pressiona **Enter** para aceitar o local padrão.

### Passo 3: Criar uma senha para a chave SSH (opcional)

Em seguida, o terminal vai pedir para você criar uma senha para a chave. Isso é opcional. Se você quiser maior segurança, pode colocar uma senha aqui. Se preferir não colocar, só aperte **Enter**.

---

### Passo 4: Verificar se a chave foi criada

Agora, vamos garantir que sua chave foi criada. Digite o comando:

```bash
ls -al ~/.ssh
```

Você deve ver algo como:

```
id_rsa   (a chave privada)
id_rsa.pub (a chave pública)
```

A chave pública é a que você vai adicionar ao GitHub, então copie o conteúdo do arquivo `id_rsa.pub`.

### Passo 5: Adicionar a chave SSH ao GitHub

Agora, vamos adicionar essa chave pública ao GitHub.

1. **Copiar a chave pública**:
   Para copiar a chave pública (o arquivo `id_rsa.pub`), você pode usar o seguinte comando:

   No **Linux** ou **macOS**:

   ```bash
   cat ~/.ssh/id_rsa.pub | pbcopy  # Para Mac
   cat ~/.ssh/id_rsa.pub | xclip -sel clip  # Para Linux
   ```

   No **Windows**, se estiver usando o Git Bash, use:

   ```bash
   cat ~/.ssh/id_rsa.pub | clip
   ```

   Isso vai copiar o conteúdo da chave para sua área de transferência.

2. **Adicionar a chave no GitHub**:

   * Vá até [GitHub - Settings - SSH and GPG keys](https://github.com/settings/keys).
   * Clique no botão **New SSH key**.
   * No campo **Title**, coloque um nome para identificar essa chave (ex.: "Minha chave SSH").
   * No campo **Key**, cole a chave que você copiou (pressione `Ctrl + V` ou `Cmd + V`).
   * Clique em **Add SSH key**.

### Passo 6: Testar a chave SSH no GitHub

Agora, vamos testar se a chave está funcionando. No terminal, digite:

```bash
ssh -T git@github.com
```

Se tudo tiver sido configurado corretamente, você verá uma mensagem como essa:

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

Isso significa que sua chave SSH está funcionando com o GitHub!

---

### Resumo:

1. Geramos uma chave SSH com `ssh-keygen`.
2. Copiamos a chave pública (o arquivo `id_rsa.pub`).
3. Adicionamos a chave no GitHub.
4. Testamos a autenticação com `ssh -T git@github.com`.

Agora você pode usar o GitHub sem precisar digitar sua senha toda vez!
