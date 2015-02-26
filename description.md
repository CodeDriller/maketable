## Welcome to the maketable() wiki!

As you might already know _maketable()_ is HTML Table Generator for PHP PDO Database Queries.

In essence it's a carefully crafted PHP function that allows a developer to easily create
professional-looking and standards-compliant (X)HTML tables from results of PDO database queries
while maintaning fine control over table's style and markup.

A short tutorial can be found on project's [main page](https://github.com/CodeDriller/maketable).

And here it goes a complete list of parameters with thorough description.

***

### Function definition

    function maketable(
        $executed_pdo_statement,
        $column_headers = true,
        $column_align = false,
        $first_indent = '    ',
        $indent = '  ',
        $id = '',
        $class = 'auto-generated',
        $style = '',
        $caption = '',
        $column_classes = false,
        $even_row_class = '',
        $column_footers = false
    )

***

### Parameters

**_PDOStatement_ $executed_pdo_statement**  
The [_PDOStatement_ object](http://php.net/manual/en/class.pdostatement.php)
returned by `query()` method,  
or _PDOStatement_ object with prepared query on which `execute()` method was called.  
This is the only required parameter.

**_array_ or _boolean_ $column_headers**  
A string array containing headers for table columns.
If _$column_headers_ parameter is set to `true` (the default),
then the function will try to get column headers from _PDOStatement_ object.  
To omit headers row completely set _$column_headers_ to `false`.

**_array_ or _boolean_ $column_align**  
A string array containing text alignment directives for table columns that will be added
in _style_ attribute to every cell.
Allowed values for array elements are `'left'`, `'right'` and `'center'`.
If _$column_align_ parameter is set to `true`, than all textual columns will be left-aligned
and all other columns will be center-aligned.  
Set _$column_align_ to `false` for default alignment.

**_string_ $first_indent**  
An indent that will be inserted between the beginning of the line and the `<table>` tag.  
Default is four spaces.

**_string_ $indent**  
An indent to separate `<table>..<tr>..<td>` tags. It can be a space `' '`, a tab `"\t"`, etc.  
Default is double space.

**_string_ $id**  
A value of _id_ attribute that will be added to `<table>` tag.
You can use it to distinguish one table from another in CSS.  
Default is empty string (attribute _id_ will not be added).

**_string_ $class**  
A value of _class_ attribute that will be added to `<table>` tag.
You can use it to apply your own CSS styles.  
Default class name is `'auto-generated'`.  
Pass empty string `''` to omit class specification for the table.

**_string_ $style**  
A value of _style_ attribute that will be added to `<table>` tag.  
Default is empty string (attribute _style_ will not be added).

**_string_ $caption**  
Table caption.  
Default is empty string (no caption will be added).

**_array_ or _boolean_ $column_classes**  
A string array containing classes that will be added to every cell in every column:
first element of array to the cells of first column, second element of array
to the cells of second column, etc.  
If _$column_classes_ parameter is set to `true`, classes `col-1`, `col-2`, etc. will be added.  
Default is `false` (no classes will be added).

**_string_ $even_row_class**  
A name of class that will be added to every even row of the table. This allows
a browser to use different colors for odd and even rows, if table style has such option.   
If _$even_row_class_ parameter is set to `true`, class `tinted` will be added.  
Default is empty string (no class).

**_array_ or _boolean_ $column_footers**  
A string array containing labels for table footer columns and optionally
functions to calculate the numeric values, e.g., `array('Total: SUM()', 'Average: AVG()')`.  
Allowed functions are: `SUM()`, `AVG()`, `MIN()`, `MAX()`, `COUNT()`.
These would be replaced by actual values.  
Only `COUNT()` function may be applied to non-numeric data.  
Providing any label forces the table to be divided into `<thead>`, `<tfoot>` and `<tbody>`.  
Default is `false` (no footer).

### Returns

**_string_**  
Returns fully formatted table: `<table>...</table>`.