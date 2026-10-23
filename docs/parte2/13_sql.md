# A Linguagem SQL

Vimos no [Capítulo 10](10_introducao_bd.md) que os SGBDs atuais usam a arquitetura cliente/servidor: são servidores especializados em armazenar e recuperar dados, que atendem a diversos programas clientes, escritos em diferentes linguagens e rodando em diferentes sistemas operacionais. Para permitir essa comunicação, surgiu a **SQL** (*Structured Query Language*, Linguagem de Consulta Estruturada), proposta por pesquisadores da IBM na década de 1970 e adotada pela maioria dos SGBDs relacionais e objeto-relacionais.

Antes de se tornar padrão, a linguagem se chamava **SEQUEL** (*Structured English QUEry Language*) e era a interface de um sistema relacional experimental, o **System R** (ELMASRI; NAVATHE, 2005). Desde então, passou por sucessivas atualizações:

| Ano | Versão | Características |
|:---:|---|---|
| 1974 | SEQUEL | Linguagem original, desenvolvida na IBM |
| 1976 | SEQUEL 2 | Extensão da SEQUEL, adotada no System R |
| 1986 | SQL-86 (SQL1) | Primeiro padrão, publicado pela ANSI e ratificado pela ISO em 1987 |
| 1989 | SQL-89 | Extensão do SQL-86 (integridade referencial) |
| 1992 | SQL-92 (SQL2) | Padrão amplamente adotado pela ANSI e pela ISO |
| 1999 | SQL:1999 (SQL3) | Recursos objeto-relacionais, gatilhos, consultas recursivas |
| 2003 | SQL:2003 | Pequenas atualizações e inclusão do SQL/XML |
| 2006 | SQL:2006 | Integração entre XML e SQL (XQuery) |

Mais recentemente foram publicadas as versões SQL:2008, SQL:2011, SQL:2016 (que incorporou JSON) e SQL:2023.

A SQL costuma ser dividida em três sublinguagens:

- **DDL** (*Data Definition Language*) — definição de dados: criar, alterar e remover tabelas, índices e restrições de integridade. Comandos: `CREATE TABLE`, `ALTER TABLE`, `DROP TABLE`.
- **DML** (*Data Manipulation Language*) — manipulação de dados: consultar, inserir, alterar e remover registros. Comandos: `SELECT`, `INSERT`, `UPDATE`, `DELETE`.
- **DCL** (*Data Control Language*) — controle de acesso: definir quais dados cada usuário pode acessar e de que forma. Comandos: `GRANT`, `REVOKE`.

A SQL costuma ser **transparente** para os usuários de SIG — as interfaces de importação criam tabelas e inserem dados sem que o usuário veja um comando sequer. Mas conhecer alguns comandos básicos dá maior controle sobre a base de dados e permite extrair informações de modo muito mais rápido, às vezes sem abrir um SIG.

!!! tip "Pratique"
    Execute todos os exemplos deste capítulo no banco `curso` criado no [Capítulo 12](12_instalacao.md), pelo *Query Tool* do pgAdmin ou pelo `psql`.

---

## 🏗️ Criando tabelas

Uma **tabela** é uma coleção de registros. Cada **linha** (tupla, registro) descreve um item, e cada **coluna** (campo, atributo) descreve uma característica desse item:

**Tabela `produto`**

| nome | preco | categoria | marca |
|---|---:|---|---|
| Galaxy A9 SM-A910 | 1198 | Celular | Samsung |
| S04 Modo Expresso | 299.99 | Eletrodoméstico | Três Corações |
| Bella Arome II C-09 | 149.99 | Eletrodoméstico | Mondial |
| Smart TV HD Série 4 LED 32 polegadas | 1250 | TV | Samsung |

Todo campo tem um **domínio**: precisa ter um **tipo de dado** definido. Os tipos convencionais mais usados no PostgreSQL são:

| Categoria | Tipos |
|---|---|
| Texto | `char(20)` (tamanho fixo), `varchar(50)` (tamanho variável até o limite), `text` |
| Números inteiros | `smallint`, `integer` (ou `int`), `bigint` |
| Números reais | `real`, `float` (ou `double precision`), `numeric(10,2)` (precisão exata, ideal para valores monetários) |
| Data e hora | `date`, `time`, `timestamp` |
| Lógico | `boolean` |

