On Azure portal go to >Log Analytics workspaces>Logs 


#### Heartbeat:
```sh
Heartbeat
| summarize Lastbeat = arg_max(TimeGenerated, *) by Computer, ComputerEnvironment
| where Lastbeat < ago(5m)
| summarize by Computer, ComputerEnvironment

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
| summarize AggregatedValue= avg(CounterValue) by Computer, ComputerEnvironment, CounterName, bin(TimeGenerated, 5m)
```



