<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "40b1bbffdb8ce6812bf6e701cad876b6",
  "translation_date": "2025-07-17T19:08:04+00:00",
  "source_file": "03-GettingStarted/06-http-streaming/README.md",
  "language_code": "tl"
}
-->
# HTTPS Streaming gamit ang Model Context Protocol (MCP)

Ang kabanatang ito ay nagbibigay ng komprehensibong gabay sa pagpapatupad ng ligtas, scalable, at real-time na streaming gamit ang Model Context Protocol (MCP) sa pamamagitan ng HTTPS. Tinutukoy nito ang dahilan ng streaming, mga available na mekanismo ng transportasyon, kung paano ipatupad ang streamable HTTP sa MCP, mga pinakamahusay na kasanayan sa seguridad, paglipat mula sa SSE, at praktikal na gabay sa paggawa ng sarili mong streaming MCP na mga aplikasyon.

## Mga Mekanismo ng Transportasyon at Streaming sa MCP

Tinutuklas ng seksyong ito ang iba't ibang mekanismo ng transportasyon na available sa MCP at ang kanilang papel sa pagpapagana ng streaming para sa real-time na komunikasyon sa pagitan ng mga kliyente at server.

### Ano ang Transport Mechanism?

Ang transport mechanism ay tumutukoy kung paano ipinagpapalitan ang data sa pagitan ng kliyente at server. Sinusuportahan ng MCP ang iba't ibang uri ng transport upang umangkop sa iba't ibang kapaligiran at pangangailangan:

- **stdio**: Standard input/output, angkop para sa lokal at CLI-based na mga tool. Simple ngunit hindi angkop para sa web o cloud.
- **SSE (Server-Sent Events)**: Pinapayagan ang mga server na mag-push ng real-time na updates sa mga kliyente sa pamamagitan ng HTTP. Maganda para sa web UI, ngunit limitado sa scalability at flexibility.
- **Streamable HTTP**: Modernong HTTP-based na streaming transport, sumusuporta sa mga notification at mas mahusay na scalability. Inirerekomenda para sa karamihan ng production at cloud na mga senaryo.

### Talahanayan ng Paghahambing

Tingnan ang talahanayan sa ibaba upang maunawaan ang pagkakaiba ng mga mekanismong ito:

| Transport         | Real-time Updates | Streaming | Scalability | Use Case                |
|-------------------|------------------|-----------|-------------|-------------------------|
| stdio             | Hindi            | Hindi     | Mababa      | Lokal na CLI tools      |
| SSE               | Oo               | Oo        | Katamtaman  | Web, real-time updates  |
| Streamable HTTP   | Oo               | Oo        | Mataas      | Cloud, multi-client     |

> **Tip:** Ang pagpili ng tamang transport ay nakakaapekto sa performance, scalability, at karanasan ng gumagamit. **Streamable HTTP** ang inirerekomenda para sa mga modernong, scalable, at cloud-ready na aplikasyon.

Pansinin ang mga transport na stdio at SSE na ipinakita sa mga naunang kabanata at kung paano ang streamable HTTP ang tinalakay sa kabanatang ito.

## Streaming: Mga Konsepto at Dahilan

Mahalagang maunawaan ang mga pangunahing konsepto at dahilan sa likod ng streaming para sa epektibong pagpapatupad ng real-time na komunikasyon.

Ang **streaming** ay isang teknik sa network programming na nagpapahintulot na maipadala at matanggap ang data sa maliliit na bahagi o bilang sunud-sunod na mga pangyayari, sa halip na maghintay na matapos ang buong tugon. Ito ay kapaki-pakinabang lalo na para sa:

- Malalaking file o dataset.
- Real-time na updates (hal., chat, progress bars).
- Mahahabang proseso kung saan nais mong ipaalam agad sa gumagamit ang progreso.

Narito ang mga pangunahing dapat malaman tungkol sa streaming:

- Unti-unting naihahatid ang data, hindi sabay-sabay.
- Maaaring iproseso ng kliyente ang data habang dumarating ito.
- Nakababawas ng latency na nararamdaman at nagpapabuti ng karanasan ng gumagamit.

### Bakit gamitin ang streaming?

Narito ang mga dahilan kung bakit ginagamit ang streaming:

