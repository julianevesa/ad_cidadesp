# Análise Habitacional por Setor Censitário — São Paulo

Metodologia de identificação de padrões de precariedade habitacional e infraestrutural por setor censitário desenvolvida usando dados do Censo Demográfico 2022 (IBGE) e o algoritmo K-Means.

## Como obter os dados

Os arquivos do IBGE são muito grandes para o GitHub e, por isso, **não estão neste repositório**. Eles devem ser baixados da fonte oficial e colocados na pasta `data/`.

### 1. Baixe os arquivos no site do IBGE

Acesse a aba de downloads do Censo Demográfico 2022 no site do IBGE:

**https://www.ibge.gov.br/estatisticas/sociais/saude/22827-censo-demografico-2022.html?=&t=downloads**

Na lista de pastas, abra:

**Agregados por Setores Censitários → Agregados_por_Setor_[formato]**

Baixe estes **quatro** arquivos (o de alfabetização não é usado):

| Arquivo no IBGE | Conteúdo | Versão usada |
|---|---|---|
| `Agregados_por_setores_basico_BR_20260520.zip` | Tabela Básico (identificação dos setores, municípios e totais) | 20/05/2026 |
| `Agregados_por_setores_caracteristicas_domicilio1_BR_20261021.zip` | Características dos Domicílios 1 | 21/10/2026 |
| `Agregados_por_setores_caracteristicas_domicilio2_BR_20250417.zip` | Características dos Domicílios 2 | 17/04/2025 |
| `Agregados_por_setores_caracteristicas_domicilio3_BR_20250417.zip` | Características dos Domicílios 3 | 17/04/2025 |

> A data no nome do arquivo indica a versão publicada pelo IBGE. Se houver uma versão mais recente, os resultados podem diferir ligeiramente dos apresentados.

### 2. Descompacte e renomeie

Descompacte os quatro arquivos e salve as tabelas na pasta `data/` com estes nomes:

```
data/
├── basico.csv
├── domicilio1.csv
├── domicilio2.csv
└── domicilio3.csv
```

Os notebooks esperam arquivos `.csv` com separador `;` e codificação `latin1` (padrão do IBGE). Se os arquivos baixados estiverem em outro formato ou separador, ajuste os parâmetros `SEP` e `ENCODING` no início do notebook `BD_setores_RMSP.ipynb`.

## Estrutura do projeto

```
ad_cidadesp/
├── data/                          # dados brutos do IBGE (não versionado — ver .gitignore)
│   ├── domicilio1.csv
│   ├── domicilio2.csv
│   ├── domicilio3.csv
│   └── basico.csv
├── filtrar_setores_sp.py          # filtra e consolida os setores de São Paulo capital
├── AN_KMEANS_SP.ipynb             # notebook principal da análise (clustering)
├── .gitignore
└── README.md
```

## Metodologia (resumo)

1. Limpeza numérica (tratamento de sigilo estatístico `'X'` e vírgula decimal)
2. Estatística descritiva e correlação de Pearson nas variáveis originais do Censo
3. Seleção de variáveis de privação habitacional (água, esgoto, moradia, resíduos), com base na fundamentação teórica do SDG 11.1 (ONU)
4. Transformação em taxas percentuais e normalização Min-Max
5. K-Means (Elbow Method + Silhouette Score para escolha do K)
6. Visualizações: dispersão 2D/3D e mapa espacial (via `geobr`)
7. Perfil comparativo dos clusters

## Requisitos

```bash
pip install pandas numpy scikit-learn matplotlib seaborn plotly geobr geopandas
```


