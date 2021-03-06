# WmiLight [![wmilight MyGet Build Status](https://www.myget.org/BuildSource/Badge/wmilight?identifier=ec18dcc7-d42a-4704-94cf-e7dc6d3a8a98)](https://www.myget.org/feed/wmilight/package/nuget/WmiLight)

## What is WmiLight?
A simple and light wmi framework. It has only one function: sending WMI queries.
It's a subset of the System.Management.Instrumentation namespace.

## In which case should you use WmiLight?
The .Net framework implementation has one big problem.
It leaks a little bit memory on each remote operation.
Use this framework if your application is a service or runes a long time and you're sending a lot of remote queries.

## Installation

This project is being distributed as a sNuGet package, so open your Package Manager Console window and execute the following command.

<a href="https://www.nuget.org/packages/WmiLight/" target="_blank">
<img title="NuGet" src="https://github.com/MartinKuschnik/WmiLight/blob/master/doc/pics/install_nuget_package.JPG" alt="NuGet"/>
</a>



## How to use?

Query all running processes for the local machine:
```C#
using (WmiConnection conncetion = new WmiConnection())
{
    foreach (WmiObject process in conncetion.CreateQuery("SELECT * FROM Win32_Process"))
    {
        Console.WriteLine(process["Name"]);
    }
}
```

Query all partitions for a remote machine:
```C#

var opt = new WmiConnectionOptions() { EnablePackageEncryption = true };
var cred = new NetworkCredential("USERNAME", "PASSWORD", "DOMAIN");

using (WmiConnection conncetion = new WmiConnection(@"\\MACHINENAME\root\cimv2", cred, opt))
{
    foreach (WmiObject partition in conncetion.CreateQuery("SELECT * FROM Win32_DiskPartition"))
    {
        Console.WriteLine(partition["Name"]);
    }
}
```

## Other benefits:

* easy usage

* no distinction between local and remote queries

* Debugger Preview 

    ![Debugger_Preview](https://github.com/MartinKuschnik/WmiLight/blob/master/doc/pics/debugger_preview.jpg "Debugger Preview")

