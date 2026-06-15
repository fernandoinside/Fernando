---
title: "Cybersecurity Intelligence MCP"
subtitle: "Servidor MCP para Integração do Metasploit com IA"
description: "Servidor MCP (Model Context Protocol) que integra o Metasploit Framework com assistentes de IA, expondo 18 ferramentas para automação de pentests, com sistema de workspaces, aprendizado contínuo, habilidades plugáveis e scanner de rede assíncrono."
status: "disponivel"
published: true
exclude_from_listing: false
category: "Segurança Ofensiva"
tech_stack:
  - "Python"
  - "FastMCP"
  - "Metasploit RPC"
  - "FastAPI"
  - "Pydantic"
  - "asyncio"
  - "Rich"
  - "pytest"
  - "pymetasploit3"
featured_image:
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
      - "Configuração inicial"
      - "Orientação de uso e integração com IA"
      - "Ajustes conforme ambiente"
  - name: "Suporte e Evolução"
    price: "Sob consulta"
    features:
      - "Correções e manutenção"
      - "Novas funcionalidades e skills"
      - "Suporte técnico contínuo"
demo_url: ""
docs_url: ""
repo_url: ""
---

# Cybersecurity Intelligence MCP

**Cybersecurity Intelligence MCP** é um servidor **MCP (Model Context Protocol)** que integra o **Metasploit Framework (MSF)** com assistentes de IA, permitindo automação de testes de penetração através de chamadas de ferramentas padronizadas. O projeto inclui sistema de workspaces por alvo, histórico de aprendizado, habilidades plugáveis e scanner de rede assíncrono.

> Uso recomendado apenas em ambientes próprios, laboratórios controlados ou operações autorizadas por contrato.

## Visão geral

O Cybersecurity Intelligence MCP funciona como uma ponte entre assistentes de IA (Claude, GPT, etc.) e o Metasploit Framework, expondo **18 ferramentas MCP** que cobrem desde varredura de portas e busca de exploits até execução de módulos e gerenciamento de sessões. Cada operação é registrada em workspaces individuais por alvo, com histórico de aprendizado persistente em `learning_log.jsonl`.

O servidor suporta **transporte duplo**: stdio para integração direta com assistentes de IA, e HTTP (SSE) para integração web via FastAPI + Uvicorn.

## Tecnologias Utilizadas

| Tecnologia | Finalidade |
|---|---|
| **Python 3.14+** | Linguagem principal |
| **FastMCP / MCP SDK** | Implementação do protocolo MCP |
| **pymetasploit3** | Bindings Python para API RPC do Metasploit |
| **FastAPI + Uvicorn** | Transporte HTTP para o MCP |
| **Pydantic / pydantic-settings** | Configuração via .env |
| **asyncio** | Operações concorrentes |
| **Rich** | Interface CLI (tabelas, banners) |
| **pytest** | Testes unitários |
| **JSON-RPC 2.0** | Protocolo de comunicação |

## Estrutura do Projeto

```
MCPs/Cybersecurity-Intelligence/
├── opencode.json              # Configuração MCP
├── mcp_client.py              # Cliente MCP genérico (testes sem IA)
│
├── fusion_mcp/                # Core do projeto
│   ├── .env                   # Configuração ativa
│   ├── .env.example           # Template de configuração
│   ├── requirements.txt       # Dependências Python
│   ├── README.md              # Documentação (português)
│   ├── mcp_bridge.py          # Bridge legada
│   ├── pytest.ini             # Configuração de testes
│   │
│   ├── fusion_msf_mcp/        # Pacote principal
│   │   ├── __init__.py        # Exports: mcp, settings
│   │   ├── __main__.py        # Entry point
│   │   ├── config.py          # Settings (Pydantic)
│   │   ├── core.py            # Ciclo de vida do MSF RPC
│   │   ├── server.py          # Definição das ferramentas MCP (18 tools)
│   │   ├── cli.py             # Interface de linha de comando
│   │   ├── network_scanner.py # Scanner de rede async
│   │   ├── skill_loader.py    # Carregador dinâmico de skills
│   │   │
│   │   └── skills/            # Habilidades plugáveis
│   │       ├── README.md
│   │       └── sqli_boost.py  # Gerador de PoC SQLi
│   │
│   └── tests/                 # Testes unitários
│       ├── test_core.py
│       ├── test_network_scanner.py
│       ├── test_server_import.py
│       └── test_workspace_helpers.py
```

## Funcionalidades Principais

### 1. Ferramentas MCP (18 ferramentas expostas)

| Ferramenta | Descrição |
|---|---|
| `check_msf_connection` | Testa conexão com o Metasploit RPC |
| `create_target_workspace` | Cria workspace para um alvo |
| `scan_target` | Varredura TCP via MSF (scanner/portscan/tcp) |
| `list_target_workspaces` | Lista todos os workspaces |
| `get_learning_history` | Histórico de aprendizado de um alvo |
| `advanced_ip_scanner` | Scanner de rede local rápido (async) |
| `list_exploits` | Lista/busca exploits disponíveis |
| `list_payloads` | Lista/busca payloads disponíveis |
| `generate_payload` | Gera e salva um payload |
| `run_exploit` | Executa um exploit (com polling de sessão) |
| `run_auxiliary_module` | Executa módulo auxiliar/scanner |
| `list_active_sessions` | Lista sessões Meterpreter/Shell ativas |
| `list_listeners` | Lista jobs/listeners ativos |
| `start_listener` | Inicia um multi/handler |
| `stop_job` | Para um job em execução |
| `send_session_command` | Envia comandos para sessão ativa |
| `terminate_session` | Mata uma sessão |
| `run_post_module` | Executa módulo de pós-exploração |
| `search_modules` | Busca módulos no MSF |
| `get_module_info` | Informações detalhadas de um módulo |

