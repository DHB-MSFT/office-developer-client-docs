---
title: "Count Property Example (VB)"
  
  
manager: soliver
ms.date: 11/16/2014
ms.audience: Developer
 
  
localization_priority: Normal
ms.assetid: 9fea66f7-a4ed-fe2e-c199-672b910fef47
description: "This example demonstrates the Count property with two collections in the Employee database. The property obtains the number of objects in each collection, and sets the upper limit for loops that enumerate these collections. Another way to enumerate these collections without using the Count property would be to use statements."
---

# Count Property Example (VB)

This example demonstrates the [Count](count-property-ado.md) property with two collections in the ** *Employee* ** database. The property obtains the number of objects in each collection, and sets the upper limit for loops that enumerate these collections. Another way to enumerate these collections without using the **Count** property would be to use statements. 
  
```
 
'BeginCountVB 
 
 'To integrate this code 
 'replace the data source and initial catalog values 
 'in the connection string 
 
Public Sub Main() 
 On Error GoTo ErrorHandler 
 
 ' recordset and connection variables 
 Dim rstEmployees As ADODB.Recordset 
 Dim Cnxn As ADODB.Connection 
 Dim strSQLEmployees As String 
 Dim strCnxn As String 
 
 Dim intLoop As Integer 
 
 ' Open a connection 
 Set Cnxn = New ADODB.Connection 
 strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" &amp; _ 
 "Initial Catalog='Northwind';Integrated Security='SSPI';" 
 Cnxn.Open strCnxn 
 
 ' Open recordset with data from Employee table 
 Set rstEmployees = New ADODB.Recordset 
 strSQLEmployees = "Employees" 
 'rstEmployees.Open strSQLEmployee, Cnxn, , , adCmdTable 
 rstEmployees.Open strSQLEmployees, Cnxn, adOpenForwardOnly, adLockReadOnly, adCmdTable 
 'the above two lines opening the recordset are identical as 
 'the default values for CursorType and LockType arguments match those specified 
 
 ' Print information about Fields collection 
 Debug.Print rstEmployees.Fields.Count &amp; " Fields in Employee" 
 
 For intLoop = 0 To rstEmployees.Fields.Count - 1 
 Debug.Print " " &amp; rstEmployees.Fields(intLoop).Name 
 Next intLoop 
 
 ' Print information about Properties collection 
 Debug.Print rstEmployees.Properties.Count &amp; " Properties in Employee" 
 
 For intLoop = 0 To rstEmployees.Properties.Count - 1 
 Debug.Print " " &amp; rstEmployees.Properties(intLoop).Name 
 Next intLoop 
 
 ' clean up 
 rstEmployees.Close 
 Cnxn.Close 
 Set rstEmployees = Nothing 
 Set Cnxn = Nothing 
 Exit Sub 
 
ErrorHandler: 
 ' clean up 
 If Not rstEmployees Is Nothing Then 
 If rstEmployees.State = adStateOpen Then rstEmployees.Close 
 End If 
 Set rstEmployees = Nothing 
 
 If Not Cnxn Is Nothing Then 
 If Cnxn.State = adStateOpen Then Cnxn.Close 
 End If 
 Set Cnxn = Nothing 
 
 If Err <> 0 Then 
 MsgBox Err.Source &amp; "-->" &amp; Err.Description, , "Error" 
 End If 
End Sub 
'EndCountVB 

```

