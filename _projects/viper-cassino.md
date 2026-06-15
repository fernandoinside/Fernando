---
title: "Viper Cassino"
subtitle: "Plataforma de Cassino Online Completa"
description: "Plataforma web completa de cassino online com Node.js + PostgreSQL, oferecendo 12 jogos slots locais (Construct 3), provedores terceiros, carteira digital, gateways PIX, sistema de afiliados e painel administrativo completo."
status: "disponivel"
published: true
exclude_from_listing: false
category: "Fintech & Gaming"
tech_stack:
  - "Node.js"
  - "Fastify"
  - "PostgreSQL"
  - "Sequelize"
  - "EJS"
  - "Construct 3"
  - "Docker"
  - "JWT"
  - "bcryptjs"
  - "Axios"
featured_image: "/assets/img/viper-cassino-1.png"
pricing:
  - name: "Licenciamento do Projeto"
    price: "Sob consulta"
    features:
      - "Acesso ao código-fonte privado"
      - "Direitos conforme negociação"
      - "Documentação técnica completa"
  - name: "Implementação Assistida"
    price: "Sob consulta"
    features:
      - "Configuração inicial em produção"
      - "Orientação de uso e operação"
      - "Ajustes conforme ambiente"
  - name: "Suporte e Evolução"
    price: "Sob consulta"
    features:
      - "Correções e manutenção"
      - "Novas funcionalidades"
      - "Suporte técnico contínuo"
demo_url: ""
docs_url: ""
repo_url: ""
---

# Viper Cassino

**Viper Cassino** é uma plataforma web completa de cassino online, construída com **Node.js (Fastify) + PostgreSQL**, oferecendo jogos de caça-níqueis (slots) locais em HTML5 (Construct 3) e de provedores terceiros, sistema de carteira digital com saldo real e bônus, integração com gateways de pagamento PIX, sistema de afiliados (RevShare/CPA), painel administrativo completo e ferramentas de marketing.

![Viper Cassino Dashboard]({{ '/assets/img/viper-cassino-1.png' | relative_url }})

## Visão geral

A plataforma foi projetada para operadores de cassino online que precisam de uma solução completa e customizável, com motor de jogos próprio, suporte a agregadores de jogos terceiros, e infraestrutura pronta para deploy em nuvem via Docker ou Render. O sistema conta com 22 modelos de dados, autenticação JWT, RBAC completo e múltiplos gateways de pagamento.

## Tecnologias Utilizadas

| Tecnologia | Finalidade |
|---|---|
| **Node.js v24.15.0** | Runtime |
| **Fastify 5.x** | Framework HTTP |
| **Sequelize** | ORM (PostgreSQL/MySQL) |
| **PostgreSQL** | Banco de dados principal |
| **EJS** | Template engine (server-side) |
| **bcryptjs** | Hash de senhas |
| **JWT** | Tokens de autenticação |
| **Axios** | Cliente HTTP (APIs externas) |
| **Docker** | Containerização |
| **StandardJS** | Linter |
| **Jest** | Testes |
| **Construct 3** | Engine dos jogos slots (HTML5 exports) |

## Estrutura do Projeto

```
Bets/Cassino/
├── src/
│   ├── index.js              # Entry point da aplicação
│   ├── routes/               # Rotas (web, admin, panel, auth, games, gateways)
│   ├── controllers/          # Lógica de negócio (jogos, pagamentos, provedores, marketing)
│   ├── models/               # Modelos Sequelize (22 models)
│   └── ...
├── views/                    # Templates EJS (admin, panel, web, auth)
├── public/
│   ├── css/app.css           # Estilos do tema cassino
│   └── vgames/               # 12 jogos slots em HTML5 (Construct 3)
├── scripts/                  # Seeds para banco de dados
├── Dockerfile
├── docker-compose.yml
└── render.yaml               # Deploy na Render
```

## Funcionalidades Principais

### 1. Sistema de Usuários
- Registro com email, CPF, telefone e senha
- Autenticação por sessão (Fastify session) com proteção CSRF
- Controle de acesso baseado em papéis (RBAC): Admin (role_id=1) e Usuário (role_id=2)
- Sistema de indicação por afiliados via campo `inviter`

