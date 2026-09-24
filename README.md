<h1 align="center">MoveUP — Artificial Intelligence & Chatbot</h1>

<p align="center"><img src="https://img.shields.io/badge/PYTHON-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/><img src="https://img.shields.io/badge/PANDAS-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas"/><img src="https://img.shields.io/badge/NUMPY-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy"/><img src="https://img.shields.io/badge/MATPLOTLIB-11557C?style=for-the-badge&logoColor=white" alt="Matplotlib"/><img src="https://img.shields.io/badge/SEABORN-4C72B0?style=for-the-badge&logoColor=white" alt="Seaborn"/><img src="https://img.shields.io/badge/GOOGLE_COLAB-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=black" alt="Google Colab"/><img src="https://img.shields.io/badge/FIAP-ED145B?style=for-the-badge&logoColor=white" alt="FIAP"/><img src="https://img.shields.io/badge/SPRINT_3-202020?style=for-the-badge&logoColor=white" alt="Sprint 3"/></p>

<p align="center"><strong>Challenge FIAP | Sprint 3 — Construção da base de dados para IA</strong></p>

## Sobre o MoveUP

O **MoveUP** é uma proposta de funcionalidade integrada à plataforma **SoulUp** para converter pontos acumulados pelos usuários em créditos de transporte público. A ideia é aproximar o engajamento digital de benefícios concretos, incentivando a mobilidade urbana sustentável.

Este repositório corresponde à entrega da disciplina **Artificial Intelligence & Chatbot — Sprint 3**: construção, análise e preparação de uma base de dados relacionada ao transporte público e à conversão de tarifas em pontos MoveUP.

> **Escopo desta etapa:** preparação do dataset para uma *futura* solução de inteligência artificial. Esta entrega não apresenta um chatbot funcional nem o treinamento de um modelo de IA.

## Objetivo da entrega

Preparar dados que permitam estudar deslocamentos e perfis de usuários e servir de base para uma futura aplicação capaz de associar tarifas de transporte à quantidade de pontos MoveUP necessária para sua conversão.

A regra de conversão adotada **neste trabalho** é **5.000 pontos = R$ 45,00**. As tarifas são valores de referência usados na elaboração do dataset, não uma consulta de preços em tempo real.

## Fontes dos dados

| Fonte | Utilização no projeto |
|---|---|
| [Pesquisa Origem e Destino 2023 — Metrô de São Paulo](https://www.metro.sp.gov.br/pesquisa-od/) | Dados de deslocamentos, modos de transporte, quantidade de viagens, perfil dos usuários, motivos e horários. |
| [Tabela de tarifas — SPTrans](https://www.sptrans.com.br/tarifas) | Valores de referência para relacionar modalidades de transporte às tarifas e aos pontos MoveUP. |

A base original da Pesquisa Origem e Destino foi mantida sem alterações; os tratamentos são feitos no notebook sobre os dados carregados.

## Etapas realizadas

1. **Carregamento e diagnóstico:** leitura do CSV original; avaliação das colunas, tipos de dados, valores ausentes, duplicidades e valores únicos.
2. **Tratamento:** identificação e remoção de registros sem viagem, sem eliminar automaticamente valores extremos que poderiam representar deslocamentos reais.
3. **Análise exploratória:** estatística descritiva, histogramas, boxplots, gráficos de barras, relações entre variáveis e matriz de correlação.
4. **Engenharia e seleção de atributos:** transformação de códigos da pesquisa em informações compreensíveis, como transporte, frequência de uso, perfil, motivo e período.
5. **Enriquecimento com tarifas:** associação dos modos de transporte a tarifas de referência e cálculo dos pontos correspondentes.
6. **Validação e exportação:** verificação da base preparada e geração de `dataset_moveup.csv`.

## Resumo das bases

| Etapa | Registros | Colunas |
|---|---:|---:|
| Base original da Pesquisa OD 2023 | 143.038 | 147 |
| Após a retirada de 30.125 registros sem viagem | 112.913 | — |
| Base final específica do MoveUP | 24.312 | 10 |

A análise exploratória documentou correlação de **0,74** entre duração e distância dos deslocamentos. Esse resultado descreve uma associação observada na base analisada; não demonstra causalidade.

## Estrutura do dataset final

| Coluna | Descrição |
|---|---|
| `tipo_transporte` | Principal modo considerado no projeto: Metrô, Trem ou Ônibus municipal. |
| `quantidade_viagens` | Quantidade de viagens associada ao registro. |
| `frequencia_uso` | Aproximação da frequência **diária**: baixa, média ou alta, com base na quantidade de viagens. |
| `perfil_usuario` | Categoria derivada de idade e renda familiar. |
| `motivo_viagem` | Motivo do deslocamento em categoria legível. |
| `periodo` | Madrugada, manhã, tarde ou noite, conforme o horário de saída. |
| `categoria_tarifa` | Categoria utilizada para relacionar o transporte à tarifa. |
| `tarifa_referencia` | Valor de referência em reais. |
| `ano_referencia` | Ano associado à tarifa utilizada. |
| `pontos_necessarios` | Pontos correspondentes à tarifa, segundo a regra do projeto. |

### Exemplo da conversão adotada

```text
5.000 pontos = R$ 45,00
Ônibus municipal: R$ 5,30 → 589 pontos
Metrô:           R$ 5,40 → 600 pontos
Trem:            R$ 5,40 → 600 pontos
```

O campo `pontos_necessarios` foi definido na documentação como **rótulo proposto para uma futura aplicação supervisionada**. Nesta sprint, os valores são calculados pela regra de conversão; não são previsões de um modelo treinado.

## Tecnologias utilizadas

| Tecnologia | Finalidade |
|---|---|
| Python | Tratamento, transformação e validação dos dados. |
| Pandas e NumPy | Manipulação de tabelas, cálculos e valores ausentes. |
| Matplotlib e Seaborn | Gráficos e análise exploratória. |
| Google Colab / Jupyter Notebook | Desenvolvimento e execução do notebook. |
| CSV | Entrada e exportação das bases de dados. |

## Arquivos da entrega

Os arquivos analisados para esta documentação foram:

| Arquivo | Conteúdo |
|---|---|
| `MoveUP_Challenge.ipynb` | Notebook com a análise exploratória, tratamento, preparação e exportação dos dados. |
| `Banco2023_OD2023_original.csv` | Base original utilizada no estudo. |
| `dataset_moveup.csv` | Base final preparada para o MoveUP. |

## Como reproduzir a análise

1. Abra `MoveUP_Challenge.ipynb` no **Google Colab**.
2. Ao executar a célula de upload (`files.upload()`), envie o arquivo `Banco2023_OD2023_original.csv`.
3. Execute as células do notebook na ordem apresentada, incluindo as etapas de tratamento e integração tarifária.
4. Ao final, o notebook exporta o arquivo **`dataset_moveup.csv`**.

Para executar em outro ambiente Jupyter, adapte a etapa de upload do Google Colab e instale as dependências utilizadas no notebook: `pandas`, `numpy`, `matplotlib` e `seaborn`.

## Integrantes

- André Luiz Ramos Forastieri — RM572203
- Eduardo Damasio Guelere — RM569960
- Isabelle Ferreira Neri Feitoza — RM573507
- Marina Fernandes Gomes Mesquita — RM571265
- Milena Silva Conegin — RM568923

---

**FIAP — Challenge MoveUP | Artificial Intelligence & Chatbot — Sprint 3**
