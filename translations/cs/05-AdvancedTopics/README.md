<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "adaf47734a5839447b5c60a27120fbaf",
  "translation_date": "2025-06-11T16:18:14+00:00",
  "source_file": "05-AdvancedTopics/README.md",
  "language_code": "cs"
}
-->
# Advanced Topics in MCP 

This chapter covers a series of advanced topics in Model Context Protocol (MCP) implementation, including multi-modal integration, scalability, security best practices, and enterprise integration. These subjects are vital for building robust and production-ready MCP applications capable of meeting the demands of modern AI systems.

## Overview

This lesson delves into advanced concepts in Model Context Protocol implementation, emphasizing multi-modal integration, scalability, security best practices, and enterprise integration. These topics are key to creating production-grade MCP applications that can address complex requirements in enterprise settings.

## Learning Objectives

By the end of this lesson, you will be able to:

- Implement multi-modal capabilities within MCP frameworks
- Design scalable MCP architectures for high-demand scenarios
- Apply security best practices aligned with MCP's security principles
- Integrate MCP with enterprise AI systems and frameworks
- Optimize performance and reliability in production environments

## Lessons and sample Projects

| Link | Title | Description |
|------|-------|-------------|
| [5.1 Integration with Azure](./mcp-integration/README.md) | Integrate with Azure | Learn how to integrate your MCP Server on Azure |
| [5.2 Multi modal sample](./mcp-multi-modality/README.md) | MCP Multi modal samples  | Samples for audio, image and multi modal response |
| [5.3 MCP OAuth2 sample](../../../05-AdvancedTopics/mcp-oauth2-demo) | MCP OAuth2 Demo | Minimal Spring Boot app demonstrating OAuth2 with MCP, serving as both Authorization and Resource Server. Shows secure token issuance, protected endpoints, Azure Container Apps deployment, and API Management integration. |
| [5.4 Root Contexts](./mcp-root-contexts/README.md) | Root contexts  | Learn more about root context and how to implement them |
| [5.5 Routing](./mcp-routing/README.md) | Routing | Explore different types of routing |
| [5.6 Sampling](./mcp-sampling/README.md) | Sampling | Learn how to work with sampling |
| [5.7 Scaling](./mcp-scaling/README.md) | Scaling  | Understand scaling concepts |
| [5.8 Security](./mcp-security/README.md) | Security  | Secure your MCP Server |
| [5.9 Web Search sample](./web-search-mcp/README.md) | Web Search MCP | Python MCP server and client integrating with SerpAPI for real-time web, news, product search, and Q&A. Demonstrates multi-tool orchestration, external API integration, and robust error handling. |
| [5.10 Realtime Streaming](./mcp-realtimestreaming/README.md) | Streaming  | Real-time data streaming is essential in today’s data-driven world, where businesses and applications require immediate access to information to make timely decisions.|

## Additional References

For the latest information on advanced MCP topics, refer to:
- [MCP Documentation](https://modelcontextprotocol.io/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [GitHub Repository](https://github.com/modelcontextprotocol)

## Key Takeaways

- Multi-modal MCP implementations extend AI capabilities beyond text processing
- Scalability is critical for enterprise deployments and can be achieved through horizontal and vertical scaling
- Comprehensive security measures protect data and ensure proper access control
- Enterprise integration with platforms like Azure OpenAI and Microsoft AI Foundry enhances MCP capabilities
- Advanced MCP implementations benefit from optimized architectures and careful resource management

## Exercise

Design an enterprise-grade MCP implementation for a specific use case:

1. Identify multi-modal requirements for your use case
2. Outline the security controls needed to protect sensitive data
3. Design a scalable architecture that can handle varying loads
4. Plan integration points with enterprise AI systems
5. Document potential performance bottlenecks and mitigation strategies

## Additional Resources

- [Azure OpenAI Documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/)
- [Microsoft AI Foundry Documentation](https://learn.microsoft.com/en-us/ai-services/)

---

## What's next

- [5.1 MCP Integration](./mcp-integration/README.md)

**Prohlášení o vyloučení odpovědnosti**:  
Tento dokument byl přeložen pomocí AI překladatelské služby [Co-op Translator](https://github.com/Azure/co-op-translator). Přestože usilujeme o přesnost, mějte prosím na paměti, že automatizované překlady mohou obsahovat chyby nebo nepřesnosti. Původní dokument v jeho rodném jazyce by měl být považován za autoritativní zdroj. Pro důležité informace se doporučuje profesionální lidský překlad. Nejsme odpovědní za jakékoliv nedorozumění nebo nesprávné výklady vyplývající z použití tohoto překladu.