---
title: 'OD: activities'
date: 'March 08, 2021'
author:
- Arnau Abella
---

# Cypher

1. Return all nodes

```
MATCH (n)
RETURN n
```

2. Return all edges

```
MATCH ()-[e]-()
RETURN e
```

3. Return all neighbour nodes of 'John'

```
MATCH (:{name: 'John'})-[]-(n)
RETURN n
```

4. Return the incident nodes of all edges

```
MATCH (n)-[]-()
RETURN n
```

or

```
MATCH (n1)-[]-(n2)
RETURN n1, n2
```

# Adjacency list vs Incidence list

First adjacency then incidence.

1. Tree

```
[ 1 -> [4]
, 2 -> [4]
, 3 -> [4]
, 4 -> [1,2,3]
]
```

```
e1 :=  (1,4)
e2 :=  (2,4)
e3 :=  (3,4)

[ 1 -> [e1]
, 2 -> [e2]
, 3 -> [e3]
, 4 -> [e1,e2,e3]
]
```

2. CC

```
[ 1 -> [2,4]
, 2 -> [1,3]
, 3 -> [2,4]
, 4 -> [1,3]
]
```

```

e1 :=  (1,2)
e2 :=  (1,4)
e3 :=  (2,3)
e4 :=  (3,4)

[ 1 -> [e1, e2]
, 2 -> [e1, e3]
, 3 -> [e3, e4]
, 4 -> [e2, e4]
]
```

3. Clique

```
[ 1 -> [2,3,4]
, 2 -> [1,3,4]
, 3 -> [1,2,4]
, 4 -> [1,2,3]
]
```

```
e1 :=  (1,2)
e2 :=  (1,3)
e3 :=  (1,4)
e4 :=  (2,4)
e5 :=  (2,3)
e6 :=  (3,4)

[ 1 -> [e1,e2,3]
, 2 -> [e1,e4,e5]
, 3 -> [e2,e5,e6]
, 4 -> [e3,e4,e6]
]
```

Some operations are not possible in adjacency lists. For example, a pattern-match on edge properties (because adjacency don't have information about edges).
This is the reason why neo4j and other graph databases choose to implement incidence lists.