### 2. Sistema de Workspaces
- Cada alvo recebe um diretório em `workspaces_root_dir/<target>/`
- Resultados de scans são salvos como arquivos texto
- Eventos de aprendizado são registrados em `learning_log.jsonl`
- Organização por domínio com descrição e histórico

### 3. Scanner de Rede Avançado
- Inspirado no **Advanced IP Scanner**
- Varredura assíncrona de ranges CIDR
- Probe de portas concorrente (configurável, default 150)
- Timeout configurável (default 80ms por porta)
- Resolução DNS reversa opcional
- Detecção automática da rede local

### 4. Sistema de Skills (Habilidades Plugáveis)
- Scripts Python em `skills/` são carregados automaticamente
- Cada skill expõe: `SKILL_NAME`, `SKILL_DESCRIPTION`, `async def run(args)`
- Skill atual: **`sqli_boost`** - gera script PoC de SQL Injection
- Arquitetura extensível para novas habilidades

### 5. CLI (Interface de Linha de Comando)
- Banner ASCII com tema Rich
- Comandos: `check`, `scan <target>`, `list`, `history <target>`, `skills list`, `skills run`
- Saída formatada em tabelas ou JSON

### 6. Duplo Transporte
- **stdio:** Para integração com assistentes de IA
- **HTTP (SSE):** Para integração web via FastAPI + Uvicorn

## Arquitetura

```
+-------------------+     JSON-RPC 2.0      +---------------------------+
|                   |  ──────────────────►  |                           |
| AI Assistant /    |    (stdio ou HTTP)    |   fusion_mcp MCP Server   |
| mcp_client.py     |  ◄──────────────────  |                           |
|                   |                       |   FastMCP + FastAPI       |
+-------------------+                       +----------+---------------+
                                                         |
                                                     pymetasploit3
                                                     (RPC calls)
                                                         |
                                               +---------+---------+
                                               |                   |
                                               |   Metasploit      |
                                               |   (msfrpcd)       |
                                               |   - Exploits      |
                                               |   - Payloads      |
                                               |   - Sessions      |
                                               +-------------------+
                                                         |
                                                         | Saídas
                                                         v
                                               +---------+---------+
                                               |   Workspace Dir    |
                                               |   ~/mcp_workspaces/|
                                               |   learning_log     |
                                               +-------------------+
```

## Fluxo de Operação

1. Agente IA (ou CLI) envia requisição de ferramenta MCP (ex: `scan_target`)
2. Servidor `fusion_msf_mcp` recebe e valida parâmetros
3. Conecta ao Metasploit RPC (`msfrpcd`) via `pymetasploit3`
4. MSF executa o módulo solicitado
5. Resultados são coletados, salvos no workspace do alvo
6. Evento de aprendizado é registrado em `learning_log.jsonl`
7. Resposta JSON estruturada é retornada ao chamador

## Configuração (.env)

| Variável | Descrição | Default |
|---|---|---|
| `MSF_SERVER` | Host do msfrpcd | `127.0.0.1` |
| `MSF_PORT` | Porta do msfrpcd | `55552` |
| `MSF_PASSWORD` | Senha do msfrpcd | (obrigatório) |
| `MSF_SSL` | Usar SSL | `false` |
| `WORKSPACES_ROOT_DIR` | Diretório de workspaces | `~/mcp_workspaces` |
| `PAYLOAD_SAVE_DIR` | Diretório de payloads | `~/payloads` |
| `MCP_TRANSPORT` | Transporte (stdio/http) | `stdio` |
| `MCP_HOST` | Host do servidor HTTP | `0.0.0.0` |
| `MCP_PORT` | Porta do servidor HTTP | `8080` |

## Instalação e Execução

```bash
# Instalar dependências
pip install -r requirements.txt

# Executar como servidor MCP (stdio - para IAs)
python -m fusion_msf_mcp --transport stdio

# Executar como servidor HTTP
python -m fusion_msf_mcp --transport http --host 0.0.0.0 --port 8080

# Usar CLI
python -m fusion_msf_mcp --cli scan target.com.br
```

## Testes

```bash
pytest tests/ -v
```

Marcadores: `unit` (testes unitários), `integration` (testes de integração).

## Licenciamento e comercialização

O Cybersecurity Intelligence MCP está disponível para negociação de licenciamento, implementação e evolução.

Condições comerciais podem incluir:
- Licenciamento de uso do código
- Transferência parcial ou total conforme acordo
- Customizações específicas (novas skills, integrações com outros frameworks)
- Configuração em ambiente do cliente
- Suporte técnico inicial
- Manutenção contínua

Para tratar valores, escopo e condições de entrega, entre em contato informando o interesse no **Cybersecurity Intelligence MCP**.
