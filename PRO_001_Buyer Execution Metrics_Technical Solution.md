# Power Query

## Set up M parameter & SQL_Query

### ServerName
```
"Server url" meta [IsParameterQuery=true, List={"dsn=SnowflakeDEV", "dsn=SnowflakeSTG", "dsn=SnowflakePRD", "Server url"},
DefaultValue="Server url", Type="Text", IsParameterQueryRequired=true]
```
### Warehouse
```
"WH_DEV" meta [IsParameterQuery=true, List={"WH_DEV", "WH_STG", "WH_PRD"},
DefaultValue="WH_DEV", Type="Text", IsParameterQueryRequired=true]
```

### Database
```
"DEV_BI" meta [IsParameterQuery=true, List={"DEV", "DEV_BI", "STG", "PRD"},
DefaultValue="DEV_BI", Type="Text", IsParameterQueryRequired=true]
```

### Role
```
"xxxx_D_BI" meta [IsParameterQuery=true, List={"xxxx_D_BI", "xxxx_S_BI", "xxxx_P_BI"},
DefaultValue=..., Type="Text", IsParameterQueryRequired=true]
```

### DataLimit
```
"100" meta [IsParameterQuery=true, Type="Text", IsParameterQueryRequired=false]
```

### SQL_Query
```
"
SELECT " & (if #"DataLimit" = null then "" else " TOP " & #"DataLimit" & "") & "
	Plant key								AS ""Plant key"",
	Snapshot Date Key						AS ""Snapshot Date Key"",
	Buyer Key								AS ""Buyer Key"",
	Profit center Key						AS ""Profit center Key"",
	Columns                   
FROM
	SAP.V_View
"
```

## Query Table
```
Value.NativeQuery(Snowflake.Databases(ServerName,Warehouse,[Role=Role]){[Name=Database]}[Data],
#"SQL_Query", null, [EnableFolding=true])
```
## 

# Data Model 

<img width="1551" height="800" alt="image" src="https://github.com/user-attachments/assets/810115fc-6905-4630-bae1-39edd9f09663" />

# Dax

```
Select Filter =
IF (
    ISBLANK ( SELECTEDVALUE ( Cancellation_Details[Priority Text] ) ),
    IF (
        CONCATENATEX (
            DISTINCT ( Cancellation_Details[Is Un-executed (New)] ),
            [Is Un-executed (New)]
        ) = "TRUE",
        "Un-Executed",
        "Show all Details"
    ),
    SELECTEDVALUE ( Cancellation_Details[Priority Text] )
        & SELECTEDVALUE ( Cancellation_Details[Result Text] )
)
```

```
Cancellation Execution % =
VAR __TotalCancels =
    [Total Cancels (Inside)] +
    [Total Cancels (No Demand)] +
    [Total Cancels (Week1)] +
    [Total Cancels (NCNR)]
VAR __Unexecuted =
    [Un-executed (New)]
VAR __Rate =
    DIVIDE ( __Unexecuted, __TotalCancels, 0 )
VAR __Result =
    1 - __Rate
RETURN
    __Result			
```

```
Sorted Cancellation Execution = 
IF(
    ISINSCOPE(Cancellation[Snapshot Date]),
    [Cancellation Execution %],
    CALCULATE(
        [Cancellation Execution %],
        Cancellation[Snapshot Date] = MAX(Cancellation[Snapshot Date])
    )
)				    
```
```
Last Week Partial Received (Week1 and No Demand) =
CALCULATE (
    SUM ( Cancellation[Partial Received] ),
    Cancellation[Priority Bucket] IN { 2, 3 },
    Cancellation[Snapshot Date] = MAX ( Cancellation[Snapshot Date] )
) + 0

```
