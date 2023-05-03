On Azure portal go to >Log Analytics workspaces>Logs 
#### https://github.com/tobiasmcvey/kusto-queries


#### Heartbeat:
```sh
Heartbeat
| summarize Lastbeat = arg_max(TimeGenerated, *) by Computer, ComputerEnvironment
| where Lastbeat < ago(5m)
| summarize by Computer, ComputerEnvironment
```
#### Query to show Machines with less than 10 Gb. With free diskspace.
```sh
InsightsMetrics
| where Name == "FreeSpacePercentage"
| summarize arg_max(TimeGenerated, *) by Tags
// arg_max over TimeGenerated returns the latest record
| project TimeGenerated, Computer, Val, Tags
| where Val < 10
```
#### Or

```sh
Perf
| where ObjectName == "LogicalDisk" and CounterName == "% Free Space"
| summarize FreeSpace = min(CounterValue) by Computer, InstanceName
| where strlen(InstanceName) ==2 and  InstanceName contains ":"
| where FreeSpace < 10
| sort by FreeSpace asc

| render barchart kind=unstacked

```
### Or
```sh
// New capacity query
let setpctvalue = 60; // enter a % value to check
Perf
| where TimeGenerated > ago(1d)
| where ObjectName == "LogicalDisk" and CounterName == "% Free Space"
| where InstanceName contains ":"
| summarize FreeSpace = min(CounterValue) by Computer, InstanceName
| where FreeSpace < setpctvalue
| render barchart kind = stacked

```
#### Create azure monitor alert when my disk space low in virtual machine
```sh
let setgbvalue = 200;//Set the disk space you want to check for. 
 Perf 
 | where TimeGenerated > ago(6h)
 | where ObjectName == "LogicalDisk" and CounterName == "Free Megabytes" 
// exclude all others as we are checking for C: here 
 | where InstanceName != "D:"  
 | where InstanceName  != "_Total" 
 | where InstanceName != "HarddiskVolume1" 
 | extend FreeSpaceGB = CounterValue/1024 // converting the counter value to GB 
 | summarize FreeSpace = min(FreeSpaceGB) by Computer, InstanceName 
 | where FreeSpace < setgbvalue //setting condition to check if the value is less than our set value . 
```

#### Disk Utilization:

```sh
let MB=Perf|where ObjectName=="LogicalDisk" and CounterName=="Free Megabytes"|summarize T=arg_max(TimeGenerated,*) by C=Computer,I=InstanceName|where strlen(I)==2 and I contains ":"|project T,C,I,M=CounterValue|where M<5024|sort by M asc;let P=Perf|where ObjectName=="LogicalDisk" and CounterName=="% Free Space"|summarize T=arg_max(TimeGenerated,*) by C=Computer, I=InstanceName|where strlen(I)==2 and I contains ":"|project T,C,I,P=CounterValue|where P<10|sort by P asc;MB|join (P) on C,I|project Time=T,Computer=C,Drive=I,FreeSpacePercent=round(P,2),FreeSpaceMB=M|sort by FreeSpacePercent asc
```

#### CPU Utilization:

```sh
let a=Heartbeat
| summarize arg_max(TimeGenerated, *) by Computer, ComputerEnvironment
| distinct Computer, ComputerEnvironment;
let b= Perf
| where CounterName contains "% Processor Time" ;
a
| join
(
b
)
on Computer
| summarize AggregatedValue= avg(CounterValue) by Computer, ComputerEnvironment, CounterName, bin(TimeGenerated, 5m)
```


#### Memory Utilization:
```sh
let a=Heartbeat
| summarize arg_max(TimeGenerated, *) by Computer, ComputerEnvironment
| distinct Computer, ComputerEnvironment;
let b= Perf
| where CounterName contains "% Committed Bytes In Use";
a
| join
(
b
)
on Computer
| summarize AggregatedValue= round(avg(CounterValue),2) by Computer, ComputerEnvironment, CounterName, bin(TimeGenerated, 5m)
| sort by TimeGenerated desc 

```



