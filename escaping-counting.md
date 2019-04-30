#### 3.3 Functions

##### 3.3.1 Escape JSON to a string value

	cat small.json | jq 'tojson'
 
or

	JSON_STR=$(cat small.json | jq 'tojson')
	echo $JSON_STR | jq 'fromjson'

##### 3.3.2 Count elements in JSON

	cat small.json | jq 'length'
	
Counts key/value pairs if source is an object

	echo '[1, 2, 5]' | jq 'length'

Counts elements if source is an array (see how to count properly before throwing a [Holy Hand Grenade](https://youtu.be/xOrgLj9lOwk?t=40s))

##### 3.3.5 Complex Example

Gets the VPC where the `Name` tag's value is `special-vpc` (for reference: it is at index 21)

	cat large.json | jq '.Vpcs[] | select (has("Tags") and (.Tags | from_entries | .Name)=="special-vpc")'

