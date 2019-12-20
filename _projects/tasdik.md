---
name: tasdik
tools: [Java]
image:
description: Tasdik is bean validation library for core Java / Spring etc.
external_url: 
---

#### What is Tasdik

*Tasdik* means "validation" in **Turkish** language. 

#### What does Tasdik offer?

There is hundred of validation library in Java. 

For example:

- Any version of JSR ( Java Specification Requests )

You can check this site for more detail.

{% include elements/button.html link="https://www.baeldung.com/javax-validation" text="Java Bean Validation Basics" style="outline-dark" %}

Your stack is on *Spring Boot* you are not need to `tasdik`.

 You should use *hibernate validation*. Because there is a lot of advantage hibernate validation in spring boot projects.

**For example:**
1. `@Valid` annotation
2. Easy to create custom validation

```java
@Documented
@Constraint(validatedBy = ContactNumberValidator.class)
@Target( { ElementType.METHOD, ElementType.FIELD })
@Retention(RetentionPolicy.RUNTIME)
public @interface ContactNumberConstraint {
    String message() default "Invalid phone number";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}
```

then;

```java
public class ContactNumberValidator implements
  ConstraintValidator<ContactNumberConstraint, String> {
 
    @Override
    public void initialize(ContactNumberConstraint contactNumber) {
    }
 
    @Override
    public boolean isValid(String contactField,
      ConstraintValidatorContext cxt) {
        return contactField != null && contactField.matches("[0-9]+")
          && (contactField.length() > 8) && (contactField.length() < 14);
    }
 
}
```

```java
class SimpleBean {

    @ContactNumberConstraint
    private String phone;

    // Getter Setter
}
```

 
**But** your stack is not on *Spring Boot*, tasdik `simplify your validation tasks.`

> What do I mean?

Hibernate validation requires a lot of maven dependencies to validation.

If you want to use hibernate validation, you have to import all of these dependencies to your project.

```xml
    <dependency>
        <groupId>org.hibernate.validator</groupId>
        <artifactId>hibernate-validator</artifactId>
        <version>6.0.2.Final</version>
    </dependency>
    <dependency>
        <groupId>org.hibernate.validator</groupId>
        <artifactId>hibernate-validator-annotation-processor</artifactId>
        <version>6.0.2.Final</version>
    </dependency>

    <dependency>
        <groupId>javax.validation</groupId>
        <artifactId>validation-api</artifactId>
        <version>2.0.0.Final</version>
    </dependency>

    <dependency>
        <groupId>javax.el</groupId>
        <artifactId>javax.el-api</artifactId>
        <version>3.0.0</version>
        <scope>provided</scope>
    </dependency>

    <dependency>
        <groupId>org.glassfish</groupId>
        <artifactId>javax.el</artifactId>
        <version>3.0.1-b08</version>
    </dependency>
```











#### How does Tasdik work?

Tasdik uses *the reflection library* for validation.

Design of the project is formed two interfaces. 

















































