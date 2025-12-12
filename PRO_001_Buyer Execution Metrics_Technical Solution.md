# Power Query

## Set up M parameter

### ServerName
```
"Server url" meta [IsParameterQuery=true, List={"dsn=SnowflakeDEV", "dsn=SnowflakeSTG", "dsn=SnowflakePRD", "Server url"}, DefaultValue="Server url", Type="Text", IsParameterQueryRequired=true]
```
### Warehouse
```
"WH_DEV" meta [IsParameterQuery=true, List={"WH_DEV", "WH_STG", "WH_PRD"}, DefaultValue="WH_DEV", Type="Text", IsParameterQueryRequired=true]
```

### Database
```
"DEV_BI" meta [IsParameterQuery=true, List={"DEV", "DEV_BI", "STG", "PRD"}, DefaultValue="DEV_BI", Type="Text", IsParameterQueryRequired=true]
```

### Role
```
"xxxx_D_BI" meta [IsParameterQuery=true, List={"xxxx_D_BI", "xxxx_S_BI", "xxxx_P_BI"}, DefaultValue=..., Type="Text", IsParameterQueryRequired=true]
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

# Data Model 

<img width="1551" height="800" alt="image" src="https://github.com/user-attachments/assets/810115fc-6905-4630-bae1-39edd9f09663" />

