# tesla-fleet-openapi

## Testing / Viewing the OpenAPI Specification

To test the OpenAPI specification, you can use the following command:

```bash
docker compose up
```

This will start an instance of nginx and the OpenAPI specification will be available at `http://localhost:80/`.

A copy of the site will be available at https://vls29.github.io/tesla-fleet-openapi/ for testing the API online.

## Generating a client

To generate a client to interact with the Tesla Fleet APIs, you can use the OpenAPI Generator.  An example of generating a Java client is shown below:

```bash
docker run --rm -v ${PWD}:/local openapitools/openapi-generator-cli generate -i /local/openapi.yaml -g java -o /local/open-api-generator-output/java-client
```

Or with Maven, something like the following:

```xml
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <version>7.12.0</version>
    <executions>
        <execution>
            <id>TeslaFleetApi</id>
            <goals>
                <goal>generate</goal>
            </goals>
            <configuration>
                <inputSpec>${project.basedir}/src/main/resources/tesla/fleet/spec.yaml</inputSpec>
                <generatorName>java</generatorName>
                <typeMappings>integer=BigInteger,number+double=BigDecimal</typeMappings>
                <importMappings>BigInteger=java.math.BigInteger,BigDecimal=java.math.BigDecimal</importMappings>
                <configOptions>
                    <sourceFolder>src/gen/java/main</sourceFolder>
                    <library>resttemplate</library>
                    <generateClientAsBean>true</generateClientAsBean>
                    <useJakartaEe>true</useJakartaEe>
                    <modelPropertyNaming>original</modelPropertyNaming>
                </configOptions>
                <apiPackage>com.tesla.fleet.remote.client.api</apiPackage>
                <modelPackage>com.tesla.fleet.remote.client.model</modelPackage>
                <invokerPackage>com.tesla.fleet.remote.client</invokerPackage>
                <templateDirectory>${project.basedir}/src/main/resources/openapi-custom-templates/tesla/fleet/</templateDirectory>
            </configuration>
        </execution>
        ...
```
