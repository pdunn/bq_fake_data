#How to use
Packaging that wraps the faker.js file in a way that is compatible with BigQuery as a javascript UDF. 

```
CREATE TEMP FUNCTION entity()
RETURNS STRUCT<name String, age INT64>
LANGUAGE js 
AS """
  var f = getFaker()
  this.val = f.name.findName();
  this.age = (f.random.number() % 78) + 2
  return this;
"""
OPTIONS (
    library=["gs://path/to/bq_fake.js"]
);

SELECT entity().*
FROM `bigquery-public-data.wise_all_sky_data_release.mep_wise`
LIMIT 10
```
