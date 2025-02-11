# hisonjv [![Maven Central](https://img.shields.io/maven-central/v/io.github.hisondev/hisonjv.svg?label=Maven%20Central)](https://mvnrepository.com/artifact/io.github.hisondev/hisonjv)

hisonjv is a comprehensive library that combines the functionalities of `api-link`, `utils`, and `data-model` to provide a powerful and streamlined development experience for Java and Spring-based projects. By incorporating these libraries, `hisonjv` enables efficient data communication, simplified API management, and practical utility functions for everyday programming tasks.

## Introduction

The `hisonjv` project integrates the following libraries:  

- **`data-model`**: A library designed to simplify data communication in Spring applications. It includes the `DataWrapper` and `DataModel` classes, which streamline the process of data transfer and management. For enhanced and convenient front-end and server communication, this library can be used in conjunction with `dataModel.min.js` from [hison-js](https://github.com/hisondev/hison-js).  
- **`api-link`**: A novel solution for Spring projects, aimed at eliminating the need for individual controllers. It allows developers to invoke service layer methods using a single `cmd` value, simplifying workflow and improving productivity.  
- **`utils`**: A set of utility functions for common Java tasks such as string manipulation, date and time operations, and number formatting.  


# 1. data-model [![Maven Central](https://img.shields.io/maven-central/v/io.github.hisondev/data-model.svg?label=Maven%20Central)](https://mvnrepository.com/artifact/io.github.hisondev/data-model)
A library designed to simplify data communication in Spring applications. Primarily featuring the DataWrapper and DataModel classes to streamline the process of data transfer and management.

## Introduction
The `data-model` library is designed to simplify data communication in Spring applications. It includes the `DataWrapper` and `DataModel` classes, which streamline the process of data transfer and management.

For enhanced and convenient front-end and server communication, this library can be used in conjunction with `dataModel.min.js` from [hison-js](https://github.com/hisondev/hison-js).

## Getting Started
To start using the `data-model` library in your project, follow the installation and usage instructions below.

### Prerequisites
Before you can use the `data-model` library, you need to have the following software installed on your system:
- Java Development Kit (JDK) 8 or higher
- Apache Maven (for building the project)

### Installation
You can add the `data-model` library to your project by including the following dependency in your Maven `pom.xml` file:

```xml
<dependency>
    <groupId>io.github.hisondev</groupId>
    <artifactId>data-model</artifactId>
    <version>1.0.7</version>
</dependency>
```

## Usage
### DataWrapper and DataModel Utilities
```java
import io.github.hisondev.datamodel.DataWrapper;
import io.github.hisondev.datamodel.DataModel;

// Example of using DataWrapper
DataWrapper wrapper = new DataWrapper();
wrapper.add("key1", "value1");

// Example of using DataModel
DataModel model = new DataModel();
model.setColumns(Arrays.asList("column1", "column2"));
model.addRow(Arrays.asList("value1", "value2"));
```

### Customizing Data Conversion
The `data-model` library allows you to customize data conversion by extending the `DataConverterDefault` class. Customizing data conversion is essential when the default conversion logic does not meet the specific needs of your application. For example, you may need to handle special data formats or apply specific business rules during the conversion process.

Here is an example of how to create and register a custom data converter:

1. **Create a custom data converter:**
Define a class that extends `DataConverterDefault` and override necessary methods for customization.

```java
import io.github.hisondev.datamodel.converter.DataConverterDefault;
import io.github.hisondev.datamodel.converter.DataConverterFactory;

public class CustomDataConverter extends DataConverterDefault {
    public static void register() {
        DataConverterFactory.setCustomConverter(new CustomDataConverter());
    }

    // Override methods for custom conversion logic
    @Override
    public Object convert(Object data) {
        // Custom conversion logic
        return super.convert(data);
    }
}
```

2. **Register the custom converter in your application:**
Ensure that the custom converter is registered when your Spring application starts.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        CustomDataConverter.register();
        SpringApplication.run(DemoApplication.class, args);
    }
}
```
***This setup allows you to customize how data is converted throughout your application by providing your own implementation of the DataConverterDefault class.***

### DataModelDeserializer and DataModelSerializer
The `DataModelDeserializer` and `DataModelSerializer` classes are used to convert data between the JSON format (used for communication between the front end and back end) and the `DataModel` object format used within your application. This allows for seamless data exchange in a structured format.

Here is an example of how these classes can be utilized to serialize and deserialize data:

Serialization:
```java
import io.github.hisondev.datamodel.DataModel;
import io.github.hisondev.datamodel.model.DataModelSerializer;
import com.fasterxml.jackson.databind.ObjectMapper;

