# EchoLabs AI - MCP Extensions Directory

> **Purpose:** Model Context Protocol (MCP) implementations for agent integration and system extension

**Status:** ⚠️ Skeleton - Ready for Phase 2+ Implementation  
**Last Updated:** December 15, 2025  
**Protocol Version:** MCP 1.0+  
**Framework:** Python MCP SDK + JavaScript MCP SDK  
**Implementation Phase:** Phase 2 - Enterprise Features (Weeks 13-24)

---

## Overview

This directory contains Model Context Protocol (MCP) implementations that extend EchoLabs capabilities:
- **Research MCP** - Expose evaluation engines and datasets as MCP tools
- **Monitoring MCP** - Real-time metrics and alerts via MCP
- **Compliance MCP** - Regulatory checking and reporting as MCP resources

**Architecture Pattern:** Standard MCP servers following Anthropic MCP specification, enabling external AI agents to interact with EchoLabs platform.

---

## What is Model Context Protocol (MCP)?

**MCP** is a standardized protocol for AI systems to:
1. **Access external data** through resources
2. **Execute operations** through tools/functions
3. **Stream results** asynchronously
4. **Handle authentication** securely

**Key Benefits:**
- Standardized agent-to-system integration
- Language-agnostic communication
- Enables multi-agent orchestration
- Simplifies downstream agent development

