# Lista de Exercícios e Trabalho

Este capítulo reúne a lista de exercícios e o trabalho prático da Parte 2. Os exercícios ao final de cada capítulo servem como preparação.

---

## Lista de exercícios

### Conceitos (Capítulos 10 e 11)

1. Conceitue e exemplifique dados, banco de dados e sistema gerenciador de banco de dados.
2. Quais são os conceitos utilizados pelos principais modelos de banco de dados usados atualmente (relacional, objeto-relacional, NoSQL)?
3. Descreva a arquitetura cliente/servidor e explique o papel do QGIS e do PostgreSQL nessa arquitetura.
4. Quais perguntas um usuário de geoprocessamento precisa responder ao modelar um banco de dados geográfico?
5. No OMT-G, qual a diferença entre uma classe convencional e uma classe georreferenciada? Dê um exemplo de cada.

### SQL (Capítulo 13)

6. Foram criadas duas tabelas em um banco de dados com os comandos:

    ```sql
    CREATE TABLE aluno (matricula int, nmaluno varchar(80), cdcurso int);
    CREATE TABLE curso (cdcurso int, nmcurso varchar(80));
    ```

    Qual a consulta SQL que retorna o nome do aluno e o nome do curso?

7. Observe o banco de dados composto pelas relações a seguir, em que atributos sublinhados indicam a chave primária e atributos em itálico indicam as chaves estrangeiras:

    > Usuario (<u>CdUser</u>, Nome, Sexo, *CdGrp*)
    >
    > Post (<u>CodPost</u>, Mensagem, Data, *CdUser*)
    >
    > Grupo (<u>CdGrp</u>, Nome)

    As afirmações a seguir podem ser verdadeiras (V) ou falsas (F):

    - I – um usuário pode estar alocado em mais de um grupo;
    - II – um usuário pode estar associado a mais de um post;
    - III – um grupo pode conter mais de um usuário;
    - IV – o nome de um grupo é único.

    Marque a alternativa correta: (a) V, V, V, V; (b) V, F, V, V; (c) F, V, V, F; (d) F, F, V, V.

8. A tabela `func` e o resultado de uma consulta executada no PostgreSQL são apresentados a seguir. Qual consulta SQL foi executada para obter o resultado?

    **Tabela `func`**

    | mat | nome | cargo | sal |
    |---|---|---|---:|
    | 20161 | Maria | Professor | 1000 |
    | 20164 | Carlos | Médico | 3000 |
    | 20171 | Marcos | Engenheiro | 2200 |
    | 20174 | José | Enfermeiro | 2000 |
    | 20153 | Pedro | Programador | 1000 |
    | 20181 | Lucas | Topógrafo | 1500 |

    **Resultado**

    | nome | cargo | sal |
    |---|---|---:|
    | Carlos | Médico | 3000 |
    | Marcos | Engenheiro | 2200 |
    | José | Enfermeiro | 2000 |

9. Foi criada uma tabela com o comando a seguir. Escreva um comando SQL que insira uma nova linha na tabela `met`.

    ```sql
    CREATE TABLE met (
      cidade     varchar(80),
      temp_baixa int,
      temp_alta  int,
      precip     real
    );
    ```

### Bancos de dados geográficos (Capítulos 14 a 16)

10. Explique as duas formas de integrar bancos de dados geográficos e sistemas de informação geográfica.
11. Considere um banco de dados espacial de uma cidade, com as entidades bairro e lotes:

    ```sql
    CREATE TABLE bairro (codigo integer PRIMARY KEY, bairronm varchar(20), geom geometry(POLYGON, 0));
    CREATE TABLE lotes  (codigo integer PRIMARY KEY, lotenm   varchar(20), geom geometry(POLYGON, 0));
    ```

    Qual a consulta SQL que retorna todos os lotes localizados dentro do bairro Turu?

12. Qual a diferença entre WKT e EWKT? Em que situação o EWKT não pode ser usado?
13. Por que `ST_Distance` entre dois pontos em EPSG:4326 não retorna metros? Mostre duas formas de obter a distância em metros.
14. O que é um índice espacial? Qual comando cria um índice espacial no PostGIS?

??? success "Gabarito de alguns exercícios"
    **6.** `SELECT a.nmaluno, c.nmcurso FROM aluno a JOIN curso c ON a.cdcurso = c.cdcurso;`

    **7.** Alternativa (c): cada usuário tem uma única chave estrangeira `CdGrp` (I é falsa); `Post` referencia `CdUser`, então um usuário pode ter vários posts (II verdadeira); vários usuários podem ter o mesmo `CdGrp` (III verdadeira); nada impede nomes repetidos em `Grupo`, pois a chave é `CdGrp` (IV falsa).

    **8.** `SELECT nome, cargo, sal FROM func WHERE sal >= 2000 ORDER BY sal DESC;` (outras condições, como `sal > 1500`, também produzem o resultado).

    **11.** `SELECT l.* FROM lotes l JOIN bairro b ON ST_Within(l.geom, b.geom) WHERE b.bairronm = 'Turu';`

---

## Trabalho prático da Parte 2

Baixe os arquivos *shapefile* disponíveis em [bit.ly/3b6qN8s](https://bit.ly/3b6qN8s) e descompacte-os em uma pasta. Em seguida:

1. Crie um banco de dados geográfico no PostGIS denominado `brdata`.
2. Importe os arquivos `sede_municipio.shp`, `aeroporto_internacional.shp` e `ferrovia.shp`, em um esquema chamado `brasil`, criando índices espaciais.
3. Escreva e teste uma consulta que retorne os municípios cujas sedes estão em um raio de 100 km do aeroporto de São Luís.
4. Escreva e teste uma consulta que retorne o nome dos municípios cujas sedes estão a pelo menos 100 km de distância de **qualquer** aeroporto internacional.
5. Qual a extensão, em quilômetros, da rede ferroviária no estado do Maranhão? (Dica: importe também o [BR_UF.zip](../dados/BR_UF.zip) e combine `ST_Intersection` e `ST_Length`.)
6. No QGIS, conecte-se ao banco `brdata`, carregue como camadas os resultados das consultas 3 e 4 e produza um mapa com legenda, escala e fonte dos dados.

**Entrega:** um relatório (PDF) com, para cada item, a consulta SQL, uma captura de tela do resultado e uma breve explicação; e o mapa do item 6.

**Critérios de avaliação**

| Critério | Peso |
|---|:---:|
| Criação do banco, importação e índices (itens 1 e 2) | 15% |
| Correção das consultas espaciais (itens 3 a 5) | 50% |
| Uso correto de SRCs e unidades (metros, quilômetros) | 15% |
| Mapa e integração com o QGIS (item 6) | 20% |

!!! tip "Atenção aos sistemas de referência"
    Verifique o SRID de cada camada importada (`SELECT * FROM geometry_columns;`). Se as camadas estiverem em SRCs diferentes, use `ST_Transform`; para medir distâncias em metros, use `geography` ou um SRC projetado.
