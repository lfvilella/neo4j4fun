# Scenario

<img width="843" alt="Screen Shot 2022-02-22 at 21 35 21" src="https://user-images.githubusercontent.com/45940140/155243392-25c61a64-91bc-4126-8207-73833f9ffe9d.png">

# Building with Cypher

## Creating

```
CREATE (p:Person {name: "Jennifer"})-[rel:LIKES]->(g:Technology {type: "Graphs"})
```

```
MATCH (jennifer:Person {name: "Jennifer"})
CREATE (p:Person {name: "Michael"})<-[rel:IS_FRIENDS_WITH {since: 2018}]-(jennifer)
```

```
MATCH (jennifer:Person {name: "Jennifer"})
CREATE (jennifer)-[rel:WORKS_FOR]->(p:Company {name: "Neo4j"})
```

## Queries

```
MATCH (p:Person)<-[:LIKES]-(t:Technology) RETURN p, t  # Invalid query: Tech no likes person. Person likes tech.
MATCH (p:Person)-[:LIKES]-(t:Technology)  # works without specify the relationship direction
MATCH (p:Person)-[:LIKES]->(t:Technology)  # specifing relationship direction
```

Adding more node to assert queries
```
MATCH (jennifer:Person {name: "Jennifer"})
CREATE (tod:Person {name: "Tod"})-[rel:IS_FRIENDS_WITH]->(jennifer)
CREATE (ana:Person {name: "Ana"})-[re:IS_FRIENDS_WITH]->(jennifer)
```

Getting all jennifer friends
```
MATCH (jennifer:Person {name: "Jennifer"})
MATCH (jennifer)-[:IS_FRIENDS_WITH]-(persons:Person)
RETURN persons
```

Getting old jennifer friends
```
MATCH (jennifer:Person {name: "Jennifer"})
MATCH (jennifer)-[relationship:IS_FRIENDS_WITH]-(persons:Person)
WHERE relationship.since <= 2018
RETURN persons
```
