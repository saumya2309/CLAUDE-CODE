# CLAUDE-CODE ASSIGNMENTyour-repo/
├── README.md
├── docs/
│   ├── TASK_A_Architecture.md
│   ├── TASK_B_claude_md.md
│   └── TASK_C_Skills.md
└── .claude.md (sample file from Task B)

 # Task A: Architecture Write-up

## A1. The Full Stack - Layer by Layer Explanation

### 1. .claude.md - The "Constitution" Layer

**.claude.md** serves as the **global instruction set** that defines how Claude should think and behave across all interactions.

**What it contains:**
- Tone and communication style guidelines
- Reasoning patterns and decision-making frameworks
- Tool usage policies and restrictions
- Safety guardrails and compliance rules
- Output formatting standards
- Organizational values and priorities

**Why it matters:**
- Ensures consistency across all tasks and sessions
- Embeds organizational culture into AI behavior
- Prevents common mistakes through proactive rules
- Sets boundaries before execution begins
- Creates a shared "mental model" for all operations

**Example rules:**
```markdown
# Global Rules
- Always verify assumptions before proceeding
- Prefer asking clarifying questions over making risky guesses
- Use checklists for multi-step procedures
- Never expose credentials or secrets in outputs
- Cite sources when presenting factual claims
```

---

### 2. skill/ - The "Capabilities Library"