- Agad na nakakatanggap ng feedback ang mga gumagamit, hindi lang sa dulo.
- Nagpapahintulot ng real-time na aplikasyon at responsive na UI.
- Mas epektibong paggamit ng network at compute resources.

### Simpleng Halimbawa: HTTP Streaming Server at Client

Narito ang isang simpleng halimbawa kung paano ipinatutupad ang streaming:

## Python

**Server (Python, gamit ang FastAPI at StreamingResponse):**

### Python

```python
from fastapi import FastAPI
from fastapi.responses import StreamingResponse
import time

app = FastAPI()

async def event_stream():
    for i in range(1, 6):
        yield f"data: Message {i}\n\n"
        time.sleep(1)

@app.get("/stream")
def stream():
    return StreamingResponse(event_stream(), media_type="text/event-stream")
```


**Client (Python, gamit ang requests):**

### Python

```python
import requests

with requests.get("http://localhost:8000/stream", stream=True) as r:
    for line in r.iter_lines():
        if line:
            print(line.decode())
```


Ipinapakita ng halimbawang ito ang server na nagpapadala ng serye ng mga mensahe sa kliyente habang ito ay available, sa halip na maghintay na lahat ng mensahe ay handa na.

**Paano ito gumagana:**
- Ipinapadala ng server ang bawat mensahe kapag ito ay handa na.
- Tinatanggap at ipiniprint ng kliyente ang bawat bahagi habang dumarating.

**Mga Kinakailangan:**
- Dapat gumamit ang server ng streaming response (hal., `StreamingResponse` sa FastAPI).
- Dapat iproseso ng kliyente ang tugon bilang stream (`stream=True` sa requests).
- Karaniwang `Content-Type` ay `text/event-stream` o `application/octet-stream`.

## Java

**Server (Java, gamit ang Spring Boot at Server-Sent Events):**

```java
@RestController
public class CalculatorController {

    @GetMapping(value = "/calculate", produces = MediaType.TEXT_EVENT_STREAM_VALUE)
    public Flux<ServerSentEvent<String>> calculate(@RequestParam double a,
                                                   @RequestParam double b,
                                                   @RequestParam String op) {
        
        double result;
        switch (op) {
            case "add": result = a + b; break;
            case "sub": result = a - b; break;
            case "mul": result = a * b; break;
            case "div": result = b != 0 ? a / b : Double.NaN; break;
            default: result = Double.NaN;
        }

        return Flux.<ServerSentEvent<String>>just(
                    ServerSentEvent.<String>builder()
                        .event("info")
                        .data("Calculating: " + a + " " + op + " " + b)
                        .build(),
                    ServerSentEvent.<String>builder()
                        .event("result")
                        .data(String.valueOf(result))
                        .build()
                )
                .delayElements(Duration.ofSeconds(1));
    }
}
```

**Client (Java, gamit ang Spring WebFlux WebClient):**

```java
@SpringBootApplication
public class CalculatorClientApplication implements CommandLineRunner {

    private final WebClient client = WebClient.builder()
            .baseUrl("http://localhost:8080")
            .build();

    @Override
    public void run(String... args) {
        client.get()
                .uri(uriBuilder -> uriBuilder
                        .path("/calculate")
                        .queryParam("a", 7)
                        .queryParam("b", 5)
                        .queryParam("op", "mul")
                        .build())
                .accept(MediaType.TEXT_EVENT_STREAM)
                .retrieve()
                .bodyToFlux(String.class)
                .doOnNext(System.out::println)
                .blockLast();
    }
}
```

**Mga Tala sa Implementasyon ng Java:**
- Gumagamit ng reactive stack ng Spring Boot gamit ang `Flux` para sa streaming
- `ServerSentEvent` ay nagbibigay ng structured event streaming na may mga uri ng event
- `WebClient` gamit ang `bodyToFlux()` ay nagpapahintulot ng reactive streaming consumption
- `delayElements()` ay nagsisimula ng processing time sa pagitan ng mga event
- Maaaring magkaroon ng mga uri ng event (`info`, `result`) para sa mas mahusay na paghawak ng kliyente

### Paghahambing: Classic Streaming vs MCP Streaming

Ang mga pagkakaiba sa pagitan ng klasikong paraan ng streaming at kung paano ito ginagawa sa MCP ay maaaring ipakita tulad nito:

