[Back to the top](README.md)

## Asynchonrous Database Access
This section assumes you understand the OPGEDF in more detail. To find out more please [click here](Relational.md).
The DIYEDF offers asynchronous access to the database. Each object in the model has a factory that include asynchronous access.
For example the Find method in the factory class offers an asynchronous option:
```
    public async Task<IEnumerable<Survey>> GetByNameWildcardAsync(string name) 
    {
        DataHandler dataHandler = new DataHandler();
        dataHandler.CommandText = SelectAllStatement + " WHERE " 
                                + FIELD_NAME_NAME + " LIKE " + PARAMETER_NAME_NAME;
        this.AddNameParameter(dataHandler, "%" + name + "%");
        return await this.FindAsync(dataHandler);
    }
```
The above code offers an asynchronous task which when used will begin to access the database and make the rows available
as an asynchronous Enumerable list.

The next section describes a more dynamic DataTable for accessing large datasets. [Click here](Datatable.md) to find out more.