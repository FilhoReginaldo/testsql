# Título: Desafio Bike Stores Inc

## Descrição
Este projeto tem como objetivo ajudar a Bike Stores Inc a obter informações valiosas sobre seus clientes, produtos e vendas. Usando dados sobre clientes, vendas, estoque e funcionários.

## Tecnologias
 - Banco de dados: Postgres.
 - SQL.

## Instruções de Instalação e Uso (tópico gerado por IA):

Instruções de Instalação e Uso do PostgreSQL no PgAdmin
Para realizar as consultas do projeto utilizando o PostgreSQL no PgAdmin, siga os passos abaixo:

#### 1. Instalação do PostgreSQL e PgAdmin
Baixar e instalar o PostgreSQL:

Acesse o site oficial do PostgreSQL: https://www.postgresql.org/download/
Selecione a versão correspondente ao seu sistema operacional e siga as instruções para instalação.
Durante a instalação, defina uma senha para o superusuário (usuário postgres) e anote-a.
Baixar e instalar o PgAdmin:

O PgAdmin é uma interface gráfica para gerenciar o PostgreSQL. Normalmente, ele é instalado automaticamente junto com o PostgreSQL, mas caso precise de uma instalação separada, baixe o PgAdmin em: https://www.pgadmin.org/download/.
Siga as instruções de instalação para o seu sistema operacional.

#### 2. Conectando-se ao PostgreSQL no PgAdmin
Abrir o PgAdmin:

Após a instalação, abra o PgAdmin.
Na tela inicial, você verá a opção de conectar ao servidor PostgreSQL.
Conectar ao servidor PostgreSQL:

Clique com o botão direito em "Servers" no painel à esquerda e escolha "Create" > "Server".
Na janela "Create - Server", insira as seguintes informações:
Name: Dê um nome para o seu servidor (por exemplo, PostgreSQL).
Connection:
Host name/address: localhost (se o PostgreSQL estiver instalado localmente).
Port: 5432 (porta padrão do PostgreSQL).
Username: postgres (usuário padrão).
Password: A senha que você definiu durante a instalação.
Clique em "Save" para salvar a conexão.
Acessando a base de dados:

Após a conexão, expanda o servidor na barra lateral do PgAdmin.
Encontre a base de dados onde você deseja realizar as consultas. Caso ainda não tenha a base de dados, você pode criar uma nova clicando com o botão direito em "Databases" > "Create" > "Database".
#### 3. Criando e Executando Consultas no PgAdmin
Abrir o Query Tool:

Selecione o banco de dados onde você irá trabalhar.
No painel superior, clique em "Query Tool" para abrir a ferramenta de consultas.
Escrever e Executar as Consultas:

Na janela do Query Tool, escreva as consultas SQL que você deseja executar.
Clique no botão Executar (ícone de raio) ou pressione F5 para executar a consulta.
Visualizar os Resultados:

Após executar uma consulta, os resultados serão exibidos na parte inferior da tela.
Você pode salvar os resultados ou exportá-los em diferentes formatos (CSV, Excel, etc.).
#### 4. Finalizando a Sessão
Após finalizar suas consultas, você pode desconectar o PgAdmin clicando com o botão direito no servidor e selecionando "Disconnect" ou simplesmente fechando o PgAdmin.
Agora você está pronto para realizar as consultas necessárias e trabalhar com o PostgreSQL no PgAdmin! Se precisar de mais ajuda, a documentação oficial do PostgreSQL e PgAdmin oferece informações detalhadas sobre o uso do sistema.

## Selects

- Listar todos Clientes que não tenham realizado uma compra
  ```
  select 
   c.customer_id, 
   c.fisrt_name, 
   c.last_name 
  from
	  Sales.customers c
	   left join Sales.orders o on c.customer_id = o.customer_id
  where o.customer_id IS NULL

- Listar os Produtos que não tenham sido comprados
  ```
  select
	  p.product_id,
	  p.product_name
  from
	  Production.products p
	   left join Sales.order_items oi on p.product_id = oi.product_id
   where oi.product_id IS NULL;
- Listar os Produtos sem Estoque
  ```
  select
	  p.product_id,
	  p.product_name
  from
	  Production.products p
		  inner join Production.stocks s on p.product_id = s.product_id
  where
	 s.quantily = 0
- Agrupar a quantidade de vendas que uma determinada Marca por Loja.
  ```
  select 
	  b.brand_name, 
	  st.store_name, 
	  count(o.order_id) total_sales
  from Production.brands b
	  inner join Production.products p on b.brand_id = p.brand_id
	  inner join Sales.order_items oi on p.product_id = oi.product_id
	  inner join sales.orders o on oi.order_id = o.order_id
	  inner join Sales.stores st on o.store_id = st.store_id
  group by
	  b.brand_name, 
	  st.store_name;
- Listar os Funcionarios que não estejam relacionados a um Pedido.
  ```
  select 
   s.staff_id, 
   s.fisrt_name, 
   s.last_name 
  from
   Sales.staffs s
    left join Sales.orders o on s.staff_id = o.staff_id
  where o.staff_id IS NULL


>  This is a challenge by [Coodesh](https://coodesh.com/)

## Finalização e Instruções para a Apresentação

1. Adicione o link do repositório com a sua solução no teste
2. Verifique se o Readme está bom e faça o commit final em seu repositório;
3. Envie e aguarde as instruções para seguir. Sucesso e boa sorte. =)
