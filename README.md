# Análise Habitacional por Setor Censitário — São Paulo

Metodologia de identificação de padrões de precariedade habitacional e infraestrutural por setor censitário desenvolvida usando dados do Censo Demográfico 2022 (IBGE) e o algoritmo K-Means.

## Dados

Os dados brutos do Censo Demográfico 2022 foram baixados diretamente do IBGE (Agregados por Setores Censitários) e **não estão neste repositório**.

Em vez disso, disponibilizamos apenas a **base já consolidada** — após a seleção dos setores de São Paulo capital e o merge das tabelas de Domicílios (1, 2 e 3) com a tabela Básico. Os arquivos originais do IBGE, por serem muito grandes e de fácil obtenção na fonte oficial, não são redistribuídos aqui.

**Fonte original:** Censo Demográfico 2022 — Agregados por Setores Censitários (IBGE)
🔗 Base consolidada (pós seleção e merge): _[adicionar link do Google Drive aqui]_

Tabelas originais utilizadas na consolidação:
- Características dos Domicílios 1, 2 e 3
- IBGE Básico

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

## Como rodar

1. Baixe a base consolidada (link acima) e salve como `data/setores_censitarios_sp_capital.csv`
2. Abra e rode o notebook `AN_KMEANS_SP.ipynb`, célula por célula, do início ao fim (ou use "Run All" após reiniciar o kernel)

> Caso queira reproduzir a etapa de consolidação a partir dos dados brutos do IBGE, o script `filtrar_setores_sp.py` está disponível neste repositório — mas não é necessário se você já tem a base consolidada.

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

## Status

🚧 Em desenvolvimento.
