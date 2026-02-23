# 📜 Análise de Logs com journalctl

O `journalctl` é a ferramenta utilizada para consultar os logs centralizados do systemd, armazenados pelo serviço `journald`.

Ele permite visualizar eventos do sistema, mensagens de serviços e informações do processo de boot.

---

# 📌 Visualizar Todos os Logs

```bash
journalctl
```

Exibe todos os logs armazenados no journal.

Para navegar:
- `↑ ↓` → mover
- `q` → sair

---

# 🎯 Logs do Boot Atual

```bash
journalctl -b
```

Mostra apenas os logs da inicialização atual do sistema.

Para ver boots anteriores:

```bash
journalctl --list-boots
```

E para visualizar um boot específico:

```bash
journalctl -b -1
```

---

# 🔍 Logs de um Serviço Específico

```bash
journalctl -u nome.service
```

Exemplo:

```bash
journalctl -u sshd.service
```

Mostra apenas os logs relacionados àquela unit.

---

# ⚠️ Logs com Erros Recentes

```bash
journalctl -xe
```

- `-x` → adiciona explicações detalhadas
- `-e` → vai direto para o final do log

Muito utilizado para diagnosticar falhas.

---

# ⏱️ Filtrar por Período

```bash
journalctl --since "2026-02-20"
journalctl --since "1 hour ago"
journalctl --since "10 minutes ago"
```

Permite análise temporal de eventos.

---

# 🔄 Logs em Tempo Real

```bash
journalctl -f
```

Semelhante ao comando:

```bash
tail -f /var/log/syslog
```

Útil para monitoramento ao vivo.

---

# 📊 Filtrar por Prioridade

```bash
journalctl -p err
journalctl -p warning
journalctl -p info
```

Principais níveis:

- emerg
- alert
- crit
- err
- warning
- notice
- info
- debug

---

# 💾 Logs Persistentes

Por padrão, algumas distribuições mantêm logs apenas em memória.

Para habilitar persistência:

```bash
sudo mkdir -p /var/log/journal
sudo systemctl restart systemd-journald
```

Isso garante que os logs sobrevivam a reinicializações.

---
- Monitoramento em tempo real

O domínio do `journalctl` é essencial para troubleshooting eficiente em ambientes Linux modernos.
