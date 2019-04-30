#### 3.4 Transforming structure

Simple filtering of the key/value pairs

	cat small.json | jq '{ VpcId, CidrBlock }'
	
Renaming the keys

	cat small.json | jq '{ id: .VpcId, address: .CidrBlock }'

Renaming the keys and converting key/value array into object

	cat small.json | jq '{ id: .VpcId, address: .CidrBlock, tags: (.Tags | from_entries) }'

