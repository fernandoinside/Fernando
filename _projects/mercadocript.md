---
title: "MercadoCript"
subtitle: "Bot de Trading Automatizado para Criptomoedas"
description: "Bot de trading automatizado para criptomoedas na exchange NovaDAX com análise técnica multi-indicador, Machine Learning (Random Forest), dashboard web em tempo real via WebSocket, Grid Trading, Trailing Stop e 3 perfis de risco configuráveis."
status: "disponivel"
published: true
exclude_from_listing: false
category: "Fintech & Trading"
tech_stack:
  - "Python"
  - "NovaDAX API"
  - "WebSocket"
  - "HTML/CSS/JS"
  - "Random Forest"
  - "Pandas"
  - "Web Audio API"
  - "Push API"
  - "Scikit-learn"
featured_image: "/assets/img/mercadocript-1.png"
pricing:
  - name: "Assinatura Mensal"
    price: "R$ 199,00 / mês"
    mp_link: "https://www.mercadopago.com.br/subscriptions/checkout?preapproval_plan_id=YOUR_PLAN_ID"
    features:
      - "Uso em 1 conta NovaDAX"
      - "Atualizações inclusas"
      - "Suporte via Email/WhatsApp"
      - "Hospedagem não inclusa"
  - name: "Licença Vitalícia (Código-Fonte)"
    price: "R$ 2.499,00"
    mp_link: "https://www.mercadopago.com.br/checkout/v1/redirect?pref_id=YOUR_PREF_ID_COMPRA"
    features:
      - "Código-fonte completo (Python)"
      - "Direito a modificações"
      - "Instalação assistida inclusa"
      - "Sem taxas mensais"
  - name: "Consultoria Customizada"
    price: "Sob consulta"
    features:
      - "Novas estratégias exclusivas"
      - "Integração com outras exchanges"
      - "Otimização de ML para seu perfil"
demo_url: ""
docs_url: ""
repo_url: ""
---

# MercadoCript

**MercadoCript** é um bot de trading automatizado para criptomoedas que opera na exchange brasileira **NovaDAX**. O sistema combina **análise técnica multi-indicador**, **Machine Learning (Random Forest)** para aprimorar decisões, **dashboard web em tempo real** via WebSocket, e múltiplas estratégias avançadas como Grid Trading, Trailing Stop, Rotação Inteligente e Análise de Tendência BTC.

> Trading envolve risco de perda de capital. Não há garantias de retorno. O bot foi projetado para operar 24/7 de forma autônoma com monitoramento via dashboard.

![Dashboard MercadoCript]({{ '/assets/img/mercadocript-1.png' | relative_url }})

## Visão geral

O MercadoCript foi desenvolvido para automatizar operações de compra e venda de criptomoedas na exchange NovaDAX, utilizando análise técnica combinada com Machine Learning para gerar sinais de trading. O sistema monitora **8 pares de criptomoedas** simultaneamente (BTC_BRL, ETH_BRL, SOL_BRL, XRP_BRL, ADA_BRL, DOT_BRL, LINK_BRL, MATIC_BRL), executa estratégias configuráveis e disponibiliza um dashboard web responsivo para acompanhamento em tempo real com notificações visuais e sonoras.

## Tecnologias Utilizadas

| Tecnologia | Finalidade |
|---|---|
| **Python 3.8+** | Linguagem principal do bot |
| **NovaDAX API** | Exchange brasileira para operações |
| **WebSocket** | Comunicação em tempo real bot-dashboard |
| **HTML/CSS/JS** | Dashboard web responsivo (dark mode) |
| **Web Audio API** | Notificações sonoras no navegador |
| **Push API** | Notificações push do navegador |
| **Random Forest** | Modelo de ML para predição de preços |
| **Indicadores Técnicos** | RSI, EMA, MACD, Bollinger Bands, Volume |

## Estrutura do Projeto

