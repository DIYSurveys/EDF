[Back to the top](README.md)

## Updating Using Your Model
This section assumes you have read the previous section. [Click here](Custom.md) for more information.
This section focuses on updating a database using your model. Each basic entity within the model includes a set of properties
inherited from the DataObject class (found in the OnePoint.Data library). These include:

Name | Description
---- | -----------
IsNew | A boolean value indicating whether the object is new and should be inserted.
IsModified | A boolean value indicating whether the object has been modified since is was created or retrieved. This is a manual flag.

Depending on these flags the factory can decide whether to insert or update the row in the database.
Using the factory method Save, this can be easily achieved.
```
    new GroupsFactory().Save(group);
```

This will:
1. Open the database.
2. Either `INSERT` or `UPDATE` the row using the data in the instance of the object.
3. Close the database.

### Delete
Delete is not available and would have to be added as a custom method. For more information on this [click here](Custom.md).

To manage relational databases [click here](Relational.md).
