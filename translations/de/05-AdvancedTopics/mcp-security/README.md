<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "50d9cd44fa74ad04f716fe31daf0c850",
  "translation_date": "2025-06-12T21:54:26+00:00",
  "source_file": "05-AdvancedTopics/mcp-security/README.md",
  "language_code": "de"
}
-->
# Sicherheitsbest Practices

Sicherheit ist entscheidend für MCP-Implementierungen, besonders in Unternehmensumgebungen. Es ist wichtig, sicherzustellen, dass Werkzeuge und Daten vor unbefugtem Zugriff, Datenlecks und anderen Sicherheitsbedrohungen geschützt sind.

## Einführung

In dieser Lektion werden wir Sicherheitsbest Practices für MCP-Implementierungen untersuchen. Wir behandeln Authentifizierung und Autorisierung, Datenschutz, sichere Ausführung von Werkzeugen und die Einhaltung von Datenschutzbestimmungen.

## Lernziele

Am Ende dieser Lektion werden Sie in der Lage sein:

- Sichere Authentifizierungs- und Autorisierungsmechanismen für MCP-Server zu implementieren.
- Sensible Daten durch Verschlüsselung und sichere Speicherung zu schützen.
- Die sichere Ausführung von Werkzeugen mit passenden Zugriffskontrollen zu gewährleisten.
- Best Practices für Datenschutz und Compliance anzuwenden.

## Authentifizierung und Autorisierung

Authentifizierung und Autorisierung sind unerlässlich, um MCP-Server abzusichern. Authentifizierung beantwortet die Frage „Wer sind Sie?“, während Autorisierung klärt „Was dürfen Sie tun?“.

Schauen wir uns Beispiele an, wie man sichere Authentifizierung und Autorisierung in MCP-Servern mit .NET und Java umsetzt.

### .NET Identity Integration

ASP .NET Core Identity bietet ein robustes Framework zur Verwaltung von Benutzer-Authentifizierung und -Autorisierung. Wir können es in MCP-Server integrieren, um den Zugriff auf Werkzeuge und Ressourcen abzusichern.

Einige zentrale Konzepte, die wir verstehen müssen, wenn wir ASP.NET Core Identity mit MCP-Servern integrieren, sind:

- **Identity-Konfiguration**: Einrichtung von ASP.NET Core Identity mit Benutzerrollen und Claims. Ein Claim ist eine Information über den Benutzer, z. B. seine Rolle oder Berechtigungen wie „Admin“ oder „User“.
- **JWT-Authentifizierung**: Verwendung von JSON Web Tokens (JWT) für sicheren API-Zugriff. JWT ist ein Standard zur sicheren Übertragung von Informationen zwischen Parteien als JSON-Objekt, das verifiziert und vertraut werden kann, da es digital signiert ist.
- **Autorisierungsrichtlinien**: Definition von Richtlinien zur Steuerung des Zugriffs auf bestimmte Werkzeuge basierend auf Benutzerrollen. MCP verwendet Autorisierungsrichtlinien, um zu bestimmen, welche Benutzer auf welche Werkzeuge basierend auf ihren Rollen und Claims zugreifen können.

```csharp
public class SecureMcpStartup
{
    public void ConfigureServices(IServiceCollection services)
    {
        // Add ASP.NET Core Identity
        services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();
        
        // Configure JWT authentication
        services.AddAuthentication(options =>
        {
            options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
            options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;
        })
        .AddJwtBearer(options =>
        {
            options.TokenValidationParameters = new TokenValidationParameters
            {
                ValidateIssuer = true,
                ValidateAudience = true,
                ValidateLifetime = true,
                ValidateIssuerSigningKey = true,
                ValidIssuer = Configuration["Jwt:Issuer"],
                ValidAudience = Configuration["Jwt:Audience"],
                IssuerSigningKey = new SymmetricSecurityKey(
                    Encoding.UTF8.GetBytes(Configuration["Jwt:Key"]))
            };
        });
        
        // Add authorization policies
        services.AddAuthorization(options =>
        {
            options.AddPolicy("CanUseAdminTools", policy =>
                policy.RequireRole("Admin"));
                
            options.AddPolicy("CanUseBasicTools", policy =>
                policy.RequireAuthenticatedUser());
        });
        
        // Configure MCP server with security
        services.AddMcpServer(options =>
        {
            options.ServerName = "Secure MCP Server";
            options.ServerVersion = "1.0.0";
            options.RequireAuthentication = true;
        });
        
        // Register tools with authorization requirements
        services.AddMcpTool<BasicTool>(options => 
            options.RequirePolicy("CanUseBasicTools"));
            
        services.AddMcpTool<AdminTool>(options => 
            options.RequirePolicy("CanUseAdminTools"));
    }
    
    public void Configure(IApplicationBuilder app)
    {
        // Use authentication and authorization
        app.UseAuthentication();
        app.UseAuthorization();
        
        // Use MCP server middleware
        app.UseMcpServer();
    }
}
```

Im obigen Code haben wir:

