# FlaskTFGensonDocker

This is a dirty little form based app that runs a modified version of Genson, called TFGenson, through a Python Flask front end, in a Docker container.

*Note: Ensure your working directory is fine in the Docker file*

```bash
git clone https://github.com/davedotdev/flasktfgensondocker.git && cd flasktfgensondocker
docker build -t flaskgenson .
docker run -it -d -p 5000:5000 --name genson flaskgenson
```

You can then run HTTP POSTs against the Flask app like so:

```bash
curl -X POST \
  http://TFGensonFlaskIPAddress:5000/ \
  -H 'cache-control: no-cache' \
  -H 'content-type: multipart/form-data' \
  -F 'payload={"resource":{"canonical":{"config-group-name":{"string1": "foo44", "bool1": false, "float1": 46, "int1": 48, "liststring9": ["bar49", "barbar49"], "map1": {"foo50": "bar50", "foofoo50": "barbar50"}, "listset3": [{"bool3": false, "float3": 52, "int3": 53, "string3": "foo54"}], "set2": {"bool2": false, "float2": 56, "int2": 57, "string2": "foo58"}, "setnested4": {"int4": 59, "string4": "foo60", "bool4": false, "float4": 62, "listset8": [{"bool8": false, "float8": 64, "int8": 65, "string8": "foo66"}], "set5": {"bool5": false, "float5": 68, "int5": 69, "string5": "foo70", "listset7": [{"bool7": false, "float7": 72, "int7": 73, "string7": "foo74"}], "set6": {"bool6": false, "float6": 76, "int6": 77, "string6": "foo78"}}}}}}}'
```

The only difference between this version of Genson and the original [Wolverdude Genson](https://github.com/wolverdude/GenSON), is that this one ensures only the first three keys are required, the rest are not. This is for a specific type of schemas (for Terraform) and may not suite your use case.

The code for the TFGenson is here: [https://github.com/davedotdev/tfgenson](https://github.com/davedotdev/tfgenson)
