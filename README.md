# Versionamento de Dados e Modelos (`aula-ml`)

Repositório da **Atividade Prática 07** (Engenharia de Sistemas Inteligentes – CK0444 / UFC) dedicado ao versionamento conjunto de dados, partições, código, parâmetros e modelos com **Git** e **DVC**.

## Pré-requisitos

- **Git** 2.x ou superior
- **Python** 3.10 ou superior (utiliza apenas a biblioteca padrão)
- **DVC** 3.x (`pip install dvc` ou `pipx install 'dvc>=3,<4'`)

## Configuração de Acesso ao Armazenamento DVC

Os ficheiros de dados (`data/chamados.csv`, `data/split.csv`) e o modelo treinado (`models/model.json`) são armazenados fora do Git no *remote* local configurado no diretório irmão `../dvc-storage` (definido em `.dvc/config`).

Para confirmar ou ajustar o caminho do armazenamento após clonar:

```bash
dvc remote list
# Se necessário, aponte para o diretório onde os dados foram armazenados:
# dvc remote modify storage url /caminho/para/dvc-storage
```

## Comandos de Restauração

Para recuperar os dados e o modelo exatos de uma versão anterior (`modelo-r1` ou `modelo-r2`) num clone limpo sem executar novo treino:

```bash
git clone [https://github.com/FelipeBomfim-prog/aula-ml.git](https://github.com/FelipeBomfim-prog/aula-ml.git) aula-ml-restauracao
cd aula-ml-restauracao
git switch --detach modelo-r1
dvc pull
```
