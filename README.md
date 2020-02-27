# OnePoint Global Entity Data Framework
Welcome to the OnePoint Global Entity Data Framework (OPGEDF). A set of libraries that supports access to Microsoft SQL Server and other databases. It provides a fast, light way to map a Database into code and prvoide a simple way to insert, update and delete data, with full access to stored procedures.

This contains the documentation to use the OPGEDF.

## Current Status
The OPGEDF is currently undergoing some enhancements to support asynchronous access to MS SQL Server, but the library and tools are stable and will support existing projects.

## Modeller
The OnePoint Modeller is a tool that provides fast mapping of a Microsoft SQL Database into c# for immediate use in an application. The Modeller is based around a an XML language and a set of templates that are used to generate the c# code. The example below shows a sample of an XML model:
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
  <table name="Groups" database="$db{Framework}" javaName="Groups">
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
</database>
```

This is converted into a set of c# classes:

Name | Description
---- | -----------
Groups.cs | A simple class that inherits the GroupsBase.cs for custom code.
GroupsBase.cs | A class that maps the data layout of the Microsoft SQL DB table.
GroupsFactory.cs | A simple class that inheirts the GroupsFactoryBase.cs for custom data access definition.
GroupsFactoryBase.cs | A class that include all the basic code for accessing an mapping the database table to c#.
IGroupsData.cs | Interface to the base data layout.
IGroupsFactoryData.cs | Interface to the base factory for accessing the data.

The template files are

The Modeller is available for use with Microsoft Visual Studio 2019 and can be downloaded from here.