Uma tabela pode ser descrita textualmente pelo seu nome e pelos seus campos, com a **chave primária** sublinhada — o campo que identifica unicamente cada registro: Produto (<u>nome</u>, preco, categoria, marca).

Ao usar um SIG, a criação de tabelas é normalmente feita de modo implícito pelas interfaces de importação. Ainda assim, é importante conhecer o comando — no [Capítulo 14](14_tipos_espaciais.md) ele destacará os tipos de dados espaciais. A sintaxe básica do `CREATE TABLE` é:

```sql
CREATE TABLE <nome_tabela> (
  <nome_coluna1> <tipo_coluna1>,
  <nome_coluna2> <tipo_coluna2>,
  ...
);
```

A tabela `produto` seria criada assim:

```sql
CREATE TABLE produto (
  nome      varchar(255),
  preco     float,
  categoria varchar(100),
  marca     varchar(100)
);
```

O `CREATE TABLE` apenas prepara o banco para receber os dados, que serão inseridos com o `INSERT`.

---

## ➕ Armazenando dados

A inserção de registros é feita com o comando `INSERT INTO`:

```sql
INSERT INTO nome_tabela (coluna1, coluna2, coluna3, ...)
VALUES (valor1, valor2, valor3, ...);
```

Quando são informados valores para **todas** as colunas, na ordem em que foram criadas, os nomes das colunas podem ser omitidos:

```sql
INSERT INTO produto
VALUES ('Galaxy A9 SM-A910', 1198, 'Celular', 'Samsung');
```

Vários registros podem ser inseridos de uma vez:

```sql
INSERT INTO produto (nome, preco, categoria, marca) VALUES
  ('S04 Modo Expresso', 299.99, 'Eletrodoméstico', 'Três Corações'),
  ('Bella Arome II C-09', 149.99, 'Eletrodoméstico', 'Mondial'),
  ('Smart TV HD Série 4 LED 32 polegadas', 1250, 'TV', 'Samsung');
```

!!! warning "Aspas simples"
    Em SQL, textos e datas são escritos entre **aspas simples** (`'Samsung'`). Aspas duplas são usadas para **nomes** de tabelas e colunas que contenham maiúsculas, espaços ou acentos (`"Nome do Município"`). Evite esses nomes: prefira letras minúsculas, sem acentos, com `_` no lugar de espaços.

---

## 🔍 Recuperando dados

A consulta de dados é feita com o comando `SELECT` — de longe o mais usado. Sua forma básica é:

```sql
SELECT <lista de colunas>
FROM <lista de tabelas>
WHERE <condição>;
```

- **lista de colunas:** os atributos cujos valores devem ser recuperados; `*` recupera todos.
- **lista de tabelas:** as tabelas necessárias para processar a consulta.
- **condição:** uma expressão lógica (booleana), verdadeira ou falsa para cada registro, que identifica os registros a recuperar. É opcional.

Na condição, são comuns os **operadores relacionais**:

| Operador | Significado |
|:---:|---|
| `=` | igual a |
| `<>` | diferente de |
| `>` e `>=` | maior que; maior ou igual a |
| `<` e `<=` | menor que; menor ou igual a |

e os **operadores lógicos**, que combinam os resultados de outras operações:

| Operador | Resultado |
|:---:|---|
| `AND` | verdadeiro apenas quando **ambas** as condições são verdadeiras |
| `OR` | falso apenas quando **ambas** as condições são falsas |
| `NOT` | inverte o valor: verdadeiro vira falso e vice-versa |

O resultado de um `SELECT` pode ser entendido como uma **nova tabela temporária**, que só existe na memória. Por exemplo, todos os produtos da categoria *Eletrodoméstico*:

```sql
SELECT *
FROM produto
WHERE categoria = 'Eletrodoméstico';
```

| nome | preco | categoria | marca |
|---|---:|---|---|
| S04 Modo Expresso | 299.99 | Eletrodoméstico | Três Corações |
| Bella Arome II C-09 | 149.99 | Eletrodoméstico | Mondial |

