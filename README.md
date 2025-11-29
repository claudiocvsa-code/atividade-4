# atividade-4
atividade 4
1. Criação das tabelas (modelo lógico simples)
```sqlCREATE TABLE Autor (    id_autor INT PRIMARY KEY,    nome VARCHAR(100),    email VARCHAR(100) UNIQUE);
CREATE TABLE Livro (    id_livro INT PRIMARY KEY,    titulo VARCHAR(150),    preco DECIMAL(10,2),    id_autor INT,    FOREIGN KEY (id_autor) REFERENCES Autor(id_autor));
CREATE TABLE Usuario (    id_usuario INT PRIMARY KEY,    nome VARCHAR(100),    email VARCHAR(100) UNIQUE);
CREATE TABLE Venda (    id_venda INT PRIMARY KEY,    id_usuario INT,    id_livro INT,    valor_total DECIMAL(10,2),    data_venda DATE,    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario),    FOREIGN KEY (id_livro) REFERENCES Livro(id_livro));```
---
2. Comandos INSERT para popular as tabelas
```sqlINSERT INTO Autor VALUES (1, 'João Silva', 'joao@email.com');INSERT INTO Autor VALUES (2, 'Maria Souza', 'maria@email.com');
INSERT INTO Livro VALUES (1, 'Banco de Dados 101', 59.90, 1);INSERT INTO Livro VALUES (2, 'SQL Avançado', 79.90, 2);
INSERT INTO Usuario VALUES (1, 'Carlos Pereira', 'carlos@email.com');INSERT INTO Usuario VALUES (2, 'Ana Lima', 'ana@email.com');[29/11, 00:49] ChatGPT: INSERT INTO Venda VALUES (1, 1, 2, 79.90, '2025-11-29');INSERT INTO Venda VALUES (2, 2, 1, 59.90, '2025-11-28');```
---
3. Consultas (SELECT) com cláusulas variadas
```sql-- Consulta 1: Todos os livros com preço maior que 60SELECT * FROM Livro WHERE preco > 60;
-- Consulta 2: Vendas ordenadas por data (mais recente primeiro)SELECT * FROM Venda ORDER BY data_venda DESC;
-- Consulta 3: Top 1 livro mais caroSELECT * FROM Livro ORDER BY preco DESC LIMIT 1;
-- Consulta 4: Vendas do usuário 'Carlos Pereira' (join entre tabelas)SELECT v.id_venda, u.nome, l.titulo, v.valor_totalFROM Venda vJOIN Usuario u ON v.id_usuario = u.id_usuarioJOIN Livro l ON v.id_livro = l.id_livroWHERE u.nome = 'Carlos Pereira';
-- Consulta 5: Total vendido por cada autorSELECT a.nome, SUM(v.valor_total) as total_vendidoFROM Autor aJOIN Livro l ON a.id_autor = l.id_autorJOIN Venda v ON l.id_livro = v.id_livroGROUP BY a.nome;```
---
4. Atualizações (UPDATE) com condições
```sql-- Atualizar o preço do livro 'SQL Avançado' para 89.90UPDATE Livro SET preco = 89.90 WHERE titulo = 'SQL Avançado';
-- Atualizar o email do usuário 'Ana Lima'UPDATE Usuario SET email = 'ana.lima@email.com' WHERE nome = 'Ana Lima';
-- Atualizar o valor total de uma venda específica UPDATE Venda SET valor_total = 85.00 WHERE id_venda = 1;```
---
5. Deleções (DELETE) com condições
```sql-- Deletar autor com id 2 (apagar Maria Souza)DELETE FROM Autor WHERE id_autor = 2;
-- Deletar vendas anteriores a 2025-11-29DELETE FROM Venda WHERE data_venda < '2025-11-29';
-- Deletar livros com preço menor que 60DELETE FROM Livro WHERE preco < 60;```
---
6. README.md exemplo