| Katangian             | Classic HTTP Streaming         | MCP Streaming (Notifications)      |
|-----------------------|-------------------------------|-----------------------------------|
| Pangunahing tugon      | Chunked                       | Isa lang, sa dulo                 |
| Progress updates      | Ipinapadala bilang data chunks | Ipinapadala bilang notifications  |
| Kinakailangan ng kliyente | Kailangang iproseso ang stream | Kailangang mag-implement ng message handler |
| Use case              | Malalaking file, AI token streams | Progreso, logs, real-time feedback |

### Mga Pangunahing Pagkakaiba

Bukod dito, narito ang ilang mahahalagang pagkakaiba:

- **Pattern ng Komunikasyon:**
   - Classic HTTP streaming: Gumagamit ng simpleng chunked transfer encoding para magpadala ng data sa mga bahagi
   - MCP streaming: Gumagamit ng structured notification system gamit ang JSON-RPC protocol

- **Format ng Mensahe:**
   - Classic HTTP: Plain text chunks na may mga newline
   - MCP: Structured LoggingMessageNotification objects na may metadata

- **Implementasyon ng Kliyente:**
   - Classic HTTP: Simpleng kliyente na nagpoproseso ng streaming responses
   - MCP: Mas sopistikadong kliyente na may message handler para iproseso ang iba't ibang uri ng mensahe

- **Progress Updates:**
   - Classic HTTP: Bahagi ng pangunahing response stream ang progreso
   - MCP: Ipinapadala ang progreso sa pamamagitan ng hiwalay na notification messages habang ang pangunahing tugon ay dumarating sa dulo

### Mga Rekomendasyon

Narito ang ilang mga bagay na inirerekomenda kapag pipili sa pagitan ng klasikong streaming (bilang endpoint na ipinakita sa itaas gamit ang `/stream`) at streaming sa MCP.

- **Para sa simpleng pangangailangan sa streaming:** Mas madali ang Classic HTTP streaming at sapat na para sa mga basic na pangangailangan.
- **Para sa mas kumplikado at interactive na aplikasyon:** Nagbibigay ang MCP streaming ng mas istrukturadong paraan na may mas mayamang metadata at paghihiwalay ng notifications at final results.
- **Para sa AI na aplikasyon:** Lalo na kapaki-pakinabang ang notification system ng MCP para sa mahahabang AI tasks kung saan nais mong ipaalam agad sa mga gumagamit ang progreso.

## Streaming sa MCP

Ngayon, nakita mo na ang ilang mga rekomendasyon at paghahambing tungkol sa pagkakaiba ng klasikong streaming at streaming sa MCP. Tingnan natin nang mas detalyado kung paano mo magagamit ang streaming sa MCP.

Mahalagang maunawaan kung paano gumagana ang streaming sa loob ng MCP framework para makabuo ng mga responsive na aplikasyon na nagbibigay ng real-time na feedback sa mga gumagamit habang tumatakbo ang mahahabang operasyon.

Sa MCP, ang streaming ay hindi tungkol sa pagpapadala ng pangunahing tugon sa mga chunks, kundi tungkol sa pagpapadala ng **notifications** sa kliyente habang pinoproseso ng tool ang isang request. Ang mga notification na ito ay maaaring maglaman ng mga update sa progreso, logs, o iba pang mga pangyayari.

### Paano ito gumagana

Ang pangunahing resulta ay ipinapadala pa rin bilang isang solong tugon. Gayunpaman, ang mga notification ay maaaring ipadala bilang hiwalay na mga mensahe habang nagpapatuloy ang proseso at sa gayon ay ina-update ang kliyente nang real time. Dapat kayang hawakan at ipakita ng kliyente ang mga notification na ito.

## Ano ang Notification?

Nabanggit natin ang "Notification", ano ang ibig sabihin nito sa konteksto ng MCP?

Ang notification ay isang mensahe na ipinapadala mula sa server papunta sa kliyente upang ipaalam ang progreso, status, o iba pang mga pangyayari habang tumatakbo ang isang mahahabang operasyon. Pinapabuti ng mga notification ang transparency at karanasan ng gumagamit.

Halimbawa, ang kliyente ay inaasahang magpadala ng notification kapag nagawa na ang initial handshake sa server.

Ganito ang hitsura ng notification bilang isang JSON message:

```json
{
  jsonrpc: "2.0";
  method: string;
  params?: {
    [key: string]: unknown;
  };
}
```

