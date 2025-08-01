<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7b4b9bfacd2926725e6f1cda82bc8ff5",
  "translation_date": "2025-07-17T07:32:39+00:00",
  "source_file": "06-CommunityContributions/README.md",
  "language_code": "vi"
}
-->
# Cộng đồng và Đóng góp

## Tổng quan

Bài học này tập trung vào cách tham gia cộng đồng MCP, đóng góp vào hệ sinh thái MCP và tuân theo các thực hành tốt nhất trong phát triển hợp tác. Hiểu cách tham gia các dự án MCP mã nguồn mở là điều cần thiết cho những ai muốn định hình tương lai của công nghệ này.

## Mục tiêu học tập

Sau bài học này, bạn sẽ có thể:
- Hiểu cấu trúc của cộng đồng và hệ sinh thái MCP
- Tham gia hiệu quả vào các diễn đàn và thảo luận của cộng đồng MCP
- Đóng góp vào các kho mã nguồn mở MCP
- Tạo và chia sẻ các công cụ và máy chủ MCP tùy chỉnh
- Tuân theo các thực hành tốt nhất trong phát triển và hợp tác MCP
- Khám phá các tài nguyên và framework cộng đồng dành cho phát triển MCP

## Hệ sinh thái cộng đồng MCP

Hệ sinh thái MCP bao gồm nhiều thành phần và người tham gia cùng làm việc để phát triển giao thức.

### Các thành phần chính của cộng đồng

