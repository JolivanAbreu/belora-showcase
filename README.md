# 💅 Belora — Plataforma de agendamento para estética

> **Vitrine do projeto.** O código-fonte é privado por ser um produto comercial. Se quiser ver uma demonstração ou conversar sobre a implementação, me chame no [LinkedIn](https://www.linkedin.com/in/jolivan-abreu-teixeira-5a27961b0/).

SaaS **multi-tenant** de agendamento para profissionais de estética. Substitui a marcação manual por WhatsApp: a profissional acompanha a agenda por um painel e as clientes marcam horário sozinhas por um link público. **Em produção.**

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)
![Sequelize](https://img.shields.io/badge/Sequelize-52B0E7?style=flat&logo=sequelize&logoColor=white)
![React](https://img.shields.io/badge/React_19-20232A?style=flat&logo=react&logoColor=61DAFB)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS_v4-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Jest](https://img.shields.io/badge/Jest-C21325?style=flat&logo=jest&logoColor=white)
![Railway](https://img.shields.io/badge/Railway-0B0D0E?style=flat&logo=railway&logoColor=white)

## 🧩 Componentes

| Módulo | Descrição |
|---|---|
| **API** | REST em Node.js/Express com PostgreSQL |
| **Painel administrativo** | React: agenda, serviços, clientes, relatórios e configurações |
| **Página de agendamento** | React: link público por profissional, sem login para a cliente |
| **Deploy** | Docker Compose e guias de publicação |

## ✨ Funcionalidades

- Cálculo automático de disponibilidade, respeitando a duração do serviço, o horário de funcionamento e os bloqueios
- Serviços com duração fixa ou em faixa (ex.: de 1h a 1h30)
- Bloqueios de agenda pontuais ou recorrentes (por dia do mês ou da semana), com desbloqueio parcial
- **Prevenção de conflito de horário sob concorrência**, com advisory lock no PostgreSQL
- Confirmação e **lembretes automáticos por WhatsApp** (24h, 2h e 30min antes), com textos editáveis
- Cancelamento e confirmação de presença pela cliente, por link com token
- Cadastro de clientes com histórico de atendimentos
- Relatórios de faturamento, taxa de não comparecimento e ranking de serviços
- **Autenticação em duas etapas (2FA/TOTP)** no painel

## 🏗️ Arquitetura e decisões técnicas

- **Multi-tenant com banco compartilhado:** toda tabela de domínio tem `tenant_id`, e o escopo vem do JWT (painel) ou do slug da URL (página pública), nunca de um parâmetro enviado pelo cliente
- A disponibilidade é calculada em um único ponto do backend, consumido pelo painel e pela página pública
- Jobs agendados (node-cron) para o envio dos lembretes
- Segurança: Helmet, rate limiting, bcrypt e JWT

## 🧪 Testes

Testes de integração contra PostgreSQL real cobrindo **isolamento entre tenants**, conflito de horário sob concorrência, autorização dos links de cancelamento, o job de lembretes, 2FA, relatórios e a lógica de fuso horário. Os frontends também têm testes de componentes.

---

Desenvolvido por **[Jolivan Abreu](https://github.com/JolivanAbreu)**.
