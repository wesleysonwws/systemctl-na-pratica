# ⚙️ Systemctl na Prática

Este repositório contém um estudo prático sobre o **gerenciamento de serviços no Linux utilizando o systemctl**, ferramenta central do **systemd**.
O objetivo é demonstrar, de forma clara e aplicada, como administrar serviços, analisar logs, diagnosticar falhas e controlar o comportamento do sistema durante e após o boot.

Este material faz parte do meu portfólio de estudos em Administração de Sistemas Linux.

---

## 📚 Objetivos do Projeto

- Entender o papel do systemd no processo de inicialização
- Aprender a gerenciar serviços via systemctl
- Controlar inicialização automática de serviços
- Analisar logs com journalctl
- Diagnosticar falhas de serviços
- Trabalhar com dependências e targets
- Aplicar troubleshooting em cenários reais

---

## 🧠 Conceitos Abordados

- SysV Init vs Systemd
- Units (Service, Target, Socket, Timer…)
- Targets (equivalente aos runlevels)
- Paralelismo de inicialização
- Dependências de serviços
- Logs centralizados (journald)
- Estados de serviços

---

## 🗂️ Estrutura do Repositório

```text
systemctl-na-pratica/
│
├── README.md
├── criando-um-servico.md
├── gerenciamento-com-systemctl.md
├── journalctl-e-logs.md
├── timers-no-systemd.md
└── units-e-targets.md
└── troubleshooting-real.md
