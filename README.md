## 1. Introduction

JQ is a "filter" style CLI program that can work with JSON on the command line or in shell scripts. 

## 2. Installtion

JQ is distributed as a single binary file for all platforms so installation is as simple as putting it on your execution `$PATH`. Donwload it from [https://stedolan.github.io/jq/download/](https://stedolan.github.io/jq/download/). On some platforms, installation is easier than the instructions above. 

#### 2.1 Linux

	sudo apt-get install jq

#### 2.2 MacOS

	brew install jq

## 3. Usage

The full manual is available at [https://stedolan.github.io/jq/manual/](https://stedolan.github.io/jq/manual/). The two basic styles of usage are:

```jq <jq-expression> <file-containing-json> [optional-flags]```

Use this style when the JSON content is already available in a file

```some-program-that-produces-json | jq <jq-expression> [optional-flags]```

Use this style when the JSON is being generated as an output of another command (like `curl`) 

Here are some sample usages of `jq`:

#### 3.1 Make JSON pretty

	jq . small.json

or

	cat small.json | jq .
 
#### 3.2 Sort the keys while looking pretty

	cat small.json | jq . -S

#### 3.3 Test JSON fragment validity

	cat bad.json | jq .

#### 3.4 Escape JSON to a string value

	cat small.json | jq 'tojson'
 
#### 3.5 Unescape string value to  JSON

	JSON_STR=$(cat small.json | jq 'tojson')
	echo $JSON_STR | jq 'fromjson'

#### 3.6 Count elements in JSON

	cat small.json | jq 'length'
	
Counts key/value pairs if source is an object

	echo '[1, 2, 5]' | jq 'length'

Counts elements if source is an array (see how to count properly before throwing a [Holy Hand Grenade](https://youtu.be/xOrgLj9lOwk?t=40s))

#### 3.7 Select element(s) from JSON

	cat small.json | jq '.Tags'

Gets the whole `Tags` array

	cat small.json | jq '.VpcId'
	cat small.json | jq '.VpcId' -r

Gets the `VpcId` attribute value

	cat large.json | jq '.Vpcs[0]'

Gets the first VPC

	cat large.json | jq '.Vpcs[-1]'

Gets the last VPC

	cat large.json | jq '.Vpcs[0].VpcId' -r

Gets `VpcId` of the first VPC

	cat large.json | jq '.Vpcs[0].Tags' | jq 'from_entries' | jq '.Name' -r
	
or

	cat large.json | jq '.Vpcs[0].Tags | from_entries | .Name' -r

Gets the `Name` tag's value of the first VPC

	cat large.json | jq '.Vpcs[] | select (has("Tags") and (.Tags | from_entries | .Name)=="special-vpc")'

Gets the VPC where the `Name` tag's value is `special-vpc` (for reference: it is at index 21)

#### 3.8 Transform JSON structure

	cat small.json | jq '{ VpcId, CidrBlock }'
	
Simple filtering of the key/value pairs

	cat small.json | jq '{ id: .VpcId, address: .CidrBlock }'

Renaming the keys

	cat small.json | jq '{ id: .VpcId, address: .CidrBlock, tags: (.Tags | from_entries) }'

Renaming the keys and converting key/value array into object
