# OpenAPI Generator Setup

To begin using the OpenAPI Generator, follow these steps:

1. Install or download the latest [OpenAPI Generator JAR file](https://github.com/OpenAPITools/openapi-generator#1---installation):

   ```shell
   wget https://repo1.maven.org/maven2/org/openapitools/openapi-generator-cli/6.2.1/openapi-generator-cli-6.2.1.jar -O .openapi/generator/openapi-generator-cli.jar
   ```

2. Set the API version as an environmental variable:

   ```shell
   API_VERSION="v1.39.0"
   ```

3. Download the specified version of the Meraki OpenAPI spec:

   ```shell
   wget https://github.com/meraki/openapi/archive/refs/tags/$API_VERSION.zip && unzip -j $API_VERSION.zip '*/spec3.json'
   ```
   Note: *A few API endpoints had to be manually removed from the spec to avoid generator errors. Both the modified `spec3.json` and the original are included in this repository.*


4. Remove any existing client code:

   ```shell
   rm -rf proto/
   ```

5. Run the code generator JAR:

   ```shell
   java -jar .openapi/generator/openapi-generator-cli.jar generate \
     -i spec3.json \
     -g protobuf-schema \
     -o ${PWD}/proto \
     -p enumClassPrefix=true \
     -p structPrefix=true
   ```

6. Cleanup the build files:

   ```shell
   rm $API_VERSION.zip
   ```

You are now set up to generate protocol buffer schema files based on the Meraki OpenAPI specification.