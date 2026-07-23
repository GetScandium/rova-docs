---
description: >-
  Rova supports native observability integrations to help you visualize test
  execution metrics and analyze test run traces in your own monitoring stacks,
  such as Grafana or Kibana.
---

# OpenTelemetry Integrations

## Rova Observability & Monitoring Integration Guide

Rova supports native observability integrations to help you visualize test execution metrics and analyze test run traces in your own monitoring stacks, such as **Grafana** or **Kibana**.

Observability in Rova is split into two complementary features:

1. **Dynamic Dashboard Links**: Embed quick links to your Grafana or Kibana instances directly in your Rova project sidebar.
2. **OpenTelemetry (OTel) Tracing Export**: Export distributed trace spans for every test execution directly to your OTLP-compliant collector.

***

### 1. Dynamic Dashboard Links

You can link your existing dashboards directly to Rova using template variables. This allows you to jump from a Rova project directly to the filtered charts inside your observability tools.

#### Supported Variables

When defining your dashboard URLs, you can use the following placeholder variables:

* `{projectId}`: The UUID of the current Rova project.
* `{workspaceId}`: The UUID of the current Rova workspace.

#### Setup Instructions

1. Navigate to **Workspace Settings** > **Integrations**.
2. Click **Configure** on the **Observability & Monitoring** integration card.
3. Provide your dashboard URL templates:
   * **Grafana URL Template**: E.g. `https://your-org.grafana.net/explore?left=["now-1h","now","grafanacloud-traces",{"query":"{projectId}"}]`
   * **Kibana URL Template**: E.g. `https://kibana.yourcompany.com/app/discover#/?_a=(query:(language:kuery,query:'project_id:"{projectId}"'))`
   * **Custom URL Template**: Any custom tool link. Specify the custom name in the **Custom Dashboard Label** field (e.g. `SigNoz`, `Datadog`).
4. Click **Save**.
5. Navigate to your project page. The links will resolve dynamically and appear under the **Observability Dashboards** section in the project sidebar.

***

### 2. OpenTelemetry Tracing Export

When enabled, Rova acts as an OTel client, publishing distributed trace spans of your test suite runs directly to your collector (e.g., Tempo, Jaeger, Elastic APM, Honeycomb).

#### Span Structure

* **Parent Span**: `Suite Run: <Suite Name>` (Attributes: `rova.workspace.id`, `rova.project.id`, `rova.status`, passed/failed counts).
* **Child Spans**: `Test Case: <Test Title>` (Attributes: `rova.test.id`, `rova.browser`, duration, and detailed error messages/exceptions on failure).

#### Setup Instructions

1. In your **Observability & Monitoring** integration settings, toggle **Enable OpenTelemetry Trace Export** to `ON`.
2. Input your **OTLP Exporter Endpoint** (e.g., `https://otlp-gateway.grafana.net/otlp/v1/traces`).
3. Set your **OTLP Headers** (one key-value pair per line, e.g., `Authorization=Basic <base64-token>`).
4. Click **Test** to dispatch a verification span (`Rova Connection Test`) and ensure Rova can successfully authenticate with your OTLP gateway.

***

### 3. Pulling Metrics via Grafana Infinity Plugin

Rather than pushing metrics, you can pull live time-series summary metrics directly from Rova's public API to display on your Grafana Dashboards.

#### Setup Instructions

1. Generate an API Key in Rova (**Workspace Settings** > **API Keys**).
2. Install the **Infinity** plugin in your Grafana instance.
3. Add a new **Infinity** datasource in Grafana:
   * Name: `Rova Metrics`
   * Authentication: Add a header named `Authorization` with value `Bearer rova_<your-api-key>`.
4.  Create a panel using this datasource, selecting the query type as **JSON**, source as **URL**, and set the endpoint to:

    ```
    https://api.rova.ai/api/v1/workspaces/{workspaceId}/projects/{projectId}/metrics
    ```
5. You can import our [Pre-Baked Grafana Dashboard Template](prebaked-grafana-template.md) to instantly get visual tables, pass-rates, and test suite duration trends.
