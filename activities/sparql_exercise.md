# Example of RDF(S) Graph 

> I am assuming inference rules (with entailment regime)

- a) Get the name of all actors that participated in Juno

``` sparql
PREFIX mov: <www.example.com/movies/>
SELECT ?name
WHERE
{
    :juno mov:stars ?actor.
    ?actor mov:name ?name.
}
```

``` sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX mov: <www.example.com/movies/>
SELECT ?name
WHERE {
  ?juno a Movie .
  ?juno mov:title ?title
  FILTER regex(?title, "[j|J]uno")
  ?juno mov:stars/mov:name ?name
}
```

- b) Get the name of all directors

``` sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX mov: <www.example.com/movies/>
SELECT ?name
WHERE {
  ?director a Director .
  ?director mov:name ?name
}
```

- c) Get the name of all persons

Without inference:

``` sparql
PREFIX mov: <www.example.com/movies/>
SELECT ?name
WHERE {
  ?x mov:directs ?y .
  ?x mov:name ?name
}
UNION {
  ?x mov:stars ?y .
  ?x mov:name ?name
}
```

With inference:


``` sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX mov: <www.example.com/movies/>
SELECT ?name
WHERE {
  ?person rdfs:class Person .
  ?person mov:name ?name
}
```

- d) Get the title of all movies

With inference:

``` sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX mov: <www.example.com/movies/>
SELECT ?title
WHERE {
  ?movie a Movie .
  ?movie mov:title ?title
}
```
