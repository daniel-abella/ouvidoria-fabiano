
# Operacoes-BD

This project, `operacoes-bd`, provides a simple and efficient way to perform basic database operations using the MySQL database in Python. The library focuses on creating, managing, and closing database connections, as well as executing essential CRUD (Create, Read, Update, Delete) operations with exception handling. The main goal is to facilitate interaction with a MySQL database using a minimal, straightforward interface.

## Features

1. **Database Connection**: Establishes and closes a connection to a MySQL database.
2. **Insert Data**: Inserts records into the database using prepared statements and handles exceptions.
3. **Retrieve Data**: Retrieves records from the database with optional query parameters.
4. **Update Data**: Updates existing records in the database with exception handling.
5. **Delete Data**: Deletes records from the database while managing potential errors.

## Requirements

- Python 3.x
- `mysql-connector-python` library

To install the necessary library, run:

```bash
pip install mysql-connector-python
```

## Usage

### 1. Initialize a Database Connection

The `criarConexao` function initializes a connection to the database using the provided host, user, password, and database name.

```python
from operacoes_bd import criarConexao

connection = criarConexao("localhost", "username", "password", "database_name")
```

### 2. Insert Data into the Database

The `insertNoBancoDados` function inserts a new record into the database. It uses prepared statements for security and supports automatic transaction rollback in case of errors.

```python
sql = "INSERT INTO table_name (column1, column2) VALUES (%s, %s)"
data = ("value1", "value2")
inserted_id = insertNoBancoDados(connection, sql, data)
print(f"Inserted record ID: {inserted_id}")
```

### 3. Retrieve Data from the Database

Use the `listarBancoDados` function to retrieve data from the database. You can specify SQL parameters to filter results.

```python
sql = "SELECT column1, column2 FROM table_name WHERE column3 = %s"
params = ("value3",)
results = listarBancoDados(connection, sql, params)
for row in results:
    print(row)
```

### 4. Update Data in the Database

The `atualizarBancoDados` function updates existing records. It also uses prepared statements and rolls back transactions if an error occurs.

```python
sql = "UPDATE table_name SET column1 = %s WHERE column2 = %s"
data = ("new_value", "condition_value")
affected_rows = atualizarBancoDados(connection, sql, data)
print(f"Rows affected: {affected_rows}")
```

### 5. Delete Data from the Database

The `excluirBancoDados` function deletes records from the database based on the given parameters. It manages exceptions and rolls back the transaction on error.

```python
sql = "DELETE FROM table_name WHERE column1 = %s"
data = ("value1",)
affected_rows = excluirBancoDados(connection, sql, data)
print(f"Rows deleted: {affected_rows}")
```

### 6. Close the Database Connection

When done, make sure to close the database connection using `encerrarConexao` to release resources.

```python
encerrarConexao(connection)
```

## Error Handling

Each function includes error handling to ensure database stability and data integrity. In cases where an error occurs during insertion, update, or deletion, the transaction is automatically rolled back to prevent partial or corrupted data entries.

## License

This project is open-source and available for contributions.
