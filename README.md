# Product Test API – TMF769 (v5.0)

The **Product Test API** is a REST‑based interface that lets Communication Service Providers (CSPs) and their partners **schedule, execute and query tests on commercial products and the services that compose them**.  By exposing a consistent set of endpoints for creating test specifications, running product tests and retrieving results, it helps organisations assure quality, performance and regulatory compliance across complex service portfolios. :contentReference[oaicite:0]{index=0}

---

## At‑a‑Glance

| Item | Value |
|------|-------|
| **API number** | TMF769 |
| **Stable version** | 5.0 |
| **Release date** | 31 May 2024 :contentReference[oaicite:1]{index=1} |
| **Domain** | Product |
| **License** | Apache 2.0 (unless stated otherwise) |

---

## When to Use It

Typical scenarios include:  

* **Service‑quality assurance** – continuously test live products for speed, latency or reliability issues.  
* **New‑product validation** – run regression and interoperability tests before launch.  
* **Partner onboarding & certification** – verify that wholesale or partner offerings meet contractual KPIs.  
* **Fault isolation & troubleshooting** – trigger on‑demand tests to pinpoint root causes.  
* **Performance benchmarking & regulatory audits** – produce repeatable measurements for compliance reports. :contentReference[oaicite:2]{index=2}

---

## Key Resources

| Resource | Path | Purpose |
|----------|------|---------|
| **ProductTest** | `/productTest` | A concrete test instance executed against a product (holds schedule, parameters, results). |
| **ProductTestSpecification** | `/productTestSpecification` | Template describing how a product test should be performed (characteristics, thresholds, measures). |

Both resources follow TMF REST design guidelines for **GET / POST / PATCH / DELETE** operations, including attribute filtering (`?fields=`) and standard pagination. :contentReference[oaicite:3]{index=3}

---

## Core Operations

> Base URL shown as `/tmf-api/productTestManagement/v5` – adjust to your deployment.

| Purpose | Verb & Path | Notes |
|---------|-------------|-------|
| List / search tests | `GET /productTest?mode=onDemand&state=completed` | Supports attribute selection & filter operators. |
| Retrieve a test | `GET /productTest/{id}` | Returns full representation. |
| Create a test | `POST /productTest` | Body must reference a `ProductTestSpecification` and target product. |
| Partial update | `PATCH /productTest/{id}` | RFC 7396 merge‑patch (mandatory) or JSON‑patch (optional). |
| List / create / update / delete specifications | `/productTestSpecification` endpoints | Same pattern as above. :contentReference[oaicite:4]{index=4}

### Minimal create example

```http
POST /productTest
Content-Type: application/json
{
  "name": "FTTH line‑rate check",
  "mode": "onDemand",
  "testSpecification": { "id": "ba01e0f0-8e6a-452d-9535-6b72ea67e712" },
  "relatedProduct": { "id": "12345" },
  "@type": "ProductTest"
}
