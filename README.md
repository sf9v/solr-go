![Github Actions](https://github.com/sf9v/solr-go/workflows/test/badge.svg)
[![Coverage Status](https://coveralls.io/repos/github/sf9v/solr-go/badge.svg?branch=main)](https://coveralls.io/github/sf9v/solr-go?branch=main)
[![Go Report Card](https://goreportcard.com/badge/github.com/sf9v/solr-go)](https://goreportcard.com/report/github.com/sf9v/solr-go)

# Solr-go

A [Solr](https://lucene.apache.org/solr) client for [Go](https://golang.org/).

## Example

```go
query := solr.NewQuery().
    QueryParser(solr.NewDisMaxQueryParser("solr rocks")).
    Queries(solr.M{
        "query_filters": []solr.M{
            {
                "#size_tag": solr.M{
                    "field": solr.M{
                        "f":     "size",
                        "query": "XL",
                    },
                },
            },
            {
                "#color_tag": solr.M{
                    "field": solr.M{
                        "f":     "color",
                        "query": "Red",
                    },
                },
            },
        },
    }).
    Facets(
        solr.NewTermsFacet("categories").
            Field("cat").Limit(10),
        solr.NewQueryFacet("high_popularity").
            Query("popularity:[8 TO 10]"),
    ).
    Sort("score").
    Offset(1).
    Limit(10).
    Filter("inStock:true").
    Fields("name price")
```

## Contributing

All contributions are welcome!

## License

MIT
