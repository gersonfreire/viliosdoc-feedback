# ViliosDoc Web - Plano de Novas Funcionalidades v2.2

> **Atualização da aplicação web** para paridade com o ViliosDoc HTML Standalone v2.2
>
> Baseado na análise do Manual do Usuário v2.2 (Fevereiro 2026) e engenharia reversa do `vilios-doc16.html`

---

IMPORTANTE: CORRREÇÃO EFETUADA NO SISTEMA DE ANÁLISES REALIZADA EM 02/03/2026 AS 21:58

---
TESTE DE NOTIFICAÇÃO RSS
---

## Sumário

1. [Visão Geral](#1-visão-geral)
2. [Análise de Gap](#2-análise-de-gap)
3. [Fase 1 - Parser de Variáveis](#3-fase-1---parser-de-variáveis)
4. [Fase 2 - Detector de APIs/WebServices](#4-fase-2---detector-de-apiswebservices)
5. [Fase 3 - Tabelas Customizadas](#5-fase-3---tabelas-customizadas)
6. [Fase 4 - Dependências User Functions](#6-fase-4---dependências-user-functions)
7. [Fase 5 - Mapa de Migração MsDialog](#7-fase-5---mapa-de-migração-msdialog)
8. [Fase 6 - Mapa de Funções User→Static](#8-fase-6---mapa-de-funções-userstatic)
9. [Fase 7 - Análise Avançada de SQL (Queries × Fontes)](#9-fase-7---análise-avançada-de-sql-queries--fontes)
10. [Fase 8 - Fluxo de Processo / BPMN](#10-fase-8---fluxo-de-processo--bpmn)
11. [Fase 9 - Governança e Políticas](#11-fase-9---governança-e-políticas)
12. [Fase 10 - Compliance & BPMN ISO 27001](#12-fase-10---compliance--bpmn-iso-27001)
13. [Fase 11 - Melhorias em Funcionalidades Existentes](#13-fase-11---melhorias-em-funcionalidades-existentes)
14. [Fase 12 - Exportações Adicionais](#14-fase-12---exportações-adicionais)
15. [Fase 13 - Testes e Validação](#15-fase-13---testes-e-validação)
16. [Resumo de Arquivos](#16-resumo-de-arquivos)

---

## 1. Visão Geral

### Estado Atual da Aplicação Web

A aplicação web ViliosDoc possui atualmente:

- **21 visualizações** (views) no frontend
- **13 parsers** no backend (+ 2 calculadores: Score TOTVS e Complexidade)
- **3 formatos de exportação** (Word, HTML, TXT)
- **Motor de análise** com pipeline de 5 fases

### O que há de novo no v2.2 (HTML Standalone)

O ViliosDoc HTML v2.2 expandiu para **34 módulos de análise**, adicionando funcionalidades significativas:

| # | Módulo Novo | Complexidade | Prioridade |
|---|-------------|-------------|------------|
| 1 | Variáveis (auditoria completa) | Alta | Alta |
| 2 | APIs/WebServices | Média | Média |
| 3 | Tabelas Customizadas | Baixa | Média |
| 4 | Dependências User Functions | Média | Alta |
| 5 | Migração MsDialog | Baixa | Baixa |
| 6 | Mapa de Funções User→Static | Baixa | Média |
| 7 | Queries × Fontes (SQL Analytics) | Muito Alta | Alta |
| 8 | Fluxo de Processo / BPMN | Alta | Média |
| 9 | Governança e Políticas | Alta | Alta |
| 10 | Compliance & BPMN ISO 27001 | Alta | Média |
| 11 | Melhorias em issues existentes | Média | Alta |
| 12 | Exportações adicionais (PNG, Tutorial IA) | Média | Baixa |

---

## 2. Análise de Gap

### Módulos do v2.2 vs Web Atual

| # | Módulo v2.2 | Tab | Web Atual | Status |
|---|------------|-----|-----------|--------|
| 1 | Workspace | 5.1 | WorkspaceView | ✅ Implementado |
| 2 | Estrutura de Pastas | 5.2 | FolderStructureView | ✅ Implementado |
| 3 | Inventário | 5.3 | InventoryView | ✅ Implementado |
| 4 | Métricas | 5.4 | MetricsView | ✅ Implementado |
| 5 | Complexidade | 5.5 | ComplexityView | ✅ Implementado |
| 6 | Tabelas | 5.6 | TablesView | ✅ Implementado |
| 7 | Parâmetros | 5.7 | ParametersView | ✅ Implementado |
| 8 | Includes | 5.8 | IncludesView | ✅ Implementado |
| 9 | Possíveis Falhas | 5.9 | IssuesView | ⚠️ Parcial (menos regras) |
| 10 | Boas Práticas TOTVS | 5.10 | BestPracticesView | ✅ Implementado |
| 11 | Mapa Mental | 5.11 | MentalMapView | ✅ Implementado |
| 12 | Relacionamentos (5 mapas) | 5.11.x | RelationshipsView | ⚠️ 4 de 5 mapas |
| 13 | **Variáveis** | **5.17** | — | ❌ Não existe |
| 14 | Fluxograma Estrutural | 5.18 | FlowchartView | ✅ Implementado |
| 15 | Fluxograma Gráfico | 5.19 | GraphicFlowView | ✅ Implementado |
| 16 | **Mapa de Funções User→Static** | **5.20** | — | ❌ Não existe |
| 17 | **Fluxo de Processo / BPMN** | **5.21** | — | ❌ Não existe |
| 18 | **APIs/WebServices** | **5.22** | — | ❌ Não existe |
| 19 | **Tabelas Customizadas** | **5.23** | — | ❌ Não existe |
| 20 | **Dependências User Fn** | **5.24** | — | ❌ Não existe |
| 21 | **Migração MsDialog** | **5.25** | — | ❌ Não existe |
| 22 | Usuários | 5.26 | UsersView | ✅ Implementado |
| 23 | Emails | 5.27 | EmailsView | ✅ Implementado |
| 24 | **Queries × Fontes** | **5.28** | — | ❌ Não existe |
| 25 | **Governança & Políticas** | **5.29** | — | ❌ Não existe |
| 26 | Tutorial IA | 5.30 | TutorialView | ✅ Implementado |
| 27 | **Compliance & BPMN** | **5.31** | — | ❌ Não existe |
| 28 | Autores | — | AuthorsView | ✅ Implementado |
| 29 | Funções | — | FunctionsView | ✅ Implementado |
| 30 | Pontos de Entrada | — | EntryPointsView | ✅ Implementado |
| 31 | ExecBlock Map | — | ExecBlockMapView | ✅ Implementado |

**Resumo**: 10 módulos novos + 2 melhorias em existentes = **12 itens de trabalho**

---

## 3. Fase 1 - Parser de Variáveis

> Tab 5.17 do v2.2: Auditoria completa de variáveis declaradas nos fontes

### 3.1 Backend - Parser de Variáveis

- [ ] Criar `backend/app/core/parsers/variables.py` — **VariablesParser**

**Lógica de extração:**
```python
# Regex principal para declaração de variáveis
VARIABLE_DECL_RE = re.compile(
    r"^\s*(Local|Private|Public|Static|Default)\s+(.+)",
    re.IGNORECASE | re.MULTILINE
)
```

**Detecção de tipo por inicialização:**

| Padrão | Tipo |
|--------|------|
| `^["']` | Character |
| `.T.` ou `.F.` | Logical |
| `^\d+\.?\d*$` | Numeric |
| `^\{` | Array |
| `CToD\|dDataBase\|Date(` | Date |
| `^NIL$` | NIL |
| Sem inicialização | "Indefinido" |

**Detecção de variáveis não utilizadas:**
- Após extrair a declaração, verificar se o nome da variável aparece em alguma outra linha do código (excluindo a própria declaração e comentários)

**Rastreamento de variáveis Public:**
- Para variáveis Public, rastrear em quais outros arquivos/funções são referenciadas

**Modelo de dados:**
```python
@dataclass
class VariableInfo:
    name: str
    scope: str          # Local | Private | Public | Static | Default
    type: str           # Character | Logical | Numeric | Array | Date | NIL | Indefinido
    owner_function: str
    file_name: str
    line: int
    is_used: bool
    type_mismatch: str | None  # Ex: "Recebe Numeric (era Character)"
```

- [ ] Adicionar ao `AnalysisResult` em `backend/app/core/models.py`:
  ```python
  variables: list[VariableInfo] = field(default_factory=list)
  unused_variables: list[VariableInfo] = field(default_factory=list)
  ```

- [ ] Integrar no pipeline em `backend/app/core/engine.py` (Fase 3: processamento de arquivos)

### 3.2 Frontend - VariablesView

- [ ] Criar `frontend/src/components/views/VariablesView.tsx`

**Layout:**
1. **Cards de estatísticas**: Total de variáveis, não utilizadas, incompatibilidades de tipo, escopos únicos
2. **Distribuição por escopo**: Barras horizontais coloridas (Local: azul, Private: amarelo, Public: vermelho, Static: roxo)
3. **Seção "Variáveis Não Utilizadas"**: Tabela com destaque vermelho
4. **Seção "Incompatibilidades de Tipo"**: Lista de warnings
5. **Árvore agrupada por escopo**: Accordions com indicador de uso (✅/❌)
6. **Mapa de uso de variáveis Public**: Quais arquivos referenciam variáveis públicas

- [ ] Adicionar tipo `VariableInfo` em `frontend/src/types/analysis-result.ts`
- [ ] Adicionar item no sidebar e no mapa de views em `AnalysisPage.tsx`
- [ ] Adicionar traduções PT/EN/ES

### 3.3 Validação

- [ ] Parser detecta variáveis Local, Private, Public, Static
- [ ] Tipo inferido corretamente pela inicialização
- [ ] Variáveis não utilizadas identificadas
- [ ] View renderiza todas as seções

---

## 4. Fase 2 - Detector de APIs/WebServices

> Tab 5.22 do v2.2: Detecção de chamadas HTTP, REST e SOAP nos fontes

### 4.1 Backend - Detector de APIs

- [ ] Criar `backend/app/core/parsers/api_detector.py` — **ApiDetector**

**Padrões de detecção:**
```python
API_PATTERNS = {
    "HttpGet":       re.compile(r"\bHttpGet\b", re.IGNORECASE),
    "HttpPost":      re.compile(r"\bHttpPost\b", re.IGNORECASE),
    "HttpPut":       re.compile(r"\bHttpPut\b", re.IGNORECASE),
    "HttpDelete":    re.compile(r"\bHttpDelete\b", re.IGNORECASE),
    "FwRest":        re.compile(r"\bFwRest\b", re.IGNORECASE),
    "FwCallRest":    re.compile(r"\bFwCallRest\b", re.IGNORECASE),
    "WsReceive":     re.compile(r"\bWsReceive\b", re.IGNORECASE),
    "WsSend":        re.compile(r"\bWsSend\b", re.IGNORECASE),
    "FWHttpClient":  re.compile(r"\bFWHttpClient\b", re.IGNORECASE),
}

# Extração de URL
URL_RE = re.compile(r'''["'](https?://[^"']+)["']''')
```

**Modelo de dados:**
```python
@dataclass
class ApiReference:
    file_name: str
    line: int
    api_type: str       # HttpGet | HttpPost | FwRest | etc.
    url: str | None     # URL extraída quando disponível
    description: str    # Descrição funcional do tipo de API
    context: str        # Trecho da linha de código
```

- [ ] Adicionar `api_references: list[ApiReference]` ao `AnalysisResult`
- [ ] Integrar no pipeline

### 4.2 Frontend - ApiWebServicesView

- [ ] Criar `frontend/src/components/views/ApiWebServicesView.tsx`

**Layout:**
1. **Stats**: Total de chamadas API, fontes distintos, URLs únicas, tipos de API
2. **Agrupado por tipo de API**: Accordions expansíveis
3. **Cards de detalhe**: Badge de tipo, arquivo/linha, descrição, link URL, código

- [ ] Adicionar tipo, sidebar, traduções

### 4.3 Validação

- [ ] Detecta HttpGet, HttpPost, FwRest, WsReceive, FWHttpClient
- [ ] Extrai URLs quando presentes
- [ ] View agrupa por tipo corretamente

---

## 5. Fase 3 - Tabelas Customizadas

> Tab 5.23 do v2.2: Identificação de campos customizados (_X, _Y) no dicionário de dados

### 5.1 Backend - Detector de Campos Customizados

- [ ] Criar `backend/app/core/parsers/custom_tables.py` — **CustomTableDetector**

**Padrões de detecção:**
```python
# Campos _X (padrão clássico TOTVS)
FIELD_X_RE = re.compile(r"([A-Z][A-Z0-9])->([A-Z0-9]{2,3}_X[A-Z0-9_]+)", re.IGNORECASE)

# Campos _Y (padrão analista/consultor)
FIELD_Y_RE = re.compile(r"([A-Z][A-Z0-9])->([A-Z0-9]{2,3}_Y[A-Z0-9_]+)", re.IGNORECASE)
```

**Modelo de dados:**
```python
@dataclass
class CustomFieldInfo:
    table: str          # Ex: SA1, SC5
    field: str          # Ex: A1_XNOME, A1_YCAMPO
    field_type: str     # "_X" | "_Y"
    files: list[str]    # Arquivos que referenciam

@dataclass
class CustomTableInfo:
    table: str
    table_description: str
    fields: list[CustomFieldInfo]
    file_count: int
```

- [ ] Adicionar `custom_tables: list[CustomTableInfo]` ao `AnalysisResult`
- [ ] Integrar no pipeline

### 5.2 Frontend - CustomTablesView

- [ ] Criar `frontend/src/components/views/CustomTablesView.tsx`

**Layout:**
1. **Stats**: Tabelas com campos custom, total de campos, _X count, _Y count
2. **Legenda**: Convenção SX3 (X3_ORIGEM = "U")
3. **Accordion por tabela**: Grid de cards de campos com badge [_X]/[_Y] e borda colorida

- [ ] Adicionar tipo, sidebar, traduções

---

## 6. Fase 4 - Dependências User Functions

> Tab 5.24 do v2.2: Mapa de chamadas entre User Functions (prefixo U_)

### 6.1 Backend - Parser de Dependências

- [ ] Criar `backend/app/core/parsers/user_fn_deps.py` — **UserFnDepsParser**

**Padrão de detecção:**
```python
# Chamadas a U_ functions
U_CALL_RE = re.compile(r"U_(\w+)\s*\(", re.IGNORECASE)

# Para encontrar função chamadora
FUNC_START_RE = re.compile(r"(User|Static)\s+Function\s+(\w+)", re.IGNORECASE)
```

**Lógica:**
1. Iterar cada linha do arquivo
2. Para cada match de `U_(\w+)\(`, fazer scan reverso para encontrar a função que contém a chamada
3. Registrar: função origem → função chamada, arquivo, linha, contexto
4. Deduplicar por chave `file|from→to`

**Modelo de dados:**
```python
@dataclass
class UserFnDependency:
    caller_function: str    # Função que faz a chamada
    called_function: str    # Função U_ chamada
    file_name: str
    line: int
    context: str            # Trecho da linha (80 chars max)
```

- [ ] Adicionar `user_fn_dependencies: list[UserFnDependency]` ao `AnalysisResult`
- [ ] Integrar no pipeline

### 6.2 Frontend - UserFnDepsView

- [ ] Criar `frontend/src/components/views/UserFnDepsView.tsx`

**Layout:**
1. **Stats**: Total dependências, arquivos afetados, chamadores únicos, funções chamadas
2. **Accordion por arquivo fonte**: Tabela com Função Origem → Função Chamada, Linha
3. Ordenado por quantidade de dependências (decrescente)

- [ ] Adicionar tipo, sidebar, traduções

---

## 7. Fase 5 - Mapa de Migração MsDialog

> Tab 5.25 do v2.2: Fontes que usam componentes deprecated e precisam migrar

### 7.1 Backend - Detector de Migração

- [ ] Criar `backend/app/core/parsers/migration.py` — **MigrationDetector**

**Padrões de detecção:**
```python
MIGRATION_PATTERNS = {
    "MsDialog": {
        "pattern": re.compile(r"MsDialog|DEFINE\s+MSDIALOG", re.IGNORECASE),
        "target": "FWDialogModal",
    },
    "Processa()": {
        "pattern": re.compile(r"Processa\s*\(", re.IGNORECASE),
        "target": "FWMsgRun()",
    },
    "SetProcedure()": {
        "pattern": re.compile(r"SetProcedure\s*\(", re.IGNORECASE),
        "target": "ProcRegua()",
    },
}
```

**Modelo de dados:**
```python
@dataclass
class MigrationItem:
    file_name: str
    line: int
    deprecated_api: str    # "MsDialog" | "Processa()" | "SetProcedure()"
    target_api: str        # "FWDialogModal" | "FWMsgRun()" | "ProcRegua()"
    context: str           # Trecho do código (70 chars)
```

- [ ] Adicionar `migration_items: list[MigrationItem]` ao `AnalysisResult`
- [ ] Integrar no pipeline

### 7.2 Frontend - MigrationView

- [ ] Criar `frontend/src/components/views/MigrationView.tsx`

**Layout:**
1. **Stats**: Total migrações, fontes afetados, tipos
2. **Accordion por tipo**: "MsDialog → FWDialogModal (N)", tabela com arquivo, linha, contexto
3. Se nenhum encontrado: "Nenhum componente deprecated detectado"

- [ ] Adicionar tipo, sidebar, traduções

---

## 8. Fase 6 - Mapa de Funções User→Static

> Tab 5.20 do v2.2: Tabela mostrando relação entre User Functions e Static Functions por fonte

### 8.1 Backend

- [ ] O parser de funções (`functions.py`) já extrai User e Static Functions
- [ ] Adicionar helper no `AnalysisResult` para agrupar funções por arquivo e tipo

### 8.2 Frontend - FunctionMapView

- [ ] Criar `frontend/src/components/views/FunctionMapView.tsx`

**Layout:**
1. Tabela estilo planilha: arquivo na coluna esquerda
2. Colunas: User Functions (público) e Static Functions (privado)
3. Código de cores para facilitar visualização de dependências internas
4. Cada célula lista as funções daquele tipo naquele arquivo

- [ ] Adicionar no sidebar, traduções

---

## 9. Fase 7 - Análise Avançada de SQL (Queries × Fontes)

> Tab 5.28 do v2.2: Extração avançada de SQL com análise de qualidade em 4 dimensões

### 9.1 Backend - Analisador de SQL Avançado

**Esta é a funcionalidade mais complexa do plano.**

- [ ] Criar `backend/app/core/parsers/sql_analyzer.py` — **SqlAnalyzer**

**Três padrões de extração:**

1. **BeginSql...EndSql**: Captura bloco completo, resolve variáveis `%exp:varName%`
2. **Variáveis cQuery/cSql**: Reconstrói SQL montado por concatenação de strings
3. **TCQuery/TCSqlExec inline**: Captura SQL embutido diretamente na chamada

**Extração de Variáveis:**
```python
# BeginSql: resolve %exp:varName%
VAR_REF_RE = re.compile(r"%exp:(\w+)%")

# Concatenação: cQuery := "SELECT..." + cQuery += "FROM..."
CQUERY_INIT_RE = re.compile(r"(cQuery|cSql)\s*:=\s*(.+)", re.IGNORECASE)
CQUERY_CONCAT_RE = re.compile(r"(cQuery|cSql)\s*(\+\=|:=\s*\1\s*\+)\s*(.+)", re.IGNORECASE)

# Execução inline
INLINE_SQL_RE = re.compile(
    r"(?:TCQuery|TCSqlExec|TCGENQRY)\s*\(\s*[\"'](.{20,})[\"']",
    re.IGNORECASE
)
```

**Modelo de dados:**
```python
@dataclass
class SqlQueryInfo:
    query_type: str         # "BeginSql" | "Variable" | "Inline"
    file_name: str
    line_start: int
    line_end: int
    raw_sql: str            # SQL limpo reconstruído
    sql_type: str           # SELECT | INSERT | UPDATE | DELETE
    tables_used: list[str]  # Tabelas identificadas no SQL
    variables: dict[str, SqlVariable]  # Variáveis rastreadas
    var_name: str | None    # Para tipo Variable: nome da variável
    execution_context: str | None  # TCQuery, TCSqlExec, DBUseArea
    quality: SqlQualityScore | None

@dataclass
class SqlVariable:
    name: str
    value: str              # Valor atribuído (80 chars max)
    line: int
    declaration: str        # Linha de declaração

@dataclass
class SqlQualityScore:
    overall: float          # 0-100
    grade: str              # A | B | C | D | F
    performance: float      # 0-100 (peso 35%)
    organization: float     # 0-100 (peso 15%)
    efficiency: float       # 0-100 (peso 25%)
    security: float         # 0-100 (peso 25%)
    issues: list[SqlQualityIssue]
    suggestions: list[str]
    suggested_query: str | None  # Quando nota < 70%

@dataclass
class SqlQualityIssue:
    rule: str
    severity: str           # "Alta" | "Média" | "Baixa" | "Dica"
    penalty: int
    description: str
    category: str           # "performance" | "organization" | "efficiency" | "security"
```

- [ ] Criar `backend/app/core/parsers/sql_quality.py` — **SqlQualityAnalyzer**

**Regras de qualidade (4 dimensões):**

**Performance (35%):**

| Regra | Severidade | Penalidade |
|-------|-----------|------------|
| SELECT * | Alta | -25 |
| SELECT sem WHERE | Alta | -30 |
| LIKE com % inicial | Média | -15 |
| OR no WHERE | Baixa | -8 |
| JOIN 3+ tabelas | Média | -10 |
| Sem NOLOCK | Dica | -5 |
| Subquery no WHERE | Média | -15 |
| DISTINCT | Baixa | -5 |

**Organização (15%):**

| Regra | Severidade | Penalidade |
|-------|-----------|------------|
| Query > 20 linhas | Dica | -10 |
| Sem aliases | Baixa | -10 |
| Campos não qualificados | Baixa | -8 |

**Eficiência (25%):**

| Regra | Severidade | Penalidade |
|-------|-----------|------------|
| SQL por concatenação | Dica | -10 |
| JOIN implícito (vírgula) | Média | -15 |
| ORDER BY sem TOP | Dica | -5 |
| DELETE/UPDATE sem WHERE | Alta | -40 |

**Segurança (25%):**

| Regra | Severidade | Penalidade |
|-------|-----------|------------|
| SQL Injection (MV_PAR, cGet, ReadVar, M->) | Alta | -35 |

**Geração de query sugerida (quando nota < 70%):**
- Substituir `SELECT *` por campos específicos
- Adicionar `WITH(NOLOCK)` em cada tabela
- Incluir `WHERE D_E_L_E_T_ = ' '`
- Adicionar `TOP 1000` quando há ORDER BY sem limite
- Formatar SQL padronizado

- [ ] Adicionar `sql_queries: list[SqlQueryInfo]` e `sql_quality_summary: SqlQualitySummary` ao `AnalysisResult`
- [ ] Integrar no pipeline (pode substituir/complementar o `SqlDetector` existente)

### 9.2 Frontend - QueriesView

- [ ] Criar `frontend/src/components/views/QueriesView.tsx`

**Layout:**
1. **Painel Agregado (topo):**
   - Nota média geral com badge colorido
   - 4 cards com médias por categoria (Performance, Organização, Eficiência, Segurança) com barras de progresso
   - Distribuição de notas (quantas A, B, C, D, F)

2. **Lista de queries agrupadas por arquivo:**
   - Campo de pesquisa global
   - Accordion por arquivo fonte

3. **Para cada query:**
   - Badge de tipo (SELECT verde, INSERT azul, UPDATE amarelo, DELETE vermelho)
   - SQL formatado com syntax highlighting
   - Lista de tabelas com descrição Protheus
   - Variáveis rastreadas (nome, valor, linha)
   - Contexto de execução (TCQuery, TCSqlExec, etc.)
   - Painel de qualidade com 4 barras de score
   - Issues detectados com severidade
   - Query sugerida (quando nota < 70%)
   - Botão "Copiar SQL"

- [ ] Adicionar tipos em `analysis-result.ts`
- [ ] Adicionar no sidebar e traduções

### 9.3 Validação

- [ ] Extrai BeginSql...EndSql com resolução de variáveis %exp:
- [ ] Reconstrói SQL de concatenação de cQuery/cSql
- [ ] Captura SQL inline em TCQuery/TCSqlExec
- [ ] Análise de qualidade calcula scores em 4 dimensões
- [ ] Query sugerida gerada quando nota < 70%
- [ ] View renderiza todas as seções corretamente

---

## 10. Fase 8 - Fluxo de Processo / BPMN

> Tab 5.21 do v2.2: Visão de negócio com diagramas BPMN 2.0 por fonte

### 10.1 Backend - Mapeador de Processos

- [ ] Criar `backend/app/core/parsers/process_flow.py` — **ProcessFlowMapper**

**Mapeamento de módulos ERP por tabela:**
```python
ERP_MODULES = {
    ("SC5", "SC6", "SC9"): {"name": "Pedidos de Venda", "icon": "shopping_cart"},
    ("SC7", "SC8"): {"name": "Pedidos de Compra", "icon": "package"},
    ("SD1", "SF1"): {"name": "Notas Fiscais de Entrada", "icon": "inbox"},
    ("SD2", "SF2"): {"name": "Notas Fiscais de Saída", "icon": "outbox"},
    ("SE1",): {"name": "Contas a Receber", "icon": "dollar_sign"},
    ("SE2",): {"name": "Contas a Pagar", "icon": "credit_card"},
    ("SE5",): {"name": "Movimentos Bancários", "icon": "landmark"},
    ("SA1",): {"name": "Cadastro de Clientes", "icon": "users"},
    ("SA2",): {"name": "Cadastro de Fornecedores", "icon": "factory"},
    ("SB1", "SB2", "SB5"): {"name": "Estoque e Produtos", "icon": "bar_chart_3"},
    ("SD3",): {"name": "Movimentos Internos", "icon": "refresh_cw"},
    ("CTT", "CT2"): {"name": "Contabilidade", "icon": "book_open"},
    ("SC1",): {"name": "Solicitações de Compra", "icon": "file_text"},
    ("SRA", "SRB"): {"name": "Gestão de Pessoas", "icon": "user"},
}
```

**Descrição semântica por arquivo:**
- Gerar descrição baseada em: User Functions, Static Functions, tabelas, pontos de entrada, parâmetros SX6, SQL nativo, tamanho do arquivo, nota TOTVS

**Modelo de dados:**
```python
@dataclass
class ProcessInfo:
    name: str               # Nome do processo ERP
    icon: str               # Ícone (Lucide icon name)
    color: str              # Cor do processo
    description: str        # Descrição do negócio
    tables: list[str]       # Tabelas Protheus envolvidas
    files: list[ProcessFileInfo]

@dataclass
class ProcessFileInfo:
    file_name: str
    lines: int
    user_functions: list[str]
    static_functions: list[str]
    tables: list[str]
    entry_points: list[str]
    parameters: int
    sql_count: int
    totvs_score: float | None
    totvs_grade: str | None
    semantic_description: str  # Descrição gerada
```

- [ ] Adicionar `processes: list[ProcessInfo]` ao `AnalysisResult`
- [ ] Integrar no pipeline (após fase 4 de consolidação)

### 10.2 Backend - Gerador de Diagramas BPMN

- [ ] Criar `backend/app/core/bpmn_generator.py` — **BpmnGenerator**

**Elementos do diagrama BPMN 2.0 (ISO 19510):**

| Elemento | Forma | Cor |
|----------|-------|-----|
| Evento de início | Círculo | Verde |
| Evento de fim | Círculo grosso | Vermelho |
| Tarefa | Retângulo arredondado | Azul |
| Gateway exclusivo (✕) | Losango | Amarelo |
| Gateway condicional (?) | Losango | Azul |
| Entrada/Saída de dados | Paralelogramo | Cinza |
| Subprocesso | Retângulo dupla borda | Azul |
| Erro/Recover | Retângulo | Vermelho |
| Evento intermediário | Círculo dupla borda | Amarelo |

**Fluxo gerado por arquivo:**
1. Início → Coleta Parâmetros (se Pergunte/ParamBox) → User Functions → Pontos de Entrada → Leitura SX6 → Validação → Tabelas → Begin Sequence → RecLock → MsUnlock → Recover → SQL → Static Functions → Fim

- [ ] O diagrama será gerado como dados JSON estruturados para renderização no frontend com ReactFlow

### 10.3 Frontend - ProcessFlowView

- [ ] Criar `frontend/src/components/views/ProcessFlowView.tsx`

**Layout:**
1. **Stats**: Processos identificados, fontes, tabelas
2. **Accordion por processo ERP:**
   - Descrição do processo de negócio
   - Badges de tabelas com descrição
   - Cards por arquivo com: nome, linhas, funções, score, descrição semântica
3. **Diagrama BPMN** renderizado com ReactFlow (reuso da infraestrutura existente do GraphicFlowView)

- [ ] Adicionar tipos, sidebar, traduções

---

## 11. Fase 9 - Governança e Políticas

> Tab 5.29 do v2.2: 9 políticas configuráveis com toggle on/off e peso percentual

### 11.1 Backend - Motor de Governança

- [ ] Criar `backend/app/core/governance/` (novo diretório)
- [ ] Criar `backend/app/core/governance/__init__.py`
- [ ] Criar `backend/app/core/governance/engine.py` — **GovernanceEngine**
- [ ] Criar `backend/app/core/governance/policies.py` — Definição das 9 políticas

**9 Políticas:**

| # | ID | Política | Peso Padrão | Lógica de Avaliação |
|---|-----|----------|-------------|---------------------|
| 1 | `versioning` | Controle de Versão | 15% | Referências a Git, SVN, changelog, versão |
| 2 | `code_review` | Revisão de Código | 15% | Evidências de code review, aprovação em comentários |
| 3 | `audit` | Auditoria e Rastreabilidade | 10% | Autor E data identificados no cabeçalho |
| 4 | `security` | Segurança e Acesso | 15% | Riscos de SQL injection, dados sensíveis expostos |
| 5 | `transaction` | Controle Transacional | 15% | Begin Sequence, RecLock, ErrorBlock |
| 6 | `naming` | Padrão de Nomenclatura | 5% | User Functions com prefixos padronizados |
| 7 | `testing` | Testes e Homologação | 10% | Referências a testes, validação, homologação |
| 8 | `deploy` | Processo de Deploy | 10% | Referências a ambiente, RPO, PRD, HML |
| 9 | `documentation` | Documentação | 5% | Cabeçalho documentado nos primeiros 500 caracteres |

**Modelo de dados:**
```python
@dataclass
class GovernancePolicy:
    id: str
    name: str
    weight: float           # 0.0 - 1.0
    enabled: bool
    description: str

@dataclass
class GovernancePolicyResult:
    policy_id: str
    policy_name: str
    score: float            # 0-100
    max_score: float
    passed: bool
    findings: list[str]     # Detalhes encontrados

@dataclass
class GovernanceResult:
    overall_score: float
    overall_grade: str      # A | B | C | D | F
    min_grade: str          # Nota mínima configurada
    policies_passed: int
    policies_total: int
    policy_results: list[GovernancePolicyResult]
```

- [ ] Adicionar `governance: GovernanceResult | None` ao `AnalysisResult`
- [ ] A governança é calculada sob demanda (não automaticamente), similar ao v2.2 que tem botão "Recalcular"

### 11.2 Backend - API de Governança

- [ ] Criar endpoint `POST /api/v1/analysis/{id}/governance` que recebe configuração de políticas e retorna resultado:
  ```python
  @router.post("/{analysis_id}/governance")
  def calculate_governance(
      analysis_id: int,
      config: GovernanceConfig,  # políticas habilitadas, pesos, nota mínima
      current_user: User = Depends(get_current_user),
      db: Session = Depends(get_db),
  ) -> GovernanceResult:
  ```

### 11.3 Frontend - GovernanceView

- [ ] Criar `frontend/src/components/views/GovernanceView.tsx`

**Layout:**
1. **Painel de Configuração:**
   - Dropdown para nota mínima aceitável (A/B/C/D/F)
   - Toggle on/off para cada política com peso em badge
   - Descrição por política
   - Botão "Recalcular Governança"

2. **Painel de Resultados (após recalcular):**
   - Nota geral com badge colorido e percentual
   - Contagem de conformidade (ex: "7/9 políticas")
   - Para cada política ativa: status ✅/❌, barra de progresso, percentual, findings
   - Conclusão executiva com ações recomendadas

- [ ] Adicionar tipos, sidebar, traduções

---

## 12. Fase 10 - Compliance & BPMN ISO 27001

> Tab 5.31 do v2.2: Relatório integrado de conformidade com ISO 27001 e BPMN

### 12.1 Backend - Analisador de Compliance

- [ ] Criar `backend/app/core/compliance/` (novo diretório)
- [ ] Criar `backend/app/core/compliance/__init__.py`
- [ ] Criar `backend/app/core/compliance/analyzer.py` — **ComplianceAnalyzer**

**8 Recomendações avaliadas:**

| # | Recomendação | Detecção Automática |
|---|-------------|---------------------|
| 1 | Log Estruturado | conLog, FwLogMsg, LogExec |
| 2 | Controle Transacional | Begin Sequence, RecLock, MsUnlock |
| 3 | Tratamento Formal de Exceção | Begin Sequence, TryCatch |
| 4 | ProtheusDoc | @author, @since, @version, @description |
| 5 | Regras de Negócio Documentadas | Verificação manual |
| 6 | GetArea / RestArea | GetArea() com RestArea() correspondente |
| 7 | Testes Unitários | Verificação manual |
| 8 | APIs REST | FwRest, HttpGet, FwCallRest |

**9 Controles ISO 27001:**

| Controle | Auto | Evidência |
|----------|------|-----------|
| A.9.2.1 | ✅ | Cadastro de usuários Protheus |
| A.9.2.3 | ✅ | Controle de acesso por rotina (SIGACFG) |
| A.12.1.2 | 📝 | Processo de gestão de mudanças |
| A.12.1.4 | 📝 | Segregação de ambientes DEV/QAS/PRD |
| A.12.4.1 | ✅ | Detecção de conLog, FwLogMsg |
| A.12.6.1 | ✅ | Contagem de vulnerabilidades |
| A.14.2.1 | ✅ | Nota de qualidade TOTVS |
| A.14.2.3 | 📝 | Processo de revisão de código |
| A.14.2.8 | 📝 | Framework de testes de segurança |

**Modelo de dados:**
```python
@dataclass
class ComplianceRecommendation:
    name: str
    concept: str
    count: int              # Fontes em conformidade
    total: int              # Total de fontes
    percentage: float
    files_affected: list[str]

@dataclass
class IsoControl:
    id: str                 # Ex: "A.9.2.1"
    description: str
    auto_detected: bool
    evidence: str
    status: str             # "compliant" | "non_compliant" | "manual_review"

@dataclass
class ComplianceResult:
    seal: str               # "APROVADO" | "REPROVADO"
    recommendations: list[ComplianceRecommendation]
    iso_controls: list[IsoControl]
    bpmn_diagrams: list[BpmnDiagram]  # Diagramas por arquivo
    overall_metrics: dict
```

- [ ] Adicionar `compliance: ComplianceResult | None` ao `AnalysisResult`

### 12.2 Frontend - ComplianceView

- [ ] Criar `frontend/src/components/views/ComplianceView.tsx`

**Layout:**
1. **Selo header**: APROVADO (verde) ou REPROVADO (vermelho)
2. **Cards de métricas**: Fontes, Linhas, Tabelas, Nota Média
3. **Accordion "Recomendações"**: 8 itens com barras de progresso
4. **Accordion "Declaração de Conformidade"**: Por arquivo com checkmarks
5. **Accordion "BPMN 2.0"**: Diagramas SVG/ReactFlow por arquivo
6. **Accordion "ISO 27001"**: Checklist de controles com indicador auto/manual
7. **Conclusão executiva**: Estatísticas e selo final

- [ ] Adicionar tipos, sidebar, traduções

---

## 13. Fase 11 - Melhorias em Funcionalidades Existentes

### 13.1 Melhoria no IssueDetector

- [ ] Expandir `backend/app/core/parsers/issues.py` com novas regras do v2.2:

| # | Issue Nova | Severidade |
|---|-----------|-----------|
| 1 | SQL Injection (variáveis de entrada em SQL) | Alta |
| 2 | Variáveis não declaradas | Alta |
| 3 | WHILE sem saída clara | Alta |
| 4 | RecLock sem validação | Alta |
| 5 | Private que poderia ser Local | Média |
| 6 | SELECT sem alias | Média |
| 7 | Código comentado (dead code) | Baixa |
| 8 | Sem Begin Sequence em operação crítica | Média |

### 13.2 Melhoria no RelationshipsView

- [ ] Adicionar 5º mapa de relacionamento: **PRW × ExecBlock**
- [ ] Atualizar `frontend/src/components/views/RelationshipsView.tsx`

### 13.3 Melhoria no Scoring TOTVS

- [ ] Adicionar regra de penalidade para variáveis não utilizadas (requer Fase 1)
- [ ] Adicionar regra para complexidade ciclomática elevada

---

## 14. Fase 12 - Exportações Adicionais

### 14.1 Exportação PNG

- [ ] Adicionar botão "Exportar PNG" nos componentes SVG (MentalMapView, GraphicFlowView, diagramas BPMN)
- [ ] Implementar conversão SVG → PNG via Canvas API no frontend
- [ ] Componente reutilizável `ExportPngButton.tsx`

### 14.2 Exportação Tutorial IA

- [ ] Adicionar formato de exportação "Tutorial IA" no backend
- [ ] Criar `export_tutorial_ia()` em `export_service.py`
- [ ] Gerar documento Word otimizado para treinamento de LLM/MCP/RAG:
  - Descrição semântica de cada fonte
  - Contexto ERP
  - Tabelas com descrição
  - Funções com propósito
  - Fluxo de processo
  - Parâmetros, issues e sugestões

### 14.3 Exportação Word Completa

- [ ] Expandir `export_service.py` para incluir as novas seções:
  - Variáveis
  - APIs/WebServices
  - Tabelas Customizadas
  - Dependências User Fn
  - Queries × Fontes com análise de qualidade
  - Governança
  - Compliance & BPMN com imagens

---

## 15. Fase 13 - Testes e Validação

### 15.1 Testes Backend

- [ ] Testes unitários para cada novo parser:
  - `test_variables.py`
  - `test_api_detector.py`
  - `test_custom_tables.py`
  - `test_user_fn_deps.py`
  - `test_migration.py`
  - `test_sql_analyzer.py`
  - `test_sql_quality.py`
  - `test_process_flow.py`
  - `test_governance.py`
  - `test_compliance.py`

### 15.2 Testes Frontend

- [ ] Testes de componente para cada nova view
- [ ] Testes de integração para o fluxo completo

### 15.3 Validação de Paridade

- [ ] Comparar resultados da análise web com a aplicação HTML standalone usando os mesmos fontes de teste
- [ ] Verificar que todos os 34 módulos do v2.2 estão cobertos
- [ ] Verificar exportações incluem novas seções

---

## 16. Resumo de Arquivos

### Novos Arquivos Backend

| Arquivo | Descrição |
|---------|-----------|
| `app/core/parsers/variables.py` | Parser de variáveis |
| `app/core/parsers/api_detector.py` | Detector de APIs/WebServices |
| `app/core/parsers/custom_tables.py` | Detector de campos customizados |
| `app/core/parsers/user_fn_deps.py` | Parser de dependências U_ |
| `app/core/parsers/migration.py` | Detector de migração MsDialog |
| `app/core/parsers/sql_analyzer.py` | Analisador avançado de SQL |
| `app/core/parsers/sql_quality.py` | Análise de qualidade SQL (4 dimensões) |
| `app/core/parsers/process_flow.py` | Mapeador de processos ERP |
| `app/core/bpmn_generator.py` | Gerador de diagramas BPMN |
| `app/core/governance/__init__.py` | Pacote de governança |
| `app/core/governance/engine.py` | Motor de governança |
| `app/core/governance/policies.py` | Definição das 9 políticas |
| `app/core/compliance/__init__.py` | Pacote de compliance |
| `app/core/compliance/analyzer.py` | Analisador de compliance ISO 27001 |
| `tests/test_parsers/test_variables.py` | Testes parser de variáveis |
| `tests/test_parsers/test_api_detector.py` | Testes detector de APIs |
| `tests/test_parsers/test_custom_tables.py` | Testes tabelas customizadas |
| `tests/test_parsers/test_user_fn_deps.py` | Testes dependências U_ |
| `tests/test_parsers/test_migration.py` | Testes migração |
| `tests/test_parsers/test_sql_analyzer.py` | Testes SQL analyzer |
| `tests/test_parsers/test_sql_quality.py` | Testes qualidade SQL |
| `tests/test_parsers/test_process_flow.py` | Testes fluxo de processo |
| `tests/test_governance.py` | Testes governança |
| `tests/test_compliance.py` | Testes compliance |

### Novos Arquivos Frontend

| Arquivo | Descrição |
|---------|-----------|
| `src/components/views/VariablesView.tsx` | View de variáveis |
| `src/components/views/ApiWebServicesView.tsx` | View de APIs/WebServices |
| `src/components/views/CustomTablesView.tsx` | View de tabelas customizadas |
| `src/components/views/UserFnDepsView.tsx` | View de dependências U_ |
| `src/components/views/MigrationView.tsx` | View de migração MsDialog |
| `src/components/views/FunctionMapView.tsx` | View mapa User→Static |
| `src/components/views/QueriesView.tsx` | View de SQL Analytics |
| `src/components/views/ProcessFlowView.tsx` | View de fluxo de processo |
| `src/components/views/GovernanceView.tsx` | View de governança |
| `src/components/views/ComplianceView.tsx` | View de compliance |
| `src/components/export/ExportPngButton.tsx` | Componente exportação PNG |

### Arquivos Modificados

| Arquivo | Modificação |
|---------|-------------|
| `backend/app/core/models.py` | Novos dataclasses e campos no AnalysisResult |
| `backend/app/core/engine.py` | Integrar novos parsers no pipeline |
| `backend/app/core/parsers/__init__.py` | Registrar novos parsers |
| `backend/app/core/parsers/issues.py` | Novas regras de detecção |
| `backend/app/core/scoring/calculator.py` | Novas regras de scoring |
| `backend/app/api/v1/analysis.py` | Endpoint de governança |
| `backend/app/services/export_service.py` | Novas seções + Tutorial IA |
| `frontend/src/types/analysis-result.ts` | Novos tipos TypeScript |
| `frontend/src/components/layout/Sidebar.tsx` | 10 novos itens de menu |
| `frontend/src/pages/AnalysisPage.tsx` | Mapa de 10 novas views |
| `frontend/src/components/views/RelationshipsView.tsx` | 5º mapa PRW×ExecBlock |
| `frontend/src/components/views/IssuesView.tsx` | Novas severidades |
| `public/locales/pt/translation.json` | Traduções das novas views |
| `public/locales/en/translation.json` | Traduções das novas views |
| `public/locales/es/translation.json` | Traduções das novas views |

---

### Ordem Recomendada de Implementação

| Fase | Descrição | Dependências |
|------|-----------|-------------|
| 1 | Parser de Variáveis | Nenhuma |
| 2 | Detector de APIs | Nenhuma |
| 3 | Tabelas Customizadas | Nenhuma |
| 4 | Dependências User Functions | Nenhuma |
| 5 | Migração MsDialog | Nenhuma |
| 6 | Mapa User→Static | Nenhuma |
| 7 | SQL Analytics (Queries × Fontes) | Nenhuma |
| 8 | Fluxo de Processo / BPMN | Fase 7 (usa dados SQL) |
| 9 | Governança e Políticas | Fases 1, 7 (usa dados de variáveis e SQL) |
| 10 | Compliance & BPMN ISO 27001 | Fase 8 (usa BPMN), Fase 9 (usa governança) |
| 11 | Melhorias em existentes | Fase 1 (variáveis para issues) |
| 12 | Exportações adicionais | Todas as fases anteriores |
| 13 | Testes e validação | Todas as fases anteriores |

---

> **Nota**: As fases 1-6 são independentes e podem ser implementadas em paralelo. A fase 7 (SQL Analytics) é a mais complexa e crítica. As fases 8-10 possuem dependências entre si. As fases 11-13 são transversais e devem ser feitas por último.
>
> **Gerado por**: Análise comparativa entre ViliosDoc HTML v2.2 (Manual do Usuário Oficial) e ViliosDoc Web (estado atual)