**Official Spec:** [modelcontextprotocol.io](https://modelcontextprotocol.io)

---

## Directory Structure (Phase 2+)

```
mcp-extensions/
│
├── README.md                       # This file
├── specifications.md               # Custom MCP resource/tool specs
│
├── research-mcp/                   # Research & evaluation tools
│   ├── README.md                  # Research MCP documentation
│   ├── server.py                   # MCP server implementation
│   ├── tools/                      # Tool implementations
│   │   ├── evaluation_tools.py       # Evaluation execution tools
│   │   ├── dataset_tools.py         # Dataset management tools
│   │   └── analysis_tools.py        # Result analysis tools
│   ├── resources/                  # Resource definitions
│   │   ├── evaluation_resources.py   # Evaluation results
│   │   └── dataset_resources.py     # Dataset catalog
│   ├── schemas/                    # JSON schema definitions
│   ├── tests/                      # MCP server tests
│   └── requirements.txt            # Python dependencies
│
├── monitoring-mcp/                 # Real-time monitoring tools
│   ├── README.md
│   ├── server.py                   # MCP server implementation
│   ├── tools/
│   │   ├── metrics_tools.py         # Real-time metrics
│   │   ├── alert_tools.py           # Alert management
│   │   └── health_check_tools.py    # System health
│   ├── resources/
│   │   ├── metrics_resources.py      # Current metrics
│   │   ├── alert_resources.py       # Active alerts
│   │   └── logs_resources.py        # Event logs
│   ├── schemas/
│   ├── tests/
│   └── requirements.txt
│
├── compliance-mcp/                 # Regulatory compliance tools
│   ├── README.md
│   ├── server.py                   # MCP server implementation
│   ├── tools/
│   │   ├── compliance_check_tools.py # NDMO/DIFC/ADGM checks
│   │   ├── report_tools.py          # Report generation
│   │   └── audit_tools.py           # Audit operations
│   ├── resources/
│   │   ├── compliance_rules.py      # Current compliance rules
│   │   ├── reports_resources.py     # Compliance reports
│   │   └── risk_resources.py        # Risk assessments
│   ├── rules/
│   │   ├── ndmo_rules.json          # NDMO regulations
│   │   ├── difc_rules.json          # DIFC regulations
│   │   └── adgm_rules.json          # ADGM regulations
│   ├── schemas/
│   ├── tests/
│   └── requirements.txt
│
├── client-examples/                # Example MCP client implementations
│   ├── python_client.py            # Python client example
│   ├── javascript_client.js        # JavaScript client example
│   ├── claude_integration.py        # Claude AI integration example
│   └── gpt4_integration.py         # GPT-4 integration example
│
└── shared/                         # Shared utilities
    ├── mcp_utils.py                # Common MCP utilities
    ├── auth.py                     # MCP authentication
    ├── error_handling.py           # Error handling patterns
    └── logging.py                  # Structured logging
```

---

## MCP Specification (EchoLabs Custom)

### **Research MCP - Tools**

```
Tools:
1. "create_evaluation"
   - Input: project_id, agent_name, llm_output, test_dataset_id
   - Output: evaluation_id, quality_score, bias_score, safety_score
   - Purpose: Create new evaluation

2. "get_evaluation_results"
   - Input: evaluation_id
   - Output: Complete evaluation data with all metrics
   - Purpose: Retrieve evaluation results

3. "analyze_evaluations"
   - Input: evaluation_ids[] (list of IDs)
   - Output: Comparative analysis, aggregated metrics
   - Purpose: Compare multiple evaluations

4. "upload_dataset"
   - Input: file_path, dataset_name, description
   - Output: dataset_id, record_count, validation_status
   - Purpose: Upload new test dataset

5. "list_datasets"
   - Input: (optional) filters (project_id, status)
   - Output: Array of available datasets
   - Purpose: Discover available datasets
```

### **Research MCP - Resources**

```
Resources:
1. "evaluation://" URI scheme
   - Format: evaluation://{project_id}/{evaluation_id}
   - Content: Full evaluation result data
   - Mutable: No (read-only)

2. "dataset://" URI scheme
   - Format: dataset://{project_id}/{dataset_id}
   - Content: Dataset metadata and statistics
   - Mutable: No (read-only)

3. "benchmark://" URI scheme
   - Format: benchmark://{benchmark_type}/{test_id}
   - Content: Benchmark results and analysis
   - Mutable: No
```

### **Monitoring MCP - Tools**

```
Tools:
1. "get_agent_status"
   - Input: agent_id
   - Output: status, last_activity, error_count, uptime
   - Purpose: Real-time agent health

2. "get_metrics"
   - Input: metric_type (latency, cost, success_rate), time_range
   - Output: Time-series metric data
   - Purpose: Performance metrics

3. "create_alert"
   - Input: alert_name, metric, threshold, action
   - Output: alert_id, status
   - Purpose: Set up monitoring alerts

4. "get_logs"
   - Input: (optional) agent_id, level (ERROR, INFO, DEBUG), limit
   - Output: Array of recent logs
   - Purpose: Debug issues
```

### **Compliance MCP - Tools**

```
Tools:
1. "check_compliance"
   - Input: evaluation_id, regulations[] (NDMO, DIFC, ADGM)
   - Output: compliance_status, violations[], risk_score
   - Purpose: Verify regulatory compliance

2. "generate_compliance_report"
   - Input: project_id, regulations[], time_period
   - Output: report_url (PDF), summary
   - Purpose: Generate audit reports

3. "assess_privacy"
   - Input: data_description, processing_type
   - Output: privacy_score, recommendations[], requirements[]
   - Purpose: Privacy impact analysis

4. "check_data_residency"
   - Input: data_location
   - Output: is_compliant, residency_status
   - Purpose: Verify data sovereignty
```

---

## Implementation Example - Research MCP Server (Python)

```python
# research-mcp/server.py
from mcp.server import Server, ClientSession
from mcp.types import Tool, TextContent, ToolResult
import json

app = Server("echolabs-research-mcp")

@app.tool()
def create_evaluation(project_id: str, agent_name: str, 
                      llm_output: str, test_dataset_id: str) -> dict:
    """
    Create a new evaluation in EchoLabs platform.
    
    Args:
        project_id: Organization project ID
        agent_name: Name of AI agent being evaluated
        llm_output: Text output from LLM to evaluate
        test_dataset_id: Reference dataset for context
        
    Returns:
        evaluation_id: Unique evaluation identifier
        quality_score: 0-100 quality metric
        bias_score: Bias detection score
        safety_score: Safety compliance score
    """
    # Call EchoLabs API
    from lib.api import api_client
    
    response = api_client.post('/api/v1/evaluations', json={
        'project_id': project_id,
        'agent_name': agent_name,
        'llm_output': llm_output,
        'dataset_id': test_dataset_id,
    })
    
    return {
        'evaluation_id': response['id'],
        'quality_score': response['metrics']['quality'],
        'bias_score': response['metrics']['bias'],
        'safety_score': response['metrics']['safety'],
    }

@app.resource()
def evaluation_resource(uri: str) -> TextContent:
    """
    Access evaluation results via evaluation://project/eval_id URI.
    """
    parts = uri.replace('evaluation://', '').split('/')
    project_id, eval_id = parts[0], parts[1]
    
    # Fetch from EchoLabs
    from lib.api import api_client
    data = api_client.get(f'/api/v1/evaluations/{eval_id}')
    
    return TextContent(
        uri=uri,
        mimeType='application/json',
        text=json.dumps(data, indent=2)
    )

if __name__ == '__main__':
    import asyncio
    asyncio.run(app.run())
```

---

## MCP Client Integration with Claude

```python
# Example: Using EchoLabs MCP with Claude
from anthropic import Anthropic

client = Anthropic()

# Configure MCP servers
mcp_servers = {
    "echolabs-research": {
        "command": "python",
        "args": ["./research-mcp/server.py"]
    },
    "echolabs-monitoring": {
        "command": "python",
        "args": ["./monitoring-mcp/server.py"]
    },
    "echolabs-compliance": {
        "command": "python",
        "args": ["./compliance-mcp/server.py"]
    }
}

# Initialize client with MCP
response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=1024,
    tools=[],  # MCP tools auto-discovered
    messages=[
        {
            "role": "user",
            "content": """Create an evaluation for my GPT-4 agent output 
            against the financial dataset, then check compliance with DIFC regulations."""
        }
    ]
)

print(response.content)
```

---

## Development Guidelines

### **1. MCP Server Development**
- Use official MCP SDK (Python or JavaScript)
- Implement both Tools and Resources
- Handle authentication securely
- Comprehensive error handling
- Full API documentation in tool descriptions

### **2. Testing**
```bash
# Test individual MCP server
cd research-mcp
python -m pytest tests/ -v

# Test MCP server with client
python test_mcp_client.py
```

### **3. Schema Definition**
```json
{
  "tool_name": "create_evaluation",
  "description": "Create evaluation in EchoLabs",
  "inputSchema": {
    "type": "object",
    "properties": {
      "project_id": {"type": "string", "description": "Project ID"},
      "agent_name": {"type": "string"},
      "llm_output": {"type": "string"},
      "test_dataset_id": {"type": "string"}
    },
    "required": ["project_id", "agent_name", "llm_output"]
  }
}
```

### **4. Authentication**
- Use API keys for MCP-to-EchoLabs authentication
- Implement token refresh logic
- Secure credential storage (environment variables)
- Rate limiting and request signing

---

## Integration Architecture

```
External AI Agents (Claude, GPT-4, etc.)
        ↑↓
  Model Context Protocol
        ↑↓
┌───────────────────────┐
│   MCP Servers (EchoLabs)          │
│ ┌───────────────────┐ │
│ │ Research | Monitor | Compliance │ │
│ └───────────────────┘ │
│             ↑↓                     │
│        REST API v1                  │
│             ↑↓                     │
│  ┌───────────────────┐ │
│  │   Backend Services          │ │
│  │ - Eval Engine               │ │
│  │ - Monitoring                │ │
│  │ - Compliance Checker        │ │
│  └───────────────────┘ │
└───────────────────────┘
        ↑↓
    Databases
  (PostgreSQL, Redis)
```

---

## Phase 2 Implementation Plan

**Weeks 13-18:**
1. Finalize MCP specifications
2. Implement Research MCP server
3. Implement Monitoring MCP server
4. Write comprehensive tests

**Weeks 19-24:**
1. Implement Compliance MCP server
2. Create client integration examples
3. Test with Claude and GPT-4
4. Performance optimization
5. Security audit

---

## Resources & References

**Official Documentation:**
- [Model Context Protocol Spec](https://spec.modelcontextprotocol.io/)
- [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk)
- [MCP JavaScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)

**EchoLabs References:**
- [Platform API Specs](../../platform/evaluation-framework.md)
- [Technical Specifications](../../deliverables/technical-specifications.md)

---

**Directory Status:** ⚠️ Skeleton - Ready for Phase 2  
**Implementation Start:** Phase 2, Week 13  
**Last Updated:** December 15, 2025  
**Maintainer:** EchoLabs Platform Team
