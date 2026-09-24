# codigo-dados-mysql


# Tabelas sabor express
```
use saborexpress;
-- localidade
CREATE TABLE IF NOT EXISTS localidades(
     cep varchar(8) PRIMARY KEY NOT null,
     rua varchar(100),
     bairro varchar(60),
     cidade varchar(60),
     estado varchar(02)
);
 
-- cliente
CREATE TABLE IF NOT EXISTS clientes(
     cpf varchar(11) PRIMARY KEY NOT null,
     nome varchar(100) NOT null,
     email varchar(100),
     cep varchar(8),
     FOREIGN KEY (cep) REFERENCES localidades (cep)
);
 
-- restaurante
CREATE TABLE IF NOT EXISTS restaurantes(
     id_restaurante int AUTO_INCREMENT PRIMARY KEY NOT null,
     nome varchar(100) NOT null,
     telefone varchar(11),
     cep varchar(8),
     FOREIGN KEY (cep) REFERENCES localidades(cep)
);
 
-- entregador
CREATE TABLE IF NOT EXISTS entregadores(
      id_entregador int AUTO_INCREMENT PRIMARY KEY NOT null,
      nome varchar(100) NOT null,
      telefone varchar(11),
      placa_veiculo varchar(10)
);
 
-- pedido
CREATE TABLE IF NOT EXISTS pedidos (
     id_pedido int AUTO_INCREMENT PRIMARY KEY NOT null,
     data_hora datetime NOT null,
     STATUS varchar(20) NOT null,
     cpf_cliente varchar(11),
     id_entregador int,
    FOREIGN KEY (cpf_cliente) REFERENCES clientes(cpf),
    FOREIGN KEY (id_entregador) REFERENCES entregadores(id_entregador)
);
 
-- produto 
CREATE TABLE IF NOT EXISTS produtos (
     id_produto int AUTO_INCREMENT PRIMARY KEY NOT null,
     nome varchar (100) NOT null,
     descricao varchar(255),
     preco decimal(10,2),
     id_restaurante int,
    FOREIGN KEY (id_restaurante) REFERENCES restaurantes(id_restaurante)
);
 
-- itempedido
CREATE TABLE IF NOT EXISTS item_pedidos(
     id_pedido int,
     id_produto int,
     quantidade decimal(10,2),
     preco_unitario decimal(10,2),
     PRIMARY KEY (id_pedido, id_produto),
     FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido),
     FOREIGN KEY (id_produto) REFERENCES produtos(id_produto)
);
 
-- pagamento
CREATE TABLE IF NOT EXISTS pagamentos(
     id_pagamento int AUTO_INCREMENT PRIMARY KEY NOT null,
     tipo varchar(20),
     valor decimal(10,2),
     STATUS varchar(20),
     id_pedido int UNIQUE,
     FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido)
);
 
-- telefone
CREATE TABLE IF NOT EXISTS telefones (
     id_telefone int AUTO_INCREMENT PRIMARY KEY NOT null,
     numero varchar(11) NOT null,
     cpf_cliente varchar(11),
     FOREIGN KEY (cpf_cliente) REFERENCES clientes(cpf)
);
 
 ```


 # Comandos /atividades  DML
 ```
-- Atividade 01

ALTER TABLE telefones MODIFY telefones.cpf_cliente varchar(11) NOT NULL;

-- Atividade 02

ALTER TABLE pedidos MODIFY pedidos.cpf_cliente varchar(11) NOT NULL;

-- Atividade 03
ALTER TABLE pedidos MODIFY pedidos.id_entregador int NULL


-- Atividade 04

ALTER TABLE item_pedidos DROP FOREIGN KEY fk_item_pedido_produtos;

ALTER TABLE item_pedidos ADD CONSTRAINT fk_item_pedido_produto

FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido)

ON DELETE CASCADE


-- Atividade 05

ALTER TABLE pagamentos DROP FOREIGN KEY fk_pagamento_pedido;

ALTER TABLE pagamentos add CONSTRAINT fk_pagamento_pedido

FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido)

ON DELETE CASCADE

-- Atividade 06

-- ALTER TABLE pedidos DROP FOREIGN KEY fk_pedido_entregador;

ALTER TABLE pedidos ADD CONSTRAINT fk_pedido_entregador

FOREIGN KEY (id_entregador) REFERENCES entregadores(id_entregador)

ON DELETE SET NULL


-- Atividade 07

-- ALTER TABLE produto DROP FOREIGN KEY fk_produto_restaurante;

ALTER TABLE produtos ADD CONSTRAINT fk_produtos_restaurante

FOREIGN KEY (id_restaurante) REFERENCES restaurantes(id_restaurante)

ON DELETE RESTRICT


-- Atividade 08

-- ALTER TABLE pedido DROP FOREIGN KEY fk_pedido_cliente;

ALTER TABLE pedidos ADD CONSTRAINT fk_pedidos_cpf_clientes

FOREIGN KEY (cpf_cliente) REFERENCES clientes(cpf)

ON DELETE RESTRICT

-- Atividade 09

 ALTER TABLE item_pedidos DROP FOREIGN KEY fk_item_pedidos_produtos;

-- ALTER TABLE item_pedidos ADD CONSTRAINT fk_item_pedidos_produtos 

-- FOREIGN KEY (id_produto) REFERENCES produtos(id_produto)

-- ON DELETE RESTRICT;

-- Atividade 10

CREATE INDEX `indx.clientes_nome` ON clientes(nome)

CREATE INDEX indx_clientes_nome ON clientes(nome) <-- jeito certo 

-- Atividade 11

CREATE INDEX indx_produtos_nome ON produtos(nome)

-- Atividade 12

CREATE INDEX indx_pedido_data_hora ON pedidos(data_hora)


 ```

 
 ```
É necessario cadastrar um pai sem o pai o filho nao tem como exitir 
INSERT INTO localidades (cep,rua,bairro,cidade,estado)
VALUES("23523542" , "altair stalin" , 'salan russem' ,"Getulio vargas", "ditadura" )


adicionar
INSERT INTO clientes(cpf,nome,email,cep)
VALUES ("12345678901" , "José" , "madd@gmail.com", "23523542")
55432



 ```


