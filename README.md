# table2csv
[![Build Status](https://travis-ci.com/OmbraDiFenice/table2csv.svg?branch=master)](https://travis-ci.com/OmbraDiFenice/table2csv)

A simple jQuery plugin to convert HTML tables to CSV. It allows you to download or display the content of a regular HTML
table as a CSV file.

It is useful if you want to quickly build a downloadable report from a web based tool.

Check out the [live example](https://ombradifenice.github.io/table2csv/) page.

## Installation

You can install this plugin from [npm](https://www.npmjs.com/package/table2csv)

```bash
$ npm install table2csv
```

## Usage

Import jQuery and this script

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
<script src="/path/to/table2csv.min.js"></script>
```

where `/path/to/` will be the path where you installed the plugin.
If you installed it through npm it will probably be `node_modules/table2csv/dist`

then invoke the `table2csv()` function on the jQuery object of the table

```javascript
$("table").first().table2csv(); // default action is 'download'
```

The plugin currently convert just one table at a time and must be called directly on the table you want to convert.
These limits will hopefully be removed in future versions.

`table2csv()` accepts 2 arguments, both optional:

`table2csv(action, options)`

See below for the description.


### Example

```html
<table id="tab">
  <tr>
    <th>Company</th>
    <th>Contact</th>
    <th>Country</th>
  </tr>
  <tr>
    <td>Alfreds Futterkiste</td>
    <td>Maria Anders</td>
    <td>Germany</td>
  </tr>
  <tr>
    <td>Ernst Handel</td>
    <td>Roland Mendel</td>
    <td>Austria</td>
  </tr>
  <tr>
    <td>Island Trading</td>
    <td>Helen Bennett</td>
    <td>UK</td>
  </tr>
  <tr>
    <td>Magazzini Alimentari Riuniti</td>
    <td>Giovanni Rovelli</td>
    <td>Italy</td>
  </tr>
</table>
```

```javascript
// download the content of table "tab"
$("#tab").table2csv(); // default action is 'download'
```

This will start the download of a file called 'table.csv' which will contain the following:

    "Company","Contact","Country"
    "Alfreds Futterkiste","Maria Anders","Germany"
    "Ernst Handel","Roland Mendel","Austria"
    "Island Trading","Helen Bennett","UK"
    "Magazzini Alimentari Riuniti","Giovanni Rovelli","Italy"
    
You can change the name of the downloaded file and other settings using the options.

### Actions

* 'download'  
This is the default action (i.e. the one performed if you call `table2csv()` without any argument).
Convert the table to a csv and start the download of the file. The file name can be specified in the options (default is `table.csv`).

* 'output'  
With this action the csv output is not downloaded as a file, but appended as text inside the html page.
Use the `appendTo` option to specify the [jQuery selector](http://api.jquery.com/category/selectors/) of the destination element (default is `body`).

* 'return'  
With this action the extracted csv will be returned as a string by the call to `table2csv()`.  
**WARNNG:** the other actions will return the same jQuery object they were called on, thus allowing you to chain the call with
other jQuery methods. With this action instead, since you get a string in return, you will no longer be able to do that.
For example, this will **not** work:

    ```javascript
    $("#tab").table2csv('return').find(".col2"); // TypeError: $(...).table2csv(...).find is not a function
    ```

### Options

#### General options
* separator  
`default: ','`  
The field separator to use in the csv

* newline  
`default: '\n'`  
The line separator to use in the csv

* quoteFields  
`default: true`  
Whether to quote fields in the csv

* excludeColumns  
`default: ''`  
jQuery selector for the columns you don't want to export in the csv (tipically a list of classes)

* excludeRows  
`default: ''`  
jQuery selector for the rows you don't want to export in the csv (tipically a list of classes)

* trimContent  
`default: true`   
Trims the content of individual \<th>, \<td> tags of whitespaces. This will produce valid output even if the table is indented.

* visibleOnly
`default: true`
Apply jQuery selector ":visible" on td/th.

#### Download options

These options apply only when the 'download' action is used

* filename  
`default: 'table.csv'`  
This is the name given to the file when the 'download' action is invoked

#### Output options

These options apply only when the 'output' action is used

* appendTo  
`default: 'body'`  
jQuery selector of the element inside which append the generated csv text. This is only used when the 'output' action is invoked
