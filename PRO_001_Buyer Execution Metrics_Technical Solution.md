# Power Query

Configured Power Query (M) parameters to enable one-click **data source switching** across all tables and automatic environment updates (DEV / STG / PRD) during **report deployment** through Power BI pipelines, once the parameters are configured in the service

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

Summary Fact table * : 1 Dimention table 1 ：* Detail Fact table

Summary Fact table * : 1 Bridge table 1 ：* Detail Fact table

<img width="1551" height="800" alt="image" src="https://github.com/user-attachments/assets/810115fc-6905-4630-bae1-39edd9f09663" />

# Dax

**Cancellation Execution %**

This is the North Star KPI, used to evaluate buyer execution performance.
When there are no unexecuted POs and no POs within the selected scope, the KPI defaults to 100%.

```
DIVIDE

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

**Select Filter**

This measure dynamically generates a filter label based on user selections.
It detects whether a priority is selected and whether the view is limited to unexecuted items, then displays a clear, user-friendly description of **the current filter context**.

```
*CONCATENATEX*

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

**Sorted Cancellation Execution**

When a measure is used for sorting, **ISINSCOPE** ensures that **row-level** values and total-level logic are handled separately, 
preventing total calculations from overriding the values used to rank individual rows.

```
*ISINSCOPE*

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

**Last Week Partial Received (Week1 and No Demand)**

I add **+ 0** to force BLANK results to zero, which ensures consistent numeric output for KPIs, sorting, and conditional formatting.

```
Last Week Partial Received (Week1 and No Demand) =
CALCULATE (
    SUM ( Cancellation[Partial Received] ),
    Cancellation[Priority Bucket] IN { 2, 3 },
    Cancellation[Snapshot Date] = MAX ( Cancellation[Snapshot Date] )
) + 0

```
