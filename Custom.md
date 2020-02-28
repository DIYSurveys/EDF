## Custom Queries
This section assumes you have read the previous section [Using Your Model](Using.md).

### Add a Custom Query
It is possible to enhance a factory by adding your own custom queries. Fro example, you might want to search for
Groups by name using a wildcard. The basic queries do not support this, so a simple custom query can be added.
In order to do this you need to add a new method to the GroupsFactory class:
```
    public List<Groups> GetByNameWildcard(string name) 
    {
        using (DataHandler)
    }
```