# msticpy - M365D registry_key_alerts
M365D - registry_key_alerts - Lists alerts associated with a specified registry key
```
  registry_key_alerts:
    description: Lists alerts associated with a specified registry key
    metadata:
    args:
      query: '
        {table}
        | where Timestamp >= datetime({start})
        | where Timestamp <= datetime({end})
        | join kind=inner (AlertEvidence
        | where Timestamp >= datetime({start})
        | where Timestamp <= datetime({end})) on AlertId
        | where EntityType =~ "RegistryValue"
        | where RegistryKey =~ "{key_name}"
        {add_query_items}'
    parameters:
      key_name:
        description: The Registry key name
        type: str     
```
> **GitHub** : msticpy/msticpy/data/queries/m365d/[kql_mdatp_alerts.yaml](https://github.com/microsoft/msticpy/blob/main/msticpy/data/queries/m365d/kql_mdatp_alerts.yaml)

## M365D - registry_key_alerts - Lists alerts associated with a specified registry key

```
from msticpy.data.data_providers import QueryProvider

md_prov = QueryProvider("M365D")

md_prov.connect()

md_prov.M365D.registry_key_alerts(start=-30, key_name=r"software\\policies\\microsoft\\windows defender")
```
![image](https://user-images.githubusercontent.com/120234772/221597336-44698318-9cdb-4f23-92c4-93371c6c2abe.png)