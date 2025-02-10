# hisonjv [![Maven Central](https://img.shields.io/maven-central/v/io.github.hisondev/hisonjv.svg?label=Maven%20Central)](https://mvnrepository.com/artifact/io.github.hisondev/hisonjv)

hisonjv is a comprehensive library that combines the functionalities of `api-link`, `utils`, and `data-model` to provide a powerful and streamlined development experience for Java and Spring-based projects. By incorporating these libraries, `hisonjv` enables efficient data communication, simplified API management, and practical utility functions for everyday programming tasks.

## Introduction

The `hisonjv` project integrates the following libraries:  

- **`data-model`**: A library designed to simplify data communication in Spring applications. It includes the `DataWrapper` and `DataModel` classes, which streamline the process of data transfer and management. For enhanced and convenient front-end and server communication, this library can be used in conjunction with `dataModel.min.js` from [hison-js](https://github.com/hisondev/hison-js).  
- **`api-link`**: A novel solution for Spring projects, aimed at eliminating the need for individual controllers. It allows developers to invoke service layer methods using a single `cmd` value, simplifying workflow and improving productivity.  
- **`utils`**: A set of utility functions for common Java tasks such as string manipulation, date and time operations, and number formatting.  

---

## Getting Started

### Prerequisites
Before you start using `hisonjv`, make sure you have the following installed on your system:
- Java Development Kit (JDK) 8 or higher
- Apache Maven (for building the project)

### Installation
You can add the `hisonjv` library to your project by including the following dependency in your Maven `pom.xml` file:

```xml
<dependency>
    <groupId>io.github.hisondev</groupId>
    <artifactId>hisonjv</artifactId>
    <version>1.0.0</version>
</dependency>
```

---

## Usage

### Data-Model Integration
The `data-model` library provides a set of utilities for managing structured data in Spring applications. It offers classes like `DataWrapper` and `DataModel` to handle data transfer and serialization seamlessly.

**Example of Using DataWrapper and DataModel:**
```java
import io.github.hisondev.datamodel.DataWrapper;
import io.github.hisondev.datamodel.DataModel;

DataWrapper wrapper = new DataWrapper();
wrapper.add("key1", "value1");

DataModel model = new DataModel();
model.setColumns(Arrays.asList("column1", "column2"));
model.addRow(Arrays.asList("value1", "value2"));
```

**Customizing Data Conversion:**
You can extend `DataConverterDefault` to implement custom data conversion logic.
```java
import io.github.hisondev.datamodel.converter.DataConverterDefault;
import io.github.hisondev.datamodel.converter.DataConverterFactory;

public class CustomDataConverter extends DataConverterDefault {
    public static void register() {
        DataConverterFactory.setCustomConverter(new CustomDataConverter());
    }

    @Override
    public Object convert(Object data) {
        // Custom conversion logic
        return super.convert(data);
    }
}
```

---

### API-Link Integration
The `api-link` library helps simplify your Spring application's controller layer by allowing you to map a single `cmd` value to service methods. Here's how to get started:

1. **Define your service methods:**

```java
import org.springframework.stereotype.Service;
import io.github.hisondev.datamodel.DataWrapper;

@Service
public class MyService {
    public void myMethod(DataWrapper data) {
        // Your business logic here
    }
}
```

2. **Configure the `ApiLink` controller:**

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ApiLinkApplication {
    public static void main(String[] args) {
        SpringApplication.run(ApiLinkApplication.class, args);
    }
}
```

3. **Make API Calls:**

```bash
curl -X POST http://localhost:8080/api -d '{"cmd": "myService.myMethod", "data": {...}}' -H "Content-Type: application/json"
```

---

### Utils Library Examples
The `utils` library provides handy methods for string, date, and number manipulation.

**String Utilities:**
```java
import io.github.hisondev.utils.Utils;

boolean isAlpha = Utils.isAlpha("HelloWorld");
String paddedString = Utils.getLpad("123", "0", 5);
```

**Date Utilities:**
```java
String sysDatetime = Utils.getSysDatetime();
String newDate = Utils.addDate("2023-06-09", 5);
int lastDay = Utils.getLastDay("2023-06");
```

**Number Utilities:**
```java
double roundedNumber = Utils.getRound(123.456);
int byteLength = Utils.getByteLength("Hello World");
```

---

## Configuration
You can customize certain behaviors in the `utils` library by creating a `hison-utils-config.properties` file in your project's resources directory. Example properties:

```properties
date.formatter=dd/MM/yyyy
datetime.formatter=dd/MM/yyyy HH:mm:ss
number.formatter=#,##0.#####
```

---

## Contributing
Contributions are welcome! If you have any ideas, suggestions, or bug reports, please open an issue or submit a pull request on GitHub. Make sure to follow the project's code style and add tests for any new features or changes.

---

## License
MIT License

---

## Authors
**Hani Son**  
hison0319@gmail.com