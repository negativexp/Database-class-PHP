# MYSQLi Database class for PHP
simple connector class for PHP
## How to use
### Initilazition
Please make sure you have these strings correct
```php
private $servername = ""``
private $dbusername = "";
private $dbpassword = "";
private $database = "";
```
After that we initialize the database connector like this
```php
include "db.php";
$db = new Database();
```
This connects the database, if not, it will die with a connection failed message
### Executing a query
```php
public function executeQuery($sql, $params = [], $returnResult = true)
```
#### Without a result
Example #1
```php
$db = new Database();
$sql = "DELETE FROM contact_forms WHERE id = ?";
$params = [$_GET["deleteID"]];
if(!$db->executeQuery($sql, $params, false)) {
   echo "Chyba při mazání!";
}
```
Example #2
```php
$db = new Database();
$sql = "INSERT INTO contact_forms (email, name, message, date) VALUES (?,?,?,NOW())";
$params = [$email, $name, $message];
if($db->executeQuery($sql, $params, false)) {
    header("location: ./?success=true");
}
```
#### With a result
Example #1
```php
$db = new Database();
$sql = "select * from contact_forms";
$rows = $db->fetchRows($db->executeQuery($sql));
foreach ($rows as $row) {
    echo "<tr>";
    echo "<td>{$row["date"]}</td>";
    echo "<td>{$row["name"]}</td>";
    echo "<td>{$row["email"]}</td>";
    echo "<td><textarea disabled>{$row["message"]}</textarea></td>";
    echo "<td><a class='button' href='?delete={$row["ID"]}'>Delete</a></td>";
    echo "</tr>";
}
```