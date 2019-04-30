## 3. Usage

The full manual is available at [https://stedolan.github.io/jq/manual/](https://stedolan.github.io/jq/manual/). The two basic styles of usage are:

```jq <jq-expression> <file-containing-json> [optional-flags]```

Use this style when the JSON content is already available in a file

```some-program-that-produces-json | jq <jq-expression> [optional-flags]```

Use this style when the JSON is being generated as an output of another command (like `curl`) 


1. [Basics](basics.md)
2. [Escaping & counting](escaping-counting.md)
3. [Selecting Elements](selecting.md)
4. [Transforming structure](transforming.md)
