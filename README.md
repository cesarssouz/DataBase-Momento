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

* O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento.  

### Funcionários

* Quantos funcionários da empresa Momento possuem conjuges?

* Qual o funcionário contratado há mais tempo na empresa?

* Qual o funcionário contratado há menos tempo na empresa?

* Quem são os funcionários com mais tempo na empresa, considerando a `data_contratacao`?

* Como a média salarial dos funcionários da "Momento" evoluiu nos últimos anos?
Dica: utilize a função `AVG()` para calcular a média salarial dos funcionários. e `GROUP BY` para agrupar os resultados por ano.

### Médias salariais

* Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO, CMO e CFO?

* Qual a média salarial do departamento de tecnologia? 

* Qual o departamento com a maior média salarial?

* Qual o departamento com o menor número de funcionários?

### Produtos

* Pensando na relação quantidade e valor unitario, qual o produto mais valioso da empresa?

* Qual o produto mais vendido da empresa?

* Qual o produto menos vendido da empresa?

### Escritórios

* Quantos escritórios a "Momento" possui em cada região? (Dica: relacione as tabelas regioes e escritorios).

* Qual é o custo total de suprimentos em cada escritório? Que tal ordenar os resultados para ver qual escritório possui os suprimentos mais caros?