```
MercadoCript/
├── bot.py                    # Lógica principal do bot (loop de verificação)
├── config.py                 # Parâmetros centralizados
├── novadax_client.py         # Integração com API NovaDAX
├── strategy.py               # Estratégias de trading
├── web.py                    # Servidor web + WebSocket (ponto de entrada)
├── run.py                    # Script auxiliar de execução
├── requirements.txt          # Dependências Python
├── .env                      # Credenciais da API (access key + secret key)
│
├── web/
│   ├── static/               # Arquivos estáticos (CSS, JS)
│   └── templates/
│       └── index.html        # Dashboard HTML (responsivo, dark mode)
│
├── data/
│   ├── state.json            # Estado atual do bot (checkpoint)
│   ├── trades.json           # Histórico de operações
│   ├── ml_data/              # Dados históricos para ML
│   └── ml_models/            # Modelos treinados (Random Forest)
│
├── logs/
│   ├── bot.log               # Logs de operação do bot
│   └── web.log               # Logs do servidor web
│
└── docs/
    ├── CONFIGURACAO.md       # Guia de configuração
    ├── ESTRATEGIAS.md        # Detalhes das estratégias
    ├── USO.md                # Guia de uso
    ├── API.md                # Documentação da API do dashboard
    ├── FAQ.md                # Perguntas frequentes
    └── MACHINE_LEARNING.md   # Documentação do ML
```

## Funcionalidades Principais

### 1. Estratégias de Trading

| Estratégia | Descrição |
|---|---|
| **Multi-Indicador** | Combina RSI, EMA Cross, Bollinger Bands, MACD e Volume em sistema de pontuação (score) |
| **Grid Trading** | 10 níveis de ordens (5 acima, 5 abaixo) com espaçamento de 2% |
| **Trailing Stop** | Ativa após +3% de lucro; vende se preço cair 1.5% do pico |
| **Análise de Tendência BTC** | Ajusta scores das altcoins baseado na tendência do Bitcoin (peso 30%) |
| **Rotação Inteligente** | Mantém até 3 posições simultâneas; vende a pior para comprar a melhor |
| **Stop Loss / Take Profit** | -5% / +8% por padrão |

![Estratégias de Trading]({{ '/assets/img/mercadocript-2.png' | relative_url }})

### 2. Criptomoedas Monitoradas (8 pares)

`BTC_BRL`, `ETH_BRL`, `SOL_BRL`, `XRP_BRL`, `ADA_BRL`, `DOT_BRL`, `LINK_BRL`, `MATIC_BRL`

### 3. Dashboard Web

- Atualização em tempo real via WebSocket
- Cards de estatísticas (Patrimônio Total, Saldo BRL, Valor em Crypto, Lucro/Prejuízo)
- Tabela de Sinais com scores de todas as moedas
- Posições Abertas com P&L em tempo real
- Gráfico de evolução do patrimônio
- Histórico de Trades completo
- Design dark mode responsivo
- **Notificações visuais e sonoras** para compras, vendas e metas de lucro

![Dashboard em Tempo Real]({{ '/assets/img/mercadocript-3.png' | relative_url }})

### 4. Machine Learning (Random Forest)

- **Modelo:** Random Forest Classifier treinado por moeda
- **Features:** 40+ indicadores técnicos + features temporais
- **Predição:** Movimento nas próximas 12 horas (3 classes: Alta +2%, Lateral, Queda -2%)
- **Integração:** Ajusta sinais do bot com peso de 30% (configurável)
- **Confiança mínima:** 60% para usar a predição

#### Resultados do Treinamento (v2.0)

| Moeda | Acurácia | Status |
|---|---|---|
| BTC_BRL | 87.88% | Excelente |
| DOT_BRL | 75.95% | Bom |
| ADA_BRL | 62.30% | Aceitável |
| XRP_BRL | 62.12% | Aceitável |
| SOL_BRL | 58.02% | Regular |
| LINK_BRL | 36.63% | Fraco |
| ETH_BRL | 32.58% | Fraco |
| **Média** | **59.35%** | |