### 2. Sistema de Carteira (Wallet)
- Cada usuário possui carteira com `balance` (saldo real) e `balance_bonus` (saldo bônus)
- Estatísticas vitalícias: total_bet, total_won, total_lose
- **Carteira do Sistema (System Wallet):** Conta da casa com controle de RTP
  - `pay_upto_percentage`: Percentual máximo de pagamento (default 45%)
  - `balance_min`: Saldo mínimo de segurança

### 3. Jogos

#### Jogos Locais (Construct 3) - 12 Slots
Cada jogo é um export HTML5 do Construct 3 com injeção de JavaScript para comunicação com o backend via `window.VGAMES_API_URL`.

**Fluxo de uma rodada:**
1. Usuário acessa `/games/{gameId}` → jogo carregado em iframe
2. Engine do jogo chama `/api/vgames/{gameId}/session` → retorna saldo e config
3. Usuário gira → `POST /api/vgames/{gameId}/spin`
4. Servidor debita saldo, calcula resultado (RTP + house_edge), credita ganhos
5. Resultado é retornado para exibição no jogo

**Lista de Jogos:**
Treasures of Aztec, Hood vs Wolf, Songkran Party, Fortune Tiger, Queen of Bounty, Fortune Rabbit, Fortune Panda, Phoenix Rises, Jack Frost, Fortune Mouse, Bikini Paradise, Fortune Ox

![Jogos Viper Cassino]({{ '/assets/img/viper-cassino-2.png' | relative_url }})

#### Jogos de Provedores Externos
- **Fivers (FiversLive):** Agregador com múltiplos provedores (PRAGMATIC, etc.)
- **Slotegrator:** Integração de provedores
- **Salsa:** Provedor com categorias
- **Vibra Casino Games:** Fonte adicional de jogos

### 4. Gateways de Pagamento (PIX)
- **BsPay** - Geração de QR Code PIX
- **SuitPay** - Pagamentos via PIX
- **Mercado Pago** - PIX com suporte a loja física/POS

**Fluxo de Depósito:**
1. Usuário submete depósito → criação de registro pendente
2. Sistema retorna QR Code PIX
3. Usuário paga via app bancário
4. Webhook do gateway confirma → saldo é creditado

**Fluxo de Saque:**
1. Usuário solicita saque → saldo é bloqueado
2. Admin revisa e aprova → sistema debita da carteira da casa
3. Usuário recebe notificação

![Gateways de Pagamento]({{ '/assets/img/viper-cassino-3.png' | relative_url }})

### 5. Sistema de Afiliados
- Dois tipos de comissão: **RevShare** e **CPA**
- Rastreamento de usuários convidados
- Comissão paga ao afiliado quando convidado faz depósito >= baseline
- Notificação ao admin sobre depósitos de afiliados

### 6. Painel Administrativo
Acesso em `/admin` (requer role_id=1):
- Dashboard com resumo financeiro + gráfico 30 dias + ranking de jogos
- CRUD completo: Usuários, Carteiras, Depósitos, Saques, Transações
- Gerenciamento de Jogos (locais e externos), Categorias, Provedores
- Configuração de Gateways, Banners, Integrações
- Sistema de Papéis e Permissões (ACL/RBAC)
- Gerenciamento de Afiliados, Notificações, Marketing
- Uploads e Visualizador de Logs

![Painel Administrativo]({{ '/assets/img/viper-cassino-4.png' | relative_url }})

### 7. Sistema de Notificações
- Notificações por tipo (depósito, saque, admin)
- Broadcast para todos os usuários
- API de contagem de não lidas
- Marcação como lida/vista

![Notificações]({{ '/assets/img/viper-cassino-5.png' | relative_url }})

### 8. Sistema de Marketing
- Publicação multicanal via integrações
- Integração com Telegram
- Templates com hashtags

## Galeria do Sistema

