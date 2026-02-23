# ⚙️ Criando um Serviço no systemd

Nesta seção será demonstrado como criar um serviço personalizado (unit file) no systemd.

O objetivo é entender como o systemd gerencia processos e como podemos integrar scripts próprios ao sistema de inicialização.

---

# 📁 Localização dos Arquivos de Serviço

Os arquivos de serviço (units) podem estar em:

- `/usr/lib/systemd/system/` → serviços padrão do sistema
- `/etc/systemd/system/` → serviços criados ou modificados pelo administrador

Para criar um serviço customizado, utilizaremos:

```bash
cd /etc/systemd/system
```

---

# 🧾 Estrutura de um Arquivo .service

Crie o arquivo:

```bash
sudo nano meu-servico.service
```

Exemplo de conteúdo:

```ini
[Unit]
Description=Meu Serviço de Teste
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/bash /usr/local/bin/meu-script.sh
Restart=always
User=root

[Install]
WantedBy=multi-user.target
```

---

# 🔍 Explicação das Seções

## 🔹 [Unit]
Define informações gerais e dependências.

- `Description` → descrição do serviço
- `After` → ordem de inicialização

## 🔹 [Service]
Define como o serviço será executado.

- `Type=simple` → processo principal é o próprio ExecStart
- `ExecStart` → comando que será executado
- `Restart=always` → reinicia automaticamente se falhar
- `User` → usuário que executará o serviço

## 🔹 [Install]
Define em qual target o serviço será ativado.

- `WantedBy=multi-user.target` → equivalente ao antigo runlevel 3

---

# 🔄 Recarregar o systemd

Após criar ou editar um serviço:

```bash
sudo systemctl daemon-reload
```

Isso faz o systemd reconhecer a nova unit.

---

# ▶️ Iniciar o Serviço

```bash
sudo systemctl start meu-servico
```

Verificar status:

```bash
systemctl status meu-servico
```

---

# 🚀 Habilitar na Inicialização

```bash
sudo systemctl enable meu-servico
```

Isso cria um link simbólico para iniciar automaticamente no boot.

---

# 📜 Ver Logs do Serviço

```bash
journalctl -u meu-servico
```

---

# 🛑 Parar e Desabilitar

```bash
sudo systemctl stop meu-servico
sudo systemctl disable meu-servico
```
---
- Habilitação no boot

Criar serviços customizados é uma habilidade essencial para administradores Linux, especialmente em ambientes corporativos e servidores.
