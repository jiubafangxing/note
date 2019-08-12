```
GET /bank/_search
{
  "query": {
    "bool": {
      "must": { "match_all": {} },
      "filter": {
        "range": {
          "balance": {
            "gte": 20000,
            "lte": 30000
          }
        }
      }
    }
  }
}
```

 如果使用filter 并不影响socre分数的判定 ，filter目前来看只能用于bool里面的复杂查询