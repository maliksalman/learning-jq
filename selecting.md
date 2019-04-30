#### 3.2 Selecting elements

Gets the whole `Tags` array

	cat small.json | jq '.Tags'

Gets the `VpcId` attribute value

	cat small.json | jq '.VpcId'
	cat small.json | jq '.VpcId' -r

Gets the first VPC

	cat large.json | jq '.Vpcs[0]'

Gets the last VPC

	cat large.json | jq '.Vpcs[-1]'

Gets `VpcId` of the first VPC

	cat large.json | jq '.Vpcs[0].VpcId' -r


##### 3.2.2 Pipes

Gets the `Name` tag's value of the first VPC

	cat large.json | jq '.Vpcs[0].Tags' | jq 'from_entries' | jq '.Name' -r
	
or

	cat large.json | jq '.Vpcs[0].Tags | from_entries | .Name' -r
