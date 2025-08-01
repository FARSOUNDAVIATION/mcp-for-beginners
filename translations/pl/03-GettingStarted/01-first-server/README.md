<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "004572534b5c86f847fac76bcbb76e89",
  "translation_date": "2025-07-22T09:01:32+00:00",
  "source_file": "03-GettingStarted/01-first-server/README.md",
  "language_code": "pl"
}
-->
# Pierwsze kroki z MCP

Witamy w Twojej pierwszej przygodzie z Model Context Protocol (MCP)! Niezależnie od tego, czy dopiero zaczynasz swoją przygodę z MCP, czy chcesz pogłębić swoją wiedzę, ten przewodnik przeprowadzi Cię przez kluczowe etapy konfiguracji i procesu tworzenia. Dowiesz się, jak MCP umożliwia płynną integrację między modelami AI a aplikacjami oraz jak szybko przygotować środowisko do budowy i testowania rozwiązań opartych na MCP.

> TLDR; Jeśli tworzysz aplikacje AI, wiesz, że możesz dodawać narzędzia i inne zasoby do swojego LLM (large language model), aby uczynić go bardziej wszechstronnym. Jednakże, jeśli umieścisz te narzędzia i zasoby na serwerze, aplikacja i możliwości serwera mogą być wykorzystywane przez dowolnego klienta, z LLM lub bez.

## Przegląd

Ta lekcja dostarcza praktycznych wskazówek dotyczących konfiguracji środowisk MCP i budowy pierwszych aplikacji MCP. Nauczysz się, jak skonfigurować niezbędne narzędzia i frameworki, stworzyć podstawowe serwery MCP, utworzyć aplikacje hostujące oraz przetestować swoje implementacje.

Model Context Protocol (MCP) to otwarty protokół, który standaryzuje sposób, w jaki aplikacje dostarczają kontekst do LLM. Można o nim myśleć jak o porcie USB-C dla aplikacji AI – zapewnia ustandaryzowany sposób łączenia modeli AI z różnymi źródłami danych i narzędziami.

## Cele nauki

Po ukończeniu tej lekcji będziesz w stanie:

- Skonfigurować środowiska deweloperskie dla MCP w językach C#, Java, Python, TypeScript i JavaScript
- Tworzyć i wdrażać podstawowe serwery MCP z niestandardowymi funkcjami (zasoby, podpowiedzi i narzędzia)
- Tworzyć aplikacje hostujące, które łączą się z serwerami MCP
- Testować i debugować implementacje MCP

## Konfiguracja środowiska MCP

Zanim zaczniesz pracę z MCP, ważne jest, aby przygotować swoje środowisko deweloperskie i zrozumieć podstawowy przepływ pracy. Ta sekcja przeprowadzi Cię przez początkowe kroki konfiguracji, aby zapewnić płynny start z MCP.

### Wymagania wstępne

Przed rozpoczęciem pracy z MCP upewnij się, że masz:

