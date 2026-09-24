# spring-mvc-greeting-app

A Spring Boot web application built as part of Task 1 for the Spring Framework course at Akademia Finansów i Biznesu Vistula.

---

## Description

This is a simple Spring Boot MVC application that demonstrates:
- Creating a Spring Boot project from scratch using Spring Initializr
- Writing a Spring Controller using `@Controller`
- Handling HTTP GET requests using `@GetMapping`
- Using `@RequestParam` to read query parameters from the URL
- Passing data to a Thymeleaf HTML view using `Model`
- Understanding the difference between `@Controller` and `@RestController`

---

## Project Structure

```
first-project-java-spring/
├── src/
│   └── main/
│       ├── java/
│       │   └── pl/edu/vistula/first_project_java_spring/
│       │       ├── controller/
│       │       │   └── HelloController.java
│       │       └── FirstProjectJavaSpringApplication.java
│       └── resources/
│           ├── static/
│           └── templates/
│               └── greeting.html
├── .gitignore
├── pom.xml
└── README.md
```

---

## Technologies Used

- Java 17
- Spring Boot
- Spring Web (MVC)
- Thymeleaf
- Maven

---

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/Ramzi-Lafi/FisrtProjectJavaDevolpment.git
   ```

2. Open the project in IntelliJ IDEA

3. Right-click the project → Maven → Reload Project

4. Run `FirstProjectJavaSpringApplication.java`

5. Open your browser and go to `localhost:8080/greeting`

---

## Use Cases / HTTP Endpoints

### 1. GET `/greeting` — Default greeting (no parameter)

**URL:** `http://localhost:8080/greeting`

**Description:** When no `name` parameter is provided, the application uses the default value `"Vistula"` and displays a greeting message in the browser via a Thymeleaf HTML view.

**Result:**

<img width="1914" height="969" alt="greeting_default png" src="https://github.com/user-attachments/assets/d34bc53d-1d3e-4761-a1a1-7ae8424b277f" />


---

### 2. GET `/greeting?name=YourName` — Custom greeting

**URL:** `http://localhost:8080/greeting?name=YourName`

**Description:** When a `name` query parameter is provided in the URL, the application reads it and passes it to the Thymeleaf template, which then displays a personalized greeting.

**Result:**

<img width="1914" height="966" alt="greeting_with_name png" src="https://github.com/user-attachments/assets/2b525b29-73ee-435f-bcc0-d91c1055d19f" />


---

## Code Explanation

### `HelloController.java`

```java
@Controller
public class HelloController {

    @GetMapping("/greeting")
    public String greeting(@RequestParam(name="name", required=false, defaultValue="Vistula") String name, Model model) {
        model.addAttribute("name", name);
        return "greeting";
    }
}
```

**Line by line explanation:**

| Annotation / Code | What it does |
|---|---|
| `@Controller` | Marks this class as a Spring MVC controller. Unlike `@RestController`, it returns **view names** (HTML pages), not raw data |
| `@GetMapping("/greeting")` | Maps HTTP GET requests sent to `/greeting` to this method |
| `@RequestParam(name="name", required=false, defaultValue="Vistula")` | Reads the `name` parameter from the URL query string. If not provided, defaults to `"Vistula"` |
| `Model model` | A Spring object used to pass data from the controller to the HTML view |
| `model.addAttribute("name", name)` | Adds the `name` variable to the model so Thymeleaf can use it in the HTML template |
| `return "greeting"` | Tells Spring to render the `greeting.html` file located in `src/main/resources/templates/` |

---

### `@Controller` vs `@RestController`

| `@Controller` | `@RestController` |
|---|---|
| Returns the **name of an HTML view** to render | Returns **data directly** (JSON, plain text) in the HTTP response body |
| Used with Thymeleaf templates | Used for REST APIs |
| Needs `@ResponseBody` on each method if you want to return raw data | `@ResponseBody` is applied automatically to every method |

> In Task 1 we use `@Controller` because we are rendering an HTML page with Thymeleaf.  
> `@ResponseBody` can be added to a method inside a `@Controller` class when you want that specific method to return raw data instead of a view name.

---

### `greeting.html` (Thymeleaf template)

```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Getting Started: Serving Web Content</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
    <p th:text="'Hello, ' + ${name} + '! Welcome to my project.'" />
</body>
</html>
```

`th:text` is a Thymeleaf attribute that replaces the text content of the element with the value of the expression. `${name}` reads the `name` variable we added to the model in the controller.

---

## .gitignore

The project includes a `.gitignore` file that excludes:
- `target/` — compiled build files
- `.idea/` — IntelliJ IDEA settings
- `*.iml` — IntelliJ module files
- `mvnw`, `mvnw.cmd` are included as they are needed to run Maven without a local installation

---
