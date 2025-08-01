<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ac67652abc453e2a7e2c75cd7a8897ae",
  "translation_date": "2025-07-13T18:07:32+00:00",
  "source_file": "03-GettingStarted/01-first-server/solution/typescript/README.md",
  "language_code": "sr"
}
-->
# Покретање овог примера

Препоручује се да инсталирате `uv`, али није обавезно, погледајте [упутства](https://docs.astral.sh/uv/#highlights)

## -1- Инсталирајте зависности

```bash
npm install
```

## -3- Покрените пример


```bash
npm run build
```

## -4- Тестирајте пример

Док сервер ради у једном терминалу, отворите други терминал и покрените следећу команду:

```bash
npm run inspector
```

Ово би требало да покрене веб сервер са визуелним интерфејсом који вам омогућава да тестирате пример.

Када се сервер повеже:

- покушајте да набројите алате и покренете `add` са аргументима 2 и 4, требало би да видите резултат 6.
- идите на resources и resource template и позовите "greeting", унесите име и требало би да видите поздрав са именом које сте унели.

### Тестирање у CLI режиму

Инспектор који сте покренули је у ствари Node.js апликација, а `mcp dev` је омотач око ње.

Можете га покренути директно у CLI режиму покретањем следеће команде:

```bash
npx @modelcontextprotocol/inspector --cli node ./build/index.js --method tools/list
```

Ово ће набројати све алате доступне на серверу. Требало би да видите следећи излаз:

```text
{
  "tools": [
    {
      "name": "add",
      "description": "Add two numbers",
      "inputSchema": {
        "type": "object",
        "properties": {
          "a": {
            "title": "A",
            "type": "integer"
          },
          "b": {
            "title": "B",
            "type": "integer"
          }
        },
        "required": [
          "a",
          "b"
        ],
        "title": "addArguments"
      }
    }
  ]
}
```

Да бисте позвали алат укуцајте:

```bash
nnpx @modelcontextprotocol/inspector --cli node ./build/index.js --method tools/call --tool-name add --tool-arg a=1 --tool-arg b=2
```

Требало би да видите следећи излаз:

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
> Обично је много брже покренути инспектор у CLI режиму него у прегледачу.
> Више о инспектору прочитајте [овде](https://github.com/modelcontextprotocol/inspector).

**Одрицање од одговорности**:  
Овај документ је преведен коришћењем AI сервиса за превођење [Co-op Translator](https://github.com/Azure/co-op-translator). Иако се трудимо да превод буде тачан, молимо вас да имате у виду да аутоматски преводи могу садржати грешке или нетачности. Оригинални документ на његовом изворном језику треба сматрати ауторитетним извором. За критичне информације препоручује се професионални људски превод. Нисмо одговорни за било каква неспоразума или погрешна тумачења настала коришћењем овог превода.