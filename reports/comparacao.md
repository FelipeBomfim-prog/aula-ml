# Relatório de Comparação de Modelos (`chamados-r1` vs. `chamados-r2`)

## 1. Alteração Realizada

Na *branch* `correcao-rotulo` (tag `dados-v2`), foi corrigido o rótulo do chamado `006` (`"bloqueio de acesso"`) em `data/chamados.csv`, alterando a classe de `comum` para `urgente`, de acordo com a regra de rotulagem definida em `data/manifesto.json`. A partição de treino e teste (`data/split.csv`) foi mantida inalterada.

## 2. Tabela de Métricas (Partição de Teste Fixa)

| Métrica / Identificador | `chamados-r1` (`dados-v1`) | `chamados-r2` (`dados-v2`) | Diferença |
| :--- | :---: | :---: | :---: |
| **Acurácia** | 0.75 (3/4) | 1.00 (4/4) | **+0.25** |
| **Recall — `urgente`** | 0.50 (1/2) | 1.00 (2/2) | **+0.50** |
| **Recall — `comum`** | 1.00 (2/2) | 1.00 (2/2) | **0.00** |
| **SHA-256 `data/split.csv`** | `2ef82017...6961d981` | `2ef82017...6961d981` | Inalterado |

## 3. Hashes Verificados no Clone Limpo (`modelo-r1`)

Validação realizada após `git switch --detach modelo-r1` e `dvc pull` contra `reports/modelo.json`:

- **Commit SHA (`modelo-r1`):** `a323faccddba7038466351621d9e3620d4ce8474`
- **`data/chamados.csv` (`chamados-v1`):** `bc3fd86a3a5f598841a58839a9726d901fa7e8361ffe79c5b43873ad8a1328ac`
- **`data/split.csv` (partição fixa):** `2ef820171c1a4625fe216e6da67c7c8dcf9d97a08288c0239cd23f1a6961d981`
- **`models/model.json` (`chamados-r1`):** `09d965544c9298c5586af0a1becbf07fb3f3c7b7c228a803ab91179f8b458a09`

*(Em `chamados-r2`, o SHA-256 de `data/chamados.csv` passou para `4ca2e29cb930a9161c2a851b3c71f5529dbb812db607ee4a5ea95d2223baa14d` e o de `models/model.json` para `3bcddff15fe272fe16e092dfb76dab30fa3786cd8c2ce4849ccf5ace002c6ee6`.)*

## 4. Critério e Decisão da Revisão

- **Critério:** Melhorar o *recall* da classe `urgente` sem reduzir o *recall* da classe `comum`, utilizando exatamente a mesma partição de teste.
- **Análise:** Com a correção do ID `006`, o token `"bloqueio"` passou a ser associado à classe `urgente`, corrigindo a classificação do chamado de teste `010` (`"bloqueio de conta"`). O *recall* de `urgente` subiu de **0.50 para 1.00**, o *recall* de `comum` manteve-se em **1.00** e a acurácia subiu de **0.75 para 1.00**.
- **Decisão:** **ACEITAR** o modelo `chamados-r2` para integração na *branch* `main`.
