# 🛠️ Troubleshooting Real no systemd

Esta seção apresenta cenários reais de falhas em serviços gerenciados pelo systemd, simulando situações comuns em ambientes corporativos.

O objetivo é demonstrar como identificar, investigar e corrigir problemas utilizando ferramentas como `systemctl` e `journalctl`.

---

# 🔥 Cenário 1 – Erro 203/EXEC (ExecStart incorreto)

## 📌 Situação

Arquivo de serviço:

```ini
ExecStart=/usr/local/bin/script-inexistente.sh
```

Ao iniciar o serviço:

```bash
sudo systemctl start meu-servico
```

Verificando status:

```bash
systemctl status meu-servico
```

Erro exibido:

```
code=exited, status=203/EXEC
```

---

## 🧠 O que significa?

O erro **203/EXEC** indica que o systemd não conseguiu executar o comando definido em `ExecStart`.

Possíveis causas:

- Caminho incorreto
- Arquivo inexistente
- Permissão incorreta
- Binário inválido

---

## 🔍 Investigação

```bash
journalctl -xe
```

Ou:

```bash
journalctl -u meu-servico
```

Verificar existência do arquivo:

```bash
ls -l /usr/local/bin/script-inexistente.sh
```

---

## ✅ Correção

Criar ou corrigir o script:

```bash
sudo nano /usr/local/bin/meu-script.sh
sudo chmod +x /usr/local/bin/meu-script.sh
```

Recarregar e reiniciar:

```bash
sudo systemctl daemon-reload
sudo systemctl restart meu-servico
```

---

# 🔥 Cenário 2 – Permissão Negada

## 📌 Situação

O script existe, mas não possui permissão de execução.

Erro no status:

```
Permission denied
```

---

## 🔍 Diagnóstico

```bash
ls -l /usr/local/bin/meu-script.sh
```

Exemplo problemático:

```
-rw-r--r--
```

---

## ✅ Correção

```bash
sudo chmod +x /usr/local/bin/meu-script.sh
```

Se necessário:

```bash
sudo chown root:root /usr/local/bin/meu-script.sh
```

---

# 🔥 Cenário 3 – Serviço Reiniciando em Loop

## 📌 Situação

Arquivo de serviço:

```ini
Restart=always
RestartSec=1
```

Se o script falhar imediatamente, o serviço entra em loop.

Status pode mostrar:

```
Active: activating (auto-restart)
```

---

## 🔍 Investigação

```bash
journalctl -u meu-servico -f
```

Analisar causa da falha no log.

---

## 🧠 Possível causa

O script finaliza rapidamente ou retorna erro.

Se for tarefa única, usar:

```ini
Type=oneshot
```

Ou remover:

```ini
Restart=always
```

---

# 🔥 Cenário 4 – Problema com Dependência de Rede

## 📌 Situação

Arquivo de serviço:

```ini
After=network.target
```

Mas a aplicação precisa da rede totalmente configurada (IP ativo).

---

## 🧠 Diferença Importante

- `network.target` → Rede inicializada
- `network-online.target` → Rede configurada e operacional

---

## ✅ Correção

```ini
After=network-online.target
Wants=network-online.target
```

Recarregar:

```bash
sudo systemctl daemon-reload
```

---

# 🔥 Cenário 5 – Serviço Falhando no Boot

Diagnóstico inicial:

```bash
systemctl list-units --failed
journalctl -b -p err
systemctl status nome.service
```

Esses comandos permitem identificar serviços que falharam durante a inicialização do sistema.

---

- Entendimento de dependências

A capacidade de diagnosticar e resolver falhas é essencial para administradores de sistemas Linux em ambientes reais.
