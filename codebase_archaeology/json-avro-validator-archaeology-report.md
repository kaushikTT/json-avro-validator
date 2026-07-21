# Codebase Archaeology Report: kaushikTT/json-avro-validator

**Generated:** 2026-07-21T05:15:00Z
**Branch:** main
**Analysis Type:** full

---

## 1. Executive Summary

| Item | Value |
|---|---|
| Total Modules/Services | 1 |
| Primary Language | Java 17 |
| Primary Framework | Apache Avro 1.11.0 |
| Architecture Pattern | Single-module utility |
| Architectural Violations | 0 |
| Top Risk File | AvroTest.java (LOW) |
| ADRs Found | 0 |
| Commit History Window | 2022-01-27 to 2026-07-21 |

---

## 2. Repository Metadata

| Field | Value |
|---|---|
| Repository | kaushikTT/json-avro-validator |
| Description | Sample on how to validate JSON against an AVRO file in Java and get usable feedback |
| Default Branch | main |
| Languages | Java |
| Topics | â€” |
| License | MIT License |
| Created | 2022-03-07T10:16:29Z |
| Last Updated | 2026-07-21T04:35:55Z |

---

## 3. Technology Stack

| Category | Technologies |
|---|---|
| Languages | Java 17 |
| Frameworks | Apache Avro 1.11.0 |
| Build Tools | Maven (with avro-maven-plugin) |
| Infrastructure | â€” |
| Test Frameworks | â€” |

---

## 4. Module / Service Map

| Module | Path | Language | Framework | Description |
|---|---|---|---|---|
| json-avro-validator | / (root) | Java | Apache Avro | Sample on how to validate JSON against an AVRO file in Java and get usable feedback |

---

## 5. Architecture Pattern and Layer Map

**Identified Pattern:** Single-module utility application
**Evidence:** Single source directory with one entry point (AvroTest.java main method), no layered architecture, no service boundaries. The application demonstrates three approaches to AVRO schema validation.

### Layer Map

| Layer | Files |
|---|---|
| Application Entry | src/main/java/AvroTest.java |
| Domain Model (Generated) | src/main/java/com/demo/avro/Customer.java |
| Resources | src/main/resources/file.avsc, src/main/resources/file.json |

---

## 6. Architectural Violations

No violations detected. This is a single-layer utility application with no inter-layer dependencies to violate.

---

## 7. Call Graph (Top Entry Points)

### AvroTest.main(String[] args)

- `ClassLoader.getResourceAsStream("file.avsc")` â€” Loads AVRO schema file
- `ClassLoader.getResourceAsStream("file.json")` â€” Loads JSON data file
- `Schema.Parser().parse(InputStream)` â€” Parses AVRO schema
- **Validation Approach 1: Generic Schema Validation**
  - `GenericDatumReader(Schema)` â€” Creates generic reader
  - `DecoderFactory.get().jsonDecoder(Schema, InputStream)` â€” Creates JSON decoder
  - `reader.read(null, decoder)` â€” Validates JSON against schema
- **Validation Approach 2: Specific Class Validation**
  - `SpecificDatumReader<Customer>(Customer.class)` â€” Creates typed reader
  - `reader.read(null, decoder)` â€” Validates and deserializes to Customer
- **Validation Approach 3: Jackson + Avro Serialization**
  - `ObjectMapper.readValue(InputStream, Customer.class)` â€” Jackson deserialization
  - `Customer.toByteBuffer()` â€” Avro binary serialization (validates schema constraints)

---

## 8. Service-to-Service Dependencies

None. This is a standalone utility with no external service calls.

---

## 9. Event Flow Map

None. No event publishing or consumption patterns detected.

---

## 10. Ownership Map

| Module | Primary Owner | CODEOWNERS Entry | Commit Count | Last Modified |
|---|---|---|---|---|
| json-avro-validator | Maarten Smeets (maartensmeets) | No CODEOWNERS file | 5 (original) + 4 (archaeology) | 2026-07-21 |

### Contributor Breakdown

| Contributor | Commits | Role |
|---|---|---|
| Maarten Smeets (maartensmeets) | 5 | Original author |
| kaushikTT | 4 | Repository owner / archaeology runs |

---

## 11. Ownership Gaps

| Module | Risk Type | Details |
|---|---|---|
| json-avro-validator | Single Owner | Only original code contributor: Maarten Smeets |
| json-avro-validator | Stale | No code changes since 2022-01-27 (4+ years) |

---

## 12. High-Churn Files (Top 20)

| File | Commit Count | Distinct Authors | Churn Level |
|---|---|---|---|
| src/main/java/AvroTest.java | 3 | 1 | LOW |
| README.md | 2 | 1 | LOW |
| pom.xml | 1 | 1 | LOW |
| src/main/java/com/demo/avro/Customer.java | 1 | 1 | LOW |
| src/main/resources/file.avsc | 1 | 1 | LOW |
| src/main/resources/file.json | 1 | 1 | LOW |

Note: With only 5 original code commits, no files qualify as HIGH churn.

---

## 13. Scar-Tissue Analysis (CRITICAL and HIGH)

No scar tissue detected. No commits contain revert, hotfix, rollback, or emergency keywords.

| File | Revert Count | Hotfix Count | Score | Risk Level |
|---|---|---|---|---|
| (none) | 0 | 0 | 0 | LOW |

---

## 14. Pre-Edit Risk Warnings

No high-risk files identified. All files are LOW risk.

---

## 15. Decision Intelligence

### Architecture Decision Records

No ADR files found in the repository (checked: docs/adr, docs/decisions, adr).

### Notable Pull Requests

No pull requests found in this repository.

---

## 16. Knowledge Graph

```mermaid
graph TD
    AvroTest_java["AvroTest.java"] -->|owned_by| Maarten_Smeets["Maarten Smeets"]
    Customer_java["Customer.java"] -->|owned_by| Maarten_Smeets
    AvroTest_java -->|calls| Customer_java
    AvroTest_java -->|uses| Schema_Parser["Schema.Parser"]
    AvroTest_java -->|uses| GenericDatumReader["GenericDatumReader"]
    AvroTest_java -->|uses| SpecificDatumReader["SpecificDatumReader"]
    AvroTest_java -->|uses| ObjectMapper["Jackson ObjectMapper"]
    AvroTest_java -->|uses| DecoderFactory["DecoderFactory"]
    json_avro_validator["json-avro-validator"] -->|built_with| Maven["Maven"]
    json_avro_validator -->|uses| Apache_Avro["Apache Avro 1.11.0"]
    json_avro_validator -->|risk| LOW["LOW Risk"]
    json_avro_validator -->|status| Stale["Stale (4+ years)"]
```

---

## 17. Analysis Metadata

| Field | Value |
|---|---|
| Analysis Timestamp | 2026-07-21T05:15:00Z |
| Analysis Type | full |
| Repository | https://github.com/kaushikTT/json-avro-validator |
| Branch | main |
| Total API Calls | 6 |
| Analysis Duration | ~15s |
| Artifacts Pushed To | codebase_archaeology/ in branch main |