- **Środowisko deweloperskie**: Dla wybranego języka (C#, Java, Python, TypeScript lub JavaScript)
- **IDE/Edytor**: Visual Studio, Visual Studio Code, IntelliJ, Eclipse, PyCharm lub dowolny nowoczesny edytor kodu
- **Menedżery pakietów**: NuGet, Maven/Gradle, pip lub npm/yarn
- **Klucze API**: Dla usług AI, które planujesz wykorzystać w swoich aplikacjach hostujących

## Podstawowa struktura serwera MCP

Typowy serwer MCP zawiera:

- **Konfigurację serwera**: Ustawienia portu, uwierzytelniania i inne
- **Zasoby**: Dane i kontekst udostępniane LLM
- **Narzędzia**: Funkcjonalności, które modele mogą wywoływać
- **Podpowiedzi**: Szablony do generowania lub strukturyzowania tekstu

Oto uproszczony przykład w TypeScript:

```typescript
import { Server, Tool, Resource } from "@modelcontextprotocol/typescript-server-sdk";

// Create a new MCP server
const server = new Server({
  port: 3000,
  name: "Example MCP Server",
  version: "1.0.0"
});

// Register a tool
server.registerTool({
  name: "calculator",
  description: "Performs basic calculations",
  parameters: {
    expression: {
      type: "string",
      description: "The math expression to evaluate"
    }
  },
  handler: async (params) => {
    const result = eval(params.expression);
    return { result };
  }
});

// Start the server
server.start();
```

W powyższym kodzie:

- Importujemy niezbędne klasy z MCP TypeScript SDK.
- Tworzymy i konfigurujemy nową instancję serwera MCP.
- Rejestrujemy niestandardowe narzędzie (`calculator`) z funkcją obsługi.
- Uruchamiamy serwer, aby nasłuchiwał na przychodzące żądania MCP.

## Testowanie i debugowanie

Zanim rozpoczniesz testowanie swojego serwera MCP, ważne jest, aby zrozumieć dostępne narzędzia i najlepsze praktyki debugowania. Skuteczne testowanie zapewnia, że serwer działa zgodnie z oczekiwaniami i pomaga szybko zidentyfikować oraz rozwiązać problemy. Poniższa sekcja przedstawia zalecane podejścia do weryfikacji implementacji MCP.

MCP oferuje narzędzia, które pomogą Ci testować i debugować serwery:

- **Narzędzie Inspector**: Graficzny interfejs umożliwiający połączenie z serwerem i testowanie narzędzi, podpowiedzi oraz zasobów.
- **curl**: Możesz również połączyć się z serwerem za pomocą narzędzia wiersza poleceń, takiego jak curl, lub innych klientów, które mogą tworzyć i wykonywać polecenia HTTP.

### Korzystanie z MCP Inspector

[MCP Inspector](https://github.com/modelcontextprotocol/inspector) to wizualne narzędzie testowe, które pozwala:

1. **Odkrywać możliwości serwera**: Automatycznie wykrywać dostępne zasoby, narzędzia i podpowiedzi
2. **Testować wykonanie narzędzi**: Wypróbowywać różne parametry i obserwować odpowiedzi w czasie rzeczywistym
3. **Przeglądać metadane serwera**: Analizować informacje o serwerze, schematy i konfiguracje

```bash
# ex TypeScript, installing and running MCP Inspector
npx @modelcontextprotocol/inspector node build/index.js
```

Po uruchomieniu powyższych poleceń MCP Inspector otworzy lokalny interfejs w przeglądarce. Powinieneś zobaczyć pulpit nawigacyjny wyświetlający zarejestrowane serwery MCP, ich dostępne narzędzia, zasoby i podpowiedzi. Interfejs umożliwia interaktywne testowanie narzędzi, przeglądanie metadanych serwera i obserwowanie odpowiedzi w czasie rzeczywistym, co ułatwia weryfikację i debugowanie implementacji serwera MCP.

Oto zrzut ekranu, jak to może wyglądać:

![](../../../../translated_images/connected.73d1e042c24075d386cacdd4ee7cd748c16364c277d814e646ff2f7b5eefde85.pl.png)

## Typowe problemy z konfiguracją i ich rozwiązania

| Problem | Możliwe rozwiązanie |
|--------|----------------------|
| Odmowa połączenia | Sprawdź, czy serwer działa i czy port jest poprawny |
| Błędy wykonania narzędzi | Przejrzyj walidację parametrów i obsługę błędów |
| Problemy z uwierzytelnianiem | Zweryfikuj klucze API i uprawnienia |
| Błędy walidacji schematu | Upewnij się, że parametry pasują do zdefiniowanego schematu |
| Serwer nie uruchamia się | Sprawdź konflikty portów lub brakujące zależności |
| Błędy CORS | Skonfiguruj odpowiednie nagłówki CORS dla żądań między domenami |
| Problemy z tokenami uwierzytelniającymi | Zweryfikuj ważność tokenów i uprawnienia |

## Rozwój lokalny

Do lokalnego rozwoju i testowania możesz uruchamiać serwery MCP bezpośrednio na swoim komputerze:

1. **Uruchom proces serwera**: Uruchom aplikację serwera MCP
2. **Skonfiguruj sieć**: Upewnij się, że serwer jest dostępny na oczekiwanym porcie
3. **Podłącz klientów**: Użyj lokalnych adresów URL, takich jak `http://localhost:3000`

```bash
# Example: Running a TypeScript MCP server locally
npm run start
# Server running at http://localhost:3000
```

## Tworzenie pierwszego serwera MCP

Omówiliśmy [Podstawowe pojęcia](/01-CoreConcepts/README.md) w poprzedniej lekcji, teraz czas wykorzystać tę wiedzę w praktyce.

### Co może robić serwer

Zanim zaczniemy pisać kod, przypomnijmy sobie, co może robić serwer:

Serwer MCP może na przykład:

- Uzyskiwać dostęp do lokalnych plików i baz danych
- Łączyć się z zdalnymi API
- Wykonywać obliczenia
- Integracja z innymi narzędziami i usługami
- Udostępniać interfejs użytkownika do interakcji

Świetnie, teraz gdy wiemy, co możemy zrobić, zacznijmy kodować.

## Ćwiczenie: Tworzenie serwera

Aby stworzyć serwer, należy wykonać następujące kroki:

- Zainstalować MCP SDK.
- Utworzyć projekt i skonfigurować jego strukturę.
- Napisać kod serwera.
- Przetestować serwer.

### -1- Utwórz projekt

#### TypeScript

```sh
# Create project directory and initialize npm project
mkdir calculator-server
cd calculator-server
npm init -y
```

#### Python

```sh
# Create project dir
mkdir calculator-server
cd calculator-server
# Open the folder in Visual Studio Code - Skip this if you are using a different IDE
code .
```

#### .NET

```sh
dotnet new console -n McpCalculatorServer
cd McpCalculatorServer
```

#### Java

Dla Javy utwórz projekt Spring Boot:

```bash
curl https://start.spring.io/starter.zip \
  -d dependencies=web \
  -d javaVersion=21 \
  -d type=maven-project \
  -d groupId=com.example \
  -d artifactId=calculator-server \
  -d name=McpServer \
  -d packageName=com.microsoft.mcp.sample.server \
  -o calculator-server.zip
```

Wypakuj plik zip:

```bash
unzip calculator-server.zip -d calculator-server
cd calculator-server
# optional remove the unused test
rm -rf src/test/java
```

Dodaj następującą pełną konfigurację do pliku *pom.xml*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <!-- Spring Boot parent for dependency management -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.5.0</version>
        <relativePath />
    </parent>

    <!-- Project coordinates -->
    <groupId>com.example</groupId>
    <artifactId>calculator-server</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>Calculator Server</name>
    <description>Basic calculator MCP service for beginners</description>

    <!-- Properties -->
    <properties>
        <java.version>21</java.version>
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
    </properties>

    <!-- Spring AI BOM for version management -->
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.ai</groupId>
                <artifactId>spring-ai-bom</artifactId>
                <version>1.0.0-SNAPSHOT</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <!-- Dependencies -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.ai</groupId>
            <artifactId>spring-ai-starter-mcp-server-webflux</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-test</artifactId>
         <scope>test</scope>
      </dependency>
    </dependencies>

    <!-- Build configuration -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <release>21</release>
                </configuration>
            </plugin>
        </plugins>
    </build>

    <!-- Repositories for Spring AI snapshots -->
    <repositories>
        <repository>
            <id>spring-milestones</id>
            <name>Spring Milestones</name>
            <url>https://repo.spring.io/milestone</url>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
        <repository>
            <id>spring-snapshots</id>
            <name>Spring Snapshots</name>
            <url>https://repo.spring.io/snapshot</url>
            <releases>
                <enabled>false</enabled>
            </releases>
        </repository>
    </repositories>
</project>
```

### -2- Dodaj zależności

Teraz, gdy masz utworzony projekt, dodajmy zależności:

#### TypeScript

```sh
# If not already installed, install TypeScript globally
npm install typescript -g

# Install the MCP SDK and Zod for schema validation
npm install @modelcontextprotocol/sdk zod
npm install -D @types/node typescript
```

#### Python

```sh
# Create a virtual env and install dependencies
python -m venv venv
venv\Scripts\activate
pip install "mcp[cli]"
```

#### Java

```bash
cd calculator-server
./mvnw clean install -DskipTests
```

### -3- Utwórz pliki projektu

#### TypeScript

Otwórz plik *package.json* i zastąp jego zawartość następującą, aby upewnić się, że możesz zbudować i uruchomić serwer:

```json
{
  "name": "calculator-server",
  "version": "1.0.0",
  "main": "index.js",
  "type": "module",
  "scripts": {
    "start": "tsc && node ./build/index.js",
    "build": "tsc && node ./build/index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": "A simple calculator server using Model Context Protocol",
  "dependencies": {
    "@modelcontextprotocol/sdk": "^1.16.0",
    "zod": "^3.25.76"
  },
  "devDependencies": {
    "@types/node": "^24.0.14",
    "typescript": "^5.8.3"
  }
}
```

Utwórz plik *tsconfig.json* z następującą zawartością:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "Node16",
    "moduleResolution": "Node16",
    "outDir": "./build",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

Utwórz katalog na kod źródłowy:

```sh
mkdir src
touch src/index.ts
```

#### Python

Utwórz plik *server.py*

```sh
touch server.py
```

#### .NET

Zainstaluj wymagane pakiety NuGet:

```sh
dotnet add package ModelContextProtocol --prerelease
dotnet add package Microsoft.Extensions.Hosting
```

#### Java

Dla projektów Spring Boot struktura projektu jest tworzona automatycznie.

### -4- Utwórz kod serwera

#### TypeScript

Utwórz plik *index.ts* i dodaj następujący kod:

```typescript
import { McpServer, ResourceTemplate } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";
 
// Create an MCP server
const server = new McpServer({
  name: "Calculator MCP Server",
  version: "1.0.0"
});
```

Teraz masz serwer, ale nie robi on zbyt wiele. Naprawmy to.

#### Python

```python
# server.py
from mcp.server.fastmcp import FastMCP

# Create an MCP server
mcp = FastMCP("Demo")
```

#### .NET

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using ModelContextProtocol.Server;
using System.ComponentModel;

var builder = Host.CreateApplicationBuilder(args);
builder.Logging.AddConsole(consoleLogOptions =>
{
    // Configure all logs to go to stderr
    consoleLogOptions.LogToStandardErrorThreshold = LogLevel.Trace;
});

builder.Services
    .AddMcpServer()
    .WithStdioServerTransport()
    .WithToolsFromAssembly();
await builder.Build().RunAsync();

// add features
```

#### Java

Dla Javy utwórz podstawowe komponenty serwera. Najpierw zmodyfikuj główną klasę aplikacji:

*src/main/java/com/microsoft/mcp/sample/server/McpServerApplication.java*:

```java
package com.microsoft.mcp.sample.server;

import org.springframework.ai.tool.ToolCallbackProvider;
import org.springframework.ai.tool.method.MethodToolCallbackProvider;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import com.microsoft.mcp.sample.server.service.CalculatorService;

@SpringBootApplication
public class McpServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(McpServerApplication.class, args);
    }
    
    @Bean
    public ToolCallbackProvider calculatorTools(CalculatorService calculator) {
        return MethodToolCallbackProvider.builder().toolObjects(calculator).build();
    }
}
```

Utwórz usługę kalkulatora *src/main/java/com/microsoft/mcp/sample/server/service/CalculatorService.java*:

```java
package com.microsoft.mcp.sample.server.service;

import org.springframework.ai.tool.annotation.Tool;
import org.springframework.stereotype.Service;

/**
 * Service for basic calculator operations.
 * This service provides simple calculator functionality through MCP.
 */
@Service
public class CalculatorService {

    /**
     * Add two numbers
     * @param a The first number
     * @param b The second number
     * @return The sum of the two numbers
     */
    @Tool(description = "Add two numbers together")
    public String add(double a, double b) {
        double result = a + b;
        return formatResult(a, "+", b, result);
    }

    /**
     * Subtract one number from another
     * @param a The number to subtract from
     * @param b The number to subtract
     * @return The result of the subtraction
     */
    @Tool(description = "Subtract the second number from the first number")
    public String subtract(double a, double b) {
        double result = a - b;
        return formatResult(a, "-", b, result);
    }

    /**
     * Multiply two numbers
     * @param a The first number
     * @param b The second number
     * @return The product of the two numbers
     */
    @Tool(description = "Multiply two numbers together")
    public String multiply(double a, double b) {
        double result = a * b;
        return formatResult(a, "*", b, result);
    }

    /**
     * Divide one number by another
     * @param a The numerator
     * @param b The denominator
     * @return The result of the division
     */
    @Tool(description = "Divide the first number by the second number")
    public String divide(double a, double b) {
        if (b == 0) {
            return "Error: Cannot divide by zero";
        }
        double result = a / b;
        return formatResult(a, "/", b, result);
    }

    /**
     * Calculate the power of a number
     * @param base The base number
     * @param exponent The exponent
     * @return The result of raising the base to the exponent
     */
    @Tool(description = "Calculate the power of a number (base raised to an exponent)")
    public String power(double base, double exponent) {
        double result = Math.pow(base, exponent);
        return formatResult(base, "^", exponent, result);
    }

    /**
     * Calculate the square root of a number
     * @param number The number to find the square root of
     * @return The square root of the number
     */
    @Tool(description = "Calculate the square root of a number")
    public String squareRoot(double number) {
        if (number < 0) {
            return "Error: Cannot calculate square root of a negative number";
        }
        double result = Math.sqrt(number);
        return String.format("√%.2f = %.2f", number, result);
    }

    /**
     * Calculate the modulus (remainder) of division
     * @param a The dividend
     * @param b The divisor
     * @return The remainder of the division
     */
    @Tool(description = "Calculate the remainder when one number is divided by another")
    public String modulus(double a, double b) {
        if (b == 0) {
            return "Error: Cannot divide by zero";
        }
        double result = a % b;
        return formatResult(a, "%", b, result);
    }

    /**
     * Calculate the absolute value of a number
     * @param number The number to find the absolute value of
     * @return The absolute value of the number
     */
    @Tool(description = "Calculate the absolute value of a number")
    public String absolute(double number) {
        double result = Math.abs(number);
        return String.format("|%.2f| = %.2f", number, result);
    }

    /**
     * Get help about available calculator operations
     * @return Information about available operations
     */
    @Tool(description = "Get help about available calculator operations")
    public String help() {
        return "Basic Calculator MCP Service\n\n" +
               "Available operations:\n" +
               "1. add(a, b) - Adds two numbers\n" +
               "2. subtract(a, b) - Subtracts the second number from the first\n" +
               "3. multiply(a, b) - Multiplies two numbers\n" +
               "4. divide(a, b) - Divides the first number by the second\n" +
               "5. power(base, exponent) - Raises a number to a power\n" +
               "6. squareRoot(number) - Calculates the square root\n" + 
               "7. modulus(a, b) - Calculates the remainder of division\n" +
               "8. absolute(number) - Calculates the absolute value\n\n" +
               "Example usage: add(5, 3) will return 5 + 3 = 8";
    }

    /**
     * Format the result of a calculation
     */
    private String formatResult(double a, String operator, double b, double result) {
        return String.format("%.2f %s %.2f = %.2f", a, operator, b, result);
    }
}
```

**Opcjonalne komponenty dla gotowej do produkcji usługi:**

Utwórz konfigurację startową *src/main/java/com/microsoft/mcp/sample/server/config/StartupConfig.java*:

```java
package com.microsoft.mcp.sample.server.config;

import org.springframework.boot.CommandLineRunner;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class StartupConfig {
    
    @Bean
    public CommandLineRunner startupInfo() {
        return args -> {
            System.out.println("\n" + "=".repeat(60));
            System.out.println("Calculator MCP Server is starting...");
            System.out.println("SSE endpoint: http://localhost:8080/sse");
            System.out.println("Health check: http://localhost:8080/actuator/health");
            System.out.println("=".repeat(60) + "\n");
        };
    }
}
```

Utwórz kontroler zdrowia *src/main/java/com/microsoft/mcp/sample/server/controller/HealthController.java*:

```java
package com.microsoft.mcp.sample.server.controller;

import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import java.time.LocalDateTime;
import java.util.HashMap;
import java.util.Map;

@RestController
public class HealthController {
    
    @GetMapping("/health")
    public ResponseEntity<Map<String, Object>> healthCheck() {
        Map<String, Object> response = new HashMap<>();
        response.put("status", "UP");
        response.put("timestamp", LocalDateTime.now().toString());
        response.put("service", "Calculator MCP Server");
        return ResponseEntity.ok(response);
    }
}
```

Utwórz obsługę wyjątków *src/main/java/com/microsoft/mcp/sample/server/exception/GlobalExceptionHandler.java*:

```java
package com.microsoft.mcp.sample.server.exception;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(IllegalArgumentException.class)
    public ResponseEntity<ErrorResponse> handleIllegalArgumentException(IllegalArgumentException ex) {
        ErrorResponse error = new ErrorResponse(
            "Invalid_Input", 
            "Invalid input parameter: " + ex.getMessage());
        return new ResponseEntity<>(error, HttpStatus.BAD_REQUEST);
    }

    public static class ErrorResponse {
        private String code;
        private String message;

        public ErrorResponse(String code, String message) {
            this.code = code;
            this.message = message;
        }

        // Getters
        public String getCode() { return code; }
        public String getMessage() { return message; }
    }
}
```

Utwórz niestandardowy baner *src/main/resources/banner.txt*:

```text
_____      _            _       _             
 / ____|    | |          | |     | |            
| |     __ _| | ___ _   _| | __ _| |_ ___  _ __ 
| |    / _` | |/ __| | | | |/ _` | __/ _ \| '__|
| |___| (_| | | (__| |_| | | (_| | || (_) | |   
 \_____\__,_|_|\___|\__,_|_|\__,_|\__\___/|_|   
                                                
Calculator MCP Server v1.0
Spring Boot MCP Application
```

### -5- Dodanie narzędzia i zasobu

Dodaj narzędzie i zasób, dodając następujący kod:

#### TypeScript

```typescript
server.tool(
  "add",
  { a: z.number(), b: z.number() },
  async ({ a, b }) => ({
    content: [{ type: "text", text: String(a + b) }]
  })
);

server.resource(
  "greeting",
  new ResourceTemplate("greeting://{name}", { list: undefined }),
  async (uri, { name }) => ({
    contents: [{
      uri: uri.href,
      text: `Hello, ${name}!`
    }]
  })
);
```

Twoje narzędzie przyjmuje parametry `a` i `b` i uruchamia funkcję, która zwraca odpowiedź w formie:

```typescript
{
  contents: [{
    type: "text", content: "some content"
  }]
}
```

Twój zasób jest dostępny przez ciąg "greeting" i przyjmuje parametr `name`, zwracając podobną odpowiedź jak narzędzie:

```typescript
{
  uri: "<href>",
  text: "a text"
}
```

#### Python

```python
# Add an addition tool
@mcp.tool()
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b


# Add a dynamic greeting resource
@mcp.resource("greeting://{name}")
def get_greeting(name: str) -> str:
    """Get a personalized greeting"""
    return f"Hello, {name}!"
```

W powyższym kodzie:

- Zdefiniowano narzędzie `add`, które przyjmuje parametry `a` i `p`, oba jako liczby całkowite.
- Utworzono zasób o nazwie `greeting`, który przyjmuje parametr `name`.

#### .NET

Dodaj to do pliku Program.cs:

```csharp
[McpServerToolType]
public static class CalculatorTool
{
    [McpServerTool, Description("Adds two numbers")]
    public static string Add(int a, int b) => $"Sum {a + b}";
}
```

#### Java

Narzędzia zostały już utworzone w poprzednim kroku.

### -6- Ostateczny kod

Dodajmy ostatni kod, aby serwer mógł się uruchomić:

#### TypeScript

```typescript
// Start receiving messages on stdin and sending messages on stdout
const transport = new StdioServerTransport();
await server.connect(transport);
```

Oto pełny kod:

```typescript
// index.ts
import { McpServer, ResourceTemplate } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

// Create an MCP server
const server = new McpServer({
  name: "Calculator MCP Server",
  version: "1.0.0"
});

// Add an addition tool
server.tool(
  "add",
  { a: z.number(), b: z.number() },
  async ({ a, b }) => ({
    content: [{ type: "text", text: String(a + b) }]
  })
);

// Add a dynamic greeting resource
server.resource(
  "greeting",
  new ResourceTemplate("greeting://{name}", { list: undefined }),
  async (uri, { name }) => ({
    contents: [{
      uri: uri.href,
      text: `Hello, ${name}!`
    }]
  })
);

// Start receiving messages on stdin and sending messages on stdout
const transport = new StdioServerTransport();
server.connect(transport);
```

#### Python

```python
# server.py
from mcp.server.fastmcp import FastMCP

# Create an MCP server
mcp = FastMCP("Demo")


# Add an addition tool
@mcp.tool()
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b


# Add a dynamic greeting resource
@mcp.resource("greeting://{name}")
def get_greeting(name: str) -> str:
    """Get a personalized greeting"""
    return f"Hello, {name}!"

# Main execution block - this is required to run the server
if __name__ == "__main__":
    mcp.run()
```

#### .NET

Utwórz plik Program.cs z następującą zawartością:

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using ModelContextProtocol.Server;
using System.ComponentModel;

var builder = Host.CreateApplicationBuilder(args);
builder.Logging.AddConsole(consoleLogOptions =>
{
    // Configure all logs to go to stderr
    consoleLogOptions.LogToStandardErrorThreshold = LogLevel.Trace;
});

builder.Services
    .AddMcpServer()
    .WithStdioServerTransport()
    .WithToolsFromAssembly();
await builder.Build().RunAsync();

[McpServerToolType]
public static class CalculatorTool
{
    [McpServerTool, Description("Adds two numbers")]
    public static string Add(int a, int b) => $"Sum {a + b}";
}
```

#### Java

Twoja kompletna główna klasa aplikacji powinna wyglądać tak:

```java
// McpServerApplication.java
package com.microsoft.mcp.sample.server;

import org.springframework.ai.tool.ToolCallbackProvider;
import org.springframework.ai.tool.method.MethodToolCallbackProvider;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import com.microsoft.mcp.sample.server.service.CalculatorService;

@SpringBootApplication
public class McpServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(McpServerApplication.class, args);
    }
    
    @Bean
    public ToolCallbackProvider calculatorTools(CalculatorService calculator) {
        return MethodToolCallbackProvider.builder().toolObjects(calculator).build();
    }
}
```

### -7- Testowanie serwera

Uruchom serwer za pomocą następującego polecenia:

#### TypeScript

```sh
npm run build
```

#### Python

```sh
mcp run server.py
```

> Aby użyć MCP Inspector, użyj `mcp dev server.py`, co automatycznie uruchamia Inspector i dostarcza wymagany token sesji proxy. Jeśli używasz `mcp run server.py`, będziesz musiał ręcznie uruchomić Inspector i skonfigurować połączenie.

#### .NET

Upewnij się, że znajdujesz się w katalogu projektu:

```sh
cd McpCalculatorServer
dotnet run
```

#### Java

```bash
./mvnw clean install -DskipTests
java -jar target/calculator-server-0.0.1-SNAPSHOT.jar
```

### -8- Uruchom za pomocą Inspectora

Inspector to świetne narzędzie, które pozwala uruchomić serwer i umożliwia interakcję z nim, aby przetestować jego działanie. Uruchommy go:

> [!NOTE]
> Może wyglądać inaczej w polu "command", ponieważ zawiera polecenie do uruchomienia serwera z Twoim konkretnym środowiskiem uruchomieniowym.

#### TypeScript

```sh
npx @modelcontextprotocol/inspector node build/index.js
```

lub dodaj to do swojego *package.json* w następujący sposób: `"inspector": "npx @modelcontextprotocol/inspector node build/index.js"` i następnie uruchom `npm run inspect`

Python korzysta z narzędzia Node.js o nazwie inspector. Można je wywołać w następujący sposób:

```sh
mcp dev server.py
```

Jednakże nie implementuje wszystkich dostępnych metod, dlatego zaleca się uruchomienie narzędzia Node.js bezpośrednio, jak poniżej:

```sh
npx @modelcontextprotocol/inspector mcp run server.py
```

Jeśli używasz narzędzia lub IDE, które pozwala konfigurować polecenia i argumenty do uruchamiania skryptów, 
upewnij się, że ustawisz `python` w polu `Command` i `server.py` jako `Arguments`. Dzięki temu skrypt uruchomi się poprawnie.

#### .NET

Upewnij się, że znajdujesz się w katalogu projektu:

```sh
cd McpCalculatorServer
npx @modelcontextprotocol/inspector dotnet run
```

#### Java

Upewnij się, że serwer kalkulatora działa. Następnie uruchom Inspector:

```cmd
npx @modelcontextprotocol/inspector
```

W interfejsie webowym Inspectora:

1. Wybierz "SSE" jako typ transportu
2. Ustaw URL na: `http://localhost:8080/sse`
3. Kliknij "Connect"

![Connect](../../../../translated_images/tool.163d33e3ee307e209ef146d8f85060d2f7e83e9f59b3b1699a77204ae0454ad2.pl.png)

**Teraz jesteś połączony z serwerem**
**Sekcja testowania serwera Java została zakończona**

Następna sekcja dotyczy interakcji z serwerem.

Powinieneś zobaczyć następujący interfejs użytkownika:

![Connect](../../../../translated_images/connect.141db0b2bd05f096fb1dd91273771fd8b2469d6507656c3b0c9df4b3c5473929.pl.png)

1. Połącz się z serwerem, wybierając przycisk Connect.
   Po połączeniu z serwerem powinieneś zobaczyć następujące:

   ![Connected](../../../../translated_images/connected.73d1e042c24075d386cacdd4ee7cd748c16364c277d814e646ff2f7b5eefde85.pl.png)

1. Wybierz "Tools" i "listTools", powinieneś zobaczyć "Add", wybierz "Add" i wypełnij wartości parametrów.

   Powinieneś zobaczyć następującą odpowiedź, tj. wynik działania narzędzia "add":

   ![Result of running add](../../../../translated_images/ran-tool.a5a6ee878c1369ec1e379b81053395252a441799dbf23416c36ddf288faf8249.pl.png)

Gratulacje, udało Ci się stworzyć i uruchomić swój pierwszy serwer!

### Oficjalne SDK

MCP oferuje oficjalne SDK dla wielu języków:

- [C# SDK](https://github.com/modelcontextprotocol/csharp-sdk) - Utrzymywane we współpracy z Microsoft
- [Java SDK](https://github.com/modelcontextprotocol/java-sdk) - Utrzymywane we współpracy z Spring AI
- [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) - Oficjalna implementacja TypeScript
- [Python SDK](https://github.com/modelcontextprotocol/python-sdk) - Oficjalna implementacja Python
- [Kotlin SDK](https://github.com/modelcontextprotocol/kotlin-sdk) - Oficjalna implementacja w Kotlinie  
- [Swift SDK](https://github.com/modelcontextprotocol/swift-sdk) - Utrzymywana we współpracy z Loopwork AI  
- [Rust SDK](https://github.com/modelcontextprotocol/rust-sdk) - Oficjalna implementacja w Rust  

## Kluczowe informacje  

- Konfiguracja środowiska deweloperskiego MCP jest prosta dzięki SDK specyficznym dla języka  
- Tworzenie serwerów MCP polega na budowaniu i rejestrowaniu narzędzi z jasnymi schematami  
- Testowanie i debugowanie są kluczowe dla niezawodnych implementacji MCP  

## Przykłady  

- [Java Calculator](../samples/java/calculator/README.md)  
- [.Net Calculator](../../../../03-GettingStarted/samples/csharp)  
- [JavaScript Calculator](../samples/javascript/README.md)  
- [TypeScript Calculator](../samples/typescript/README.md)  
- [Python Calculator](../../../../03-GettingStarted/samples/python)  

## Zadanie  

Stwórz prosty serwer MCP z narzędziem według własnego wyboru:  

1. Zaimplementuj narzędzie w preferowanym języku (.NET, Java, Python lub JavaScript).  
2. Zdefiniuj parametry wejściowe i wartości zwracane.  
3. Uruchom narzędzie inspektora, aby upewnić się, że serwer działa zgodnie z oczekiwaniami.  
4. Przetestuj implementację z różnymi danymi wejściowymi.  

## Rozwiązanie  

[Rozwiązanie](./solution/README.md)  

## Dodatkowe zasoby  

- [Budowanie agentów za pomocą Model Context Protocol na platformie Azure](https://learn.microsoft.com/azure/developer/ai/intro-agents-mcp)  
- [Zdalny MCP z Azure Container Apps (Node.js/TypeScript/JavaScript)](https://learn.microsoft.com/samples/azure-samples/mcp-container-ts/mcp-container-ts/)  
- [.NET OpenAI MCP Agent](https://learn.microsoft.com/samples/azure-samples/openai-mcp-agent-dotnet/openai-mcp-agent-dotnet/)  

## Co dalej  

Dalej: [Pierwsze kroki z klientami MCP](../02-client/README.md)  

**Zastrzeżenie**:  
Ten dokument został przetłumaczony za pomocą usługi tłumaczenia AI [Co-op Translator](https://github.com/Azure/co-op-translator). Chociaż dokładamy wszelkich starań, aby tłumaczenie było precyzyjne, prosimy pamiętać, że automatyczne tłumaczenia mogą zawierać błędy lub nieścisłości. Oryginalny dokument w jego rodzimym języku powinien być uznawany za autorytatywne źródło. W przypadku informacji o kluczowym znaczeniu zaleca się skorzystanie z profesjonalnego tłumaczenia przez człowieka. Nie ponosimy odpowiedzialności za jakiekolwiek nieporozumienia lub błędne interpretacje wynikające z użycia tego tłumaczenia.