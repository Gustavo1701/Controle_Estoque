# **Controle de Inventário Simples**

### 1. **Objetivo do Sistema**
O objetivo do sistema é permitir o controle de produtos em um estoque, com funcionalidades para adicionar, editar, excluir, listar e controlar a quantidade de cada produto. Pode ser útil para pequenos comércios ou empresas que precisam monitorar o estoque de itens.

### 2. **Requisitos Funcionais**

Esses são os requisitos que o sistema deve cumprir:

1. **Cadastro de Produtos**:
   - Nome do produto.
   - Descrição do produto.
   - Preço de venda.
   - Quantidade disponível em estoque.
   - Categoria do produto (opcional, caso você queira organizar os itens).
   - Data de cadastro (opcional, mas útil para controlar quando o item foi registrado).

2. **Edição de Produtos**:
   - O sistema deve permitir a atualização dos dados do produto: nome, descrição, preço e quantidade.

3. **Remoção de Produtos**:
   - O sistema deve permitir a exclusão de produtos do estoque.

4. **Controle de Quantidade (Entrada/Saída de Estoque)**:
   - O sistema deve permitir o aumento ou diminuição da quantidade de um produto no estoque (entrada e saída).
   - Registro de cada operação de entrada ou saída (data, quantidade, tipo de operação).
   
5. **Listagem de Produtos**:
   - O sistema deve exibir uma lista de produtos, com nome, preço, quantidade em estoque e outros detalhes relevantes.
   - A lista pode ter filtros de busca, como nome do produto e categoria.
   - O sistema também deve permitir a ordenação por nome, preço e quantidade.

6. **Relatórios (opcional)**:
   - Relatório de produtos com baixa quantidade em estoque (quantidade abaixo de um valor definido).
   - Relatório de entrada e saída de produtos por período.
   
### 3. **Requisitos Não Funcionais**

Esses requisitos definem as características gerais do sistema:

1. **Autenticação** (opcional):
   - Pode ser necessário um login para garantir que apenas usuários autorizados gerenciem o estoque.
   - A autenticação pode ser feita com um sistema simples de login (e.g., usando JWT).

2. **Armazenamento de Dados**:
   - Banco de dados MySQL para armazenar informações dos produtos.
   - A tabela principal será para os **produtos**, e você pode ter tabelas auxiliares para registros de **entradas e saídas de estoque**.

3. **Interface do Usuário**:
   - A interface deve ser simples e intuitiva, com uma dashboard de controle de estoque.
   - A navegação deve ser clara, com formulários para adicionar/editar/excluir produtos e para registrar entradas e saídas.

4. **Responsividade**:
   - O sistema deve ser responsivo para funcionar bem em dispositivos móveis e desktop, utilizando **Tailwind CSS** para o estilo.

### 4. **Modelo de Banco de Dados**

Podemos começar com as seguintes tabelas:

#### Tabela `produtos`
```sql
CREATE TABLE produtos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(255) NOT NULL,
  descricao TEXT,
  preco DECIMAL(10, 2) NOT NULL,
  quantidade INT NOT NULL DEFAULT 0,
  categoria VARCHAR(100),
  data_cadastro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Tabela `entradas_saida_estoque`
```sql
CREATE TABLE entradas_saida_estoque (
  id INT AUTO_INCREMENT PRIMARY KEY,
  produto_id INT,
  quantidade INT NOT NULL,
  tipo_operacao ENUM('entrada', 'saida') NOT NULL, -- Entrada ou saída
  data_operacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (produto_id) REFERENCES produtos(id)
);
```

### 5. **Fluxo Básico do Sistema**

1. **Cadastro de Produto**:
   - O usuário preenche o formulário com nome, descrição, preço, quantidade e categoria do produto.
   - O produto é registrado no banco de dados.

2. **Entrada/Saída de Estoque**:
   - O usuário registra uma operação de entrada ou saída de estoque, informando a quantidade.
   - O sistema atualiza a quantidade disponível no banco de dados e armazena a operação na tabela `entradas_saida_estoque`.

3. **Listagem de Produtos**:
   - O sistema exibe todos os produtos cadastrados com suas informações principais.
   - O usuário pode buscar, ordenar e filtrar a lista de produtos.

4. **Edição e Exclusão de Produtos**:
   - O usuário pode editar ou excluir um produto da lista de produtos.

### 6. **Tecnologias Utilizadas**

- **Frontend**: React.js + Tailwind CSS
- **Backend**: Node.js + Express
- **Banco de Dados**: MySQL
- **Autenticação** (opcional): JWT (JSON Web Token)

---

### Próximos Passos

1. **Configuração do Banco de Dados**: Criar as tabelas `produtos` e `entradas_saida_estoque` no MySQL.
2. **Desenvolvimento do Backend**: Criar a API RESTful usando Node.js e Express para gerenciar produtos e operações de estoque.
3. **Desenvolvimento do Frontend**: Criar as páginas de cadastro, listagem e controle de estoque em React.js com estilo usando Tailwind.
4. **Testes e Validação**: Testar as funcionalidades do sistema, como a entrada/saída de estoque e a manipulação de produtos.

Agora, que já temos os requisitos e uma ideia geral do sistema, qual parte você gostaria de começar a desenvolver primeiro? Podemos seguir passo a passo!