- ASP.NET Core Identity für die Benutzerverwaltung konfiguriert.
- JWT-Authentifizierung für sicheren API-Zugriff eingerichtet. Dabei wurden Token-Validierungsparameter wie Aussteller, Zielgruppe und Signaturschlüssel definiert.
- Autorisierungsrichtlinien definiert, um den Zugriff auf Werkzeuge basierend auf Benutzerrollen zu steuern. Zum Beispiel erfordert die Richtlinie „CanUseAdminTools“, dass der Benutzer die Rolle „Admin“ hat, während „CanUseBasic“ eine Authentifizierung des Benutzers voraussetzt.
- MCP-Werkzeuge mit spezifischen Autorisierungsanforderungen registriert, sodass nur Benutzer mit den passenden Rollen Zugriff erhalten.

### Java Spring Security Integration

Für Java verwenden wir Spring Security, um sichere Authentifizierung und Autorisierung für MCP-Server umzusetzen. Spring Security bietet ein umfassendes Sicherheitsframework, das sich nahtlos in Spring-Anwendungen integriert.

Zentrale Konzepte hier sind:

- **Spring Security-Konfiguration**: Einrichtung von Sicherheitskonfigurationen für Authentifizierung und Autorisierung.
- **OAuth2 Resource Server**: Verwendung von OAuth2 für sicheren Zugriff auf MCP-Werkzeuge. OAuth2 ist ein Autorisierungsframework, das Drittanbieterdiensten ermöglicht, Zugriffstoken für sicheren API-Zugriff auszutauschen.
- **Security Interceptors**: Implementierung von Sicherheits-Interceptors, um Zugriffskontrollen bei der Werkzeugausführung durchzusetzen.
- **Rollenbasierte Zugriffskontrolle**: Verwendung von Rollen zur Steuerung des Zugriffs auf spezifische Werkzeuge und Ressourcen.
- **Sicherheitsanmerkungen**: Einsatz von Annotationen, um Methoden und Endpunkte abzusichern.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .csrf().disable()
            .authorizeRequests()
                .antMatchers("/mcp/discovery").permitAll() // Allow tool discovery
                .antMatchers("/mcp/tools/**").hasAnyRole("USER", "ADMIN") // Require authentication for tools
                .antMatchers("/mcp/admin/**").hasRole("ADMIN") // Admin-only endpoints
                .anyRequest().authenticated()
            .and()
            .oauth2ResourceServer().jwt();
    }
    
    @Bean
    public McpSecurityInterceptor mcpSecurityInterceptor() {
        return new McpSecurityInterceptor();
    }
}

// MCP Security Interceptor for tool authorization
public class McpSecurityInterceptor implements ToolExecutionInterceptor {
    @Autowired
    private JwtDecoder jwtDecoder;
    
    @Override
    public void beforeToolExecution(ToolRequest request, Authentication authentication) {
        String toolName = request.getToolName();
        
        // Check if user has permissions for this tool
        if (toolName.startsWith("admin") && !authentication.getAuthorities().contains("ROLE_ADMIN")) {
            throw new AccessDeniedException("You don't have permission to use this tool");
        }
        
        // Additional security checks based on tool or parameters
        if ("sensitiveDataAccess".equals(toolName)) {
            validateDataAccessPermissions(request, authentication);
        }
    }
    
    private void validateDataAccessPermissions(ToolRequest request, Authentication auth) {
        // Implementation to check fine-grained data access permissions
    }
}
```

Im obigen Code haben wir:

- Spring Security konfiguriert, um MCP-Endpunkte abzusichern, öffentlichen Zugriff auf Tool-Discovery zu erlauben und Authentifizierung für die Werkzeugausführung zu verlangen.
- OAuth2 als Resource Server verwendet, um sicheren Zugriff auf MCP-Werkzeuge zu ermöglichen.
- Einen Security Interceptor implementiert, der Zugriffskontrollen bei der Werkzeugausführung durchsetzt und Benutzerrollen sowie Berechtigungen prüft, bevor der Zugriff auf bestimmte Werkzeuge erlaubt wird.
- Rollenbasierte Zugriffskontrolle definiert, um den Zugriff auf Admin-Werkzeuge und den Zugriff auf sensible Daten basierend auf Benutzerrollen einzuschränken.

## Datenschutz und Privatsphäre

Datenschutz ist entscheidend, um sicherzustellen, dass sensible Informationen sicher behandelt werden. Dazu gehört der Schutz personenbezogener Daten (PII), Finanzdaten und anderer sensibler Informationen vor unbefugtem Zugriff und Datenlecks.

### Python Beispiel für Datenschutz

Schauen wir uns ein Beispiel an, wie man Datenschutz in Python mit Verschlüsselung und PII-Erkennung umsetzt.

```python
from mcp_server import McpServer
from mcp_tools import Tool, ToolRequest, ToolResponse
from cryptography.fernet import Fernet
import os
import json
from functools import wraps

