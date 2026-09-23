# Parte 2 — Banco de Dados Geográficos e QGIS (14h)

## Identificação

| | |
|---|---|
| **Parte** | 2 de 2 |
| **Carga horária** | 14 horas (7 aulas de 2h) |
| **Pré-requisitos** | Parte 1 (conceitos de dados vetoriais, WKT e SRC) |
| **Ferramentas** | PostgreSQL + PostGIS, pgAdmin 4, QGIS (versão LTR) |

!!! info "Origem do material"
    Esta parte é uma versão revista e atualizada do fascículo *Banco de Dados Geográficos* (COSTA, 2021), produzido para o Instituto Federal do Maranhão e disponível no [ProEdu/RNP](https://proedu.rnp.br/handle/123456789/1705). Os tutoriais de instalação foram reescritos para as versões atuais do PostgreSQL, do PostGIS e do QGIS, e todos os comandos SQL foram testados.

## Objetivos de aprendizagem

Ao final desta parte, o estudante deverá ser capaz de:

1. **Conceituar** dados, bancos de dados e sistemas gerenciadores de banco de dados, reconhecendo suas arquiteturas e seus modelos (relacional, objeto-relacional, NoSQL).
2. **Explicar** as etapas do projeto de um banco de dados geográfico (modelos conceitual, lógico e físico) e interpretar modelos em OMT-G.
3. **Escrever** comandos SQL para criar tabelas, inserir dados e realizar consultas com filtros, junções e agregações.
4. **Instalar e configurar** o PostgreSQL com a extensão PostGIS e o QGIS.
5. **Utilizar** os tipos espaciais do *Simple Features* (OGC), os formatos WKT/EWKT e os códigos SRID, no PostGIS e no GeoPackage.
6. **Realizar** consultas espaciais com operações topológicas, métricas e de conjunto, e criar índices espaciais.
7. **Integrar** um banco de dados geográfico a um SIG: conectar, importar camadas, organizar esquemas e consultar dados a partir do QGIS.

## Cronograma

| Aula | CH | Conteúdo | Capítulo |
|:---:|:---:|---|---|
| 1 | 2h | Dados, bancos de dados e SGBDs; arquiteturas; modelos de banco de dados | [Introdução a Bancos de Dados](10_introducao_bd.md) |
| 2 | 2h | Projeto de bancos de dados geográficos: modelos conceitual, lógico e físico; OMT-G e ET-EDGV | [Projeto de Banco de Dados Geográficos](11_projeto_bdg.md) |
| 3 | 2h | Instalação do PostgreSQL/PostGIS e do QGIS (laboratório) | [Instalando PostgreSQL, PostGIS e QGIS](12_instalacao.md) |
| 4 | 2h | SQL: `CREATE TABLE`, `INSERT`, `SELECT`, chaves, junções e agregações | [A Linguagem SQL](13_sql.md) |
| 5 | 2h | Extensões espaciais: tipos de dados, WKT/EWKT, SRID, GeoPackage | [Tipos de Dados Espaciais](14_tipos_espaciais.md) |
| 6 | 2h | Operações espaciais e indexação espacial | [Operações e Indexação Espacial](15_operacoes_espaciais.md) |
| 7 | 2h | Integração com o QGIS; início do trabalho prático | [Integração com o QGIS](16_integracao_qgis.md) |

## Metodologia

Aulas expositivas dialogadas intercaladas com prática em laboratório. Cada comando SQL do livro deve ser executado pelo estudante no seu próprio banco. A aula 3 (instalação) e a aula 7 são integralmente práticas. Quem não puder instalar o ambiente pode praticar o SQL básico com o *SQL Tutorial* da [W3Schools](https://www.w3schools.com/sql/). Os tutoriais em vídeo da [playlist de Banco de Dados Geográficos](https://youtube.com/playlist?list=PLvNBlvS0nGg_ooGTPdxIYdzKdxBNhKLqO) apoiam quem não conseguir instalar o ambiente durante a aula.

## Avaliação

- **Lista de exercícios (30%)** — questões conceituais e de SQL do [Capítulo 17](17_exercicios.md).
- **Trabalho prático (70%)** — criação de um banco geográfico, importação de camadas e consultas espaciais integradas ao QGIS (ver [enunciado](17_exercicios.md#trabalho-pratico-da-parte-2)).

!!! note "Pesos sugeridos"
    Os pesos acima são uma sugestão e podem ser ajustados a cada oferta da disciplina.

## Bibliografia da parte

- CASANOVA, M. A. et al. (Eds.). *Bancos de Dados Geográficos*. MundoGEO, 2005 — capítulos 1 a 3 e 8.
- ELMASRI, R.; NAVATHE, S. B. *Sistemas de Banco de Dados* — capítulos 1, 2 e 8.
- HEUSER, C. A. *Projeto de Banco de Dados*. 6. ed. Bookman, 2009.
- LONGLEY, P. A. et al. *Sistemas e ciência da informação geográfica* — capítulo sobre bancos de dados geográficos.
- OBE, R.; HSU, L. *PostGIS in Action*. 3. ed. Manning, 2021 (leitura complementar).
