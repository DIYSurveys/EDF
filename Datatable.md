[Back to the top](README.md)

## Dynamic Datatables
This section assumes you have read the previous sections. [Click here](Asynchronous.md) to find out more.

Microsoft offers a Datatable as a way of collecting bulk results from a database. This in turn uses the DataReader to
fill the datatable, but the process waits until this is completed. For large amounts of data there is no access to the data
until the fill has been completed.

OPGEDF offers a more dynamic approach to the standard datatable, but with a similar interface in order to reduce the
implementation time where a standard DataTable is already in place.

To find out more about house keeping please [click here](Rules.md).