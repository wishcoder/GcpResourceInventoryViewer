## Here's is a smple BigQuery select statement for fetching assets by location and print set of labels in one column:

```
WITH
  RegionInstances AS(
  SELECT
    SPLIT(name, '/') AS nameComponents,
    resource.data.creationTimestamp AS CREATE_TIME,
    resource.data.status AS STATUS,
    name,
    (
    SELECT
      STRING_AGG(CONCAT(kv.key, ':', kv.value), ', ')
    FROM
      UNNEST(resource.data.labels) AS kv ) AS LABELS,
    SELECT value FROM UNNEST(resource.data.labels) WHERE key = 'app_id') AS app_id,
    SELECT value FROM UNNEST(resource.data.labels) WHERE key = 'component_id') AS component_id,
    SELECT value FROM UNNEST(resource.data.labels) WHERE key = 'environmant') AS environmant
  FROM
    compute_googleapis_com_Instance
  WHERE
    resource.location LIKE '%us-central1%'
    AND resource.data.status = 'RUNNING' )
SELECT
  nameComponents[
OFFSET
  (4)] AS PROJECT,
  nameComponents[
OFFSET
  (6)] AS ZONE,
  nameComponents[
OFFSET
  (8)] AS INSTANCE,
  CREATE_TIME,
  STATUS,
  LABELS
FROM
  RegionInstances
WHERE
  nameComponents[
OFFSET
  (4)] LIKE '%test-proj%'
ORDER BY
  PROJECT,
  ZONE
```
