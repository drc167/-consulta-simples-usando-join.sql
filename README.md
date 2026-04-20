# -consulta-simples-usando-join.sql
Este documento detalha as consultas SQL utilizadas para buscar informações de funcionários e seus respectivos dependentes, utilizando diferentes tipos de JOIN para filtrar os resultados de acordo com a necessidade do relatório.


 Consulta com INNER JOIN (Apenas quem tem dependentes)Retorna apenas os funcionários que possuem pelo menos um dependente cadastrado. Se o funcionário não tiver dependentes, ele não aparecerá nesta lista.
 
 SELECT 
    funcionarios.id,
    funcionarios.nome AS nome_funcionarios,
    dependentes.nome AS nome_dependentes,
    dependentes.datanascimento
FROM funcionarios
INNER JOIN dependentes ON funcionarios.id = dependentes.idFunc;

2. Consulta com LEFT JOIN (Foco nos Funcionários)Retorna todos os funcionários e seus dependentes. O filtro WHERE DEPENDENTES.NOME IS NOT NULL transforma este Left Join em um comportamento similar ao Inner Join, garantindo que apenas registros com dependentes vinculados sejam exibidos.
  
   SELECT 
    funcionarios.id,
    funcionarios.nome AS nome_funcionarios,
    dependentes.nome AS nome_dependentes,
    dependentes.datanascimento
FROM funcionarios
LEFT JOIN dependentes ON funcionarios.id = dependentes.idFunc
WHERE dependentes.nome IS NOT NULL;

Nota: Se removermos o WHERE, a consulta traria todos os funcionários, inclusive os que não têm dependentes (exibindo NULL nas colunas do dependente).

3. Consulta com RIGHT JOIN (Foco nos Dependentes)Retorna todos os registros da tabela DEPENDENTES, mesmo que, por algum erro de integridade, o ID do funcionário não exista na tabela principal. É útil para auditoria e para garantir que nenhum dependente fique "órfão" no relatório.

   SELECT 
    funcionarios.id,
    funcionarios.nome AS nome_funcionarios,
    dependentes.nome AS nome_dependentes,
    dependentes.datanascimento
FROM funcionarios
RIGHT JOIN dependentes ON funcionarios.id = dependentes.idFunc;

🗄️ Estrutura das Tabelas (Dicionário de Dados)TabelaColunaDescriçãoFUNCIONARIOSidChave Primária (PK) do funcionário.FUNCIONARIOSnomeNome completo do colaborador.DEPENDENTESnomeNome do dependente.DEPENDENTESdatanascimentoData de nascimento do dependente.DEPENDENTESidFuncChave Estrangeira (FK) que liga ao funcionário.

💡 Dicas de UsoPerformance: Certifique-se de que a coluna idFunc na tabela DEPENDENTES possua um índice, pois ela é a chave de ligação entre as tabelas.Aliases: Utilizamos nome_funcionarios e nome_dependentes para evitar confusão, já que ambas as tabelas possuem a coluna nome.

Mantido por: Daniela Coelho
Tecnologia: SQL / Relacionamento de Tabelas.