# PII Detector - identifies and protects sensitive information
class PiiDetector:
    def __init__(self):
        # Load patterns for different types of PII
        with open("pii_patterns.json", "r") as f:
            self.patterns = json.load(f)
    
    def scan_text(self, text):
        """Scans text for PII and returns detected PII types"""
        detected_pii = []
        # Implementation to detect PII using regex or ML models
        return detected_pii
    
    def scan_parameters(self, parameters):
        """Scans request parameters for PII"""
        detected_pii = []
        for key, value in parameters.items():
            if isinstance(value, str):
                pii_in_value = self.scan_text(value)
                if pii_in_value:
                    detected_pii.append((key, pii_in_value))
        return detected_pii

# Encryption Service for protecting sensitive data
class EncryptionService:
    def __init__(self, key_path=None):
        if key_path and os.path.exists(key_path):
            with open(key_path, "rb") as key_file:
                self.key = key_file.read()
        else:
            self.key = Fernet.generate_key()
            if key_path:
                with open(key_path, "wb") as key_file:
                    key_file.write(self.key)
        
        self.cipher = Fernet(self.key)
    
    def encrypt(self, data):
        """Encrypt data"""
        if isinstance(data, str):
            return self.cipher.encrypt(data.encode()).decode()
        else:
            return self.cipher.encrypt(json.dumps(data).encode()).decode()
    
    def decrypt(self, encrypted_data):
        """Decrypt data"""
        if encrypted_data is None:
            return None
        
        decrypted = self.cipher.decrypt(encrypted_data.encode())
        try:
            return json.loads(decrypted)
        except:
            return decrypted.decode()

# Security decorator for tools
def secure_tool(requires_encryption=False, log_access=True):
    def decorator(cls):
        original_execute = cls.execute_async if hasattr(cls, 'execute_async') else cls.execute
        
        @wraps(original_execute)
        async def secure_execute(self, request):
            # Check for PII in request
            pii_detector = PiiDetector()
            pii_found = pii_detector.scan_parameters(request.parameters)
            
            # Log access if required
            if log_access:
                tool_name = self.get_name()
                user_id = request.context.get("user_id", "anonymous")
                log_entry = {
                    "timestamp": datetime.now().isoformat(),
                    "tool": tool_name,
                    "user": user_id,
                    "contains_pii": bool(pii_found),
                    "parameters": {k: "***" for k in request.parameters.keys()}  # Don't log actual values
                }
                logging.info(f"Tool access: {json.dumps(log_entry)}")
            
            # Handle detected PII
            if pii_found:
                # Either encrypt sensitive data or reject the request
                if requires_encryption:
                    encryption_service = EncryptionService("keys/tool_key.key")
                    for param_name, pii_types in pii_found:
                        # Encrypt the sensitive parameter
                        request.parameters[param_name] = encryption_service.encrypt(
                            request.parameters[param_name]
                        )
                else:
                    # If encryption not available but PII found, you might reject the request
                    raise ToolExecutionException(
                        "Request contains sensitive data that cannot be processed securely"
                    )
            
            # Execute the original method
            return await original_execute(self, request)
        
        # Replace the execute method
        if hasattr(cls, 'execute_async'):
            cls.execute_async = secure_execute
        else:
            cls.execute = secure_execute
        return cls
    
    return decorator

# Example of a secure tool with the decorator
@secure_tool(requires_encryption=True, log_access=True)
class SecureCustomerDataTool(Tool):
    def get_name(self):
        return "customerData"
    
    def get_description(self):
        return "Accesses customer data securely"
    
    def get_schema(self):
        # Schema definition
        return {}
    
    async def execute_async(self, request):
        # Implementation would access customer data securely
        # Since we used the decorator, PII is already detected and encrypted
        return ToolResponse(result={"status": "success"})
```

Im obigen Code haben wir:

- Eine `PiiDetector` class to scan text and parameters for personally identifiable information (PII).
- Created an `EncryptionService` class to handle encryption and decryption of sensitive data using the `cryptography` library.
- Defined a `secure_tool` decorator that wraps tool execution to check for PII, log access, and encrypt sensitive data if required.
- Applied the `secure_tool` decorator to a sample tool (`SecureCustomerDataTool` implementiert, um sicherzustellen, dass sensible Daten sicher verarbeitet werden.

## Was kommt als Nächstes

- [5.9 Web search](../web-search-mcp/README.md)

**Haftungsausschluss**:  
Dieses Dokument wurde mit dem KI-Übersetzungsdienst [Co-op Translator](https://github.com/Azure/co-op-translator) übersetzt. Obwohl wir auf Genauigkeit achten, beachten Sie bitte, dass automatisierte Übersetzungen Fehler oder Ungenauigkeiten enthalten können. Das Originaldokument in seiner Ursprungssprache gilt als maßgebliche Quelle. Für wichtige Informationen wird eine professionelle menschliche Übersetzung empfohlen. Wir übernehmen keine Haftung für Missverständnisse oder Fehlinterpretationen, die aus der Nutzung dieser Übersetzung entstehen.