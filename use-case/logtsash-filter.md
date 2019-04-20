Query the Network Data with threat intel feeds during schema on write

Add below Filter plugin with your Network data processing to query the threat feeds matching.

So, for events that hit this filter (firewall traffic), the "dst_ip" is checked against the minemeld index and checks if the IP address exists within each range. This then adds new fields to the firewall traffic (sources/confidence) and adds a new tag (threatintel_trigger).

```
filter {
    elasticsearch {
        hosts => ["localhost:9200"]
        index => "logstash-threatintel"
        query_template => "/usr/share/logstash/search-minemeld-src.json"
        fields => {
            "sources" => "threatintel_source"
            "confidence" => "threatintel_confidence"
        }
        add_tag => [ "threatintel_trigger" ]
    }
}
```

have the following within /usr/share/logstash/search-minemeld-src.json


```
{
  "size": 1,
  "query": {
    "bool": {
      "filter": [
        { "range": { "firstIP": { "lte": "%{[dst_ip]}" }}} ,
        { "range": { "lastIP": { "gte": "%{[dst_ip]}" }}}
      ]
    }
  },
  "_source": ["sources", "confidence"]
}
```
