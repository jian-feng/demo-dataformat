# demo-dataformat

Demostrate how to use Camel [DataFormat][1] component for Dynamic Marshal/Unmarshal.

[1]: https://camel.apache.org/components/latest/dataformat-component.html

## How to implement

Step 1. Define dataformat bean as many as you neeed
```xml
<bean id="json1" class="org.apache.camel.component.jackson.JacksonDataFormat">
  <property name="unmarshalType" value="com.redhat.sample.Request"/>
</bean>
```

Step 2. Use <toD> and [Simple language][2] to call [DataFormat] component

```xml
<toD uri="dataformat:${header.dataformat_name}:unmarshal"/>
...
<toD uri="dataformat:${header.dataformat_name}:marshal"/>
``` 

[2]: https://camel.apache.org/components/latest/languages/simple-language.html


## How to run

[CamelRouteUnitTest][3] is the Junit test case. Just run it and see the result.

[3]: src/test/java/com/redhat/sample/CamelRouteUnitTest.java

```sh
cd demo-dataformat
mvn clean test
```

Sample output of unit test:
```console
o.a.camel.spring.SpringCamelContext - Route: dynamic-unmarshal started and consuming from: direct://dynamic-unmarshal
o.a.camel.spring.SpringCamelContext - Route: dynamic-marshal started and consuming from: direct://dynamic-marshal
o.a.camel.spring.SpringCamelContext - Total 2 routes, of which 2 are started
o.a.camel.spring.SpringCamelContext - Apache Camel 2.23.2.fuse-760030-redhat-00001 (CamelContext: camel-context) started in 0.250 seconds
com.redhat.sample.CamelRouteUnitTest - response is com.redhat.sample.Request@22791b75
com.redhat.sample.CamelRouteUnitTest - ********************************************************************************
com.redhat.sample.CamelRouteUnitTest - Testing done: testDynamicUnmarshal(com.redhat.sample.CamelRouteUnitTest)
com.redhat.sample.CamelRouteUnitTest - Took: 0.281 seconds (281 millis)
com.redhat.sample.CamelRouteUnitTest - ********************************************************************************
com.redhat.sample.CamelRouteUnitTest - response is {"field1":"AAA","field2":"111"}
com.redhat.sample.CamelRouteUnitTest - ********************************************************************************
com.redhat.sample.CamelRouteUnitTest - Testing done: testDynamicMarshal(com.redhat.sample.CamelRouteUnitTest)
com.redhat.sample.CamelRouteUnitTest - Took: 0.029 seconds (29 millis)
com.redhat.sample.CamelRouteUnitTest - ********************************************************************************
```