1. **Người duy trì giao thức cốt lõi**: Tổ chức [Model Context Protocol GitHub](https://github.com/modelcontextprotocol) chính thức duy trì các đặc tả cốt lõi và các triển khai tham chiếu của MCP
2. **Nhà phát triển công cụ**: Cá nhân và nhóm tạo ra các công cụ và máy chủ MCP
3. **Nhà cung cấp tích hợp**: Các công ty tích hợp MCP vào sản phẩm và dịch vụ của họ
4. **Người dùng cuối**: Các nhà phát triển và tổ chức sử dụng MCP trong ứng dụng của họ
5. **Người đóng góp**: Thành viên cộng đồng đóng góp mã, tài liệu hoặc các tài nguyên khác

### Tài nguyên cộng đồng

#### Kênh chính thức

- [Tổ chức MCP trên GitHub](https://github.com/modelcontextprotocol)
- [Tài liệu MCP](https://modelcontextprotocol.io/)
- [Đặc tả MCP](https://modelcontextprotocol.io/docs/specification)
- [Thảo luận trên GitHub](https://github.com/orgs/modelcontextprotocol/discussions)
- [Kho ví dụ & máy chủ MCP](https://github.com/modelcontextprotocol/servers)

#### Tài nguyên do cộng đồng phát triển

- [Khách hàng MCP](https://modelcontextprotocol.io/clients) - Danh sách các client hỗ trợ tích hợp MCP
- [Máy chủ MCP do cộng đồng phát triển](https://github.com/modelcontextprotocol/servers?tab=readme-ov-file#-community-servers) - Danh sách ngày càng tăng các máy chủ MCP do cộng đồng phát triển
- [Awesome MCP Servers](https://github.com/wong2/awesome-mcp-servers) - Danh sách được tuyển chọn các máy chủ MCP
- [PulseMCP](https://www.pulsemcp.com/) - Trung tâm cộng đồng & bản tin để khám phá tài nguyên MCP
- [Máy chủ Discord](https://discord.gg/jHEGxQu2a5) - Kết nối với các nhà phát triển MCP
- Các triển khai SDK theo ngôn ngữ
- Bài viết blog và hướng dẫn

## Đóng góp cho MCP

### Các loại đóng góp

Hệ sinh thái MCP chào đón nhiều loại đóng góp khác nhau:

1. **Đóng góp mã nguồn**:
   - Cải tiến giao thức cốt lõi
   - Sửa lỗi
   - Triển khai công cụ và máy chủ
   - Thư viện client/server bằng các ngôn ngữ khác nhau

2. **Tài liệu**:
   - Cải thiện tài liệu hiện có
   - Tạo hướng dẫn và bài học
   - Dịch tài liệu
   - Tạo ví dụ và ứng dụng mẫu

3. **Hỗ trợ cộng đồng**:
   - Trả lời câu hỏi trên diễn đàn và thảo luận
   - Kiểm thử và báo cáo lỗi
   - Tổ chức sự kiện cộng đồng
   - Hướng dẫn người đóng góp mới

### Quy trình đóng góp: Giao thức cốt lõi

Để đóng góp vào giao thức MCP cốt lõi hoặc các triển khai chính thức, hãy tuân theo các nguyên tắc từ [hướng dẫn đóng góp chính thức](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/CONTRIBUTING.md):

1. **Đơn giản và Tối giản**: Đặc tả MCP đặt tiêu chuẩn cao cho việc thêm khái niệm mới. Việc thêm vào đặc tả dễ hơn là loại bỏ.
2. **Cách tiếp cận cụ thể**: Thay đổi đặc tả nên dựa trên các thách thức triển khai cụ thể, không phải ý tưởng suy đoán.
3. **Các giai đoạn của đề xuất**:
   - Định nghĩa: Khám phá vấn đề, xác nhận rằng người dùng MCP khác cũng gặp vấn đề tương tự
   - Nguyên mẫu: Xây dựng giải pháp mẫu và chứng minh ứng dụng thực tế
   - Viết: Dựa trên nguyên mẫu, viết đề xuất đặc tả

### Thiết lập môi trường phát triển

```bash
# Fork the repository
git clone https://github.com/YOUR-USERNAME/modelcontextprotocol.git
cd modelcontextprotocol

# Install dependencies
npm install

# For schema changes, validate and generate schema.json:
npm run check:schema:ts
npm run generate:schema

# For documentation changes
npm run check:docs
npm run format

# Preview documentation locally (optional):
npm run serve:docs
```

### Ví dụ: Đóng góp sửa lỗi

```javascript
// Original code with bug in the typescript-sdk
export function validateResource(resource: unknown): resource is MCPResource {
  if (!resource || typeof resource !== 'object') {
    return false;
  }
  
  // Bug: Missing property validation
  // Current implementation:
  const hasName = 'name' in resource;
  const hasSchema = 'schema' in resource;
  
  return hasName && hasSchema;
}

// Fixed implementation in a contribution
export function validateResource(resource: unknown): resource is MCPResource {
  if (!resource || typeof resource !== 'object') {
    return false;
  }
  
  // Improved validation
  const hasName = 'name' in resource && typeof (resource as MCPResource).name === 'string';
  const hasSchema = 'schema' in resource && typeof (resource as MCPResource).schema === 'object';
  const hasDescription = !('description' in resource) || typeof (resource as MCPResource).description === 'string';
  
  return hasName && hasSchema && hasDescription;
}
```

### Ví dụ: Đóng góp công cụ mới vào thư viện chuẩn

```python
# Example contribution: A CSV data processing tool for the MCP standard library

from mcp_tools import Tool, ToolRequest, ToolResponse, ToolExecutionException
import pandas as pd
import io
import json
from typing import Dict, Any, List, Optional

class CsvProcessingTool(Tool):
    """
    Tool for processing and analyzing CSV data.
    
    This tool allows models to extract information from CSV files,
    run basic analysis, and convert data between formats.
    """
    
    def get_name(self):
        return "csvProcessor"
        
    def get_description(self):
        return "Processes and analyzes CSV data"
    
    def get_schema(self):
        return {
            "type": "object",
            "properties": {
                "csvData": {
                    "type": "string", 
                    "description": "CSV data as a string"
                },
                "csvUrl": {
                    "type": "string",
                    "description": "URL to a CSV file (alternative to csvData)"
                },
                "operation": {
                    "type": "string",
                    "enum": ["summary", "filter", "transform", "convert"],
                    "description": "Operation to perform on the CSV data"
                },
                "filterColumn": {
                    "type": "string",
                    "description": "Column to filter by (for filter operation)"
                },
                "filterValue": {
                    "type": "string",
                    "description": "Value to filter for (for filter operation)"
                },
                "outputFormat": {
                    "type": "string",
                    "enum": ["json", "csv", "markdown"],
                    "default": "json",
                    "description": "Output format for the processed data"
                }
            },
            "oneOf": [
                {"required": ["csvData", "operation"]},
                {"required": ["csvUrl", "operation"]}
            ]
        }
    
    async def execute_async(self, request: ToolRequest) -> ToolResponse:
        try:
            # Extract parameters
            operation = request.parameters.get("operation")
            output_format = request.parameters.get("outputFormat", "json")
            
            # Get CSV data from either direct data or URL
            df = await self._get_dataframe(request)
            
            # Process based on requested operation
            result = {}
            
            if operation == "summary":
                result = self._generate_summary(df)
            elif operation == "filter":
                column = request.parameters.get("filterColumn")
                value = request.parameters.get("filterValue")
                if not column:
                    raise ToolExecutionException("filterColumn is required for filter operation")
                result = self._filter_data(df, column, value)
            elif operation == "transform":
                result = self._transform_data(df, request.parameters)
            elif operation == "convert":
                result = self._convert_format(df, output_format)
            else:
                raise ToolExecutionException(f"Unknown operation: {operation}")
            
            return ToolResponse(result=result)
        
        except Exception as e:
            raise ToolExecutionException(f"CSV processing failed: {str(e)}")
    
    async def _get_dataframe(self, request: ToolRequest) -> pd.DataFrame:
        """Gets a pandas DataFrame from either CSV data or URL"""
        if "csvData" in request.parameters:
            csv_data = request.parameters.get("csvData")
            return pd.read_csv(io.StringIO(csv_data))
        elif "csvUrl" in request.parameters:
            csv_url = request.parameters.get("csvUrl")
            return pd.read_csv(csv_url)
        else:
            raise ToolExecutionException("Either csvData or csvUrl must be provided")
    
    def _generate_summary(self, df: pd.DataFrame) -> Dict[str, Any]:
        """Generates a summary of the CSV data"""
        return {
            "columns": df.columns.tolist(),
            "rowCount": len(df),
            "columnCount": len(df.columns),
            "numericColumns": df.select_dtypes(include=['number']).columns.tolist(),
            "categoricalColumns": df.select_dtypes(include=['object']).columns.tolist(),
            "sampleRows": json.loads(df.head(5).to_json(orient="records")),
            "statistics": json.loads(df.describe().to_json())
        }
    
    def _filter_data(self, df: pd.DataFrame, column: str, value: str) -> Dict[str, Any]:
        """Filters the DataFrame by a column value"""
        if column not in df.columns:
            raise ToolExecutionException(f"Column '{column}' not found")
            
        filtered_df = df[df[column].astype(str).str.contains(value)]
        
        return {
            "originalRowCount": len(df),
            "filteredRowCount": len(filtered_df),
            "data": json.loads(filtered_df.to_json(orient="records"))
        }
    
    def _transform_data(self, df: pd.DataFrame, params: Dict[str, Any]) -> Dict[str, Any]:
        """Transforms the data based on parameters"""
        # Implementation would include various transformations
        return {
            "status": "success",
            "message": "Transformation applied"
        }
    
    def _convert_format(self, df: pd.DataFrame, format: str) -> Dict[str, Any]:
        """Converts the DataFrame to different formats"""
        if format == "json":
            return {
                "data": json.loads(df.to_json(orient="records")),
                "format": "json"
            }
        elif format == "csv":
            return {
                "data": df.to_csv(index=False),
                "format": "csv"
            }
        elif format == "markdown":
            return {
                "data": df.to_markdown(),
                "format": "markdown"
            }
        else:
            raise ToolExecutionException(f"Unsupported output format: {format}")
```

### Hướng dẫn đóng góp

Để đóng góp thành công vào các dự án MCP:

1. **Bắt đầu từ nhỏ**: Bắt đầu với tài liệu, sửa lỗi hoặc cải tiến nhỏ
2. **Tuân theo hướng dẫn phong cách**: Tuân thủ phong cách mã và quy ước của dự án
3. **Viết kiểm thử**: Bao gồm kiểm thử đơn vị cho các đóng góp mã
4. **Ghi chép công việc**: Thêm tài liệu rõ ràng cho tính năng hoặc thay đổi mới
5. **Gửi PR tập trung**: Giữ pull request tập trung vào một vấn đề hoặc tính năng duy nhất
6. **Phản hồi tích cực**: Phản hồi nhanh chóng với các góp ý về đóng góp của bạn

### Quy trình đóng góp mẫu

```bash
# Clone the repository
git clone https://github.com/modelcontextprotocol/typescript-sdk.git
cd typescript-sdk

# Create a new branch for your contribution
git checkout -b feature/my-contribution

# Make your changes
# ...

# Run tests to ensure your changes don't break existing functionality
npm test

# Commit your changes with a descriptive message
git commit -am "Fix validation in resource handler"

# Push your branch to your fork
git push origin feature/my-contribution

# Create a pull request from your branch to the main repository
# Then engage with feedback and iterate on your PR as needed
```

## Tạo và chia sẻ máy chủ MCP

Một trong những cách đóng góp giá trị nhất cho hệ sinh thái MCP là tạo và chia sẻ các máy chủ MCP tùy chỉnh. Cộng đồng đã phát triển hàng trăm máy chủ cho nhiều dịch vụ và trường hợp sử dụng khác nhau.

### Framework phát triển máy chủ MCP

Có nhiều framework giúp đơn giản hóa việc phát triển máy chủ MCP:

1. **SDK chính thức**:
   - [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)
   - [Python SDK](https://github.com/modelcontextprotocol/python-sdk)
   - [C# SDK](https://github.com/modelcontextprotocol/csharp-sdk)
   - [Go SDK](https://github.com/modelcontextprotocol/go-sdk)
   - [Java SDK](https://github.com/modelcontextprotocol/java-sdk)
   - [Kotlin SDK](https://github.com/modelcontextprotocol/kotlin-sdk)

2. **Framework cộng đồng**:
   - [MCP-Framework](https://mcp-framework.com/) - Xây dựng máy chủ MCP nhanh và tinh tế với TypeScript
   - [MCP Declarative Java SDK](https://github.com/codeboyzhou/mcp-declarative-java-sdk) - Máy chủ MCP dựa trên annotation với Java
   - [Quarkus MCP Server SDK](https://github.com/quarkiverse/quarkus-mcp-server) - Framework Java cho máy chủ MCP
   - [Next.js MCP Server Template](https://github.com/vercel-labs/mcp-for-next.js) - Dự án khởi đầu Next.js cho máy chủ MCP

### Phát triển công cụ có thể chia sẻ

#### Ví dụ .NET: Tạo gói công cụ có thể chia sẻ

```csharp
// Create a new .NET library project
// dotnet new classlib -n McpFinanceTools

using Microsoft.Mcp.Tools;
using System.Threading.Tasks;
using System.Net.Http;
using System.Text.Json;

namespace McpFinanceTools
{
    // Stock quote tool
    public class StockQuoteTool : IMcpTool
    {
        private readonly HttpClient _httpClient;
        
        public StockQuoteTool(HttpClient httpClient = null)
        {
            _httpClient = httpClient ?? new HttpClient();
        }
        
        public string Name => "stockQuote";
        public string Description => "Gets current stock quotes for specified symbols";
        
        public object GetSchema()
        {
            return new {
                type = "object",
                properties = new {
                    symbol = new { 
                        type = "string",
                        description = "Stock symbol (e.g., MSFT, AAPL)" 
                    },
                    includeHistory = new { 
                        type = "boolean",
                        description = "Whether to include historical data",
                        default = false
                    }
                },
                required = new[] { "symbol" }
            };
        }
        
        public async Task<ToolResponse> ExecuteAsync(ToolRequest request)
        {
            // Extract parameters
            string symbol = request.Parameters.GetProperty("symbol").GetString();
            bool includeHistory = false;
            
            if (request.Parameters.TryGetProperty("includeHistory", out var historyProp))
            {
                includeHistory = historyProp.GetBoolean();
            }
            
            // Call external API (example)
            var quoteResult = await GetStockQuoteAsync(symbol);
            
            // Add historical data if requested
            if (includeHistory)
            {
                var historyData = await GetStockHistoryAsync(symbol);
                quoteResult.Add("history", historyData);
            }
            
            // Return formatted result
            return new ToolResponse {
                Result = JsonSerializer.SerializeToElement(quoteResult)
            };
        }
        
        private async Task<Dictionary<string, object>> GetStockQuoteAsync(string symbol)
        {
            // Implementation would call a real stock API
            // This is a simplified example
            return new Dictionary<string, object>
            {
                ["symbol"] = symbol,
                ["price"] = 123.45,
                ["change"] = 2.5,
                ["percentChange"] = 1.2,
                ["lastUpdated"] = DateTime.UtcNow
            };
        }
        
        private async Task<object> GetStockHistoryAsync(string symbol)
        {
            // Implementation would get historical data
            // Simplified example
            return new[]
            {
                new { date = DateTime.Now.AddDays(-7).Date, price = 120.25 },
                new { date = DateTime.Now.AddDays(-6).Date, price = 122.50 },
                new { date = DateTime.Now.AddDays(-5).Date, price = 121.75 }
                // More historical data...
            };
        }
    }
}

// Create package and publish to NuGet
// dotnet pack -c Release
// dotnet nuget push bin/Release/McpFinanceTools.1.0.0.nupkg -s https://api.nuget.org/v3/index.json -k YOUR_API_KEY
```

#### Ví dụ Java: Tạo gói Maven cho công cụ

```java
// pom.xml configuration for a shareable MCP tool package
<!-- 
<project>
    <groupId>com.example</groupId>
    <artifactId>mcp-weather-tools</artifactId>
    <version>1.0.0</version>
    
    <dependencies>
        <dependency>
            <groupId>com.mcp</groupId>
            <artifactId>mcp-server</artifactId>
            <version>1.0.0</version>
        </dependency>
    </dependencies>
    
    <distributionManagement>
        <repository>
            <id>github</id>
            <name>GitHub Packages</name>
            <url>https://maven.pkg.github.com/username/mcp-weather-tools</url>
        </repository>
    </distributionManagement>
</project>
-->

package com.example.mcp.weather;

import com.mcp.tools.Tool;
import com.mcp.tools.ToolRequest;
import com.mcp.tools.ToolResponse;
import com.mcp.tools.ToolExecutionException;

import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.URI;
import java.util.HashMap;
import java.util.Map;

public class WeatherForecastTool implements Tool {
    private final HttpClient httpClient;
    private final String apiKey;
    
    public WeatherForecastTool(String apiKey) {
        this.httpClient = HttpClient.newHttpClient();
        this.apiKey = apiKey;
    }
    
    @Override
    public String getName() {
        return "weatherForecast";
    }
    
    @Override
    public String getDescription() {
        return "Gets weather forecast for a specified location";
    }
    
    @Override
    public Object getSchema() {
        Map<String, Object> schema = new HashMap<>();
        // Schema definition...
        return schema;
    }
    
    @Override
    public ToolResponse execute(ToolRequest request) {
        try {
            String location = request.getParameters().get("location").asText();
            int days = request.getParameters().has("days") ? 
                request.getParameters().get("days").asInt() : 3;
            
            // Call weather API
            Map<String, Object> forecast = getForecast(location, days);
            
            // Build response
            return new ToolResponse.Builder()
                .setResult(forecast)
                .build();
        } catch (Exception ex) {
            throw new ToolExecutionException("Weather forecast failed: " + ex.getMessage(), ex);
        }
    }
    
    private Map<String, Object> getForecast(String location, int days) {
        // Implementation would call weather API
        // Simplified example
        Map<String, Object> result = new HashMap<>();
        // Add forecast data...
        return result;
    }
}

// Build and publish using Maven
// mvn clean package
// mvn deploy
```

#### Ví dụ Python: Phát hành gói PyPI

```python
# Directory structure for a PyPI package:
# mcp_nlp_tools/
# ├── LICENSE
# ├── README.md
# ├── setup.py
# ├── mcp_nlp_tools/
# │   ├── __init__.py
# │   ├── sentiment_tool.py
# │   └── translation_tool.py

# Example setup.py
"""
from setuptools import setup, find_packages

setup(
    name="mcp_nlp_tools",
    version="0.1.0",
    packages=find_packages(),
    install_requires=[
        "mcp_server>=1.0.0",
        "transformers>=4.0.0",
        "torch>=1.8.0"
    ],
    author="Your Name",
    author_email="your.email@example.com",
    description="MCP tools for natural language processing tasks",
    long_description=open("README.md").read(),
    long_description_content_type="text/markdown",
    url="https://github.com/username/mcp_nlp_tools",
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
    python_requires=">=3.8",
)
"""

# Example NLP tool implementation (sentiment_tool.py)
from mcp_tools import Tool, ToolRequest, ToolResponse, ToolExecutionException
from transformers import pipeline
import torch

class SentimentAnalysisTool(Tool):
    """MCP tool for sentiment analysis of text"""
    
    def __init__(self, model_name="distilbert-base-uncased-finetuned-sst-2-english"):
        # Load the sentiment analysis model
        self.sentiment_analyzer = pipeline("sentiment-analysis", model=model_name)
    
    def get_name(self):
        return "sentimentAnalysis"
        
    def get_description(self):
        return "Analyzes the sentiment of text, classifying it as positive or negative"
    
    def get_schema(self):
        return {
            "type": "object",
            "properties": {
                "text": {
                    "type": "string", 
                    "description": "The text to analyze for sentiment"
                },
                "includeScore": {
                    "type": "boolean",
                    "description": "Whether to include confidence scores",
                    "default": True
                }
            },
            "required": ["text"]
        }
    
    async def execute_async(self, request: ToolRequest) -> ToolResponse:
        try:
            # Extract parameters
            text = request.parameters.get("text")
            include_score = request.parameters.get("includeScore", True)
            
            # Analyze sentiment
            sentiment_result = self.sentiment_analyzer(text)[0]
            
            # Format result
            result = {
                "sentiment": sentiment_result["label"],
                "text": text
            }
            
            if include_score:
                result["score"] = sentiment_result["score"]
            
            # Return result
            return ToolResponse(result=result)
            
        except Exception as e:
            raise ToolExecutionException(f"Sentiment analysis failed: {str(e)}")

# To publish:
# python setup.py sdist bdist_wheel
# python -m twine upload dist/*
```

### Chia sẻ các thực hành tốt nhất

Khi chia sẻ công cụ MCP với cộng đồng:

1. **Tài liệu đầy đủ**:
   - Ghi rõ mục đích, cách sử dụng và ví dụ
   - Giải thích các tham số và giá trị trả về
   - Ghi chú các phụ thuộc bên ngoài (nếu có)

2. **Xử lý lỗi**:
   - Triển khai xử lý lỗi chắc chắn
   - Cung cấp thông báo lỗi hữu ích
   - Xử lý các trường hợp đặc biệt một cách khéo léo

3. **Cân nhắc hiệu năng**:
   - Tối ưu cả tốc độ và sử dụng tài nguyên
   - Áp dụng caching khi phù hợp
   - Xem xét khả năng mở rộng

4. **Bảo mật**:
   - Sử dụng khóa API và xác thực an toàn
   - Kiểm tra và làm sạch dữ liệu đầu vào
   - Giới hạn tần suất gọi API bên ngoài

5. **Kiểm thử**:
   - Bao gồm kiểm thử toàn diện
   - Kiểm thử với các loại đầu vào và trường hợp đặc biệt khác nhau
   - Ghi chép quy trình kiểm thử

## Hợp tác cộng đồng và thực hành tốt nhất

Hợp tác hiệu quả là chìa khóa cho sự phát triển bền vững của hệ sinh thái MCP.

### Kênh giao tiếp

- GitHub Issues và Discussions
- Microsoft Tech Community
- Các kênh Discord và Slack
- Stack Overflow (tag: `model-context-protocol` hoặc `mcp`)

### Đánh giá mã nguồn

Khi đánh giá các đóng góp MCP:

1. **Rõ ràng**: Mã có rõ ràng và được tài liệu đầy đủ không?
2. **Chính xác**: Mã hoạt động như mong đợi không?
3. **Nhất quán**: Có tuân theo quy ước dự án không?
4. **Đầy đủ**: Có bao gồm kiểm thử và tài liệu không?
5. **Bảo mật**: Có vấn đề bảo mật nào không?

### Tương thích phiên bản

Khi phát triển cho MCP:

1. **Phiên bản giao thức**: Tuân thủ phiên bản giao thức MCP mà công cụ của bạn hỗ trợ
2. **Tương thích client**: Xem xét khả năng tương thích ngược
3. **Tương thích server**: Tuân theo hướng dẫn triển khai máy chủ
4. **Thay đổi phá vỡ**: Ghi rõ các thay đổi phá vỡ nếu có

## Dự án cộng đồng mẫu: MCP Tool Registry

Một đóng góp quan trọng cho cộng đồng có thể là phát triển một registry công khai cho các công cụ MCP.

```python
# Example schema for a community tool registry API

from fastapi import FastAPI, HTTPException, Depends
from pydantic import BaseModel, Field, HttpUrl
from typing import List, Optional
import datetime
import uuid

# Models for the tool registry
class ToolSchema(BaseModel):
    """JSON Schema for a tool"""
    type: str
    properties: dict
    required: List[str] = []

class ToolRegistration(BaseModel):
    """Information for registering a tool"""
    name: str = Field(..., description="Unique name for the tool")
    description: str = Field(..., description="Description of what the tool does")
    version: str = Field(..., description="Semantic version of the tool")
    schema: ToolSchema = Field(..., description="JSON Schema for tool parameters")
    author: str = Field(..., description="Author of the tool")
    repository: Optional[HttpUrl] = Field(None, description="Repository URL")
    documentation: Optional[HttpUrl] = Field(None, description="Documentation URL")
    package: Optional[HttpUrl] = Field(None, description="Package URL")
    tags: List[str] = Field(default_factory=list, description="Tags for categorization")
    examples: List[dict] = Field(default_factory=list, description="Example usage")

class Tool(ToolRegistration):
    """Tool with registry metadata"""
    id: uuid.UUID = Field(default_factory=uuid.uuid4)
    created_at: datetime.datetime = Field(default_factory=datetime.datetime.now)
    updated_at: datetime.datetime = Field(default_factory=datetime.datetime.now)
    downloads: int = Field(default=0)
    rating: float = Field(default=0.0)
    ratings_count: int = Field(default=0)

# FastAPI application for the registry
app = FastAPI(title="MCP Tool Registry")

# In-memory database for this example
tools_db = {}

@app.post("/tools", response_model=Tool)
async def register_tool(tool: ToolRegistration):
    """Register a new tool in the registry"""
    if tool.name in tools_db:
        raise HTTPException(status_code=400, detail=f"Tool '{tool.name}' already exists")
    
    new_tool = Tool(**tool.dict())
    tools_db[tool.name] = new_tool
    return new_tool

@app.get("/tools", response_model=List[Tool])
async def list_tools(tag: Optional[str] = None):
    """List all registered tools, optionally filtered by tag"""
    if tag:
        return [tool for tool in tools_db.values() if tag in tool.tags]
    return list(tools_db.values())

@app.get("/tools/{tool_name}", response_model=Tool)
async def get_tool(tool_name: str):
    """Get information about a specific tool"""
    if tool_name not in tools_db:
        raise HTTPException(status_code=404, detail=f"Tool '{tool_name}' not found")
    return tools_db[tool_name]

@app.delete("/tools/{tool_name}")
async def delete_tool(tool_name: str):
    """Delete a tool from the registry"""
    if tool_name not in tools_db:
        raise HTTPException(status_code=404, detail=f"Tool '{tool_name}' not found")
    del tools_db[tool_name]
    return {"message": f"Tool '{tool_name}' deleted"}
```

## Những điểm chính cần nhớ

- Cộng đồng MCP đa dạng và chào đón nhiều loại đóng góp
- Đóng góp cho MCP có thể từ cải tiến giao thức cốt lõi đến công cụ tùy chỉnh
- Tuân theo hướng dẫn đóng góp giúp tăng khả năng PR của bạn được chấp nhận
- Tạo và chia sẻ công cụ MCP là cách giá trị để phát triển hệ sinh thái
- Hợp tác cộng đồng là yếu tố thiết yếu cho sự phát triển và cải tiến MCP

## Bài tập

1. Xác định một lĩnh vực trong hệ sinh thái MCP mà bạn có thể đóng góp dựa trên kỹ năng và sở thích của mình
2. Fork kho MCP và thiết lập môi trường phát triển cục bộ
3. Tạo một cải tiến nhỏ, sửa lỗi hoặc công cụ có lợi cho cộng đồng
4. Ghi chép đóng góp của bạn với kiểm thử và tài liệu đầy đủ
5. Gửi pull request đến kho phù hợp

## Tài nguyên bổ sung

- [Dự án cộng đồng MCP](https://github.com/topics/model-context-protocol)


---

Tiếp theo: [Bài học từ việc áp dụng sớm](../07-LessonsfromEarlyAdoption/README.md)

**Tuyên bố từ chối trách nhiệm**:  
Tài liệu này đã được dịch bằng dịch vụ dịch thuật AI [Co-op Translator](https://github.com/Azure/co-op-translator). Mặc dù chúng tôi cố gắng đảm bảo độ chính xác, xin lưu ý rằng các bản dịch tự động có thể chứa lỗi hoặc không chính xác. Tài liệu gốc bằng ngôn ngữ gốc của nó nên được coi là nguồn chính xác và đáng tin cậy. Đối với các thông tin quan trọng, nên sử dụng dịch vụ dịch thuật chuyên nghiệp do con người thực hiện. Chúng tôi không chịu trách nhiệm về bất kỳ sự hiểu lầm hoặc giải thích sai nào phát sinh từ việc sử dụng bản dịch này.