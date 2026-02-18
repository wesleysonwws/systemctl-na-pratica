# 🖥️ Systemctl na Prática

## ⚙️ Gerenciamento de Serviços com systemctl

O `systemctl` é o principal comando do **systemd**, utilizado para controlar serviços, verificar status, habilitar inicialização automática e diagnosticar falhas no sistema.

---

## 🧭 Status de Serviços

```bash
systemctl status nome.service
```

Exemplo:

```bash
systemctl status sshd.service
```

Exibe:

- Estado (active, inactive, failed)
- PID
- Tempo de atividade
- Logs recentes

---

## ▶️ Controle de Serviços

```bash
sudo systemctl start nome.service
sudo systemctl stop nome.service
sudo systemctl restart nome.service
sudo systemctl reload nome.service
```

| Comando | Função |
|---------|--------|
| start   | Inicia o serviço |
| stop    | Para o serviço |
| restart | Reinicia o serviço |
| reload  | Recarrega a configuração |

> Nem todos os serviços suportam `reload`.

---

## 🚀 Inicialização no Boot

```bash
sudo systemctl enable nome.service
sudo systemctl disable nome.service
```

O `enable` cria um link simbólico no target padrão (geralmente `multi-user.target`).

---

## 📋 Listagem de Serviços

Serviços ativos:

```bash
systemctl list-units --type=service
```

Serviços instalados:

```bash
systemctl list-unit-files --type=service
```

Estados comuns:

- enabled
- disabled
- static
- masked

---

## ❌ Serviços com Falha

```bash
systemctl list-units --failed
```

Muito utilizado em troubleshooting de boot.

---

## 🔍 Detalhes do Serviço

```bash
systemctl show nome.service
```

Exibe dependências, caminhos e configurações internas.

---

## 🧠 Dependências

```bash
systemctl list-dependencies nome.service
```

---

## 📊 Análise de Inicialização

```bash
systemd-analyze
systemd-analyze blame
systemd-analyze critical-chain
```

Permite analisar o tempo de inicialização do sistema e dos serviços.

---

## 🧱 Estados de Serviço

| Estado        | Significado |
|---------------|-------------|
| active        | Em execução |
| inactive      | Parado |
| failed        | Falhou |
| activating    | Iniciando |
| deactivating  | Parando |

---

## 🔒 Mascarar Serviço

```bash
sudo systemctl mask nome.service
sudo systemctl unmask nome.service
```

Impede que o serviço seja iniciado manualmente ou automaticamente.

---

## 🔄 Recarregar o Systemd

```bash
sudo systemctl daemon-reload
sudo systemctl daemon-reexec
```

Utilizado após criar ou editar arquivos de unit.

---

## 📂 Diretórios de Units

```bash
/usr/lib/systemd/system
/etc/systemd/system
```

- `/usr/lib/systemd/system` → Units instaladas por pacotes  
- `/etc/systemd/system` → Units criadas ou modificadas pelo administrador  
