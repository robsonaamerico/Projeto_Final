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
