**O objetivo é entender melhor a distribuição dos salários, a relação entre cargos e departamentos e os padrões de remuneração por região.**  
1. Query 1 — Salário por Departamento e Cargo  
   Objetivo: analisar a distribuição de salários por departamento e cargo.
   
   1.1 As colunas selecionadas foram traduzidas para facilitar a compreensão.  
   1.2 Criados relacionamentos entre as tabelas com LEFT JOIN.  
   1.3 Criado um filtro com WHERE para não exibir as linhas com dados nulos da coluna DEPARTMENTO.  
   1.4 A ordenação pelo ORDER BY foi feita para que os DEPARTAMENTOS estejam em ordem alfabética e dentro de cada DEPARTAMENTO os SALÁRIOS estejam em ordem descendente.  

2. Query 2 — Funcionários por Região (com localização)  
   Objetivo: analisar salários e distribuição geográfica (Cidade, Estado ou País).  

   2.1 As colunas selecionadas foram traduzidas para facilitar a compreensão.  
   2.2 Criados relacionamentos entre as tabelas com LEFT JOIN.  
   2.3 Criado um filtro com WHERE para não exibir as linhas com dados nulos da coluna DEPARTAMENTO.  
   2.4 A ordenação pelo ORDER BY foi feita para que os CONTINENTES, PAÍSES, ESTADO e CIDADE estejam em ordem alfabética e dentro de cada DEPARTAMENTO os SALÁRIOS estejam em ordem descendente. 


3. **Seções Iniciais:** Falta uma introdução breve de como rodar o projeto, quais tabelas foram usadas (ou o modelo do banco) e os pré-requisitos (ex: PostgreSQL, DuckDB, MySQL).

---



```markdown
# Projeto Final - Análise de Dados de Recursos Humanos

**O objetivo é entender melhor a distribuição dos salários, a relação entre cargos e departamentos e os padrões de remuneração por região.**

---

## 📊 Estrutura das Consultas (Queries)

### 1. Salário por Departamento e Cargo
**Objetivo:** Analisar a distribuição de salários por departamento e cargo.

* **Tradução:** As colunas selecionadas foram traduzidas para facilitar a compreensão.
* **Relacionamentos:** Criados relacionamentos entre as tabelas utilizando `LEFT JOIN`.
* **Filtros:** Aplicado filtro com `WHERE` para desconsiderar linhas com dados nulos na coluna `DEPARTMENT`.
* **Ordenação:** Configurada via `ORDER BY` para exibir os departamentos em ordem alfabética e, dentro de cada um, os salários em ordem decrescente.

```sql

SELECT
d.DEPARTMENT_NAME AS Nome_Departamento,
j.JOB_TITLE AS Cargo,
e.SALARY AS Salario
FROM
HR.EMPLOYEES e
LEFT JOIN HR.DEPARTMENTS d
ON e.DEPARTMENT_ID = d.DEPARTMENT_ID
LEFT JOIN HR.JOBS j
ON e.JOB_ID = j.JOB_ID
WHERE d.DEPARTMENT_NAME IS NOT NULL
ORDER BY
d.DEPARTMENT_NAME ASC,
e.SALARY DESC,
j.JOB_TITLE

```
---

### 2. Funcionários por Região (com Localização)
**Objetivo:** Analisar salários e a distribuição geográfica (Cidade, Estado ou País).

* **Tradução:** As colunas selecionadas foram traduzidas para facilitar a compreensão.
* **Relacionamentos:** Criados relacionamentos entre as tabelas utilizando `LEFT JOIN`.
* **Filtros:** Aplicado filtro com `WHERE` para desconsiderar linhas com dados nulos na coluna `DEPARTMENT`.
* **Ordenação:** Configurada via `ORDER BY` para que continentes, países, estados e cidades estejam em ordem alfabética. Dentro de cada localidade, os salários são exibidos em ordem decrescente.

```sql

SELECT
r.REGION_NAME AS Continente,
c.COUNTRY_NAME AS País,
l.STATE_PROVINCE AS Estado,
l.CITY AS Cidade,
d.DEPARTMENT_NAME AS Departamento,
e.SALARY AS Salario
FROM
HR.EMPLOYEES e
LEFT JOIN HR.DEPARTMENTS d
ON e.DEPARTMENT_ID = d.DEPARTMENT_ID
LEFT JOIN HR.LOCATIONS l
ON d.LOCATION_ID = l.LOCATION_ID
LEFT JOIN HR.COUNTRIES c
ON l.COUNTRY_ID = c.COUNTRY_ID
LEFT JOIN HR.REGIONS r
ON c.REGION_ID = r.REGION_ID
WHERE d.DEPARTMENT_NAME IS NOT NULL
GROUP BY
r.REGION_NAME,
c.COUNTRY_NAME,
l.STATE_PROVINCE,
l.CITY,
d.DEPARTMENT_NAME,
e.SALARY
ORDER BY
r.REGION_NAME ASC,
c.COUNTRY_NAME ASC,
l.STATE_PROVINCE ASC,
l.CITY ASC,
e.SALARY DESC

```