// Create a DataModel instance
DataModel model = new DataModel();
model.setColumns(Arrays.asList("column1", "column2"));
model.addRow(Arrays.asList("value1", "value2"));

// Serialize DataModel to JSON
ObjectMapper mapper = new ObjectMapper();
String jsonString = mapper.writeValueAsString(model);
System.out.println("Serialized JSON: " + jsonString);
```

Deserialization:
```java
import io.github.hisondev.datamodel.DataModel;
import io.github.hisondev.datamodel.model.DataModelDeserializer;
import com.fasterxml.jackson.databind.ObjectMapper;

// JSON string received from the front end
String jsonString = "{\"columns\":[\"column1\",\"column2\"],\"rows\":[[\"value1\",\"value2\"]]}";

// Deserialize JSON to DataModel
ObjectMapper mapper = new ObjectMapper();
DataModel model = mapper.readValue(jsonString, DataModel.class);
System.out.println("Deserialized DataModel: " + model);
```
***By using `DataModelSerializer` and `DataModelDeserializer`, you can ensure that the data structure remains consistent and easily manageable across different layers of your application. This is particularly useful for handling complex data interactions in modern web applications.***


# 2. api-link [![Maven Central](https://img.shields.io/maven-central/v/io.github.hisondev/api-link.svg?label=Maven%20Central)](https://mvnrepository.com/artifact/io.github.hisondev/api-link)
API-Link is a novel solution for Spring projects, aimed at streamlining development by eliminating the need for individual controllers. It allows developers to use a single 'cmd' value to invoke service layer methods, simplifying workflow and boosting productivity.

## Introduction
This project, titled "ApiLink", is a novel solution designed to streamline the development process in Spring projects. It primarily aims to eliminate the need for developers to create individual controllers. Instead, ApiLink enables a more efficient approach by allowing developers to invoke service layer methods through a single 'cmd' value. This approach significantly simplifies the development workflow and enhances productivity.

Additionally, ApiLink incorporates support for caching in WebSocket, relying on the Spring Boot WebSocket dependency. This feature is particularly beneficial for real-time applications where performance and efficiency are crucial. Moreover, the project offers a customizable handler, providing users with the flexibility to tailor the WebSocket behavior according to their specific requirements.

The overarching goal of ApiLink is to provide a convenient, efficient, and flexible tool for developers working on Spring projects, making the development process more streamlined and effective.

For enhanced and convenient front-end and server communication, this library can be used in conjunction with `apiLink.min.js` from [hison-js](https://github.com/hisondev/hison-js).

## Getting Started
To start using the `api-link` library in your project, follow the installation and usage instructions below.

### Prerequisites
Before you can use the `api-link` library, you need to have the following software installed on your system:
- Java Development Kit (JDK) 8 or higher
- Apache Maven (for building the project)

### Installation
You can add the `api-link` library to your project by including the following dependency in your Maven `pom.xml` file:

```xml
<dependency>
    <groupId>io.github.hisondev</groupId>
    <artifactId>api-link</artifactId>
    <version>1.0.2</version>
</dependency>
```

## Usage
### Basic Setup
The api-link library allows you to simplify your Spring application's controller layer. Here's how to set it up:

1. **Define your service methods:**
Create api controller that you want to expose through the `api-link`
```java
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.example.demo.common.api.controller.ApiLink;

@RestController
@RequestMapping("/hison-api-link")
public class ApiController extends ApiLink{
}
```

2. **Create a custom data converter:**
Define a class that extends `DataConverterDefault` and override necessary methods for customization.

```java
import org.springframework.stereotype.Service;

@Service
public class MyService {
    public void myMethod(DataWrapper data) {
        // Your business logic here
    }
}
```

3. **Configure the API Link controller:**
Set up the `ApiLink` controller to handle HTTP requests and invoke your service methods.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```
4. **Making API Calls**
To call a service method via the `api-link`, send an HTTP request with the 'cmd' parameter specifying the service and method names.

```java
package com.example.demo.biz.member.service;

import org.springframework.stereotype.Service;
import org.springframework.web.bind.annotation.RequestBody;
import com.example.demo.common.data.wrapper.DataWrapper;

@Service
public class MemberService {
    public DataWrapper getMember(@RequestBody DataWrapper dw) {
        // Your business logic here
        return dw;
    }
}
```

