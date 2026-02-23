#  Gerenciamento de Serviços com systemctl

O `systemctl` é a principal ferramenta de administração do systemd.  
Ele permite iniciar, parar, reiniciar, habilitar e diagnosticar serviços no sistema Linux.

---

#  Verificando Status de Serviços

```bash
systemctl status nome.service
```

Exemplo:

```bash
systemctl status sshd.service
```

O comando exibe:

- Estado ativo (ActiveState)
- Subestado (SubState)
- PID principal
- Tempo de execução
- Logs recentes
- Caminho da unit

---

#  Controle de Serviços

```bash
sudo systemctl start nome.service
sudo systemctl stop nome.service
sudo systemctl restart nome.service
sudo systemctl reload nome.service
```

| Comando | Função |
|----------|----------|
| start | Inicia o serviço |
| stop | Para o serviço |
| restart | Reinicia completamente |
| reload | Recarrega configuração sem interromper (se suportado) |

> Nem todos os serviços suportam `reload`.

---

#  Habilitar ou Desabilitar no Boot

```bash
sudo systemctl enable nome.service
sudo systemctl disable nome.service
```

- `enable` cria um link simbólico dentro do target padrão
- `disable` remove o link

Verificar se está habilitado:

```bash
systemctl is-enabled nome.service
```

---

#  Listagem de Serviços

## Serviços em execução

```bash
systemctl list-units --type=service
```

## Serviços instalados

```bash
systemctl list-unit-files --type=service
```

Estados comuns:

- enabled
- disabled
- static
- masked

---

#  Serviços com Falha

```bash
systemctl list-units --failed
```

Muito utilizado para troubleshooting de boot.

---

#  Informações Detalhadas

```bash
systemctl show nome.service
```

Exibe propriedades completas da unit:

- Dependências
- Caminhos
- Configurações internas
- Estado detalhado

---

#  Dependências

```bash
systemctl list-dependencies nome.service
```

Permite visualizar a árvore de dependências da unit.

---

#  Mascarar Serviço

```bash
sudo systemctl mask nome.service
sudo systemctl unmask nome.service
```

- `mask` impede que o serviço seja iniciado manualmente ou automaticamente
- `unmask` remove o bloqueio

---

#  Recarregar o systemd

Após criar ou editar uma unit:

```bash
sudo systemctl daemon-reload
```

Reexecutar o processo PID 1 (raramente necessário):

```bash
sudo systemctl daemon-reexec
```

---

# Estados de Serviço

| Estado | Significado |
|----------|--------------|
| active | Em execução |
| inactive | Parado |
| failed | Falhou |
| activating | Iniciando |
| deactivating | Parando |

---
