# Introdução ao Geoprocessamento e Sensoriamento Remoto

Bem-vindo ao material didático da disciplina de **Introdução ao Geoprocessamento e Sensoriamento Remoto**! Este livro serve como guia completo da disciplina, organizada em **duas partes (30 horas totais)**: a primeira trata do sensoriamento remoto e do processamento de dados geográficos na nuvem com o **Google Earth Engine**; a segunda, dos **bancos de dados geográficos** (PostgreSQL/PostGIS) e da sua integração com um sistema de informação geográfica, o **QGIS**.

---

## 📋 Plano da Disciplina

| | |
|---|---|
| **Carga horária total** | 30 horas |
| **Estrutura** | Parte 1 (16h, 8 aulas de 2h) e Parte 2 (14h, 7 aulas de 2h) |
| **Ferramentas** | Google Earth Engine (Code Editor, JavaScript), PostgreSQL + PostGIS, QGIS |
| **Pré-requisitos** | Nenhum conhecimento prévio de programação ou de banco de dados é exigido |

**Ementa:** Representações Computacionais do Espaço Geográfico. Noções básicas de cartografia. Sistema de Informação Geográfica. Modelagem de dados em geoprocessamento. Princípios de Sensoriamento Remoto. Dados de sensoriamento remoto e principais sistemas de sensores. Técnicas de processamento e classificação de imagens de satélite. Exemplos de Aplicação.

Cada parte possui um **plano detalhado** com objetivos de aprendizagem, cronograma aula a aula, metodologia e critérios de avaliação — consulte a primeira página de cada parte no menu.

---

## 💡 Por que este livro usa o Google Earth Engine?

Disciplinas introdutórias de geoprocessamento e sensoriamento remoto costumam depender de laboratórios equipados com SIGs proprietários (ArcGIS) ou abertos (QGIS, SPRING). Mesmo com software livre, as práticas com imagens de satélite exigem computadores com bom poder de processamento, espaço em disco e uma conexão rápida para baixar dezenas de cenas — condições que muitos laboratórios de informática das universidades brasileiras não oferecem.

A proposta deste livro é **mover as perguntas até os dados, e não os dados até as perguntas**. O Google Earth Engine (GORELICK et al., 2017) concentra petabytes de imagens (Landsat, Sentinel, MODIS, SRTM, CHIRPS...) e executa o processamento nos servidores do Google. Basta um navegador: laboratórios com computadores modestos, sem instalação de software especializado, tornam-se suficientes para toda a Parte 1.

A Parte 2 completa o quadro. Ao sair da nuvem e voltar para a própria máquina (ou para o servidor da instituição), o profissional de geoprocessamento precisa saber **onde e como guardar seus dados**. Pastas de *shapefiles* funcionam para um mapa de artigo, mas não para um projeto institucional com vários usuários — e é aí que entram os bancos de dados geográficos.

---

## 🎯 Estrutura do Curso

### 🛰️ Parte 1: Sensoriamento Remoto com Google Earth Engine (16h)

Começamos pelos conceitos que dão sentido a todo o resto — o que é geoinformação, como representamos a Terra num plano, o que um satélite realmente mede — e então os colocamos em prática no Code Editor do Google Earth Engine:

* Geoinformação, cartografia básica (datum, projeções, SRC/EPSG) e sistemas de informação geográfica
* Princípios de sensoriamento remoto: interação da energia com os alvos, assinatura espectral e as quatro resoluções
* JavaScript no GEE: entrada → processamento → saída, cliente × servidor e o padrão *filter–map–reduce*
* Tipos de dados: geometrias, feições e coleções (vetoriais); imagens e coleções de imagens (matriciais)
* Seleção e visualização: filtros espaciais, temporais, por atributo e por metadados; paletas e composições coloridas
* Processamento: *buffer*, sobreposição, centroides e amostragem; álgebra de mapas (operações locais, focais e zonais), NDVI, NDWI e séries temporais

*Avaliação: atividades práticas no GEE (40%) e projeto de análise de uma área de estudo (60%). Veja o [plano completo da parte](parte1/00_plano_parte1.md).*

### 🗄️ Parte 2: Banco de Dados Geográficos e QGIS (14h)

Na segunda parte, adaptada do fascículo *Banco de Dados Geográficos* (COSTA, 2021), estudamos os bancos de dados que sustentam os sistemas de informação geográfica:

