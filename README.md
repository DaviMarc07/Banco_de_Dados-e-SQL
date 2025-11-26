# Integração de Python (Pandas) e SQL (SQLite)

1. Visão Geral do Projeto
Este projeto demonstra a capacidade de integrar e manipular dados utilizando dois ecossistemas fundamentais na Ciência de Dados: Python (Pandas) para manipulação de dataframes e SQL (SQLite) para gerenciamento e consulta de bancos de dados relacionais.

O objetivo principal é:

Carregar um dataset (TB_VENDAS_TAREFA.csv) no Pandas.

Transferir o dataframe para um banco de dados SQLite temporário (em memória).

Executar consultas complexas em SQL (como cálculo de média, filtros e agrupamentos) e retornar os resultados para o Pandas.

2. Configuração e Carregamento de Dados
Esta seção prepara o ambiente para a integração entre as duas linguagens.

Importação de Bibliotecas: São importadas as bibliotecas sqlite3 (para interagir com o banco de dados) e pandas (para carregar e manipular os dados).

Carregamento da Base: O arquivo TB_VENDAS_TAREFA.csv é lido pelo Pandas, com o delimitador ajustado para ponto e vírgula (;).

Conexão SQLite em Memória:

conn = sqlite3.connect(':memory:'): Cria uma conexão com um banco de dados SQLite que existe apenas na memória RAM do computador.

Justificativa: Essa abordagem é rápida e ideal para testes e manipulação temporária de dados, pois não requer salvar arquivos no disco.

Transferência para SQL:

df_vendas.to_sql('tb_vendas', conn, ...): Transfere o dataframe df_vendas para o banco de dados SQLite sob o nome de tabela tb_vendas. A opção if_exists='replace' garante que a tabela seja recriada a cada execução.

3. Execução de Consultas SQL e Conversão de Tipos
Uma função auxiliar (run_query) é definida para simplificar a execução de consultas SQL e o retorno dos resultados diretamente para um dataframe Pandas.

Consulta 1 (Verificação): SELECT * FROM tb_vendas

Propósito: Exibe todo o conteúdo da tabela para confirmar que a importação foi bem-sucedida.

Consulta 2 (Exemplo Simples): SELECT PRODUTO FROM tb_vendas LIMIT 10

Propósito: Demonstra uma consulta básica de seleção e limite.

Consulta 3 (Agregação e Transformação - Cálculo de Média):

Objetivo: Calcular a Média do VALOR_UNID agrupada por PRODUTO.

Etapas Cruciais de Limpeza dentro do SQL:

REPLACE(VALOR_UNID, ',', '.'): O SQL é usado para substituir a vírgula (,) por ponto (.) na coluna de valor.

CAST(... AS REAL): O valor é explicitamente convertido para um tipo numérico real (REAL) para que a função de agregação AVG() possa ser aplicada corretamente.

Resultado: O resultado da agregação é retornado como um dataframe Pandas, facilitando análises e visualizações posteriores.

4. Conclusão e Insights sobre Ferramentas
A parte final do notebook lista as conclusões importantes sobre o uso de Python e SQL.

Diferença entre Pandas (Python) e SQL (Banco de Dados):

Pandas/Python: É a linguagem completa usada para modelagem preditiva (Machine Learning), análise estatística avançada, visualização complexa de dados e automação de fluxos de trabalho. É ideal para manipulação de dados em memória.

SQL: É uma linguagem declarativa especializada em gerenciar e consultar dados em bancos. É ideal para consultas rápidas, filtragem e agrupamento de grandes volumes de dados que residem em um servidor.

Relacionais (SQL) vs. Não Relacionais (NoSQL):

SQL (Relacional): Baseia-se em uma estrutura tabular rígida (schema pré-definido), sendo ideal para dados estruturados e transações que exigem alta integridade.

Praticidade do SQL para Consultas: O SQL é mais prático e eficiente para consultas rápidas e transformações simples em grandes datasets que já estão no banco de dados. Por ser uma linguagem declarativa, o motor otimizado do banco executa a consulta de forma mais concisa do que a manipulação equivalente no Pandas/Python.
