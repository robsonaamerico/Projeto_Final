**O objetivo é entender melhor a distribuição dos salários, a relação entre cargos e departamentos e os padrões de remuneração por região.**  
1. Primeira consulta (query_01)  
   1.1 As colunas selecionadas foram traduzidas para facilitar a compreensão.  
   1.2 Criado um LEFT JOIN da tabela HR.DEPARTMENTS pelo DEPARTMENT_ID para buscar os dados referente ao DEPARTMENT.  
   1.3 Criado um LEFT JOIN da tabela HR.JOBS pelo JOB_ID para buscar os dados referentes ao JOB.  
   1.4 Criado um filtro com WHERE para não exibir as linhas com dados nulos da coluna DEPARTMENT_NAME.  
   1.5 A ordenação pelo ORDER BY foi feita para que os departamentos estejam em ordem alfabética e dentro de cada departamento os salários estejam em ordem descendente.  