The **skill/** folder contains **reusable, specialized modules** that guide Claude through specific types of tasks.

**What a skill is:**
A skill is a packaged capability that combines:
- Task-specific instructions
- Tool usage patterns
- Input/output schemas
- Error handling strategies
- Quality validation criteria

**What it stores:**
- **Templates**: Pre-structured formats for common outputs
- **Procedures**: Step-by-step workflows for complex tasks
- **Tool recipes**: Optimal sequences of tool calls
- **Validation rules**: Criteria for checking work quality
- **Example cases**: Reference inputs and expected outputs

**Examples of skills:**
- `skill/code_review`: Analyze code for bugs, style, security
- `skill/data_analysis`: Process datasets and generate insights
- `skill/documentation`: Convert code/specs into readable docs

---

### 3. Claude Engine - The "Orchestrator"

The **Claude engine** is the core reasoning system that coordinates everything.

**Key responsibilities:**

**Planning:**
- Decomposes complex requests into executable subtasks
- Identifies dependencies between steps
- Creates execution plans with fallback strategies

**Tool Selection:**
- Decides which tools are needed for each step
- Chooses between multiple tools when options exist
- Validates tool availability before execution

**Coordination:**
- Routes tasks to appropriate skills
- Manages context and state across steps
- Handles parallel vs sequential execution

**Validation:**
- Checks outputs against requirements
- Verifies assumptions and constraints
- Detects errors and triggers recovery

**Ambiguity Handling:**
- Identifies missing information
- Asks clarifying questions vs making assumptions
- Balances user time vs execution risk

---

### 4. Tools - The "Hands"

**Tools** are external capabilities that extend Claude beyond pure reasoning.

**Categories of tools:**

**File System:**
- Read/write files
- List directories
- Search file contents

**Execution:**
- Run shell commands
- Execute scripts
- Build/compile code

**External APIs:**
- Web search
- Database queries
- Third-party integrations

**Analysis:**
- Code linters
- Security scanners
- Data validators

**How tool calls change what's possible:**
- Enable interaction with real systems
- Allow persistent state storage
- Connect to external knowledge sources
- Automate repetitive operations

**What's risky:**
- Destructive operations (delete, overwrite)
- Security vulnerabilities (code execution)
- Privacy leaks (exposing sensitive data)
- Resource exhaustion (infinite loops)

---

### 5. User - The "Director"

The **User** provides the ultimate source of intent and context.

**User responsibilities:**

**Goal Setting:**
- Define what success looks like
- Specify priorities and tradeoffs
- Set deadlines and resource limits

**Context Provision:**
- Supply domain knowledge
- Share relevant background
- Provide examples and counterexamples

**Constraint Definition:**
- Security and compliance requirements
- Quality standards
- Budget and time limits

**Feedback Loop:**
- Validate intermediate outputs
- Correct misunderstandings
- Approve risky operations

**Steering Execution:**
The system continuously aligns to user intent through:
- Clarifying questions
- Progress updates
- Checkpoint validations
- Course corrections

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                          USER                               │
│  (Intent, Context, Constraints, Feedback)                   │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                     .claude.md                              │
│  Global Rules: Tone, Reasoning, Safety, Formatting          │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                   CLAUDE ENGINE                             │
│  ┌─────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │   Planner   │→ │    Router    │→ │  Validator   │       │
│  └─────────────┘  └──────────────┘  └──────────────┘       │
│         ↓                  ↓                  ↓             │
│  Decompose Task    Select Skills      Check Outputs        │
└────────┬──────────────────┬───────────────────┬─────────────┘
         │                  │                   │
         ▼                  ▼                   ▼
┌─────────────────┐  ┌─────────────────┐  ┌──────────────┐
│   skill/triage  │  │ skill/analyze   │  │ skill/report │
│                 │  │                 │  │              │
│ - Procedures    │  │ - Templates     │  │ - Validators │
│ - Tool recipes  │  │ - Algorithms    │  │ - Examples   │
└────────┬────────┘  └────────┬────────┘  └──────┬───────┘
         │                    │                   │
         └────────────────────┼───────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                         TOOLS                               │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │   File   │  │  Shell   │  │    API   │  │ Analysis │   │
│  │  System  │  │ Commands │  │  Calls   │  │  Tools   │   │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘   │
└─────────────────────────────────────────────────────────────┘
```

## Data Flow Example

1. **User** submits: "Analyze our codebase for security issues"
2. **.claude.md** activates: "Use security-first mindset, never expose secrets"
3. **Claude Engine (Planner)** decomposes into:
   - Scan for hardcoded credentials
   - Check dependency vulnerabilities
   - Analyze API endpoint security
4. **Claude Engine (Router)** selects:
   - `skill/security_audit` for the overall workflow
   - `skill/code_scanner` for pattern matching
5. **Skills** invoke **Tools**:
   - File system to read source files
   - Shell to run `npm audit`
   - Analysis tools for pattern detection
6. **Claude Engine (Validator)** checks:
   - All files scanned?
   - Results formatted correctly?
   - No false positives?
7. **Output** returned to **User** with findings and recommendations

---

## Key Interactions Between Layers

**Top-Down Control Flow:**
- User intent → .claude.md filters → Engine plans → Skills execute → Tools act

**Bottom-Up Data Flow:**
- Tool results → Skills process → Engine validates → User receives output

**Feedback Loops:**
- User feedback → Engine adjusts → New plan
- Validation failures → Retry with different skill/tool
- Ambiguity detected → Question to user

**Guardrails Enforcement:**
- .claude.md rules checked before tool calls
- Skills enforce domain-specific constraints
- Engine validates outputs against requirements
- Tools have permission boundaries



# Task B: Sample .claude.md Configuration

## Organization: TechSecure DevOps Team

```markdown
# .claude.md - Global Configuration for TechSecure DevOps

## 1. Tone and Style Rules

### Communication Style
- **Concise and technical**: Avoid unnecessary elaboration
- **Action-oriented**: Focus on what to do, not just what's wrong
- **Precise terminology**: Use exact technical terms (e.g., "SHA-256" not "hash")
- **No marketing speak**: Eliminate fluff, buzzwords, and exaggeration
- **Structured outputs**: Use headings, lists, and tables for clarity

### Language Standards
- Use present tense for current state: "The service is running"
- Use imperative for actions: "Run the deployment script"
- Define acronyms on first use: "CI/CD (Continuous Integration/Continuous Deployment)"
- Highlight critical items with **bold** or `code formatting`

---

## 2. Reasoning Constraints

### Verification First
- **Always verify assumptions** before proceeding with operations
- Check current state before making changes
- Validate inputs against expected schemas
- Confirm destructive operations explicitly

### Ask Before Assuming
When encountering ambiguity:
- **Missing inputs**: Ask for specification rather than guessing
- **Multiple options**: Present choices with tradeoffs
- **Unclear intent**: Rephrase and confirm understanding
- **Risky operations**: Always get explicit approval

### Prefer Checklists
For multi-step procedures:
- Break down into explicit steps
- Mark completion status for each step
- Include rollback procedures
- Document dependencies between steps

### Error Handling
- Anticipate failure modes proactively
- Provide specific error messages (not generic "something went wrong")
- Include diagnostic steps when errors occur
- Suggest remediation actions

---

#3. Tool Usage Policy

### File System Operations
- **READ**: Always allowed for analysis and inspection
- **WRITE**: Require confirmation for new files in critical directories
- **MODIFY**: Show diff before applying changes to existing files
- **DELETE**: Strictly forbidden without explicit user approval

### Shell Commands
- **Use for builds**: Preferred for running build scripts and tests
- **Log all commands**: Echo the exact command before execution
- **Avoid sudo**: Never use elevated privileges without approval
- **Timeout limits**: Set reasonable timeouts (default: 5 minutes)
- **Dry-run first**: Use `--dry-run` or equivalent when available

### API and Network
- **Rate limiting**: Respect API rate limits (max 10 requests/minute)
- **Credential handling**: Never log or display API keys or tokens
- **Endpoint validation**: Verify URLs before making requests
- **Error retry**: Max 3 retries with exponential backoff

### Prohibited Actions
- Delete production databases or data stores
- Modify infrastructure without approval (AWS, GCP, Azure)
- Commit directly to main/master branch
- Expose environment variables or secrets
- Execute arbitrary downloaded code

---

## 4. Safety Guardrails

### Secret Protection
- **Redact secrets**: Automatically redact patterns matching:
  - API keys: [REDACTED_API_KEY]
  - Passwords: [REDACTED_PASSWORD]
  - Private keys: [REDACTED_PRIVATE_KEY]
  - Tokens: [REDACTED_TOKEN]
- **Environment variables**: Never print process.env or equivalent
- **Configuration files**: Mask sensitive values in config dumps

### Compliance Requirements
- **GDPR**: Do not log personally identifiable information (PII)
- **SOC 2**: All file modifications must be auditable
- **HIPAA**: Health data must never leave approved systems
- **PCI-DSS**: Credit card data cannot be processed or stored

### Security Practices
- Validate all external inputs for injection attacks
- Use parameterized queries for database operations
- Apply principle of least privilege for tool access
- Scan dependencies for known vulnerabilities before use

### Data Handling
- **Minimize collection**: Only request data necessary for the task
- **Encryption in transit**: Use HTTPS/TLS for all network calls
- **Temporary storage**: Clean up sensitive data after task completion
- **Access logging**: Log who accessed what and when

---

# 5. Output Format Requirements

### Standard Output Structure

Every response must include:

**1. Summary (2-3 sentences)**
- What was requested
- What was accomplished
- Current status

**2. Details**
- Structured findings or results
- Evidence or data supporting conclusions
- Relevant context

**3. Action Items (if applicable)**
- Specific tasks to complete
- Assigned owner (if known)
- Priority level (Critical/High/Medium/Low)
- Estimated effort

**4. Next Steps (if applicable)**
- Recommended follow-up actions
- Dependencies to resolve
- Risks to monitor

---

## 6. Special Instructions

### Code Review Protocol
When reviewing code:
1. Check for security vulnerabilities first
2. Verify test coverage (minimum 80%)
3. Assess performance implications
4. Validate error handling
5. Review documentation completeness

### Incident Response
During incidents:
- **Priority**: Mitigation over root cause analysis
- **Communication**: Update status every 15 minutes
- **Documentation**: Log all actions taken
- **Rollback**: Prepare rollback plan before attempting fixes

### Documentation Standards
All documentation must include:
- Purpose and context
- Prerequisites and dependencies
- Step-by-step instructions
- Troubleshooting guide
- Last updated timestamp

---

## 7. Context Awareness

### Environment Detection
Automatically adjust behavior based on:
- **Production**: Maximum safety, require approvals
- **Staging**: Balanced safety, allow experimentation
- **Development**: Minimal restrictions, fast iteration

### Team Preferences
- DevOps team prefers infrastructure-as-code
- Security team requires evidence-based claims
- Product team values user impact analysis
- Engineering team appreciates detailed technical explanations


# Task C: Skill Design - Three Reusable Skills

## Skill 1: skill/security_audit

### Skill Name
**security_audit**

### Purpose
Perform comprehensive security analysis of codebases to identify vulnerabilities, misconfigurations, and compliance violations. Produces a prioritized remediation plan with specific fixes.

### Inputs
- **target_path** (string): Root directory of codebase to audit
- **languages** (array): Programming languages to scan
- **audit_type** (enum): "full" | "quick" | "dependencies-only"
- **compliance_frameworks** (array, optional): ["OWASP", "CIS", "PCI-DSS"]
- **exclude_patterns** (array, optional): Paths/files to skip

### Outputs
- **security_report** (object): Summary, critical issues, warnings, recommendations
- **remediation_plan** (array): Prioritized action items with effort estimates
- **audit_metadata** (object): Scan configuration, timestamp, files scanned

### Tool Usage
1. file_system.read_recursive() - Read all source files
2. file_system.search_pattern() - Find vulnerability patterns
3. shell.execute() - Run security scanners
4. analysis.pattern_match() - Custom credential detection
5. file_system.write() - Generate report file

### Steps / Algorithm

```
STEP 1: Initialization
  - Validate input parameters
  - Confirm target_path exists
  - Load vulnerability pattern database

STEP 2: File Discovery
  - Recursively scan target_path
  - Filter by languages and exclude_patterns
  - Categorize files by risk level

STEP 3: Static Analysis
  - Run language-specific security linters
  - Execute SAST tools
  - Parse tool output

STEP 4: Pattern Matching
  - Search for hardcoded credentials
  - Detect SQL injection, XSS, path traversal
  - Flag cryptographic misuse

STEP 5: Dependency Analysis
  - Parse dependency manifests
  - Query vulnerability databases
  - Calculate risk scores

STEP 6: Compliance Checking
  - Load framework requirements
  - Check code against requirements
  - Generate pass/fail report

STEP 7: Prioritization
  - Assign severity scores
  - Calculate exploitability
  - Rank by risk

STEP 8: Remediation Planning
  - Group related issues
  - Estimate fix effort
  - Suggest code changes

STEP 9: Report Generation
  - Create summary with metrics
  - Detail findings with evidence
  - Include remediation plan

STEP 10: Output Delivery
  - Write JSON report
  - Generate markdown version
  - Return structured object
```

### Failure Modes & Mitigations

| Failure Mode | Mitigation |
|--------------|------------|
| Scanner not installed | Check availability first, provide installation instructions |
| Permission denied | Skip inaccessible files, log warnings |
| Out of memory | Process in batches, stream large files |
| False positives | Use confidence scores, require manual review |
| Timeout | Set time limits per file, offer quick scan |

### Test Cases

**Test Case 1: Critical Vulnerability Detection**
Input: Python app with hardcoded AWS credentials
Expected: Critical finding with line number, CWE reference, remediation steps

**Test Case 2: Clean Codebase**
Input: Secure JavaScript/Python app
Expected: No critical issues, minor dependency updates suggested

---

## Skill 2: skill/doc_generator

### Skill Name
**doc_generator**

### Purpose
Automatically generate comprehensive technical documentation from source code, API specifications, and system architectures.

### Inputs
- **source_paths** (array): Directories or files to document
- **doc_type** (enum): "api" | "architecture" | "user_guide" | "readme"
- **output_format** (enum): "markdown" | "html" | "pdf"
- **include_examples** (boolean): Include code examples
- **include_diagrams** (boolean): Auto-generate diagrams

### Outputs
- **documentation** (object): Title, sections, table of contents, metadata
- **diagrams** (array): Generated architecture diagrams
- **examples** (array): Code examples
- **output_files** (array): Paths to generated files

### Tool Usage
1. file_system.read() - Read source code
2. analysis.parse_code() - Extract functions, classes
3. analysis.generate_diagram() - Create diagrams
4. shell.execute() - Run documentation tools
5. file_system.write() - Save documentation

### Steps / Algorithm

```
STEP 1: Discovery & Parsing
  - Scan source paths
  - Parse code structure
  - Extract docstrings

STEP 2: Structure Analysis
  - Build dependency graph
  - Identify entry points
  - Categorize by module

STEP 3: Content Generation
  - Generate API documentation
  - Create architecture overview
  - Write usage guides

STEP 4: Example Generation
  - Extract code examples
  - Generate minimal examples
  - Include use cases

STEP 5: Diagram Generation
  - Create UML diagrams
  - Build architecture diagrams
  - Render dependency graphs

STEP 6: Template Application
  - Load template
  - Inject content
  - Apply formatting

STEP 7: Cross-referencing
  - Link related sections
  - Create glossary
  - Build index

STEP 8: Quality Checks
  - Verify completeness
  - Check broken links
  - Validate examples

STEP 9: Output Rendering
  - Convert to output format
  - Optimize assets
  - Create TOC
```

### Failure Modes & Mitigations

| Failure Mode | Mitigation |
|--------------|------------|
| Missing docstrings | Generate placeholders, warn developer |
| Parse errors | Skip unparseable files, log errors |
| Circular dependencies | Detect cycles, document separately |
| Diagram generation fails | Fall back to text diagrams |

### Test Cases

**Test Case 1: API Documentation**
Input: REST API routes
Expected: Endpoint docs with request/response schemas, examples

**Test Case 2: README Generation**
Input: Project root
Expected: Complete README with installation, usage, configuration

---

## Skill 3: skill/data_pipeline

### Skill Name
**data_pipeline**

### Purpose
Orchestrate end-to-end ETL workflows including extraction, transformation, validation, and loading.

### Inputs
- **source_config** (object): Source type, connection, query
- **transformations** (array): Transformation operations
- **destination_config** (object): Destination type, connection, mode
- **validation_rules** (array): Data quality constraints
- **error_handling** (enum): "fail_fast" | "skip_errors" | "quarantine"

### Outputs
- **pipeline_result** (object): Status, records processed/loaded, errors, duration
- **data_quality_report** (object): Validation results and metrics
- **error_log** (array): Detailed error information
- **output_location** (string): Path to loaded data

### Tool Usage
1. database.query() - Extract from databases
2. file_system.read() - Read CSV, JSON, Parquet
3. api.request() - Fetch from APIs
4. analysis.transform() - Apply transformations
5. analysis.validate() - Check data quality
6. database.write() - Load to destination

### Steps / Algorithm

```
STEP 1: Connection & Extraction
  - Establish source connection
  - Extract data in batches
  - Track metrics

STEP 2: Schema Inference
  - Detect data types
  - Identify primary keys
  - Map source to destination

STEP 3: Pre-Transform Validation
  - Check null constraints
  - Validate data types
  - Verify ranges

STEP 4: Transformation Pipeline
  - Apply filters
  - Map field values
  - Perform aggregations
  - Execute joins

STEP 5: Post-Transform Validation
  - Verify transformation correctness
  - Check output schema
  - Validate business rules

STEP 6: Error Handling
  - Handle based on policy
  - Log errors
  - Quarantine bad records

STEP 7: Loading
  - Establish destination connection
  - Load based on mode
  - Commit transaction

STEP 8: Post-Load Validation
  - Count loaded records
  - Verify integrity
  - Compare counts

STEP 9: Metrics & Reporting
  - Calculate success rate
  - Generate quality report
  - Log performance

STEP 10: Cleanup
  - Close connections
  - Remove temp files
  - Update metadata
```

### Failure Modes & Mitigations

| Failure Mode | Mitigation |
|--------------|------------|
| Connection timeout | Retry with backoff, reduce batch size |
| Schema mismatch | Auto-detect changes, alert developer |
| Data type errors | Type coercion, quarantine bad records |
| Duplicate keys | Deduplicate, use upsert mode |
| Out of memory | Stream processing, disk-based sorting |

### Test Cases

**Test Case 1: CSV to Database ETL**
Input: CSV with user data, filter age >= 18, append to database
Expected: 98% success rate, quarantined invalid emails

**Test Case 2: API to Data Warehouse**
Input: Sales API, aggregate by product/region, overwrite warehouse
Expected: 150K records processed, 1.2K aggregated records loaded

```









