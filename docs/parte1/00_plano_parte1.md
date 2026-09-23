# Parte 1 — Sensoriamento Remoto com Google Earth Engine (16h)

## Identificação

| | |
|---|---|
| **Parte** | 1 de 2 |
| **Carga horária** | 16 horas (8 aulas de 2h) |
| **Pré-requisitos** | Nenhum; uma conta Google e um navegador atualizado |
| **Ferramenta** | Google Earth Engine — Code Editor (API JavaScript) |

## Objetivos de aprendizagem

Ao final desta parte, o estudante deverá ser capaz de:

1. **Explicar** o que caracteriza um dado geográfico e os problemas envolvidos em representar a Terra num plano (geoide, elipsoide, datum, projeções, SRC e códigos EPSG).
2. **Descrever** os princípios físicos do sensoriamento remoto — interação da energia com os alvos, reflectância, assinatura espectral — e as resoluções espacial, espectral, radiométrica e temporal de um sensor.
3. **Diferenciar** as visões de objetos e de campos e suas representações vetorial e matricial, relacionando-as aos tipos `ee.Geometry`, `ee.Feature`, `ee.FeatureCollection`, `ee.Image` e `ee.ImageCollection`.
4. **Escrever** *scripts* no Code Editor seguindo a estrutura entrada → processamento → saída, distinguindo objetos do cliente e do servidor e aplicando o padrão *filter–map–reduce*.
5. **Selecionar e visualizar** dados vetoriais e matriciais com filtros espaciais, temporais, por atributo e por metadados, ajustando parâmetros de visualização e composições coloridas.
6. **Processar** dados vetoriais (*buffer*, intersecção, união, diferença, centroides, amostras) e matriciais (operações locais, focais, zonais e globais; índices espectrais; séries temporais).

## Cronograma

| Aula | CH | Conteúdo | Capítulo |
|:---:|:---:|---|---|
| 1 | 2h | Geoinformação; forma da Terra, datum, projeções, SRC e EPSG; sistemas de informação geográfica | [Geoinformação e Cartografia](01_geoinformacao.md) |
| 2 | 2h | Sensoriamento remoto: definições, histórico, energia e alvos, assinatura espectral e resoluções | [Fundamentos de Sensoriamento Remoto](02_sensoriamento_remoto.md) |
| 3 | 2h | Acesso ao GEE, o Code Editor e JavaScript essencial (variáveis, dicionários, funções, cliente × servidor, *filter–map–reduce*) | [Conhecendo o Google Earth Engine](03_conhecendo_gee.md) |
| 4 | 2h | Objetos e campos; geometrias, feições e coleções; imagens e coleções de imagens | [Tipos de Dados Geográficos](04_tipos_dados.md) |
| 5 | 2h | Acesso, envio (*assets*), visualização e seleção de dados vetoriais | [Seleção e Visualização — Vetores](05_selecao_vetorial.md) |
| 6 | 2h | Visualização (min/máx, paletas, composições coloridas) e seleção de imagens | [Seleção e Visualização — Imagens](06_selecao_matricial.md) |
| 7 | 2h | Processamento vetorial: *buffer*, sobreposição, centroides e amostragem | [Processamento de Dados Vetoriais](07_processamento_vetorial.md) |
| 8 | 2h | Álgebra de mapas, NDVI/NDWI, fator de escala, séries temporais; apresentação dos projetos | [Processamento de Dados Matriciais](08_processamento_matricial.md) |

## Metodologia

Aulas expositivas dialogadas curtas, seguidas de prática imediata no Code Editor. Cada conceito teórico (por exemplo, resolução espacial ou operação focal) é acompanhado de um *script* que o torna visível no mapa. Como o processamento ocorre na nuvem, as aulas podem ser realizadas em qualquer laboratório de informática com acesso à internet. Recomenda-se que o estudante mantenha um repositório pessoal com um *script* para cada exemplo do livro.

## Avaliação

- **Atividades práticas (40%)** — ao longo das aulas 4 a 7, incluindo a atividade de [seleção e visualização](09_exercicios.md#atividade-1-selecao-e-visualizacao) e os exercícios do Capítulo 9.
- **Projeto de análise (60%)** — aula 8: cada estudante (ou dupla) escolhe uma área de estudo e produz, no GEE, uma análise que combine seleção, processamento vetorial e processamento matricial (ver [proposta de projeto](09_exercicios.md#projeto-da-parte-1)).

!!! note "Pesos sugeridos"
    Os pesos acima são uma sugestão e podem ser ajustados a cada oferta da disciplina.

## Bibliografia da parte

- GORELICK, N. et al. Google Earth Engine: Planetary-scale geospatial analysis for everyone. *Remote Sensing of Environment*, 2017.
- CÂMARA, G.; DAVIS, C.; MONTEIRO, A. M. V. *Introdução à Ciência da Geoinformação* — capítulos 1 a 3.
- JENSEN, J. R. *Sensoriamento remoto do ambiente* — capítulos 1 e 2.
- LONGLEY, P. A. et al. *Sistemas e ciência da informação geográfica* — capítulos 1 a 3.
- CARDILLE, J. A. et al. (Eds.). *Cloud-Based Remote Sensing with Google Earth Engine* — Parte F1 (leitura complementar).
