# DataBase-Momento

Você está prestes a explorar o banco de dados da empresa "Momento"! Com essa base de dados, vamos treinar consultas SQL e responder algumas perguntas intrigantes que vão revelar como a empresa está organizada. Vamos lá?

### Departamento de Tecnologia 

* Inclua suas próprias informações no departamento de Tecnologia da empresa.
```sql
INSERT INTO funcionarios(funcionario_id, primeiro_nome, sobrenome, email, senha, telefone, data_contratacao, cargo_id, salario, gerente_id, departamento_id) VALUES (307, 'César', 'Oliveira', 'cesarsouz10@gmai.com', 'cesar123', '11 998745989', 2024-25-11, 14, 100.000, NULL, 6 );
```

* Agora diga, quantos funcionários temos ao total na empresa?
 
R - 42
```sql
SELECT COUNT(*) FROM momento.funcionarios;
```

* E quanto ao Departamento de Tecnologia? 

R - 5
```sql
SELECT COUNT(*) FROM momento.funcionarios WHERE departamento_id = 6;
```

### Departamento de Vendas 

* **Quantos funcionários trabalham no Departamento de Vendas?**
 
  R - 5
 ```sql
SELECT COUNT(*) FROM momento.funcionarios WHERE departamento_id = 8;
```

* **Salários no Departamento de Vendas**
 
 R - R$ 51.500,00
```sql
SELECT SUM(salario) FROM momento.funcionarios WHERE departamento_id = 8;
```

* Quanto o departamento de Vendas gasta em salários?

  R - R$ 51.500,00
```sql
SELECT SUM(salario) FROM momento.funcionarios WHERE departamento_id = 8;
```

* Quais são os produtos mais vendidos e quais têm pouca ou nenhuma saída?

* Qual é o produto mais caro no inventário da empresa?

  R - Sabre de luz (mace windu)
```sql
SELECT * FROM momento.produtos ORDER BY produto_price DESC;
```

### Departamento de Inovações 

* **Um novo departamento foi criado. O departamento de Inovações.** 
Ele será locado no Brasil. Por favor, adicione-o no banco de dados da empresa colocando quaisquer informações que você achar relevantes.
```sql
NSERT INTO escritorios(escritorio_id,escritorio_nome,endereco,cep,cidade,estado_provincia,pais_id) VALUES (2990,"Estúdio de Inovação",'Itaim Paulista','081328567','São Paulo','São Paulo','BR');
INSERT INTO departamentos(departamento_id,departamento_nome,escritorio_id) VALUES (22,'Inovação',2990);
```

* O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento.
```sql
INSERT INTO funcionarios(funcionario_id,primeiro_nome,sobrenome,email,senha,telefone,data_contratacao,cargo_id,salario,gerente_id,departamento_id) VALUES (270,'Rogerio','Gonzaga','rogeringamer@gmail.com','rog3ri0#','11 998764524','2024-11-30',20,3.000,NULL,22);
INSERT INTO funcionarios(funcionario_id,primeiro_nome,sobrenome,email,senha,telefone,data_contratacao,cargo_id,salario,gerente_id,departamento_id) VALUES (271,'Roberto','William','roobertson9gmail.com','roBert$0n','11 998061554','2024-11-30',20,3.000,NULL,22);
INSERT INTO funcionarios(funcionario_id,primeiro_nome,sobrenome,email,senha,telefone,data_contratacao,cargo_id,salario,gerente_id,departamento_id) VALUES (272,'Jefferson','Mendez','jeffer$on9@gmail.com','Jef78#','11 997064554','2024-11-30',20,3.000,NULL,22);
```

### Funcionários

* Quantos funcionários da empresa Momento possuem conjuges?
 
  R - 37
```sql
SELECT COUNT(*) FROM momento.funcionarios
INNER JOIN dependentes ON funcionarios.funcionario_id = dependentes.funcionario_id
```

* Qual o funcionário contratado há mais tempo na empresa?

  R - Steven Wayne
```sql
SELECT CONCAT(primeiro_nome, " ", sobrenome) AS nome_funcionario, data_contratacao FROM momento.funcionarios ORDER BY data_contratacao;
```

* Qual o funcionário contratado há menos tempo na empresa?

  R - Roberto William
```sql
SELECT CONCAT(primeiro_nome, " ", sobrenome) AS nome_funcionario, data_contratacao FROM momento.funcionarios ORDER BY data_contratacao DESC;
```

