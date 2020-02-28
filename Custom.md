[Back to the top](README.md)

## Custom Queries
This section assumes you have read the previous section [Using Your Model](Using.md).

### Add a Custom Query
It is possible to enhance a factory by adding your own custom queries. Fro example, you might want to search for
Groups by name using a wildcard. The basic queries do not support this, so a simple custom query can be added.
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
The method above can now be used to return a list of Groups containing the a pattern in the name. For example:
```
    List<Groups> groups = new GroupsFactory().GetByNameWildcard("test");
```
The method also demonstrates the use of a number of constants that are automatically generated.
These are as follows:

Name | Description
---- | -----------
SelectAllStatement | A string representing the SELECT * FROM... string of a SQL statement for that table.
FIELD_NAME_name | A string representing the name of a field where `name` is the name defined in the model.
PARAMETER_NAME_name | A string representing the parameter name of the field where `name` is trhe name defined in the model.

In addition to these there is a method for each field to add a vlaue as a parameter to the SQL request.

It is recommended that these predefined constants and methods are used in order to make your code more dynamic.
for example it allows you to change the name of a field in the database and the model with no changes to the code.

The factory can also be used to update the database. [Click here](Update.md) to find out more.
