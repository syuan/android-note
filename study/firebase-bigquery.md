

## Firebase Bigquery

To open Bigquery from firebase, choose Project Overview → Settings → Integration → BigQuery → manage


```sql
SELECT * FROM [project table] WHERE is_fatal = false
```

```sql
SELECT COUNT(event_id), issue_title, issue_subtitle FROM [project table] where is_fatal = false AND DATE(event_timestamp) >= DATE_ADD(CURRENT_DATE(), INTERVAL -30 DAY) GROUP BY issue_title, issue_subtitle
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE4Mzg3MzEzMyw3MzA5OTgxMTZdfQ==
-->