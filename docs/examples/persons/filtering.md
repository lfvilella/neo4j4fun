# Scenario

![Screen Shot 2022-02-23 at 23 59 59](https://user-images.githubusercontent.com/45940140/155449408-99f61e86-9036-4361-96d2-6188eac6de22.png)

# Building with Cypher

## Creating

```
CREATE (john:Person {name: "John"})-[likes1:LIKES]->(graphs:Technology {type: "Graphs"}),
(john)-[likes2:LIKES]->(micro_services:Technology {type: "Micro Services"}),
(john)-[works_for1:WORKS_FOR {start_year: 2017}]->(xyz:Company {name: "XYZ"}),
(john)-[is_friend1:IS_FRIENDS_WITH {since: 2000}]->(saily:Person {name: "Saily"}),

(saily)-[likes3:LIKES]->(micro_services),
(saily)-[likes4:LIKES]->(graph_ql:Technology {type: "GraphQL"}),
(saily)-[works_for2:WORKS_FOR {start_year: 2015}]->(dummy_company:Company {name: "Dummy Company"}),
(saily)-[is_friend2:IS_FRIENDS_WITH {since: 2000}]->(mark:Person {name: "Mark"}),

(mark)-[likes5:LIKES]->(graphs),
(mark)-[likes6:LIKES]->(micro_services),
(mark)-[likes7:LIKES]->(graph_ql),
(mark)<-[is_friend3:IS_FRIENDS_WITH {since: 2002}]-(john),

(joe:Person {name: "Joe"})-[likes8:LIKES]->(graphs),
(joe)-[works_for3:WORKS_FOR]->(company_fake:Company {name: "Company Fake"})
```


## Filtering

```
MATCH (p: Person)
WHERE NOT p.name = 'John'
RETURN p
```

```
MATCH (p: Person)
WHERE p.name CONTAINS 'a'
RETURN p
```

```
MATCH (p:Person)
WHERE p.name =~ 'Jo.*'
RETURN p.name
```

```
MATCH (c: Company)
WHERE c.name STARTS WITH 'X'
RETURN c
```

```
MATCH (p: Person)-[rel:WORKS_FOR]->(c:Company)
WHERE EXISTS(rel.start_year)
RETURN p, rel, c
```

```
MATCH (p: Person)-[rel:WORKS_FOR]->(c:Company)
WHERE rel.start_year > 2016
RETURN p, rel, c
```

```
MATCH (p: Person)-[rel:LIKES]->(t:Technology)
WHERE NOT t.type = "Graphs"
RETURN p, rel, t
```
