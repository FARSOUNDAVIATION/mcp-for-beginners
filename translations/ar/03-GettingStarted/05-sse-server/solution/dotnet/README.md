<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2a58caa6e11faa09470b7f81e6729652",
  "translation_date": "2025-07-13T20:07:59+00:00",
  "source_file": "03-GettingStarted/05-sse-server/solution/dotnet/README.md",
  "language_code": "ar"
}
-->
# تشغيل هذا المثال

## -1- تثبيت التبعيات

```bash
dotnet restore
```

## -2- تشغيل المثال

```bash
dotnet run
```

## -3- اختبار المثال

ابدأ نافذة طرفية جديدة قبل تشغيل الأمر أدناه (تأكد من أن الخادم لا يزال يعمل).

مع تشغيل الخادم في نافذة طرفية واحدة، افتح نافذة طرفية أخرى وقم بتشغيل الأمر التالي:

```bash
npx @modelcontextprotocol/inspector http://localhost:3001
```

يجب أن يبدأ هذا خادم ويب بواجهة مرئية تتيح لك اختبار المثال.

> تأكد من اختيار **SSE** كنوع النقل، وأن عنوان URL هو `http://localhost:3001/sse`.

بمجرد اتصال الخادم:

- جرب قائمة الأدوات وقم بتشغيل `add` مع الوسيطات 2 و4، يجب أن ترى النتيجة 6.
- انتقل إلى الموارد وقالب الموارد واستدعِ "greeting"، اكتب اسمًا ويجب أن ترى تحية بالاسم الذي أدخلته.

### الاختبار في وضع CLI

يمكنك تشغيله مباشرة في وضع CLI عن طريق تنفيذ الأمر التالي:

```bash 
npx @modelcontextprotocol/inspector --cli http://localhost:3001 --method tools/list
```

سيعرض هذا جميع الأدوات المتاحة في الخادم. يجب أن ترى المخرجات التالية:

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

لاستدعاء أداة اكتب:

```bash
npx @modelcontextprotocol/inspector --cli http://localhost:3001 --method tools/call --tool-name AddNumbers --tool-arg a=1 --tool-arg b=2
```

يجب أن ترى المخرجات التالية:

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
> عادةً ما يكون تشغيل الـ inspector في وضع CLI أسرع بكثير من تشغيله في المتصفح.
> اقرأ المزيد عن الـ inspector [هنا](https://github.com/modelcontextprotocol/inspector).

**إخلاء المسؤولية**:  
تمت ترجمة هذا المستند باستخدام خدمة الترجمة الآلية [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو عدم دقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الموثوق به. للمعلومات الهامة، يُنصح بالاعتماد على الترجمة البشرية المهنية. نحن غير مسؤولين عن أي سوء فهم أو تفسير ناتج عن استخدام هذه الترجمة.