[Back to the top](README.md)

## Dynamic Datatables
This section assumes you have read the previous sections. [Click here](Asynchronous.md) to find out more.

Microsoft offers a Datatable as a way of collecting bulk results from a database. This in turn uses the DataReader to
fill the datatable, but the process waits until this is completed. For large amounts of data there is no access to the data
until the fill has been completed.

OPGEDF offers a more dynamic approach to the standard datatable, but with a similar interface in order to reduce the
implementation time where a standard DataTable is already in place.

A DataTable can be obtained through in a similar way to gaining access to a DataReader:
```
    dataHandler.CommandText = SelectAllStatement + " WHERE " 
                              + FIELD_NAME_NAME + " LIKE " + PARAMETER_NAME_NAME;
    this.AddNameParameter(dataHandler, "%" + name + "%");
    Task<IDataTable> task = dataHandler.ExecuteAsDataTableAsync();
```
The Task returned can then be used at the appropriate point to gain access to Rows and Columns.
The Rows are available as an enumerator and can support each row (as read by a DataReader) as an ISqlAsyncRow object
that includes an array accessible for each column by either name or zero based position. For example:
```
    foreach (ISqlAsyncRow row in table.Rows)
    {
        string name = row["Name"].ToString();
        long groupId = (long)row[0];
    }
```
In the above example the Enumerator is asynchronous and only accessing the data when it is requested, rather than a standard
DataTable being filled.

To find out more about house keeping please [click here](Rules.md).