Ang mga notification ay kabilang sa isang topic sa MCP na tinatawag na ["Logging"](https://modelcontextprotocol.io/specification/draft/server/utilities/logging).

Para gumana ang logging, kailangang i-enable ito ng server bilang feature/capability tulad nito:

```json
{
  "capabilities": {
    "logging": {}
  }
}
```

> [!NOTE]
> Depende sa SDK na ginagamit, maaaring naka-enable na ang logging bilang default, o kailangan mo itong i-enable nang manu-mano sa configuration ng server.

May iba't ibang uri ng notification:

| Level     | Paglalarawan                  | Halimbawa ng Paggamit          |
|-----------|------------------------------|-------------------------------|
| debug     | Detalyadong impormasyon para sa debugging | Mga entry/exit point ng function |
| info      | Pangkalahatang impormasyon    | Mga update sa progreso ng operasyon |
| notice    | Normal ngunit mahalagang mga pangyayari | Mga pagbabago sa configuration |
| warning   | Mga kondisyon na babala      | Paggamit ng deprecated na feature |
| error     | Mga kondisyon ng error       | Mga pagkabigo sa operasyon    |
| critical  | Kritikal na kondisyon         | Pagkabigo ng bahagi ng sistema |
| alert     | Kailangang agad na aksyunan   | Natuklasang data corruption   |
| emergency | Hindi magamit ang sistema     | Kumpletong pagkasira ng sistema |

## Pagpapatupad ng Notifications sa MCP

Para magpatupad ng notifications sa MCP, kailangan mong i-setup ang parehong server at client upang hawakan ang real-time na updates. Pinapayagan nito ang iyong aplikasyon na magbigay ng agarang feedback sa mga gumagamit habang tumatakbo ang mahahabang operasyon.

### Sa Server: Pagpapadala ng Notifications

Magsimula tayo sa server side. Sa MCP, nagde-define ka ng mga tool na maaaring magpadala ng notifications habang pinoproseso ang mga request. Ginagamit ng server ang context object (karaniwang `ctx`) para magpadala ng mga mensahe sa kliyente.

### Python

```python
@mcp.tool(description="A tool that sends progress notifications")
async def process_files(message: str, ctx: Context) -> TextContent:
    await ctx.info("Processing file 1/3...")
    await ctx.info("Processing file 2/3...")
    await ctx.info("Processing file 3/3...")
    return TextContent(type="text", text=f"Done: {message}")
```

Sa naunang halimbawa, ang `process_files` tool ay nagpapadala ng tatlong notifications sa kliyente habang pinoproseso ang bawat file. Ginagamit ang `ctx.info()` method para magpadala ng mga informational messages.

Bukod dito, para paganahin ang notifications, siguraduhing gumagamit ang server ng streaming transport (tulad ng `streamable-http`) at ang kliyente ay may message handler para iproseso ang notifications. Ganito ang pag-setup ng server para gamitin ang `streamable-http` transport:

```python
mcp.run(transport="streamable-http")
```

### .NET

```csharp
[Tool("A tool that sends progress notifications")]
public async Task<TextContent> ProcessFiles(string message, ToolContext ctx)
{
    await ctx.Info("Processing file 1/3...");
    await ctx.Info("Processing file 2/3...");
    await ctx.Info("Processing file 3/3...");
    return new TextContent
    {
        Type = "text",
        Text = $"Done: {message}"
    };
}
```

Sa halimbawang .NET na ito, ang `ProcessFiles` tool ay may `Tool` attribute at nagpapadala ng tatlong notifications sa kliyente habang pinoproseso ang bawat file. Ginagamit ang `ctx.Info()` method para magpadala ng informational messages.

Para paganahin ang notifications sa iyong .NET MCP server, siguraduhing gumagamit ka ng streaming transport:

```csharp
var builder = McpBuilder.Create();
await builder
    .UseStreamableHttp() // Enable streamable HTTP transport
    .Build()
    .RunAsync();
```

### Sa Client: Pagtanggap ng Notifications

Dapat mag-implementa ang kliyente ng message handler para iproseso at ipakita ang mga notification habang dumarating.

### Python

```python
async def message_handler(message):
    if isinstance(message, types.ServerNotification):
        print("NOTIFICATION:", message)
    else:
        print("SERVER MESSAGE:", message)

async with ClientSession(
   read_stream, 
   write_stream,
   logging_callback=logging_collector,
   message_handler=message_handler,
) as session:
```

Sa code na ito, sinusuri ng `message_handler` function kung ang papasok na mensahe ay notification. Kung oo, ipiniprint nito ang notification; kung hindi, ipoproseso ito bilang regular na mensahe mula sa server. Pansinin din kung paano ini-initialize ang `ClientSession` gamit ang `message_handler` para hawakan ang mga papasok na notification.

### .NET

```csharp
// Define a message handler
void MessageHandler(IJsonRpcMessage message)
{
    if (message is ServerNotification notification)
    {
        Console.WriteLine($"NOTIFICATION: {notification}");
    }
    else
    {
        Console.WriteLine($"SERVER MESSAGE: {message}");
    }
}

// Create and use a client session with the message handler
var clientOptions = new ClientSessionOptions
{
    MessageHandler = MessageHandler,
    LoggingCallback = (level, message) => Console.WriteLine($"[{level}] {message}")
};

using var client = new ClientSession(readStream, writeStream, clientOptions);
await client.InitializeAsync();

// Now the client will process notifications through the MessageHandler
```

Sa halimbawang .NET na ito, sinusuri ng `MessageHandler` function kung ang papasok na mensahe ay notification. Kung oo, ipiniprint nito ang notification; kung hindi, ipoproseso ito bilang regular na mensahe mula sa server. Ini-initialize ang `ClientSession` gamit ang message handler sa pamamagitan ng `ClientSessionOptions`.

Para paganahin ang notifications, siguraduhing gumagamit ang server ng streaming transport (tulad ng `streamable-http`) at ang kliyente ay may message handler para iproseso ang notifications.

## Progress Notifications at Mga Senaryo

Ipinaliwanag sa seksyong ito ang konsepto ng progress notifications sa MCP, bakit ito mahalaga, at kung paano ito ipinatutupad gamit ang Streamable HTTP. Makakakita ka rin ng praktikal na gawain para palalimin ang iyong pag-unawa.

Ang progress notifications ay mga real-time na mensahe na ipinapadala mula sa server papunta sa kliyente habang tumatakbo ang mahahabang operasyon. Sa halip na maghintay na matapos ang buong proseso, patuloy na ina-update ng server ang kliyente tungkol sa kasalukuyang estado. Pinapabuti nito ang transparency, karanasan ng gumagamit, at nagpapadali ng debugging.

**Halimbawa:**

```text

"Processing document 1/10"
"Processing document 2/10"
...
"Processing complete!"

```

### Bakit Gamitin ang Progress Notifications?

Mahalaga ang progress notifications dahil sa mga sumusunod:

- **Mas magandang karanasan ng gumagamit:** Nakikita ng mga gumagamit ang mga update habang nagpapatuloy ang trabaho, hindi lang sa dulo.
- **Real-time na feedback:** Maaaring magpakita ang mga kliyente ng progress bars o logs, kaya mas responsive ang app.
- **Mas madaling debugging at monitoring:** Nakikita ng mga developer at gumagamit kung saan maaaring mabagal o maipit ang proseso.

### Paano Ipatupad ang Progress Notifications

Ganito ang paraan ng pagpapatupad ng progress notifications sa MCP:

- **Sa server:** Gamitin ang `ctx.info()` o `ctx.log()` para magpadala ng notifications habang pinoproseso ang bawat item. Nagpapadala ito ng mensahe sa kliyente bago pa man maging handa ang pangunahing resulta.
- **Sa kliyente:** Mag-implementa ng message handler na nakikinig at nagpapakita ng notifications habang dumarating. Nakikilala ng handler ang pagkakaiba ng notifications at ng panghuling resulta.

**Halimbawa ng Server:**

## Python

```python
@mcp.tool(description="A tool that sends progress notifications")
async def process_files(message: str, ctx: Context) -> TextContent:
    for i in range(1, 11):
        await ctx.info(f"Processing document {i}/10")
    await ctx.info("Processing complete!")
    return TextContent(type="text", text=f"Done: {message}")
```


**Halimbawa ng Kliyente:**

### Python

```python
async def message_handler(message):
    if isinstance(message, types.ServerNotification):
        print("NOTIFICATION:", message)
    else:
        print("SERVER MESSAGE:", message)
```


## Mga Pagsasaalang-alang sa Seguridad

Kapag nagpapatupad ng MCP servers gamit ang HTTP-based transports, ang seguridad ay isang napakahalagang aspeto na nangangailangan ng maingat na pagtingin sa iba't ibang uri ng pag-atake at mga mekanismo ng proteksyon.

### Pangkalahatang-ideya

Mahalaga ang seguridad kapag inilalantad ang MCP servers sa HTTP. Nagdadala ang Streamable HTTP ng mga bagong panganib at nangangailangan ng maingat na pagsasaayos.

### Mga Pangunahing Punto
- **Pag-validate ng Origin Header**: Laging i-validate ang `Origin` header upang maiwasan ang DNS rebinding attacks.
- **Localhost Binding**: Para sa lokal na development, i-bind ang mga server sa `localhost` upang hindi ito ma-expose sa publiko.
- **Authentication**: Magpatupad ng authentication (hal., API keys, OAuth) para sa production deployment.
- **CORS**: I-configure ang Cross-Origin Resource Sharing (CORS) policies upang limitahan ang access.
- **HTTPS**: Gumamit ng HTTPS sa production para i-encrypt ang traffic.

### Mga Pinakamahusay na Kasanayan
- Huwag kailanman pagkatiwalaan ang mga papasok na request nang walang validation.
- Mag-log at mag-monitor ng lahat ng access at error.
- Regular na i-update ang mga dependencies upang ma-patch ang mga security vulnerabilities.

### Mga Hamon
- Pagtutugma ng seguridad at kadalian ng development
- Pagsiguro ng compatibility sa iba't ibang client environment

## Pag-upgrade mula SSE papuntang Streamable HTTP

Para sa mga aplikasyon na kasalukuyang gumagamit ng Server-Sent Events (SSE), ang paglipat sa Streamable HTTP ay nagbibigay ng mas pinahusay na kakayahan at mas magandang pangmatagalang sustainability para sa iyong mga implementasyon ng MCP.
### Bakit Mag-upgrade?

May dalawang mahahalagang dahilan para mag-upgrade mula SSE patungong Streamable HTTP:

- Nagbibigay ang Streamable HTTP ng mas mahusay na scalability, compatibility, at mas malawak na suporta sa mga notification kumpara sa SSE.
- Ito ang inirerekomendang transport para sa mga bagong MCP application.

### Mga Hakbang sa Paglipat

Ganito ang paraan para mag-migrate mula SSE patungong Streamable HTTP sa iyong mga MCP application:

- **I-update ang server code** upang gamitin ang `transport="streamable-http"` sa `mcp.run()`.
- **I-update ang client code** upang gamitin ang `streamablehttp_client` sa halip na SSE client.
- **Mag-implement ng message handler** sa client para iproseso ang mga notification.
- **Subukan ang compatibility** gamit ang mga kasalukuyang tools at workflows.

### Pagpapanatili ng Compatibility

Inirerekomenda na panatilihin ang compatibility sa mga kasalukuyang SSE client habang nagmi-migrate. Narito ang ilang mga estratehiya:

- Maaari mong suportahan ang parehong SSE at Streamable HTTP sa pamamagitan ng pagpapatakbo ng parehong transport sa magkaibang endpoints.
- Unti-unting ilipat ang mga client sa bagong transport.

### Mga Hamon

Siguraduhing matugunan ang mga sumusunod na hamon habang nagmi-migrate:

- Pagtiyak na lahat ng client ay na-update
- Pag-handle ng mga pagkakaiba sa paraan ng paghahatid ng notification

## Mga Pagsasaalang-alang sa Seguridad

Dapat unahin ang seguridad kapag nag-iimplementa ng anumang server, lalo na kapag gumagamit ng HTTP-based transports tulad ng Streamable HTTP sa MCP.

Kapag nag-iimplementa ng MCP server gamit ang HTTP-based transports, mahalaga ang seguridad at nangangailangan ng maingat na pagtingin sa iba't ibang paraan ng pag-atake at mga mekanismo ng proteksyon.

### Pangkalahatang-ideya

Mahalaga ang seguridad kapag inilalantad ang MCP server sa HTTP. Nagdadala ang Streamable HTTP ng mga bagong panganib at nangangailangan ng maingat na pagsasaayos.

Narito ang ilang mahahalagang pagsasaalang-alang sa seguridad:

- **Pag-validate ng Origin Header**: Laging i-validate ang `Origin` header upang maiwasan ang DNS rebinding attacks.
- **Localhost Binding**: Para sa lokal na development, i-bind ang server sa `localhost` upang hindi ito ma-expose sa pampublikong internet.
- **Authentication**: Mag-implementa ng authentication (hal. API keys, OAuth) para sa production deployment.
- **CORS**: Isaayos ang Cross-Origin Resource Sharing (CORS) policies upang limitahan ang access.
- **HTTPS**: Gumamit ng HTTPS sa production para i-encrypt ang traffic.

### Mga Pinakamahusay na Gawain

Bukod dito, narito ang ilang pinakamahusay na gawain sa pag-implementa ng seguridad sa iyong MCP streaming server:

- Huwag kailanman pagkatiwalaan ang mga papasok na request nang walang validation.
- I-log at i-monitor ang lahat ng access at error.
- Regular na i-update ang mga dependencies upang ma-patch ang mga security vulnerabilities.

### Mga Hamon

Makakaharap ka ng ilang hamon sa pag-implementa ng seguridad sa MCP streaming servers:

- Pagtutugma ng seguridad at pagiging madali sa development
- Pagtiyak ng compatibility sa iba't ibang client environment

### Takdang-Aralin: Gumawa ng Sariling Streaming MCP App

**Senaryo:**
Gumawa ng MCP server at client kung saan pinoproseso ng server ang isang listahan ng mga item (hal. mga file o dokumento) at nagpapadala ng notification para sa bawat item na naproseso. Dapat ipakita ng client ang bawat notification habang dumarating ito.

**Mga Hakbang:**

1. Mag-implementa ng server tool na nagpoproseso ng listahan at nagpapadala ng notification para sa bawat item.
2. Mag-implementa ng client na may message handler para ipakita ang mga notification nang real time.
3. Subukan ang iyong implementasyon sa pamamagitan ng pagpapatakbo ng parehong server at client, at obserbahan ang mga notification.

[Solution](./solution/README.md)

## Karagdagang Babasahin at Ano ang Susunod?

Para ipagpatuloy ang iyong paglalakbay sa MCP streaming at palawakin ang iyong kaalaman, nagbibigay ang seksyong ito ng karagdagang mga resources at mga mungkahing susunod na hakbang para sa paggawa ng mas advanced na mga application.

### Karagdagang Babasahin

- [Microsoft: Introduction to HTTP Streaming](https://learn.microsoft.com/aspnet/core/fundamentals/http-requests?view=aspnetcore-8.0&WT.mc_id=%3Fwt.mc_id%3DMVP_452430#streaming)
- [Microsoft: Server-Sent Events (SSE)](https://learn.microsoft.com/azure/application-gateway/for-containers/server-sent-events?tabs=server-sent-events-gateway-api&WT.mc_id=%3Fwt.mc_id%3DMVP_452430)
- [Microsoft: CORS in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/security/cors?view=aspnetcore-8.0&WT.mc_id=%3Fwt.mc_id%3DMVP_452430)
- [Python requests: Streaming Requests](https://requests.readthedocs.io/en/latest/user/advanced/#streaming-requests)

### Ano ang Susunod?

- Subukang gumawa ng mas advanced na MCP tools na gumagamit ng streaming para sa real-time analytics, chat, o collaborative editing.
- Tuklasin ang integrasyon ng MCP streaming sa mga frontend framework (React, Vue, atbp.) para sa live na pag-update ng UI.
- Susunod: [Utilising AI Toolkit for VSCode](../07-aitk/README.md)

**Paalala**:  
Ang dokumentong ito ay isinalin gamit ang AI translation service na [Co-op Translator](https://github.com/Azure/co-op-translator). Bagamat nagsusumikap kami para sa katumpakan, pakatandaan na ang mga awtomatikong pagsasalin ay maaaring maglaman ng mga pagkakamali o di-tumpak na impormasyon. Ang orihinal na dokumento sa orihinal nitong wika ang dapat ituring na pangunahing sanggunian. Para sa mahahalagang impormasyon, inirerekomenda ang propesyonal na pagsasalin ng tao. Hindi kami mananagot sa anumang hindi pagkakaunawaan o maling interpretasyon na maaaring magmula sa paggamit ng pagsasaling ito.