![Machine Learning]({{ '/assets/img/mercadocript-4.png' | relative_url }})

### 5. Análise Histórica e Alertas de Segurança (v3.0)

- **Treinamento massivo:** 3 anos de dados (1000 candles diários) para 8 moedas
- **Análise Histórica pré-operação:** Tendência 7 dias, 24h, volatilidade, suporte/resistência, volume
- **Alertas de segurança:** Bloqueio se preço caiu >10% (dump) ou subiu >15% (pump) em 24h
- **Notificações:** Web Audio API + notificações visuais + push notifications
- **Expectativa do ML no Dashboard:** Cards roxos com previsão de patrimônio (fim do dia / fim da semana)

### 6. Perfis de Configuração

| Perfil | MAX_POSITIONS | STOP_LOSS | TAKE_PROFIT | GRID |
|---|---|---|---|---|
| **Conservador** | 2 | -3% | +6% | Desligado |
| **Moderado** | 3 | -5% | +8% | Ligado |
| **Agressivo** | 4 | -7% | +12% | Ligado (7 níveis) |

## Galeria do Sistema

| Tela | Descrição |
|------|-----------|
| ![Tela 5]({{ '/assets/img/mercadocript-5.png' | relative_url }}) | Histórico de trades e desempenho |
| ![Tela 6]({{ '/assets/img/mercadocript-6.png' | relative_url }}) | Configurações do bot e perfis de risco |

## Arquitetura

```
web.py (servidor web + bot em background)
    │
    ├── A cada 5 minutos:
    │    ├── Busca dados de mercado (100 velas de 1h) via NovaDAX API
    │    ├── Calcula indicadores (RSI, EMA, MACD, Bollinger, Volume)
    │    ├── Gera scores para cada uma das 8 moedas
    │    ├── Aplica ML (se habilitado) para ajustar scores
    │    ├── Executa análise histórica de segurança
    │    ├── Decide comprar/vender baseado nos scores
    │    ├── Gerencia Grid Trading, Trailing Stop, SL/TP
    │    └── Atualiza dashboard via WebSocket
    │
    └── Dashboard web (tempo real):
         ├── Cards de estatísticas
         ├── Tabela de sinais
         ├── Posições abertas
         ├── Gráfico de patrimônio
         └── Notificações visuais/sonoras
```

## Scripts do Projeto

| Script | Função |
|---|---|
| `bot.py` | Lógica principal do bot (loop de verificação) |
| `config.py` | Parâmetros centralizados |
| `novadax_client.py` | Cliente da API NovaDAX |
| `strategy.py` | Estratégias de trading |
| `web.py` | Servidor web + dashboard (ponto de entrada) |
| `run.py` | Script auxiliar de execução |
| `data_collector.py` | Coleta dados históricos para ML |
| `train_models.py` | Treina modelos de ML |
| `massive_train.py` | Treinamento massivo com N dias de dados |

## Instalação e Execução

```bash
# Instalar dependências
pip install -r requirements.txt

# Configurar credenciais (access key + secret key da NovaDAX)
# Editar arquivo .env

# Iniciar bot + dashboard
python web.py
```

Acessar dashboard em: `http://localhost:<porta>`

## Versões

| Versão | Descrição | Data |
|---|---|---|
| 1.0 | Bot base com estratégias técnicas | - |
| 2.0 | Implementação de Machine Learning | 31/05/2026 |
| 3.0 | Treinamento massivo + análise histórica + notificações | 31/05/2026 |

## Licenciamento e comercialização

O MercadoCript está disponível para negociação de licenciamento, implementação e evolução.

Condições comerciais podem incluir:
- Licenciamento de uso do código
- Transferência parcial ou total conforme acordo
- Customizações específicas (novas estratégias, outras exchanges)
- Configuração em ambiente do cliente
- Suporte técnico inicial
- Manutenção contínua

Para tratar valores, escopo e condições de entrega, entre em contato informando o interesse no **MercadoCript**.