| Tela | Descrição |
|------|-----------|
| ![Tela 6]({{ '/assets/img/viper-cassino-6.png' | relative_url }}) | Interface de jogos |
| ![Tela 7]({{ '/assets/img/viper-cassino-7.png' | relative_url }}) | Dashboard financeiro |
| ![Tela 8]({{ '/assets/img/viper-cassino-8.png' | relative_url }}) | Gerenciamento de usuários |
| ![Tela 9]({{ '/assets/img/viper-cassino-9.png' | relative_url }}) | Relatórios e analytics |
| ![Tela 10]({{ '/assets/img/viper-cassino-10.png' | relative_url }}) | Configurações do sistema |
| ![Tela 11]({{ '/assets/img/viper-cassino-11.png' | relative_url }}) | Tema cassino |

## Modelos de Dados (22 models)

| Modelo | Tabela | Campos Principais |
|---|---|---|
| User | users | id, role_id, name, email, password, cpf, phone, inviter, affiliate_*, status |
| Wallet | wallets | user_id, balance, balance_bonus, total_bet/won/lose, refer_rewards |
| Deposit | deposits | user_id, payment_id, amount, status, gateway |
| Withdrawal | withdrawals | user_id, amount, status, gateway, pix_key, document |
| Transaction | transactions | user_id, amount, type (bet/win), status |
| Game | games | category_id, name, provider, type, active, status, winLength, loseLength |
| GameExclusive | game_exclusives | category_id, uuid, name, iconsJson, house_edge, winLength, loseLength |
| SystemWallet | system_wallets | label, balance, balance_min, pay_upto_percentage |
| Gateway | gateways | bspay_*, suitpay_*, mercadopago_* e outros |
| Setting | settings | software_name, prefix, min/max, redes sociais, maintenance_mode |
| Notification | notifications | user_id, type, title, message, status |
| Banner | banners | image, type (home/slide/fivers), link, order |
| Category | categories | name, slug, description, image |
| Role / Permission / ModelHasRole | RBAC | Sistema de controle de acesso |
| FiversProvider / FiversGame / FiversGgr | fivers_* | Provedores e jogos Fivers |
| AffiliateHistory | affiliate_histories | user_id, inviter, commission, type |
| Integration | integrations | platform, client_id, access_token |
| GamesKey / VibraCasinoGame | games_keys, vibra_casino_games | Chaves e jogos alternativos |

## Arquitetura

```
Navegador → Fastify Server → Rotas → Controllers → Models (Sequelize) → PostgreSQL
                          ↕
                    EJS Views (renderizadas no servidor)
```

**Fluxo de uma rodada de jogo:**
```
Browser (iframe) ←→ API REST (vgames.js)
    ↕
Construct 3 Engine (HTML5 export)
    ↕
Injeção JS (runtime patch + VGAMES_API_URL)
    ↕
Spin → POST /api/vgames/{id}/spin
    ↕
Servidor: debita → calcula resultado → credita → registra transação
```

## Deployment

- **Docker:** Multi-container (app + PostgreSQL) via `docker-compose.yml`
- **Render:** Deploy em nuvem via `render.yaml` (web service + MySQL)
- **Porta:** 3000 (configurável via env PORT)
- **Ambiente:** Configurado para produção na Render (região Oregon)

## Scripts de Seed

| Script | Finalidade |
|---|---|
| `seed.js` | Dados iniciais |
| `seed-users.js` | Usuários de teste |
| `seed-system-wallets.js` | Carteiras do sistema |
| `seed-settings.js` | Configurações do site |
| `seed-roles.js` / `seed-permissions.js` | Papéis e permissões |
| `seed-gateways.js` | Gateways de pagamento |
| `seed-games.js` | Jogos iniciais |

## Estado do Desenvolvimento

- **Status:** Desenvolvimento ativo
- Servidor roda com `npm run dev` (Fastify)
- Painel admin testado (smoke tests)
- Motor de jogos locais funcional com simulação básica de RTP
- Tema cassino com 3 variações: Gold Noir, Neon Royal, Emerald Vegas

## Licenciamento e comercialização

O Viper Cassino está disponível para negociação de licenciamento, implementação e evolução. Condições comerciais podem incluir:

- Licenciamento de uso do código
- Transferência parcial ou total conforme acordo
- Customizações específicas (tema, jogos, gateways)
- Configuração em ambiente do cliente
- Suporte técnico inicial
- Manutenção contínua

Para tratar valores, escopo e condições de entrega, entre em contato informando o interesse no **Viper Cassino**.
