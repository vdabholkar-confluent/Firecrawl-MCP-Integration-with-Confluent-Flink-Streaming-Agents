# Firecrawl MCP Integration with Confluent Flink Streaming Agents

Leverage Firecrawl’s robust, JavaScript-enabled web scraping and crawling in Confluent Flink’s streaming AI agents via the Model Context Protocol (MCP) standard.

---

## 🔗 Official Links

- [Confluents Streaming Agents](https://www.confluent.io/product/streaming-agents/)
- [Firecrawl MCP Docs](https://docs.firecrawl.dev/mcp-server)
- [Firecrawl GitHub](https://github.com/firecrawl/firecrawl-mcp-server)
- [Get Firecrawl API Key](https://www.firecrawl.dev/app/api-keys)
- [Confluent Streaming Agents Quickstart](https://github.com/confluentinc/quickstart-streaming-agents/tree/master)

---
## Streaming Agents in Confluent Flink
![](https://images.ctfassets.net/8vofjvai1hpv/1y1ZtEhyqNx85MsV2rUUFu/69ffab9a197d05b758ada979b0826fe2/2025-06-26_Flink_Agents_blog_graphic.png)

## 1. Create a Firecrawl API Key

1. Login or register at [Firecrawl](https://www.firecrawl.dev/app/api-keys)
2. Create a new API key or copy an existing one
3. Store your API key securely

---

## 2. Connect Firecrawl MCP Server to Confluent Flink

Using the Confluent CLI (`confluent`), run:

```sh
confluent flink connection create firecrawl-mcp-connection
--cloud AWS
--region us-east-1
--type mcp_server
--endpoint https://mcp.firecrawl.dev/YOUR_FIRECRAWL_API_KEY
--api-key YOUR_FIRECRAWL_API_KEY
--environment <YOUR_ENV_ID>
--sse-endpoint https://mcp.firecrawl.dev/YOUR_FIRECRAWL_API_KEY/sse
```

- Replace `YOUR_FIRECRAWL_API_KEY` with your real key.
- Ensure no brackets or spaces in the endpoint.
- You can get your environment ID from Confluent Cloud.

---

## 3. Test Scraping via Flink SQL

Run this SQL to test Firecrawl’s scraping in Flink Streaming Agents (adjust the model/tool names if you registered with different values):

```SQL
SELECT
AI_TOOL_INVOKE(
'firecrawl_mcp_model',
'Use the firecrawl scraper tool to extract page contents. Instructions: Extract the page contents from the following URL: https://www.confluent.io/blog/introducing-streaming-agents/',
MAP[],
MAP['firecrawl_scrape', 'Extract main page content from a URL'],
MAP['debug', 'true', 'on_error', 'continue']
)['firecrawl_scrape']['response'] AS scraped_content;
```

---
## Scraped Results in Kafka topics
<img width="1340" height="855" alt="image" src="https://github.com/user-attachments/assets/d4a6dfbf-a0cf-4b9d-9241-f8d8bb413696" />


## 4. Firecrawl MCP Server Tools

| Tool                    | Description                                          |
|-------------------------|-----------------------------------------------------|
| `firecrawl_scrape`      | Scrape a single page (JS-enabled, mobile, markdown) |
| `firecrawl_map`         | Crawl links from a site (get all page URLs)         |
| `firecrawl_extract`     | LLM-augmented extraction from web pages             |
| `firecrawl_search`      | Run a web search                                    |
| `firecrawl_crawl`       | Deep/multi-page site crawling                       |
| `firecrawl_check_crawl_status` | Check long-running crawl status            |

See [Firecrawl MCP Docs](https://docs.firecrawl.dev/mcp-server) for all supported methods and options.

---

## 5. Troubleshooting

- Validate that your endpoints are correct and open (test with `curl` if needed).
- Ensure you have enough Firecrawl API credits.
- Confirm that Confluent Cloud has network access to `mcp.firecrawl.dev`.
- If you see timeouts, double-check the API key, endpoint, and SSE endpoint values.

---

## 6. References & Further Reading

- [Firecrawl MCP Documentation](https://docs.firecrawl.dev/mcp-server)
- [Firecrawl GitHub](https://github.com/firecrawl/firecrawl-mcp-server)
- [Confluent Streaming Agents Quickstart](https://github.com/confluentinc/quickstart-streaming-agents/tree/master)

---

**Enjoy fast, reliable, and scalable web scraping in your Flink AI pipelines with Firecrawl MCP!**
