# Introdução ao Geoprocessamento e Sensoriamento Remoto

Livro-disciplina de **Introdução ao Geoprocessamento e Sensoriamento Remoto** (30 h), em
duas partes: sensoriamento remoto e processamento de dados geográficos na nuvem com o
**Google Earth Engine**, e **bancos de dados geográficos** com PostgreSQL/PostGIS integrados
ao **QGIS**.

📖 **Leia online:** <https://lambdageo.github.io/book-geoprocessamento-e-sensoriamento-remoto/>

## Organização

| Parte | Conteúdo | Ferramentas |
| --- | --- | --- |
| 1 — Sensoriamento Remoto com GEE (16 h) | Geoinformação e cartografia, princípios de sensoriamento remoto, tipos de dados, seleção, visualização e processamento de dados vetoriais e matriciais | Google Earth Engine (Code Editor, JavaScript) |
| 2 — Banco de Dados Geográficos e QGIS (14 h) | Bancos de dados e SGBDs, projeto de BDG, SQL, tipos e operações espaciais, indexação, integração com SIG | PostgreSQL + PostGIS, pgAdmin 4, QGIS |

Os anexos reúnem um catálogo de fontes de dados geográficos e as referências bibliográficas.

A Parte 1 deriva do minicurso *Google Earth Engine no Ensino de Introdução ao Sensoriamento
Remoto e ao Geoprocessamento* (ERCEMAPI 2023); a Parte 2, do fascículo *Banco de Dados
Geográficos* (IFMA, 2021). Ambos foram revistos: coleções Landsat migradas para a
*Collection 2*, métodos descontinuados do GEE substituídos, tutoriais de instalação
atualizados e todos os comandos SQL testados em PostgreSQL 16 + PostGIS 3.4.

## Estrutura do repositório

```
docs/                    conteúdo do livro (fonte do site MkDocs)
docs/parte1/             Parte 1 — sensoriamento remoto com Google Earth Engine
docs/parte2/             Parte 2 — banco de dados geográficos e QGIS
docs/anexos/             fontes de dados e referências
docs/dados/              dados didáticos (shapefiles simplificados) usados nos exemplos
.github/workflows/       publicação automática no GitHub Pages
mkdocs.yml               configuração do site
requirements.txt         dependências Python
```

## Build local

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

mkdocs serve                     # servidor local em http://127.0.0.1:8000
mkdocs build --strict            # valida links e navegação
```

`mkdocs build --strict` é o portão de qualidade: qualquer link quebrado ou página fora do
`nav` falha o build. Rode antes de abrir um PR.

## Publicação

O workflow em `.github/workflows/` publica no GitHub Pages a cada push na branch principal.
Não é necessário rodar `mkdocs gh-deploy` manualmente.

## Licença e atribuição

O texto e o código deste livro são de autoria do Prof. Sergio Costa e estão licenciados sob
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.pt-BR). Os dados em
`docs/dados/` são derivados de dados públicos do IBGE, da FUNAI e do MMA. Veja `LICENSE`.
