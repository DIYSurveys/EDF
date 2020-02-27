## Using Your Model
This section assumes you have successfully followed the instruction in the main section [here](readme.md).

### Configure the Environment
Once you have created a basic model you need to configure the environment for the application.
The environment uses some settings in the applications config file (web.config or app.config depending on the type of project).
These must be placed in the `AppSettings` section of the config file:
```
  <appSettings>
    <add key="ConnectionString" value="MS SQL connection string" />
    <add key="ConnectionStringFramework" value="data mapping" />   
  </appSettings>
```
There is a main connection string setting and the subsequent connection strings refer to the database mappings to allow
access to multiple databases from the same model. The database mappings take the form `ConnectionString{name}` where `{name}`
refers to the database name in the model for either the whole model or the individual table.

### Use the Model
Now you are ready to code using the model.

#### Collecting Rows From a Table
To Collect rows from a table you need to use the associated factory class. Given the basic Groups model that was created
in the [introduction](readme.md) the factory class will be called GroupsFactory. In order to collect all the row in the Groups
table you can use the built in method as follows:
```
    List<Groups> groups = new GroupsFactory().FindAllObjects();
```
This will generate a list of Groups from the database. In detail it goes through the following steps:
1. Opens the database
2. Loads up a SQL Statement `SELECT * FROM Groups`
3. Reads each row, copies it into an instance of the Group class and adds it to a list of Groups.
4. Closes the database
5. Returns the list of Groups.

Every column in the table has a corresponding Find method in the basic factory. So gor the Groups table you can access
all the group by the their name. For example:
```
    List<Groups> groups = new GroupsFactory().FindByName();
```

Each table will have a primary key and that can be used to access a single row. For example:
```
    Groups group = new GroupsFactory().FindOvject(groupId);
```

For more information on custom queries to access data click here.