* Quem são os funcionários com mais tempo na empresa, considerando a `data_contratacao`?

  R - Steven Wayne, Jeniffer Whalen
 ```sql
SELECT CONCAT(primeiro_nome, " ", sobrenome) AS nome_funcionario, data_contratacao FROM momento.funcionarios ORDER BY data_contratacao;
  ``` 

* Como a média salarial dos funcionários da "Momento" evoluiu nos últimos anos?
Dica: utilize a função `AVG()` para calcular a média salarial dos funcionários. e `GROUP BY` para agrupar os resultados por ano.

R - De forma inconsistente e variavel.
```sql
SELECT AVG(salario) AS Media_Salarial, YEAR(data_contratacao) AS Ano FROM funcionarios GROUP BY data_contratacao ORDER BY YEAR(data_contratacao);
```

### Médias salariais

* Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO, CMO e CFO?

 R - R$ 7825.341463
 ```sql
SELECT AVG(salario) AS Media_Salarial FROM funcionarios WHERE cargo_id NOT IN (4,7,10);
 ```

* Qual a média salarial do departamento de tecnologia?

   R - R$ 5760.000000
 ```sql
SELECT AVG(salario) AS Media_Salarial FROM funcionarios WHERE departamento_id = 6;
```

* Qual o departamento com a maior média salarial?

  R - O departamentos de tecnologias 
```sql
SELECT funcionarios.departamento_id, departamentos.departamento_nome, AVG(salario) AS Media_Salarial FROM funcionarios
INNER JOIN departamentos ON departamentos.departamento_id = funcionarios.departamento_id
GROUP BY departamento_id 
ORDER BY Media_Salarial DESC;
```

* Qual o departamento com o menor número de funcionários?

  R - Os departamentos de administração, Recursos humanos, Relações Publicas, Contabilidade e Biotecnologia.
```sql
SELECT funcionarios.departamento_id, departamentos.departamento_nome, COUNT(*) FROM momento.funcionarios 
INNER JOIN departamentos ON departamentos.departamento_id = funcionarios.departamento_id
GROUP BY departamento_id
ORDER BY COUNT(*);
```

### Produtos

* Pensando na relação quantidade e valor unitario, qual o produto mais valioso da empresa?

  R - Uniforme do Superman
 ```sql
SELECT produto_nome, produto_price, quantidade FROM momento.vendas
INNER JOIN produtos ON produtos.produto_id = vendas.produto_id
ORDER BY quantidade DESC;
```

* Qual o produto mais vendido da empresa?

  R - Uniforme do Superman
```sql
SELECT produto_nome, quantidade FROM momento.vendas
INNER JOIN produtos ON produtos.produto_id = vendas.produto_id
ORDER BY quantidade DESC;
```

* Qual o produto menos vendido da empresa?

  R - Batarangues
```sql
SELECT produto_nome, quantidade FROM momento.vendas
INNER JOIN produtos ON produtos.produto_id = vendas.produto_id
ORDER BY quantidade;
```

### Escritórios

* Quantos escritórios a "Momento" possui em cada região? (Dica: relacione as tabelas regioes e escritorios).

  R - 3 escritórios no Reino Unido, 3 nos EUA, 1 no Brasil, Canadá Alemanha e Wakanda.
 ```sql
SELECT paises.pais_nome, escritorios.pais_id, COUNT(*) FROM momento.escritorios
INNER JOIN paises ON paises.pais_id = escritorios.pais_id
GROUP BY pais_id
ORDER BY COUNT(*) DESC;
```

* Qual é o custo total de suprimentos em cada escritório? Que tal ordenar os resultados para ver qual escritório possui os suprimentos mais caros?

  R - Umbrella Corp: R$405.000,00 -
Baxter Building: R$403.752,85 -
Wayne escritorios: R$148.000,00 -
Shuri's Palace: R$5.505,70 -
Sala Winter: R$5.050,07 -
House of Mystery escritorios: R$4.000,00 - 
Arkham Base: R$2.000,00
```sql
SELECT escritorios.escritorio_nome, SUM(custo) FROM momento.suprimentos
INNER JOIN escritorios ON escritorios.escritorio_id = suprimentos.escritorio_id
GROUP BY escritorio_nome
ORDER BY SUM(custo) DESC;
```

