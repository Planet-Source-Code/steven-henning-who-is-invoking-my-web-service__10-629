<div align="center">

## Who is invoking my Web Service


</div>

### Description

If you want to know who is invoking your Web service, you can obtain the IP Address from the Context.Request.UserHostAddress

This will either return the invokers PC IP or the proxy they use.

In the example code below I used this to restrict a function to only respond to calls from the PC the Web Service is running on, i.e. 127.0.0.1
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Steven Henning](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/steven-henning.md)
**Level**          |Advanced
**User Rating**    |5.0 (20 globes from 4 users)
**Compatibility**  |VB\.NET
**Category**       |[Security](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/security__10-14.md)
**World**          |[\.Net \(C\#, VB\.net\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/net-c-vb-net.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/steven-henning-who-is-invoking-my-web-service__10-629/archive/master.zip)





### Source Code

```
<WebMethod()> Public Function YourIPAddress() As String
    Dim sCallersIPAddress As String = Context.Request.UserHostAddress
    Dim sReply As String
    sReply = "<<- This is either your PC's IP, or the proxy you use."
    Return (sCallersIPAddress & sReply)
  End Function
  <WebMethod()> Public Function LocalFunction(ByVal YourName As String) As String
    Dim sCallersIPAddress As String = Context.Request.UserHostAddress
    Dim sReply As String
    If sCallersIPAddress <> "127.0.0.1" Then
      ' A webservice request from an external PC
      sReply = "Hey, " & YourName & ", IP " & sCallersIPAddress & " may not execute this function!"
    Else
      ' Do something different for calls from localhost
      sReply = "Hello, " & YourName & ", IP " & sCallersIPAddress & " this app is runnning from " & Context.Request.PhysicalApplicationPath
    End If
    Return (sReply)
  End Function
```

