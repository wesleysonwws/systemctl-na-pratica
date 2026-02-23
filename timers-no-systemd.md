# ⏰ Timers no systemd

Os timers no systemd são utilizados para executar tarefas agendadas, funcionando como alternativa moderna ao cron.

Eles oferecem maior integração com o systemd, melhor controle de logs e dependências.

---

# 🧠 Timer vs Cron

Enquanto o cron utiliza o arquivo `/etc/crontab`, o systemd usa:

- Arquivo `.service` → define o que será executado
- Arquivo `.timer` → define quando será executado

Isso permite controle mais estruturado e integração com journalctl.

---

# 📁 Localização

Timers customizados devem ser criados em:

```bash
/etc/systemd/system/
```

---

# 🛠️ Exemplo Prático

## 1️⃣ Criando o Serviço

Crie o arquivo:

```bash
sudo nano /etc/systemd/system/meu-teste.service
```

Conteúdo:

```ini
[Unit]
Description=Executa script de teste

[Service]
Type=oneshot
ExecStart=/usr/bin/echo "Timer executado com sucesso"
```

---

## 2️⃣ Criando o Timer

Crie:

```bash
sudo nano /etc/systemd/system/meu-teste.timer
```

Exemplo:

```ini
[Unit]
Description=Timer para executar a cada 1 minuto

[Timer]
OnBootSec=1min
OnUnitActiveSec=1min
Unit=meu-teste.service

[Install]
WantedBy=timers.target
```

---

# 🔍 Explicação das Diretivas

## 🔹 OnBootSec
Executa após o tempo definido depois do boot.

## 🔹 OnUnitActiveSec
Executa novamente após o tempo definido desde a última execução.

## 🔹 Type=oneshot
Indica que o serviço executa uma tarefa e finaliza.

---

# 🔄 Recarregar o systemd

```bash
sudo systemctl daemon-reload
```

---

# ▶️ Iniciar e Habilitar

```bash
sudo systemctl start meu-teste.timer
sudo systemctl enable meu-teste.timer
```

---

# 📊 Verificar Timers Ativos

```bash
systemctl list-timers
```

---

# 📜 Ver Logs da Execução

```bash
journalctl -u meu-teste.service
```

---

# 🎯 Vantagens dos Timers

- Integração total com systemd
- Logs centralizados
- Controle por dependência
- Pode ser ativado por eventos (não só tempo)
- Mais previsível em ambientes corporativos

---
- Monitoramento via systemctl e journalctl

O uso de timers demonstra domínio moderno do gerenciamento de tarefas agendadas em sistemas Linux.
