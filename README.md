OLAP Facet Plugin for Elasticsearch
===================================

This plugin provides a facet for [Elasticsearch](http://www.elasticsearch.org/) to aggregate documents by a set of numeric fields. The aggregation is done across time dimension and additional dimensions. The built-in histogram facet in Elasticsearch can only perform aggregation along the time dimension so multiple requests need to be issued to aggregate documents along multiple dimensions. The goal of this plugin is to perform all the aggregation in a single request to improve performance.

To install the plugin, run:

```
bin/plugin --url file:///opt/bg/analytics/src/java/src/olap-plugin/target/releases/olap-plugin-1.0-SNAPSHOT-plugin.zip --install olap-plugin
```


Versions
--------

<table>
	<thead>
		<tr>
			<th>olap-plugin</th>
			<th>elasticsearch</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>0.0.1 -> master</td>
			<td>0.90.6</td>
		</tr>
	</tbody>
</table>


Parameters
----------

<table>
	<tbody>
		<tr>
			<th>field</th>
			<td>The name of a field of numeric type.</td>
		</tr>
		<tr>
      <th>interval</th>
      <td>Time interval. Supported intervals are day, week, month, and year.</td>
    </tr>
	</tbody>
</table>


Example
-------

Query:

```javascript
{
    "query" : { "term": { "log_type": "access" }
    "facets" : {
        "request_bytes_by_weeks" : { 
            "group_by": {
                "field" : "request_bytes",
                "interval" : "week"
            }
        }
    }
}
```

Result:

```javascript
{
    ...
    "facets" : {
      "request_bytes_by_weeks" : {
      "_type" : "group_by",
      "entries" : [ {
        "value" : 813.0
      }, {
        "value" : 9139.0
      } ]
    }
}
```


License
-------

```

Copyright 2013-2014 BitGlss, Inc.

```