```bash
curl -X POST http://localhost:8080/api -d '{"cmd": "myService.myMethod", "data": {...}}' -H "Content-Type: application/json"
```
## Customizing API Handler
You can customize how the API requests are handled by implementing your own ApiHandler.

1. **Create a custom API handler:**
Extend the ApiHandlerDefault class and override its methods.

```java
import io.github.hison.api.handler.ApiHandlerDefault;
import io.github.hison.api.handler.ApiHandlerFactory;

public class CustomApiHandler extends ApiHandlerDefault {
    public static void register() {
        ApiHandlerFactory.setCustomHandler(new CustomApiHandler());
    }

    @Override
    public DataWrapper handle(DataModel dataModel, HttpServletRequest request) {
        // Custom handling logic
        return super.handle(dataModel, request);
    }
}
```

2. **Register the custom handler in your application:**
Ensure that your custom handler is registered when the application starts.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import com.example.demo.config.CustomApiHandler;

@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        CustomApiHandler.register();
		SpringApplication.run(DemoApplication.class, args);
    }
}
```

## Exception Handling with ServiceRuntimeException
The `api-link` library provides a centralized exception handling mechanism using `ServiceRuntimeException`. This allows for consistent and clean error handling across your application.

1. **Throwing ServiceRuntimeException:**
Throw `ServiceRuntimeException` from your service methods when an error occurs.

```java
import io.github.hison.api.exception.ServiceRuntimeException;

public void myMethod(DataWrapper data) {
    if (data == null) {
        throw new ServiceRuntimeException("Data cannot be null");
    }
    // Your business logic here
}
```

2. **Handling exceptions globally:**
`ServiceRuntimeException` will be automatically handled by the `ApiLink` controller, returning an appropriate HTTP response.

## Caching with WebSocket
The api-link library supports caching through WebSockets, allowing real-time data updates and efficient data management.

1. **Implement WebSocket handler:**
Handle WebSocket messages and manage caching logic.

```java
import org.springframework.web.socket.config.annotation.WebSocketHandlerRegistration;
import org.springframework.web.socket.TextMessage;
import org.springframework.web.socket.WebSocketSession;
import org.springframework.web.socket.handler.TextWebSocketHandler;

public class WebSocketHandler extends TextWebSocketHandler {
    @Override	
        public void setRegistry(WebSocketHandlerRegistration registry) {
        // You can setAllowedOrigins via setRegistry
        registry.setAllowedOrigins("http://localhost:3000/");	
    };
    @Override
    public void handleTextMessage(WebSocketSession session, TextMessage message) {
        // Handle incoming WebSocket message and manage caching
        String payload = message.getPayload();
        // Your caching logic here
    }
}
```

2. **Register the custom handler in your application:**
Ensure that your custom handler is registered when the application starts.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import com.example.demo.config.CustomCachingHandler;

@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
		CustomCachingHandler.register();
		SpringApplication.run(DemoApplication.class, args);
    }
}
```


# 3. utils [![Maven Central](https://img.shields.io/maven-central/v/io.github.hisondev/utils.svg?label=Maven%20Central)](https://mvnrepository.com/artifact/io.github.hisondev/utils)
This is a minimal collection of utils that can be used in a Java project.

## Introduction
The `utils` library is a set of utility functions designed to simplify common tasks in Java projects. It includes a variety of methods for string manipulation, date and time operations, number formatting, and more. The goal of this library is to provide a lightweight and easy-to-use solution for everyday programming needs.

## Getting Started
To start using the `utils` library in your project, follow the installation and usage instructions below.

