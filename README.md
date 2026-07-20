```markdown
Nome do aluno: Robson de Almeida Américo
Turma: Visualização de Dados e Business Inteligence T2

# 📊 Projeto Final - Análise de Dados de Recursos Humanos (HR)

Este projeto foi desenvolvido com o objetivo de analisar a estrutura interna de uma empresa utilizando dados de Recursos Humanos (HR).
O foco está em compreender a distribuição salarial, a relação de cargos em cada departamento e a distribuição geográfica global dos colaboradores.

---

## 🛠️ Tecnologias e Ferramentas

* **Hospedagem / Servidor:** [FreeSQL](https://freesql.com) *(plataforma online utilizada para hospedar e disponibilizar o banco de dados gratuitamente)*
* **Linguagem:** SQL (Structured Query Language)

---

## 📐 Estrutura do Banco de Dados

As consultas utilizam as seguintes tabelas relacionais do clássico schema de Recursos Humanos:

| Tabela | Descrição |
| :--- | :--- |
| **`HR.EMPLOYEES`** | Contém informações dos funcionários (nome, salário, cargo, departamento). |
| **`HR.DEPARTMENTS`** | Identifica os departamentos da empresa. |
| **`HR.JOBS`** | Armazena a lista de cargos existentes e suas respectivas faixas salariais. |
| **`HR.LOCATIONS`** | Contém os endereços físicos (cidade, estado) dos departamentos. |
| **`HR.COUNTRIES`** | Relaciona as localizações aos seus respectivos países. |
| **`HR.REGIONS`** | Agrupa os países por regiões globais/continentes. |

---

## 📊 Estrutura das Consultas (Queries)

### 1. Salário por Departamento e Cargo
**Objetivo:** Analisar a distribuição de salários por departamento e cargo.

* **Tradução:** As colunas selecionadas foram traduzidas por meio de aliases (`AS`) para facilitar a compreensão.
* **Relacionamentos:** Criados relacionamentos entre as tabelas utilizando `LEFT JOIN`.
* **Filtros:** Aplicado filtro com `WHERE` para desconsiderar registros sem departamento associado.
* **Ordenação:** Configurada via `ORDER BY` para exibir os departamentos em ordem alfabética e, dentro de cada um, os salários em ordem decrescente.

```sql
SELECT
    d.DEPARTMENT_NAME AS Nome_Departamento,
    j.JOB_TITLE AS Cargo,
    e.SALARY AS Salario
FROM HR.EMPLOYEES e
LEFT JOIN HR.DEPARTMENTS d 
    ON e.DEPARTMENT_ID = d.DEPARTMENT_ID
LEFT JOIN HR.JOBS j 
    ON e.JOB_ID = j.JOB_ID
WHERE d.DEPARTMENT_NAME IS NOT NULL
ORDER BY
    d.DEPARTMENT_NAME ASC,
    e.SALARY DESC,
    j.JOB_TITLE ASC;

2. Funcionários por Região (com Localização)
Objetivo: Analisar salários e a distribuição geográfica (Cidade, Estado, País e Continente).

Tradução: As colunas selecionadas foram traduzidas para facilitar a compreensão e exibição em relatórios.

Relacionamentos: Criados relacionamentos encadeados entre as tabelas utilizando LEFT JOIN para subir na hierarquia geográfica.

Filtros: Aplicado filtro com WHERE para desconsiderar linhas com dados nulos na coluna DEPARTMENT_NAME.

Ordenação: Configurada via ORDER BY para que continentes, países, estados e cidades estejam em ordem alfabética. Dentro de cada localidade, os salários são exibidos em ordem decrescente.

SQL
SELECT
    r.REGION_NAME AS Continente,
    c.COUNTRY_NAME AS Pais,
    l.STATE_PROVINCE AS Estado,
    l.CITY AS Cidade,
    d.DEPARTMENT_NAME AS Departamento,
    e.SALARY AS Salario
FROM HR.EMPLOYEES e
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
    e.SALARY DESC;

Análises encontradas:
1. A maior média salárial são do departamento Executive.
2. A menor média salarial pertence ao departemento Shipping.
2. Os departamentos que apresentam os menores desvios de média salarial são: Administration, Human Resources e Public Relations.
3. O departamento Shipping possui mais Outliers de dados salarial.
5. O departamento Executive tem a maior média de salário. Se observarmos a segunda e terceira colocada, temos uma diferença de praticamente o dobro da méida salarial.

Como executar o projeto:
O projeto foi construído em arquivo Jupyter Notebook (.ipynb), usando a plataforma VSCODE com a versão do Pyton 3.14 instalada.

Sugestão de melhorias para as futuras verões:
Utilizar um maior cruzamento de informações para encontrar possíveis correlações e diferenças nos dados utilizando as localidades.
 
