
Create database "Airport"
```sql
CREATE CONSTRAINT ON (a: Airport) ASSERT a.id IS UNIQUE;
CREATE INDEX ON :Airport(Name);
CREATE INDEX ON :Airport(iata);
CREATE INDEX ON :Airport(location);
```


Loads the data from url
```sql
WITH "https://r.neo4j.com/airports" AS url
CALL apoc.load.jsonArray(url) YIELD value
MERGE (a: Airport {id:value.`Airport ID`})
SET a += apoc.map.clean(apoc.convert.toMap(value),
		 ["Airport ID", "Latitude", "Longitude", "DST", "Timezone", "destinations", "IATA/FAA"], ["", NULL]),
	a.iata = value.`IATA/FAA`, a.DST = toInteger(value.DST),
	a.Timezone = toInteger(value.Timezone),
	a.location = point({latitude:toFloat(value.Latitude), longitude: toFloat(value.Longitude)})
WITH *
UNWIND value.destinations as dest
MERGE (b:Airport {id:dest})
MERGE (a)-[:CONNECTS]-(b);
```

Calculates the distance from airports
```sql
MATCH (a: Airport)-[r:CONNECTS]->(b:Airport)
SET r.distance = distance(a.location, b.location) return a,b,r
```
