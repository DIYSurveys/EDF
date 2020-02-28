## Managing Relational Databases
This section assumes you have read the previous sections. [Click here](Update.md) for more information.
This section focuses on setting up automatic relations that mimic the connections in a relational database.

### One to One Relationships
Consider the following two tables in a model:
```
<?xml version="1.0" encoding="utf-8" standalone="no"?>
<!DOCTYPE database SYSTEM "Templates\norque.dtd">
<?neo path="templates"?>
<?neo userfileextension=".cs"?>
<?neo supportfileextension=".cs"?>
<?neo support="IClassNameData.vtl,IClassNameFactoryBase.vtl,ClassNameBase.vtl,ClassNameFactoryBase.vtl"?>
<?neo user="ClassName.vtl,ClassNameFactory.vtl"?>

<database name="$db{Framework}" package="OnePoint.PROM.Model" defaultJavaNamingMethod="javaname" defaultIdMethod="native">
  <!--START-PROJECT-STRUCTURE -->
  <table name="Group" database="$db{Framework}" javaName="Group">
    <column name="GroupID"  type="BIGINT" javaType="BIGINT" required="true" primaryKey="true" autoIncrement="true"  description=""  />
    <column name="UserID" type="BIGINT" javaType="BIGINT" required="true" description="" />
    <column name="Name"  type="LONGVARCHAR" javaType="TEXT" required="true" size="1024" />
    <column name="Description"  type="LONGVARCHAR" javaType="TEXT" required="true" size="4000" />
    <column name="CreatedDate"  type="DATE" javaType="DATE" required="true"  />
    <column name="LastUpdatedDate"  type="DATE" javaType="DATE" required="true" />
    <column name="ParentGroupID" type="BIGINT" javaType="BIGINT" required="true" description="" />
    <column name="Level" type="BIGINT" javaType="BIGINT" required="true" description="" />
    <column name="RefID" type="INTEGER" javaType="BIGINT" required="true" description="" />
  </table>
  <table name="User" database="$db{Framework}" javaName="User">
    <column name="UserID" type="BIGINT" javaType="BIGINT" required="true" description="" primaryKey="true" autoincrement="true" />
    <column name="Name"  type="LONGVARCHAR" javaType="TEXT" required="true" size="1024" />
    <column name="GroupID" type="BIGINT" javaType="BIGINT" required="true" />
  </table>
</database>
```
In this database a user belongs to a group. If you want to acess the group from a user you would need to Find the
Group using the GroupID in the User object. This process can be automated with OPGEDF. By changing the model to include the
following in the User table definition:
```
    <foreign-key foreignTable="Script" name="Group" onUpdate="none" onDelete="none">
      <reference local="GroupID" foreign="GroupID"/>
    </foreign-key>
```
This creates a property in the User class called Group, which is an instance of the Group class that is instantiated when accessed
based on the GroupID property of the user class.

### One to Many Relationships
It is also possible to associate the users with a single group by adding the following into the Group table definition:
```
    <iforeign-key foreignTable="User" name="Users" onUpdate="none" onDelete="none">
      <ireference local="GroupID" foreign="GroupdID"/>
    </iforeign-key>
```
This creates a property in the Group class called Users, which is a list of Users in the group.
this is only created when the property is referenced.

### Many to Many Relationships
Many to many relationships are not supported currently. You would need to implement these manually.
There are a number of options you might take:
1. Create a third table that holds a `one-to-many` ralstion between the two tables and create a model that uses that.
2. Create custom code in the objects and factories to support it.

To find out more about create custom properties for objects [click here](CustomProperties.md).