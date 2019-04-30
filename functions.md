#### 3.3 Functions

##### 3.3.1 Escape JSON to a string value

Sometimes you come across some ugly JSON like `escaped.json`

	cat escaped.json | jq .
	cat escaped.json | jq '.inner | fromjson'
	cat escaped.json | jq '.inner | fromjson | .description | fromjson'

Other times, you want to embed some JSON in some other language - like in a Java variable

	cat small.json | jq 'tojson'
	
##### 3.3.2 Count elements

Counts key/value pairs if source is an object

	cat small.json | jq 'length'
	
Counts elements if source is an array (see how to count properly before throwing a [Holy Hand Grenade](https://youtu.be/xOrgLj9lOwk?t=40s))

	echo '[1, 2, 5]' | jq 'length'


##### 3.3.5 Complex Example

Gets the VPC where the `Name` tag's value is `special-vpc` (for reference: it is at index 21)

	cat large.json | jq '.Vpcs[] | select (has("Tags") and (.Tags | from_entries | .Name)=="special-vpc")'

