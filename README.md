# Desafio de Projeto: Trilha .NET Azure da DIO

Este repositório contém a solução para o desafio de projeto final da trilha de .NET com Azure, que consiste na criação de uma API para um CRUD de Funcionários.

## Decisões de Implementação e Arquitetura

Para a conclusão deste desafio, foram tomadas algumas decisões estratégicas para garantir a funcionalidade da aplicação em um ambiente de desenvolvimento local, sem a necessidade de provisionar e incorrer em custos com serviços de nuvem.

### 1. Persistência de Dados (Banco de Dados)

O código para a conexão com um banco de dados **SQL Server** está implementado, porém comentado no arquivo `Program.cs`. A decisão de não utilizar uma instância real do SQL Server foi tomada para simplificar o setup do projeto.

Em seu lugar, a aplicação foi configurada para utilizar um **Banco de Dados em Memória** (`InMemoryDatabase`).

*   **Vantagem:** Permite que a aplicação seja executada e testada integralmente (via Swagger) sem qualquer configuração de banco de dados externo. O CRUD completo é funcional.
*   **Observação:** Como o banco de dados reside na memória, todos os dados cadastrados são perdidos ao reiniciar a aplicação.

### 2. Logging com Azure Table Storage

O requisito de registrar os logs das operações de CRUD em uma tabela do **Azure Table Storage** foi totalmente implementado no `FuncionarioController.cs`.

No entanto, as linhas de código que efetivamente se comunicam com o serviço do Azure foram comentadas. Esta decisão foi tomada para que o projeto pudesse ser executado sem a necessidade de uma conta ativa do Azure e de uma connection string real, evitando assim a geração de cobranças.

O código implementado demonstra o conhecimento do SDK e da lógica necessária para a integração.

## Como Executar a Aplicação

1.  Clone este repositório.
2.  Abra o arquivo da solução (`.sln`) no Visual Studio.
3.  Pressione `F5` ou o botão de "Play" para iniciar a aplicação.
4.  O navegador será aberto automaticamente na interface do Swagger (`/swagger/index.html`).
5.  Utilize os endpoints disponíveis no Swagger para testar as operações de `GET`, `POST`, `PUT` e `DELETE`.

## Para uma Aplicação de Produção

Para configurar este projeto para um ambiente de produção real, os seguintes passos devem ser seguidos:

1.  **Configurar o Banco de Dados SQL:**
    *   No arquivo `Program.cs`, comente a linha que usa `.UseInMemoryDatabase()` e descomente a linha que usa `.UseSqlServer()`.
    *   No arquivo `appsettings.json`, preencha a `"ConexaoPadrao"` com a string de conexão do seu banco de dados SQL Server ou Azure SQL.

2.  **Habilitar o Log no Azure Table Storage:**
    *   No arquivo `FuncionarioController.cs`, descomente as linhas de código responsáveis por criar e salvar o `FuncionarioLog` no Azure Table Storage dentro de cada método do CRUD.
    *   No arquivo `appsettings.json`, preencha a `"SAConnectionString"` com a string de conexão da sua Conta de Armazenamento do Azure.
