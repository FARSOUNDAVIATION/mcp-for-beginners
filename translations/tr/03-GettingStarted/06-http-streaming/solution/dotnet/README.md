<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4eb6a48c54555c64b33c763fba3f2842",
  "translation_date": "2025-07-13T21:04:24+00:00",
  "source_file": "03-GettingStarted/06-http-streaming/solution/dotnet/README.md",
  "language_code": "tr"
}
-->
# Bu örneği çalıştırma

## -1- Bağımlılıkları yükleyin

```bash
dotnet restore
```

## -2- Örneği çalıştırın

```bash
dotnet run
```

## -3- Örneği test edin

Aşağıdaki komutu çalıştırmadan önce ayrı bir terminal açın (sunucunun hala çalıştığından emin olun).

Sunucu bir terminalde çalışırken, başka bir terminal açın ve aşağıdaki komutu çalıştırın:

```bash
npx @modelcontextprotocol/inspector http://localhost:3001
```

Bu, örneği test etmenize olanak tanıyan görsel arayüze sahip bir web sunucusu başlatmalıdır.

> **Streamable HTTP**'nin taşıma türü olarak seçili olduğundan ve URL'nin `http://localhost:3001/mcp` olduğundan emin olun.

Sunucu bağlandıktan sonra:

- araçları listelemeyi deneyin ve `add` komutunu, argümanlar olarak 2 ve 4 ile çalıştırın, sonuçta 6 görmelisiniz.
- resources ve resource template bölümüne gidin, "greeting"i çağırın, bir isim yazın ve verdiğiniz isimle bir selamlama görmelisiniz.

### CLI modunda test etme

Aşağıdaki komutu çalıştırarak doğrudan CLI modunda başlatabilirsiniz:

```bash 
npx @modelcontextprotocol/inspector --cli http://localhost:3001 --method tools/list
```

Bu, sunucuda mevcut olan tüm araçları listeleyecektir. Aşağıdaki çıktıyı görmelisiniz:

```text
{
  "tools": [
    {
      "name": "AddNumbers",
      "description": "Add two numbers together.",
      "inputSchema": {
        "type": "object",
        "properties": {
          "a": {
            "description": "The first number",
            "type": "integer"
          },
          "b": {
            "description": "The second number",
            "type": "integer"
          }
        },
        "title": "AddNumbers",
        "description": "Add two numbers together.",
        "required": [
          "a",
          "b"
        ]
      }
    }
  ]
}
```

Bir aracı çağırmak için şunu yazın:

```bash
npx @modelcontextprotocol/inspector --cli http://localhost:3001 --method tools/call --tool-name AddNumbers --tool-arg a=1 --tool-arg b=2
```

Aşağıdaki çıktıyı görmelisiniz:

```text
{
  "content": [
    {
      "type": "text",
      "text": "3"
    }
  ],
  "isError": false
}
```

> ![!TIP]
> Inspector'ı tarayıcıda çalıştırmaktansa CLI modunda çalıştırmak genellikle çok daha hızlıdır.
> Inspector hakkında daha fazla bilgi için [buraya](https://github.com/modelcontextprotocol/inspector) bakabilirsiniz.

**Feragatname**:  
Bu belge, AI çeviri servisi [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba göstersek de, otomatik çevirilerin hatalar veya yanlışlıklar içerebileceğini lütfen unutmayın. Orijinal belge, kendi dilinde yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımı sonucu ortaya çıkabilecek yanlış anlamalar veya yorum hatalarından sorumlu değiliz.