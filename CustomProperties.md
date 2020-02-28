## Custom Properties
This section assumes you had read the previous section. [Click here](Relational.md) for more information.
This section covers custom properties and methods for an object.

It is possible that the model does not cover business rules that cannot be described in the database.
You can add custom properties and methods into the main class for a object to handle this.
Consider the Group object, which contains a Level integer. This can be one of four values that indicates the
highest level that the group can operate at in the application:

Level | Value | Description
----- | ----- | -----------
None | 0 | An inactive group
Basic | 1 | Basic access to the application
Advanced | 2 | Advanced access to the application
Admin | 99 | Full administrator rights to access the application

Whilst it is possible to code using the integer values it can sometimes be difficult to remember the individual values
and mistakes can be made. By adding an `enum` that defines the names and values and a property that support it
you can remove the chance of mistakes:
```
public enum LevelDefinition
{
    None = 0,
    Basic = 1,
    Advanced = 2,
    Admin = 99
}
```
This is used with the following property:
```
    public LevelDefinition LevelType 
    {
        get => (LevelDefinition)this.Level;
        set => this.Level = (int)value;
    }
```
The new `LevelType` property can be used instead of the `Level` property in the model. For example:
```
    if (group.LevelType == LevelDefinition.Admin) 
    {
        /// Do some admin type process
    }
```
