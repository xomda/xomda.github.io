# Code Templates

The code templates can be used to generate code out of your Object Model.
Examples can be java interfaces and classes, but also configuration files (like Liquibase changesets) or even documentation.

Below is a simple implementation of a template:

***ExampleTemplate.java***

```java
import org.xomda.core.template.Template;
import org.xomda.core.template.TemplateContext;

public class TestTemplate implements Template<Object> {

    @Override
    public void generate(Object o, TemplateContext ctx) {
        System.out.println("It works!");
    }
}
```

The templates should implement the `org.xomda.core.template.Template` interface, provided by XOMDA.
