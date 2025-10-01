# MySQL Database Functions Reference

## 1. MySQLi Functions / Methods

### a. Connection

| Function | Description |
|----------|-------------|
| `mysqli_connect($host, $user, $pass, $db)` | Creates a connection to a MySQL database. |
| `$mysqli = new mysqli($host, $user, $pass, $db)` | Object-oriented way to create a connection. |
| `$mysqli->close()` | Closes the connection. |

### b. Query Execution

| Function | Description |
|----------|-------------|
| `mysqli_query($conn, $sql)` | Executes a SQL query (procedural). |
| `$mysqli->query($sql)` | Executes a SQL query (object-oriented). |

### c. Fetching Results

| Function | Description |
|----------|-------------|
| `mysqli_fetch_assoc($result)` | Returns a row as an associative array. |
| `mysqli_fetch_row($result)` | Returns a row as a numeric array. |
| `mysqli_fetch_object($result)` | Returns a row as an object. |
| `$result->fetch_assoc()` | Object-oriented equivalent. |
| `$result->fetch_object()` | Object-oriented equivalent. |

### d. Prepared Statements

| Method | Description |
|--------|-------------|
| `$stmt = $mysqli->prepare($sql)` | Prepares a SQL statement. |
| `$stmt->bind_param($types, $var1, $var2)` | Binds variables to the prepared statement. |
| `$stmt->execute()` | Executes the prepared statement. |
| `$stmt->get_result()` | Gets result set from executed statement (requires MySQL native driver). |
| `$stmt->close()` | Closes the prepared statement. |

### e. Error Handling

| Property / Function | Description |
|---------------------|-------------|
| `$mysqli->error` | Returns the last error message. |
| `$mysqli->errno` | Returns the last error number. |

## 2. PDO Functions / Methods

### a. Connection

| Method | Description |
|--------|-------------|
| `$pdo = new PDO($dsn, $user, $pass, $options)` | Creates a database connection. `$dsn` includes driver, host, dbname. |
| `$pdo = null` | Closes the connection. |

### b. Query Execution

| Method | Description |
|--------|-------------|
| `$pdo->query($sql)` | Executes a SQL query and returns a PDOStatement. |
| `$pdo->exec($sql)` | Executes a SQL statement that doesn't return results (INSERT, UPDATE, DELETE). |

### c. Fetching Results

| Method | Description |
|--------|-------------|
| `$stmt->fetch($mode)` | Fetches one row from result set. Modes: `PDO::FETCH_ASSOC`, `PDO::FETCH_OBJ`, `PDO::FETCH_NUM`, etc. |
| `$stmt->fetchAll($mode)` | Fetches all rows. |

### d. Prepared Statements

| Method | Description |
|--------|-------------|
| `$stmt = $pdo->prepare($sql)` | Prepares a SQL statement. |
| `$stmt->execute($params)` | Executes the prepared statement with optional parameters. |
| `$stmt->bindParam($param, $var)` | Binds a variable to a parameter. |
| `$stmt->bindValue($param, $value)` | Binds a value to a parameter. |
| `$stmt->rowCount()` | Returns the number of affected rows. |

### e. Error Handling

| Method / Attribute | Description |
|--------------------|-------------|
| `$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION)` | Throws exceptions on errors. |
| `$pdo->errorInfo()` | Returns array with SQLSTATE, driver error code, and driver message. |


### f. Example Usage

**MySQLi:**
```bash
$mysqli = new mysqli("localhost", "root", "", "test");
$stmt = $mysqli->prepare("SELECT * FROM users WHERE email=?");
$stmt->bind_param("s", $email);
$stmt->execute();
$result = $stmt->get_result();
while($row = $result->fetch_assoc()){
    echo $row['name'];
}
$stmt->close();
$mysqli->close();
bash

``bash
$pdo = new PDO("mysql:host=localhost;dbname=test", "root", "");
$stmt = $pdo->prepare("SELECT * FROM users WHERE email=:email");
$stmt->execute(['email' => $email]);
while($row = $stmt->fetch(PDO::FETCH_ASSOC)){
    echo $row['name'];
}
$pdo = null;

```
