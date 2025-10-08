# Projeto-pratico-Artigo-do-GitHub-sobre-tipos-de-dados-e-regras-na-modelagem-SQL
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Tipos de Dados de String
Utilizados para armazenar texto:

- CHAR(n):	Armazena uma string de tamanho fixo. Se a string inserida for menor que o tamanho n, o restante é preenchido com espaços.
- VARCHAR(n):	Armazena uma string de tamanho variável, até um limite máximo de n caracteres.
- TEXT:	Usado para armazenar strings de texto muito longas.
- NCHAR(n):	Semelhante ao CHAR, mas para armazenar strings de caracteres Unicode de tamanho fixo (suporta uma gama maior de caracteres).
- NVARCHAR(n):	Semelhante ao VARCHAR, mas para armazenar strings de caracteres Unicode de tamanho variável.
- NVARCHAR(MAX):	Usado no SQL Server para armazenar grandes volumes de dados de texto Unicode.

## Tipos de Dados Numéricos
Utilizados para armazenar números, que podem ser exatos ou aproximados.

-Números Exatos
- INTEGER ou INT: Para armazenar números inteiros.
- SMALLINT:	Para armazenar números inteiros pequenos, economizando espaço de armazenamento em comparação com o INT.
- BIGINT:	Para armazenar números inteiros muito grandes.
- TINYINT:	Para armazenar números inteiros muito pequenos, geralmente na faixa de 0 a 255.
- BIT ou BOOLEAN:	Para armazenar valores booleanos, que podem ser TRUE, FALSE ou NULL. Em alguns sistemas, é representado por 1 e 0.
- DECIMAL(p, s) ou NUMERIC(p, s):	Para armazenar números com uma precisão e escala fixas. O p representa o número total de dígitos e o s o número de dígitos após a vírgula decimal. Ideal para valores monetários.
- MONEY e SMALLMONEY:	Tipos de dados específicos para valores monetários, com precisão fixa.

-Números aproximados
- FLOAT(n):	Para armazenar números de ponto flutuante de precisão dupla. Usado para números reais que não exigem exatidão absoluta.
- REAL: Para armazenar números de ponto flutuante de precisão simples.

-Tipos de Dados de Data e Hora
- Utilizados para armazenar informações temporais.

- DATE: Armazena apenas a data (ano, mês e dia).
- TIME: Armazena apenas a hora (hora, minuto e segundo).
- DATETIME:	Armazena tanto a data quanto a hora. A precisão pode variar entre SGBDs.
- SMALLDATETIME: mas com um intervalo de datas menor e menor precisão.
- TIMESTAMP:	Armazena um valor que é atualizado toda vez que uma linha é criada ou modificada. Não representa a data e hora atuais, mas sim uma versão da linha.
- DATETIME2:	Uma extensão do tipo DATETIME com um intervalo de datas maior e maior precisão de segundos.
- DATETIMEOFFSET:	Armazena a data e a hora com informações de fuso horário.

-Outros Tipos de Dados

- XML:	Para armazenar dados no formato XML.
- JSON:	Embora não seja um tipo de dado formal em todos os SGBDs, muitos oferecem funções para armazenar e manipular dados JSON em campos de texto.
- UNIQUEIDENTIFIER:	Para armazenar um Identificador Único Global (GUID).
- GEOMETRY e GEOGRAPHY:	Para armazenar dados espaciais e geográficos (pontos, linhas e polígonos).

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Integridade de Entidade
Faz com que cada linha (registro) em uma tabela seja única e identificável. Essencialmente, proíbe a existência de registros duplicados. É aplicada através da Chave Primária (PRIMARY KEY). Uma chave primária não pode conter valores nulos (NULL) e cada valor na coluna da chave primária deve ser único.

# Integridade Referencial
Garante a consistência e a validade dos relacionamentos entre tabelas. Impede que um registro em uma tabela se refira a um registro inexistente em outra.
Aplicada através da Chave Estrangeira (FOREIGN KEY). O valor na coluna da chave estrangeira deve corresponder a um valor existente na chave primária da tabela referenciada, ou pode ser NULL (se a regra de negócio permitir). Isso evita a criação de "registros órfãos".

# Integridade de Chave
É uma regra mais ampla que assegura que uma coluna (ou um conjunto de colunas) tenha valores únicos.
Aplicada através das restrições PRIMARY KEY e UNIQUE. Impede a inserção de valores duplicados em colunas que, por definição, não podem ter repetição, como um CPF, um e-mail ou o próprio código de identificação de um registro.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# EX: Integridade de Entidade 

Exemplo: Pense em uma lista de Autores. A Integridade de Entidade funciona como um CPF para cada autor.
Nenhum autor pode ser cadastrado sem um número de identificação único chamado de ID do Autor.
É impossível que dois autores diferentes tenham o mesmo "ID do Autor".
Na prática quando o sistema precisa atualizar o nome de "João Silva", ele usa o ID único dele para ter certeza de que está modificando a ficha da pessoa certa, e não a de outro "João Silva" que possa existir. O mesmo vale para os posts: cada post tem um ID único, garantindo que nunca haverá confusão entre eles.

# EX: Integridade Referencial 

Exemplo: Um Post precisa ser escrito por um Autor. A Integridade Referencial age como um gerente que verifica se essa ligação é válida.
Ao criar um novo post, você precisa informar quem é o autor. Essa regra impede que você atribua o post a um "ID de Autor" que não existe na sua lista de autores. O sistema basicamente confere: "Esse autor está na nossa lista de funcionários? Sim? Ok, pode continuar." Se não estiver, a operação é barrada.
Isso garante que não existam "posts órfãos", ou seja, posts que foram escritos por um autor fantasma que não está cadastrado.
E se um autor for demitido (excluído)? A regra também define o que acontece com suas ligações:
A primeira opção é: Se um post for excluído, todos os comentários ligados a ele são automaticamente apagados também. Isso evita que comentários fiquem "flutuando" no sistema sem um post para pertencer.
A segunda opção é: Se um autor for excluído, o sistema pode ser configurado para que os posts dele continuem existindo, mas o campo "autor" fique em branco (nulo). O post não é perdido, apenas a sua autoria.

# EX: Integridade de Chave 

Exemplo: Na lista de Autores, o "ID do Autor" já é único. Mas e o e-mail?
A Integridade de Chave garante que dois autores não possam se cadastrar com o mesmo endereço de e-mail. Mesmo que o ID deles seja diferente, o e-mail precisa ser exclusivo.
O mesmo vale para as Categorias. Essa regra impede que você crie duas categorias com o nome "Tecnologia". Isso mantém os dados limpos e evita redundância.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Fontes
- W3Schools - SQL Tutorial
- Link: https://www.w3schools.com/sql/
- DevMedia
- Link: https://www.devmedia.com.br/guia/sql/37209
- Alura
- Link: https://www.alura.com.br/apostila-sql-e-modelagem-de-dados
- Documentação Oficial dos Bancos de Dados
- PostgreSQL: https://www.postgresql.org/docs/current/datatype.html
- MySQL: https://dev.mysql.com/doc/refman/8.0/en/data-types.html
- SQL Server: https://docs.microsoft.com/pt-br/sql/t-sql/data-types/data-types-transact-sql

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

