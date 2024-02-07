---
outline: deep
---
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

## Java Code Template

There are helpers to help you generate Java classes. The example below generates a Java interface; it's
borrowed straight from the XOMDA codebase.

First off all, we start by creating a new `JavaClassWriter`. This special context will assist you with
indenting, tabbing, writing Javadoc and more.

### JavaImportService

Inside a `JavaClassWriter`-instance, there's an instance of a `JavaImportService`. This is a special class
which will assist you with managing class-level imports.

***GenerateEntityTemplate.java***

```java
public class GenerateEntityTemplate extends PackageTemplate {

 @Override
 public void generate(final Entity entity, final TemplateContext context) throws IOException {
  final String pkg = TemplateUtils.getJavaPackage(entity.getPackage());
  final String interfaceName = StringUtils.toPascalCase(entity.getName());
  final String fullyQualifiedName = pkg + "." + interfaceName;

  try (
    final JavaClassWriter ctx = new JavaClassWriter(fullyQualifiedName).withHeaders(
      "// THIS FILE WAS AUTOMATICALLY GENERATED", ""
    );
  ) {
   ctx
     .addDocs(docs -> Optional
       .ofNullable(entity.getDescription())
       .filter(not(String::isBlank))
       .ifPresent(docs::println)
     )
     .println("public interface {0} {", interfaceName).tab(tabbed -> tabbed
       .println()

       // generate the regular attributes
       .forEach(entity::getAttributeList, (final Attribute attribute) -> {
        final String attributeName = StringUtils.toPascalCase(attribute.getName());
        final String fullyQualifiedType = ctx.addImport(TemplateUtils.getJavaType(attribute));
        GetterSetter.create(fullyQualifiedType, attributeName)
          .declareOnly()
          .withJavaDoc(attribute.getDescription())
          .writeTo(tabbed);
       })

       // generate the reverse entity attributes
       .forEach(XOMDAUtils.findReverseEntities(entity), (final Entity e) -> {
        final String attributeName = StringUtils.toPascalCase(e.getName() + " List");
        final CharSequence fullyQualifiedType = WritableContext.format(
          "{0}<{1}>",
          ctx.addImport(List.class),
          ctx.addImport(TemplateUtils.getJavaType(e))
        );
        GetterSetter.create(fullyQualifiedType, attributeName)
          .declareOnly()
          .withJavaDoc(entity.getDescription())
          .writeTo(tabbed);
       }))

     .println("}");

   ctx.writeFile(context.outDir());
  }
 }

}
```
