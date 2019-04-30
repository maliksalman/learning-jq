#### 3.2 Escapeing & Counting

##### 3.2.1 Escape JSON to a string value

	cat small.json | jq 'tojson'
 
##### 3.2.2 Unescape string value to  JSON

	JSON_STR=$(cat small.json | jq 'tojson')
	echo $JSON_STR | jq 'fromjson'

##### 3.2.3 Count elements in JSON

	cat small.json | jq 'length'
	
Counts key/value pairs if source is an object

	echo '[1, 2, 5]' | jq 'length'

Counts elements if source is an array (see how to count properly before throwing a [Holy Hand Grenade](https://youtu.be/xOrgLj9lOwk?t=40s))