* Conceitos de bancos de dados, SGBDs, arquiteturas e modelos (relacional, objeto-relacional, NoSQL)
* Projeto de bancos de dados geográficos: modelos conceitual, lógico e físico; OMT-G e ET-EDGV
* A linguagem SQL: `CREATE TABLE`, `INSERT`, `SELECT`, junções e agregações
* Extensões espaciais: tipos do *Simple Features* (OGC), WKT/EWKT, SRID, PostGIS e GeoPackage
* Operações espaciais (topológicas, métricas e de conjunto) e indexação espacial com GiST
* Integração com o QGIS: conexões, esquemas, importação de camadas e consultas SQL espaciais

*Avaliação: lista de exercícios (30%) e trabalho prático com PostGIS e QGIS (70%). Veja o [plano completo da parte](parte2/00_plano_parte2.md).*

---

## 🧭 Como usar este livro

!!! tip "Pratique enquanto lê"
    Todos os capítulos práticos trazem códigos completos, prontos para copiar. Na Parte 1, crie um *script* novo no Code Editor para cada exemplo e salve-o com um nome que ajude a encontrá-lo depois — esse repositório pessoal de exemplos é, ele mesmo, uma das atividades da disciplina. Na Parte 2, execute cada comando SQL no seu próprio banco.

!!! info "Recursos complementares"
    * **Repositório de *scripts* do minicurso:** [users/sergiocosta/ercemapi2023](https://code.earthengine.google.com/?accept_repo=users/sergiocosta/ercemapi2023) — clique para adicioná-lo ao seu Code Editor.
    * **Vídeos da Parte 1:** [playlist do minicurso de Google Earth Engine](https://www.youtube.com/playlist?list=PLvNBlvS0nGg8j5ywcJbgFF0YDO7y5G2Jn).
    * **Vídeos da Parte 2:** [playlist de Banco de Dados Geográficos](https://youtube.com/playlist?list=PLvNBlvS0nGg_ooGTPdxIYdzKdxBNhKLqO).
    * **Fascículo original da Parte 2:** [Banco de Dados Geográficos (ProEdu/RNP)](https://proedu.rnp.br/handle/123456789/1705).

---

## 📚 Bibliografia e Referências

**Bibliografia básica**

* JENSEN, J. R. *Sensoriamento remoto do ambiente: uma perspectiva em recursos terrestres*. São José dos Campos: Parêntese, 2009.
* LONGLEY, P. A. et al. *Sistemas e ciência da informação geográfica*. 3. ed. Porto Alegre: Bookman, 2013.
* MOREIRA, M. A. *Fundamentos do sensoriamento remoto e metodologias de aplicação*. 4. ed. Viçosa: UFV, 2011.

**Bibliografia complementar**

* CÂMARA, G.; DAVIS, C.; MONTEIRO, A. M. V. *Introdução à Ciência da Geoinformação*. São José dos Campos: INPE, 2001. Disponível em [dpi.inpe.br/gilberto/livro/introd](https://www.dpi.inpe.br/gilberto/livro/introd/).
* CASANOVA, M. A. et al. (Eds.). *Bancos de Dados Geográficos*. Curitiba: MundoGEO, 2005. Disponível em [dpi.inpe.br/livros/bdados](http://www.dpi.inpe.br/livros/bdados/index.html).
* COSTA, S. S. *Banco de Dados Geográficos*. São Luís: IFMA, 2021. Disponível em [proedu.rnp.br](https://proedu.rnp.br/handle/123456789/1705).
* GORELICK, N. et al. Google Earth Engine: Planetary-scale geospatial analysis for everyone. *Remote Sensing of Environment*, v. 202, p. 18–27, 2017.
* CARDILLE, J. A. et al. (Eds.). *Cloud-Based Remote Sensing with Google Earth Engine: Fundamentals and Applications*. Springer, 2024. Disponível em [eefabook.org](https://www.eefabook.org/).

A lista completa está em [Referências](anexos/referencias.md), e um catálogo de portais de dados brasileiros e internacionais está em [Fontes de Dados Geográficos](anexos/fontes_dados.md).

* **Materiais e Tutoriais Complementares**: [LambdaGEO Research Lab](https://lambdageo.github.io).
