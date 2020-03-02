[Back to the top](README.md)

## Housekeeping
This section assumes you have read other section on how OPGEDF works. For more information please [click here](README.md).
It is important that you maintain good housekeeping with your code. Some of the house keeping is done by OPGEDF,
but it is always up to you make sure you clean up after yourself. This section discusses some of the rules.

### DataHandler Lifetime
A DataHandler is responsible for access to the database. It contains the steps for opening a database, obtain the data or
manipulating it and finally closing the database. When a Find method is used by a Factory it is performed through the
DataHandler that is passed to it and it will ensure that the lifetime of the datahandler is managed.

However if you write your own custom Factory methods you must make sure the "open, action, close" process is kept to.
A DataHandler is "Disposable" and therefore if you structure you code with this in mind it will automatically ensure
the "open, action, close" process is kept to. For example:
In order to do this you need to add a new method to the GroupsFactory class:
```
    public List<Groups> GetByNameWildcard(string name) 
    {
        using (DataHandler dataHandler = new DataHandler())
        {
            dataHandler.CommandText = SelectAllStatement + " WHERE " 
                                    + FIELD_NAME_NAME + " LIKE " + PARAMETER_NAME_NAME;
            this.AddNameParameter(dataHandler, "%" + name + "%");
            return this.Find(dataHandler);
        }
    }
```
If you do not wish to use the "Disposable" approach you can call the methods explicitly for the "open, action, close" process.
For example:
```
    public List<Groups> GetByNameWildcard(string name) 
    {
        try
        {
            dataHandler.CommandText = SelectAllStatement + " WHERE " 
                                    + FIELD_NAME_NAME + " LIKE " + PARAMETER_NAME_NAME;
            this.AddNameParameter(dataHandler, "%" + name + "%");
            dataHandler.ExecuteAsDataReader();
            return this.Build(dataHandler, false);
        }
        catch (Exception e)
        {
            throw new Exception("Error in Find()", e);
        }
        finally
        {
            dataHandler.CloseConnection();
        }
    }
```

### Using Asynchronous Methods
Asynchronous methods require the connection to be open for longer over the whole process.
To cater for this the DataReader and DataTable will automaitcally close the connection when it reaches the end of the rows.
Otherwise you can close it by accessing the Dispose() methods of the DataReader or DataTable.
