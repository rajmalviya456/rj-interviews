# AI Agent Handbook Creation Guidelines

This document serves as the definitive guide for AI Agents (AntiGravity, Augment, Claude, etc.) when creating or updating technical interview handbooks. The goal is to ensure consistency, high quality, and optimal readability for the user.

## 1. File Structure and Naming

*   **Directory**: All handbooks must be placed in the `InterviewResources` directory.
*   **Naming Convention**: Use **PascalCase** for filenames.
    *   *Correct*: `DataAnalyst.md`, `MachineLearningEngineer.md`, `ReactDeveloper.md`
    *   *Incorrect*: `data_analyst.md`, `dataAnalyst.md`, `Data-Analyst.md`
*   **Frontmatter**: While strict YAML frontmatter isn't always enforced, start the file with a clear H1 title and a metadata block.

## 2. Document Heading Structure

Every handbook should follow this standard header format:

```markdown
# [Role Name] Interview Handbook

**Target Role:** [List of target roles, e.g., Senior Data Engineer, BI Architect]
**Focus:** [Scope of the document, e.g., Fundamentals to Advanced Production Concepts]

---

## Table of Contents
```

## 3. The Table of Contents (TOC)

*   **Location**: Immediately after the header block.
*   **Format**: Use a nested bullet list. **DO NOT USE HYPERLINKS**. The TOC is for overview only.
*   **Grouping**: Group related concepts into "Sections".

**Example:**
```markdown
### Section 1 — Foundations
- Basic Concepts
- Key Definitions

### Section 2 — Advanced Concepts
...
```

## 4. Section Formatting

*   **Hierarchy**:
    *   `#` (H1) for Document Title only.
    *   `##` (H2) for Major Sections (e.g., `## Section 1 — Foundations`).
    *   `###` (H3) for Specific Topics (e.g., `### ACID Properties`).
    *   `####` (H4) for Sub-concepts or Examples.
*   **Spacing**: Add a separator `---` before starting a new Major Section (H2) content to visually break up the document.
*   **Line Breaks**: Ensure distinct blank lines between text blocks, code blocks, and headers.

## 5. Content Elements and Pedagogy

### 5.1 ELI5 (Explain Like I'm 5)
For complex theoretical concepts, start with a simple analogy using a blockquote.

```markdown
> **ELI5**: Think of an API like a waiter in a restaurant...
```

### 5.2 Comparative Tables
Use tables *frequently* to compare technologies or methodologies (e.g., SQL vs NoSQL, Monolith vs Microservices).

*   **Requirement**: Columns must be aligned.
*   **Structure**: Feature | Item A | Item B

```markdown
| Feature | Relational DB | NoSQL DB |
| :--- | :--- | :--- |
| **Schema** | Rigid, predefined | Flexible |
| **Scaling** | Vertical | Horizontal |
```

### 5.3 Code Blocks
*   **Language Tag**: ALWAYS specify the language (e.g., `sql`, `python`, `java`, `bash`).
*   **Comments**: Use comments within code to explain specific lines.

### 5.4 ASCII Diagrams
Diagrams explain architecture better than text. AI Agents often mess up alignment.
*   **Rule 1**: Use a code block syntax (usually `text` or `mermaid` if supported, but `text` is safer for pure ASCII).
*   **Rule 2**: Use standard box-drawing characters or simple hyphens/pipes.
*   **Rule 3**: **VERIFY ALIGNMENT**. Ensure creating the artifact does not mangle whitespace.

**Standard Box Style:**
```text
+---------------------+       +----------------------+
|     Source System   | ----> |    Ingestion Layer   |
|     (PostgreSQL)    |       |      (Kafka)         |
+---------------------+       +----------+-----------+
                                         |
                                         v
                              +----------------------+
                              |   Processing Layer   |
                              |   (Apache Spark)     |
                              +----------------------+
```

**Sequence Style:**
```text
Client          Load Balancer        Server
  |                  |                  |
  | --- Request ---> |                  |
  |                  | --- Forward ---> |
  |                  |                  |
  |                  | <--- Response -- |
  | <--- Response -- |                  |
```

## 6. Interview Questions and Scenarios

Handbooks must include "Scenario Based Questions" to prepare candidates for real-world discussions.

### 6.1 Standard Format
```markdown
**Scenario Question**: "[The Question]"
- **Context**: [Optional: Add constraints or details]
- **Answer**: [The ideal answer, explaining the 'Why']
```

### 6.2 "What Happens When..."
Include system design style questions.
e.g., "What happens when you type google.com and hit enter?"

## 7. Formatting Checklist for AI Agents

Before finalizing the artifact, the Agent must verify:
- [ ] **TOC**: Are TOC items plain text (NO links)?
- [ ] **Alignment**: Are all tables and ASCII diagrams properly aligned monospaced?
- [ ] **Completeness**: Are there empty sections?
- [ ] **Consistency**: Is the heading style consistent throughout?
- [ ] **Clarity**: Are there sufficient code examples for coding concepts?

## 8. Topic Coverage Requirements (Crucial)

The handbook MUST be a "single source of truth" for candidates ranging from **Fresher (0 years)** to **Principal (10+ years)**. Nothing should be missed.

### 8.1 Freshers vs Experienced
*   **Freshers**: Cover textbook definitions, basic syntax, and "What is X?" questions.
*   **Experienced**: Cover "Why X over Y?", System Design implications, tradeoffs, and failure scenarios.

### 8.2 Mandatory Content Checklist
A complete handbook must cover:
1.  **Core Fundamentals**: In-depth explanation of every key term.
2.  **Production Realities**: How things break in real life (e.g., Network partitions, Race conditions).
3.  **Tooling Ecosystem**: Specific popular tools (e.g., for DevOps: Docker, K8s, Terraform).
4.  **Best Practices**: Security, Performance, Scalability.
5.  **Soft Skills/Behavioral**: Role-specific behavioral questions (e.g., "How do you handle a production outage?").
6.  **Robust Interview Questions**: A mix of easy, medium, and hard/scenario-based questions.

---
*Follow these guidelines strictly to generate high-quality, professional interview handbooks.*