Podemos recuperar apenas algumas colunas — por exemplo, o nome e a marca dos produtos com preço acima de 1.000:

```sql
SELECT nome, marca
FROM produto
WHERE preco > 1000;
```

| nome | marca |
|---|---|
| Galaxy A9 SM-A910 | Samsung |
| Smart TV HD Série 4 LED 32 polegadas | Samsung |

Combinando condições e ordenando o resultado com `ORDER BY` (`ASC` crescente, o padrão; `DESC` decrescente):

```sql
SELECT nome, preco
FROM produto
WHERE categoria = 'Eletrodoméstico' AND preco < 200;

SELECT nome, preco
FROM produto
ORDER BY preco DESC;
```

!!! note "Maiúsculas e minúsculas"
    As palavras-chave da SQL (`SELECT`, `FROM`...) podem ser escritas em maiúsculas ou minúsculas. Já a comparação de textos **diferencia** maiúsculas de minúsculas: `marca = 'samsung'` não encontra os produtos da `'Samsung'`. Para comparações sem essa distinção, use `ILIKE`: `marca ILIKE 'samsung'`.

---

## 🔗 Relacionando tabelas: chaves e junções

Uma das grandes vantagens dos bancos relacionais é a forma como relacionam duas ou mais tabelas, por meio de **chaves**:

- A **chave primária** (*primary key*) identifica unicamente cada registro de uma tabela — como o CPF de uma pessoa ou o código de um produto.
- A **chave estrangeira** (*foreign key*) é uma referência, em uma tabela, à chave primária de outra tabela.

Por que criar várias tabelas? Para evitar **redundância**. Poderíamos incluir na tabela `produto` o país-sede de cada marca, mas teríamos de repetir essa informação para cada produto cadastrado — com o risco de erros de digitação: em alguns registros *Brasil*, em outros *Brazil*, com **z**. Isso resultaria, no futuro, em consultas imprecisas. É melhor separar as informações da empresa em outra tabela, que poderia guardar também o ano de fundação, o CNPJ etc.:

```sql
CREATE TABLE empresa (
  enome varchar(100) PRIMARY KEY,
  pais  varchar(60)
);

CREATE TABLE produto (
  pnome     varchar(255) PRIMARY KEY,
  preco     numeric(10,2),
  categoria varchar(100),
  marca     varchar(100) REFERENCES empresa (enome)  -- chave estrangeira
);
```

!!! tip "Recriando a tabela"
    Se você criou a tabela `produto` na seção anterior, remova-a antes com `DROP TABLE produto;`.

```sql
INSERT INTO empresa VALUES
  ('Samsung', 'Coreia do Sul'),
  ('Três Corações', 'Brasil'),
  ('Mondial', 'Brasil');

INSERT INTO produto VALUES
  ('Galaxy A9 SM-A910', 1198, 'Celular', 'Samsung'),
  ('S04 Modo Expresso', 299.99, 'Eletrodoméstico', 'Três Corações'),
  ('Bella Arome II C-09', 149.99, 'Eletrodoméstico', 'Mondial'),
  ('Smart TV HD Série 4 LED 32 polegadas', 1250, 'TV', 'Samsung');
```

| pnome | preco | categoria | marca → |
|---|---:|---|---|
| Galaxy A9 SM-A910 | 1198.00 | Celular | Samsung |
| S04 Modo Expresso | 299.99 | Eletrodoméstico | Três Corações |
| Bella Arome II C-09 | 149.99 | Eletrodoméstico | Mondial |
| Smart TV HD Série 4 LED 32 polegadas | 1250.00 | TV | Samsung |

| enome (chave primária) | pais |
|---|---|
| Samsung | Coreia do Sul |
| Três Corações | Brasil |
| Mondial | Brasil |

A chave estrangeira é também uma **restrição de integridade**: o SGBD não aceita um produto de uma marca que não esteja cadastrada.

```sql
INSERT INTO produto VALUES ('Liquidificador X', 99.90, 'Eletrodoméstico', 'Philips');
-- ERROR: insert or update on table "produto" violates foreign key constraint
-- DETAIL: Key (marca)=(Philips) is not present in table "empresa".
```

