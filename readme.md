# HTML Table Generator for PHP PDO Database Queries

_**maketable()**_ is a carefully crafted PHP function that allows a developer to easily create
professional-looking and standards-compliant (X)HTML tables from results of PDO database queries
while maintaning fine control over table's style and markup.

No more broken indentation, ugly text alignment and manually summing up numbers for "Total" value.  
_maketable()_ will make it all for you!

_[PDO](http://php.net/manual/en/book.pdo.php) is a state-of-the-art interface used to access
various database systems (MySQL, SQLite, MS SQL Server, Oracle and 7 others) in PHP in
a unified manner. With PDO your app can work on a dozen of database systems with minimal effort._

***

## Usage

With _maketable()_ you can make a table out of PDO SQL query in just 2 lines of code:

    include_once 'maketable.php';
    echo maketable( $pdo_connection->query( 'SELECT `name`, `city`, `orders_number` FROM `clients`' ) );

_maketable()_ will bring column headers for you automatically using information from database.  
But if you want to set custom headers, you can do it with just another one line of code:

    $column_headers = array("Client's name", 'City', 'Number of orders')

maketable() will nicely format values in the table automatically, aligning text to the left and
other data to the center.  
But if you want to set custom alignment, you can do it with just another one line of code:

    $column_align = array('left', 'left', 'center')

_maketable()_ will make a perfect HTML indentation for you.  
But if you want to set custom indents, you can do it with just another 2 lines of code:

    $first_indent = "\t\t\t",
    $indent = "\t"

_maketable()_ can easily add predefined classes to column cells.  
But if you would like to use semantic class names, you can do it with just another line of code:

    $column_classes = array('name', 'city', 'number')

You can also set custom id, caption, styles and class for the table.  
But the most interesting thing is that you can generate a complex footer for the table with...
_yes_, just another one line of code:

    $footer_columns = array('Clients: COUNT()', '', 'Total: SUM()')

_maketable()_ supports `SUM()`, `AVG()`, `MIN()`, `MAX()` and `COUNT()` functions in footer cells.

_maketable()_ also formats boolean values nicely making it appear as checkmarks instead of ugly 0/1.

***

## Complete example

Now look how all this goes together with PDO code.

    include_once 'maketable.php';
    $sql = 'SELECT `name`, `address`, `orders_number` FROM `clients`';
    try {
        $conn = new PDO( 'mysql:host=MY_HOST;dbname=MY_DATABASE', 'MY_USERNAME', 'MY_PASSWORD' );
        $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        echo maketable(
            $executed_pdo_statement = $conn->query( $sql ),
            $column_headers = array("Client's name", 'City', 'Number of orders'),
            $column_align = array('left', 'left', 'center'),
            $first_indent = "\t\t\t",
            $indent = "\t",
            $id = 'clients-table',
            $class = 'strict-blue',
            $style = 'padding: 0px; margin: 0px;',
            $caption = 'Clients',
            $column_classes = array('name', 'city', 'number'),
            $even_row_class = 'tinted',
            $footer_columns = array('Clients: COUNT()', '', 'Total: SUM()')
        );
    } catch( PDOException $e ) {
        echo '<p class="error">DATABASE ERROR:<br/>' . $e->getMessage() . '<br/>SQL query: ' . $sql . '</p>';
    }
    $conn = null;

Parameter names are given here for reference only, they can certainly be omitted.

Detailed parameters description can be found on our [wiki](https://github.com/codedriller/maketable/wiki).