This library, composed of JavaScript, can use `hison.min.js` from [hison-js](https://github.com/hisondev/hison-js).

### Prerequisites
Before you can use the `utils` library, you need to have the following software installed on your system:
- Java Development Kit (JDK) 8 or higher
- Apache Maven (for building the project)

### Installation
You can add the `utils` library to your project by including the following dependency in your Maven `pom.xml` file:

```xml
<dependency>
    <groupId>io.github.hison</groupId>
    <artifactId>utils</artifactId>
    <version>1.0.0</version>
</dependency>
```

## Usage
### Property Configuration
The `utils` library allows you to configure certain properties using a properties file. Here is an example of how to set up the properties:

1. **Create the properties file**:
   Create a file named `hison-utils-config.properties` in your project's resources directory.

2. **Add properties to the file**:
   Define the properties you want to customize in the `hison-utils-config.properties` file. Here are some example properties you can set:

   ```properties
   date.formatter=dd/MM/yyyy
   datetime.formatter=dd/MM/yyyy HH:mm:ss
   add.type=d
   diff.type=d
   dayofweek.type=day
   lessoreq.0x7ff.byte=2
   lessoreq.0xffff.byte=3
   greater.0xffff.byte=4
   number.formatter=#,##0.##### 
   propertie.file.path=./config/
   ```

***This is because the logic for retrieving information about Utils properties is as follows.***

```java
private static String DATE_FORMATTER = "yyyy-MM-dd";
private static String DATETIME_FORMATTER = "yyyy-MM-dd HH:mm:ss";
private static String ADD_TYPE = "d";
private static String DIFF_TYPE = "d";
private static String DAY_OF_WEEK_TYPE = "d";
private static int LESSOREQ_0X7FF_BYTE = 2;
private static int LESSOREQ_0XFFFF_BYTE = 3;
private static int GREATER_0XFFFF_BYTE = 4;
private static String NUMBER_FORMATTER = "#,##0.#####";
private static String PROPERTIE_FILE_PATH = "";

static {
    Properties prop = new Properties();
    try (InputStream input = Utils.class.getClassLoader().getResourceAsStream("hison-utils-config.properties")) {
        if (input != null) {
            prop.load(input);
        }
    } catch (IOException ex) {
    }
    if(!prop.isEmpty()){
        DATE_FORMATTER = prop.getProperty("date.formatter") != null ? prop.getProperty("date.formatter") : DATE_FORMATTER;
        DATETIME_FORMATTER = prop.getProperty("datetime.formatter") != null ? prop.getProperty("datetime.formatter") : DATETIME_FORMATTER;
        ADD_TYPE = prop.getProperty("add.type") != null ? prop.getProperty("add.type") : ADD_TYPE;
        DIFF_TYPE = prop.getProperty("diff.type") != null ? prop.getProperty("diff.type") : DIFF_TYPE;
        DAY_OF_WEEK_TYPE = prop.getProperty("dayofweek.type") != null ? prop.getProperty("dayofweek.type") : DAY_OF_WEEK_TYPE;
        LESSOREQ_0X7FF_BYTE = prop.getProperty("lessoreq.0x7ff.byte") != null && prop.getProperty("lessoreq.0x7ff.byte").matches("\\d+") ? Integer.parseInt(prop.getProperty("lessoreq.0x7ff.byte")) : LESSOREQ_0X7FF_BYTE;
        LESSOREQ_0XFFFF_BYTE = prop.getProperty("lessoreq.0xffff.byte") != null && prop.getProperty("lessoreq.0xffff.byte").matches("\\d+") ? Integer.parseInt(prop.getProperty("lessoreq.0xffff.byte")) : LESSOREQ_0XFFFF_BYTE;
        GREATER_0XFFFF_BYTE = prop.getProperty("greater.0xffff.byte") != null && prop.getProperty("greater.0xffff.byte").matches("\\d+") ? Integer.parseInt(prop.getProperty("greater.0xffff.byte")) : GREATER_0XFFFF_BYTE;
        NUMBER_FORMATTER = prop.getProperty("number.formatter") != null ? prop.getProperty("number.formatter") : NUMBER_FORMATTER;
        PROPERTIE_FILE_PATH = prop.getProperty("propertie.file.path") != null ? prop.getProperty("propertie.file.path") : PROPERTIE_FILE_PATH;
    }
}
```

### Ex) String Utilities
```java
import io.github.hison.utils.Utils;

// Check if a string contains only alphabetic characters
boolean isAlpha = Utils.isAlpha("HelloWorld");

// Check if a string contains only alphanumeric characters
boolean isAlphaNumber = Utils.isAlphaNumber("Hello123");

// Left pad a string with a specified character
String paddedString = Utils.getLpad("123", "0", 5);
```

### Ex) Date Utilities
```java
import io.github.hison.utils.Utils;

// Get the current system date and time
String sysDatetime = Utils.getSysDatetime();

// Add days to a given date
String newDate = Utils.addDate("2023-06-09", 5);

// Get the last day of a given month
int lastDay = Utils.getLastDay("2023-06");
```

### Ex) Number Utilities
```java
import io.github.hison.utils.Utils;

// Round a number to the nearest integer
double roundedNumber = Utils.getRound(123.456);

// Get the byte length of a string
int byteLength = Utils.getByteLength("Hello World");
```

## Contributing
Contributions are welcome! If you have any ideas, suggestions, or bug reports, please open an issue or submit a pull request on GitHub. Make sure to follow the project's code style and add tests for any new features or changes.

## License
MIT License

## Authors
**Hani Son**  
hison0319@gmail.com