Com as duas tabelas, podemos responder a perguntas que usam informações de ambas: **quais os produtos de empresas com sede no Brasil?** Uma forma é exigir, na condição, que a chave estrangeira coincida com a chave primária:

```sql
SELECT pnome, preco
FROM produto, empresa
WHERE marca = enome
  AND pais = 'Brasil';
```

A forma recomendada é a cláusula **`JOIN ... ON`**, que separa a condição de junção dos demais filtros:

```sql
SELECT pnome, preco
FROM produto
JOIN empresa ON marca = enome
WHERE pais = 'Brasil';
```

| pnome | preco |
|---|---:|
| S04 Modo Expresso | 299.99 |
| Bella Arome II C-09 | 149.99 |

---

## 📊 Agregações

A SQL oferece funções de **agregação** que resumem vários registros em um valor: `sum` (soma), `count` (contagem), `min`, `max` e `avg` (média). O preço médio dos produtos:

```sql
SELECT avg(preco)
FROM produto;
-- 724.495
```

A quantidade de produtos de uma marca:

```sql
SELECT count(*)
FROM produto
WHERE marca = 'Samsung';
-- 2
```

A soma dos preços dos produtos de empresas brasileiras (149,99 + 299,99):

```sql
SELECT sum(preco)
FROM produto
JOIN empresa ON marca = enome
WHERE pais = 'Brasil';
-- 449.98
```

Com **`GROUP BY`**, a agregação é feita por grupos — uma linha de resultado para cada valor distinto da coluna de agrupamento:

```sql
SELECT categoria,
       count(*) AS quantidade,
       round(avg(preco), 2) AS preco_medio
FROM produto
GROUP BY categoria
ORDER BY quantidade DESC, categoria;
```

| categoria | quantidade | preco_medio |
|---|:---:|---:|
| Eletrodoméstico | 2 | 224.99 |
| Celular | 1 | 1198.00 |
| TV | 1 | 1250.00 |

Essas mesmas funções serão usadas com dados geográficos: somar áreas, contar pontos dentro de polígonos, calcular a extensão de uma malha viária por estado.

---

## ✏️ Alterando e removendo dados

Para completar a DML, os comandos `UPDATE` e `DELETE` alteram e removem registros. **Sempre** use um `WHERE`: sem ele, o comando afeta **todos** os registros da tabela.

```sql
UPDATE produto
SET preco = 1099
WHERE pnome = 'Galaxy A9 SM-A910';

DELETE FROM produto
WHERE categoria = 'TV';
```

---

## 📝 Síntese

| Comando | Sublinguagem | Função |
|---|:---:|---|
| `CREATE TABLE` / `DROP TABLE` | DDL | Criar / remover tabelas |
| `INSERT INTO ... VALUES` | DML | Inserir registros |
| `SELECT ... FROM ... WHERE` | DML | Consultar registros |
| `JOIN ... ON` | DML | Relacionar tabelas |
| `count`, `sum`, `avg`, `min`, `max`, `GROUP BY` | DML | Agregar |
| `UPDATE` / `DELETE` | DML | Alterar / remover registros |
| `GRANT` / `REVOKE` | DCL | Conceder / revogar permissões |

O `SELECT` pode se tornar bem mais complexo; aqui destacamos o suficiente para um usuário de SIG. Para aprofundar, o [SQL Tutorial da W3Schools](https://www.w3schools.com/sql/) permite praticar diretamente no navegador, e a [documentação do PostgreSQL](https://www.postgresql.org/docs/current/tutorial-sql.html) tem um excelente tutorial.

## ✏️ Exercícios

1. Crie a tabela `met(cidade varchar(80), temp_baixa int, temp_alta int, precip real)` e insira três cidades.
2. Escreva uma consulta que retorne as cidades da tabela `met` com temperatura máxima acima de 30 °C, ordenadas da mais quente para a menos quente.
3. Foram criadas as tabelas `aluno(matricula int, nmaluno varchar(80), cdcurso int)` e `curso(cdcurso int, nmcurso varchar(80))`. Escreva a consulta que retorna o nome de cada aluno e o nome do seu curso.
4. Usando as tabelas `produto` e `empresa`, conte quantos produtos há por país.
5. Qual a diferença entre chave primária e chave estrangeira? Que problema a chave estrangeira evita?
