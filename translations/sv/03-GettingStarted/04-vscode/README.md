<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "8ea28e5e566edd5969337fd0b191ba3f",
  "translation_date": "2025-07-17T06:18:50+00:00",
  "source_file": "03-GettingStarted/04-vscode/README.md",
  "language_code": "sv"
}
-->
# Använda en server från GitHub Copilot Agent-läge

Visual Studio Code och GitHub Copilot kan agera som klient och använda en MCP-server. Du kanske undrar varför man skulle vilja göra det? Jo, det innebär att alla funktioner som MCP-servern har nu kan användas direkt i din IDE. Föreställ dig att du till exempel lägger till GitHubs MCP-server, vilket skulle göra det möjligt att styra GitHub via prompts istället för att skriva specifika kommandon i terminalen. Eller tänk på vad som helst som kan förbättra din utvecklarupplevelse, allt styrt med naturligt språk. Nu börjar du se fördelen, eller hur?

## Översikt

Den här lektionen visar hur du använder Visual Studio Code och GitHub Copilots Agent-läge som klient för din MCP-server.

## Lärandemål

I slutet av denna lektion kommer du att kunna:

- Använda en MCP-server via Visual Studio Code.
- Köra funktioner som verktyg via GitHub Copilot.
- Konfigurera Visual Studio Code för att hitta och hantera din MCP-server.

## Användning

Du kan styra din MCP-server på två olika sätt:

- Användargränssnitt, du kommer att se hur detta görs senare i detta kapitel.
- Terminal, det är möjligt att styra saker från terminalen med `code`-exekverbara filen:

  För att lägga till en MCP-server till din användarprofil, använd kommandoradsalternativet --add-mcp och ange JSON-serverkonfigurationen i formen {\"name\":\"server-namn\",\"command\":...}.

  ```
  code --add-mcp "{\"name\":\"my-server\",\"command\": \"uvx\",\"args\": [\"mcp-server-fetch\"]}"
  ```

### Skärmbilder

![Guided MCP server configuration in Visual Studio Code](../../../../translated_images/chat-mode-agent.729a22473f822216dd1e723aaee1f7d4a2ede571ee0948037a2d9357a63b9d0b.sv.png)  
![Verktygsval per agent-session](../../../../translated_images/agent-mode-select-tools.522c7ba5df0848f8f0d1e439c2e96159431bc620cb39ccf3f5dc611412fd0006.sv.png)  
![Felsök enkelt fel under MCP-utveckling](../../../../translated_images/mcp-list-servers.fce89eefe3f30032bed8952e110ab9d82fadf043fcfa071f7d40cf93fb1ea9e9.sv.png)

Låt oss prata mer om hur vi använder det visuella gränssnittet i nästa avsnitt.

## Tillvägagångssätt

Så här behöver vi gå tillväga på en övergripande nivå:

- Konfigurera en fil för att hitta vår MCP-server.
- Starta/anslut till servern för att få en lista över dess funktioner.
- Använd dessa funktioner via GitHub Copilot Chat-gränssnittet.

Bra, nu när vi förstår flödet, låt oss prova att använda en MCP-server genom Visual Studio Code i en övning.

## Övning: Använda en server

I denna övning ska vi konfigurera Visual Studio Code för att hitta din MCP-server så att den kan användas från GitHub Copilot Chat-gränssnittet.

### -0- Förberedelse, aktivera MCP Server-upptäckt

Du kan behöva aktivera upptäckt av MCP-servrar.

1. Gå till `File -> Preferences -> Settings` i Visual Studio Code.

1. Sök efter "MCP" och aktivera `chat.mcp.discovery.enabled` i settings.json-filen.

### -1- Skapa konfigurationsfil

Börja med att skapa en konfigurationsfil i din projektrot, du behöver en fil som heter MCP.json och placera den i en mapp som heter .vscode. Den ska se ut så här:

```text
.vscode
|-- mcp.json
```

Nästa steg är att se hur vi kan lägga till en serverpost.

### -2- Konfigurera en server

Lägg till följande innehåll i *mcp.json*:

```json
{
    "inputs": [],
    "servers": {
       "hello-mcp": {
           "command": "node",
           "args": [
               "build/index.js"
           ]
       }
    }
}
```

Här ovan är ett enkelt exempel på hur man startar en server skriven i Node.js, för andra körmiljöer anger du rätt kommando för att starta servern med `command` och `args`.

### -3- Starta servern

Nu när du har lagt till en post, låt oss starta servern:

1. Hitta din post i *mcp.json* och se till att du hittar "play"-ikonen:

  ![Starta server i Visual Studio Code](../../../../translated_images/vscode-start-server.8e3c986612e3555de47e5b1e37b2f3020457eeb6a206568570fd74a17e3796ad.sv.png)  

1. Klicka på "play"-ikonen, du bör se att verktygsikonen i GitHub Copilot Chat ökar antalet tillgängliga verktyg. Om du klickar på verktygsikonen ser du en lista över registrerade verktyg. Du kan kryssa i eller ur varje verktyg beroende på om du vill att GitHub Copilot ska använda dem som kontext:

  ![Starta server i Visual Studio Code](../../../../translated_images/vscode-tool.0b3bbea2fb7d8c26ddf573cad15ef654e55302a323267d8ee6bd742fe7df7fed.sv.png)

1. För att köra ett verktyg, skriv en prompt som du vet matchar beskrivningen av ett av dina verktyg, till exempel en prompt som "add 22 to 1":

  ![Köra ett verktyg från GitHub Copilot](../../../../translated_images/vscode-agent.d5a0e0b897331060518fe3f13907677ef52b879db98c64d68a38338608f3751e.sv.png)

  Du bör få ett svar som säger 23.

## Uppgift

Försök att lägga till en serverpost i din *mcp.json*-fil och se till att du kan starta och stoppa servern. Kontrollera också att du kan kommunicera med verktygen på din server via GitHub Copilot Chat-gränssnittet.

## Lösning

[Solution](./solution/README.md)

## Viktiga punkter

De viktigaste punkterna från detta kapitel är:

- Visual Studio Code är en utmärkt klient som låter dig använda flera MCP-servrar och deras verktyg.
- GitHub Copilot Chat-gränssnittet är hur du interagerar med servrarna.
- Du kan be användaren om indata som API-nycklar som kan skickas till MCP-servern när du konfigurerar serverposten i *mcp.json*-filen.

## Exempel

- [Java Calculator](../samples/java/calculator/README.md)
- [.Net Calculator](../../../../03-GettingStarted/samples/csharp)
- [JavaScript Calculator](../samples/javascript/README.md)
- [TypeScript Calculator](../samples/typescript/README.md)
- [Python Calculator](../../../../03-GettingStarted/samples/python)

## Ytterligare resurser

- [Visual Studio docs](https://code.visualstudio.com/docs/copilot/chat/mcp-servers)

## Vad händer härnäst

- Nästa: [Creating an SSE Server](../05-sse-server/README.md)

**Ansvarsfriskrivning**:  
Detta dokument har översatts med hjälp av AI-översättningstjänsten [Co-op Translator](https://github.com/Azure/co-op-translator). Även om vi strävar efter noggrannhet, vänligen observera att automatiska översättningar kan innehålla fel eller brister. Det ursprungliga dokumentet på dess modersmål bör betraktas som den auktoritativa källan. För kritisk information rekommenderas professionell mänsklig översättning. Vi ansvarar inte för eventuella missförstånd eller feltolkningar som uppstår vid användning av denna översättning.