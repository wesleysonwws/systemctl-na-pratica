# 🧱 Units e Targets no systemd
## 🧠 O que são Units?

No systemd, uma *unit* é um objeto de configuração que descreve como um recurso do sistema deve ser gerenciado.
Cada unit é definida por um arquivo com extensão específica, como:

- `.service`
- `.target`
- `.socket`
- `.timer`
- `.mount`
- `.device`

Esses arquivos geralmente estão localizados em:

/usr/lib/systemd/system

/etc/systemd/system

- `/usr/lib/systemd/system` → Units instaladas por pacotes do sistema  
- `/etc/systemd/system` → Units criadas ou modificadas pelo administrador  

O diretório `/etc` tem prioridade sobre `/usr/lib`.

---

# 📦 Principais Tipos de Units

## 🔹 Service

Arquivo `.service`.

Responsável por definir como um processo ou daemon deve ser executado.

Exemplos:
- `sshd.service`
- `nginx.service`

---

## 🔹 Target

Arquivo `.target`.

Representa um estado do sistema, agrupando várias units.

Substitui o conceito de *runlevels* do SysV Init.

Exemplos:

- `multi-user.target`
- `graphical.target`
- `rescue.target`

---

## 🔹 Socket

Arquivo `.socket`.

Permite ativação sob demanda.  
O serviço só é iniciado quando há conexão na porta definida.

---

## 🔹 Timer

Arquivo `.timer`.

Substitui tarefas do cron.  
Permite agendar execução automática de serviços.

---

## 🔹 Mount

Arquivo `.mount`.

Controla montagem de sistemas de arquivos.

---

# 🎯 O que são Targets?

Targets são grupos de units que representam um estado do sistema.

Eles substituem os antigos runlevels do SysV Init.

## 📊 Equivalência com Runlevels

| Runlevel (SysV) | Target (systemd) |
|-----------------|------------------|
| 0 | `poweroff.target` |
| 1 | `rescue.target` |
| 3 | `multi-user.target` |
| 5 | `graphical.target` |
| 6 | `reboot.target` |

---

# 🖥️ multi-user.target

Modo servidor:

- Sistema operacional carregado
- Serviços de rede ativos
- Sem interface gráfica

Muito utilizado em servidores Linux.

---

# 🖼️ graphical.target

Modo desktop.

Inclui tudo do `multi-user.target` + ambiente gráfico.

---

# 🔗 Dependências Entre Units

O systemd controla dependências usando diretivas como:

- `After=`
- `Before=`
- `Requires=`
- `Wants=`

Exemplo:

```
After=network.target
```

Significa que o serviço só será iniciado após a rede estar ativa.

---

# 📊 Visualizando Dependências

Comando:

```
systemctl list-dependencies nome.service
```

Permite visualizar a árvore de dependências de uma unit.

---

