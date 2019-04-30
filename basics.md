#### 3.1 Basics

##### 3.1.1 Make JSON pretty

	jq . small.json

or

	cat small.json | jq .
 
##### 3.1.2 Sort the keys while looking pretty

	cat small.json | jq . -S

##### 3.1.3 Test JSON fragment validity

	cat bad.json | jq .

