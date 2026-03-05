# ViliosDoc Web - Roadmap 

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

| # | Issue Nova                                   | Severidade |
| - | -------------------------------------------- | ---------- |
| 1 | SQL Injection (variáveis de entrada em SQL) | Alta       |
| 2 | Variáveis não declaradas                   | Alta       |
| 3 | WHILE sem saída clara                       | Alta       |
| 4 | RecLock sem validação                      | Alta       |
| 5 | Private que poderia ser Local                | Média     |
| 6 | SELECT sem alias                             | Média     |
| 7 | Código comentado (dead code)                | Baixa      |
| 8 | Sem Begin Sequence em operação crítica    | Média     |

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

### Ordem Recomendada de Implementação

| Fase | Descrição                       | Dependências                               |
| ---- | --------------------------------- | ------------------------------------------- |
| 1    | Parser de Variáveis              | Nenhuma                                     |
| 2    | Detector de APIs                  | Nenhuma                                     |
| 3    | Tabelas Customizadas              | Nenhuma                                     |
| 4    | Dependências User Functions      | Nenhuma                                     |
| 5    | Migração MsDialog               | Nenhuma                                     |
| 6    | Mapa User→Static                 | Nenhuma                                     |
| 7    | SQL Analytics (Queries × Fontes) | Nenhuma                                     |
| 8    | Fluxo de Processo / BPMN          | Fase 7 (usa dados SQL)                      |
| 9    | Governança e Políticas          | Fases 1, 7 (usa dados de variáveis e SQL)  |
| 10   | Compliance & BPMN ISO 27001       | Fase 8 (usa BPMN), Fase 9 (usa governança) |
| 11   | Melhorias em existentes           | Fase 1 (variáveis para issues)             |
| 12   | Exportações adicionais          | Todas as fases anteriores                   |
| 13   | Testes e validação              | Todas as fases anteriores                   |

---

> **Nota**: As fases 1-6 são independentes e podem ser implementadas em paralelo. A fase 7 (SQL Analytics) é a mais complexa e crítica. As fases 8-10 possuem dependências entre si. As fases 11-13 são transversais e devem ser feitas por último.
