# CLAUDE-CODE ASSIGNMENT
import React, { useState } from 'react';
import { FileText, GitBranch, Layers, Settings, Users, ChevronRight, Download } from 'lucide-react';

const ClaudeAssignment = () => {
  const [activeTab, setActiveTab] = useState('overview');

  const tabs = [
    { id: 'overview', label: 'Overview', icon: Layers },
    { id: 'architecture', label: 'Architecture', icon: GitBranch },
    { id: 'claudemd', label: '.claude.md', icon: FileText },
    { id: 'skills', label: 'Skills', icon: Settings },
    { id: 'agents', label: 'Agents', icon: Users }
  ];

  const downloadFile = (filename, content) => {
    const blob = new Blob([content], { type: 'text/plain' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = filename;
    a.click();
    URL.revokeObjectURL(url);
  };

  const downloadAllFiles = () => {
    const files = [
      { name: '.claude.md', content: claudeMdContent },
      { name: 'skill_triage.md', content: skillSpecs.triage },
      { name: 'skill_doc_summarize.md', content: skillSpecs.docSummarize },
      { name: 'skill_audit_crypto.md', content: skillSpecs.auditCrypto },
      { name: 'agent_code_reviewer.md', content: agentSpecs.codeReviewer },
      { name: 'agent_data_analyst.md', content: agentSpecs.dataAnalyst },
      { name: 'architecture_diagram.txt', content: architectureDiagram },
      { name: 'workflow_example.txt', content: workflowExample },
      { name: 'multi_agent_architecture.md', content: multiAgentArchitecture },
      { name: 'README.md', content: readmeContent }
    ];

    files.forEach(file => {
      setTimeout(() => downloadFile(file.name, file.content), 100);
    });
  };

  const readmeContent = `# Claude Architecture & Agent Creation Assignment

## Project Overview
This repository contains a complete implementation of Claude's architecture layers and agent design patterns for AI Systems & Agentic Workflows course.

## Contents

### 1. Architecture Documentation
- **architecture_diagram.txt**: Visual representation of Claude's layered architecture
- **workflow_example.txt**: Step-by-step execution trace showing how components interact

### 2. Global Configuration
- **.claude.md**: Global instructions defining tone, reasoning constraints, tool policies, and safety guardrails

### 3. Skill Modules (skill/ folder)
- **skill_triage.md**: Automated issue prioritization and remediation planning
- **skill_doc_summarize.md**: Document analysis and requirement extraction
- **skill_audit_crypto.md**: Cryptographic security scanning and compliance checking

### 4. Agent Specifications
- **agent_code_reviewer.md**: Automated code review with security and quality checks
- **agent_data_analyst.md**: Data analysis and insight generation

### 5. Multi-Agent System
- **multi_agent_architecture.md**: Coordinator-specialist pattern with routing and conflict resolution

## Key Concepts

### The Five Layers
1. **.claude.md**: "How to think" - Global rules and constraints
2. **skill/**: Specialized capabilities - Reusable task modules
3. **Claude Engine**: Orchestrator - Planning, routing, validation
4. **Tools**: External capabilities - File system, shell, web, APIs
5. **User**: Director - Provides intent and feedback

### Agent Patterns
- **Single-agent**: One agent handles entire workflow with tools
- **Multi-agent**: Coordinator delegates to specialists (Research, CodeReview, DataAnalyst, Verification)

## Architecture Highlights

### Data Flow
\`\`\`
User Intent → Claude Engine (checks .claude.md) → Planner → Router → 
Skill/Tool Selection → Execution → Validator → User Response
\`\`\`

### Coordination Pattern
\`\`\`
Coordinator Agent
    ├── Decomposes complex tasks
    ├── Routes to specialists
    ├── Aggregates results
    └── Resolves conflicts
\`\`\`

## Usage Examples

### Using a Skill
\`\`\`bash
# Triage incoming issues
skill/triage --input issues.json --output prioritized.json

# Summarize technical document
skill/doc_summarize --doc rfc-123.md --type requirements

# Audit crypto usage
skill/audit_crypto --path src/ --standards FIPS-140-2,NIST
\`\`\`

### Deploying an Agent
\`\`\`python
# Initialize Code Review Agent
agent = CodeReviewAgent(
    tools=['read_file', 'web_search'],
    guardrails=load_guardrails('.claude.md')
)

# Review pull request
result = agent.review(pr_id=1234)
print(result.summary)
\`\`\`

## Testing

Each skill includes test cases:
- **Positive tests**: Expected behavior with valid inputs
- **Edge cases**: Boundary conditions and unusual inputs
- **Failure modes**: How system handles errors

## Quality Checklist

Before deployment, verify:
- [ ] All layers documented with diagrams
- [ ] .claude.md covers all required sections
- [ ] Each skill has 2+ test cases
- [ ] Agents include example runs
- [ ] Multi-agent architecture shows message flow
- [ ] Conflict resolution strategy defined

## Evaluation Criteria

- **Clarity**: Diagrams and explanations are understandable
- **Correctness**: Architectures follow best practices
- **Examples**: Concrete, realistic use cases provided
- **Completeness**: All assignment tasks addressed
- **Design Quality**: Agents are implementable and testable

## Author
[Your Name]
Course: AI Systems & Agentic Workflows
Date: January 17, 2026

## License
Educational use only
`;



  const claudeMdContent = `# Claude AI Workflow Guidelines
## Global Instructions for TechCorp Engineering

### 1. Tone and Style Rules
- **Conciseness**: Prioritize clarity over verbosity. Use technical precision.
- **Direct Communication**: State facts, avoid hedging unless uncertainty is genuine.
- **Technical Depth**: Assume audience has engineering background.
- **No Marketing Speak**: Avoid buzzwords, hype, or promotional language.
- **Structured Output**: Use headings, lists, and clear sections.

### 2. Reasoning Constraints
- **Verify Assumptions**: Always state assumptions explicitly before proceeding.
- **Request Missing Inputs**: If critical information is missing, ask specific questions.
- **Prefer Checklists**: For multi-step processes, use numbered checklists.
- **Show Your Work**: For calculations or logic, include intermediate steps.
- **Consider Edge Cases**: Identify potential failure modes proactively.
- **Incremental Validation**: Validate outputs at each major step.

### 3. Tool Usage Policy
- **Shell Commands**: Use shell for builds, tests, and file operations.
- **Read Before Write**: Always inspect existing files before modification.
- **No Destructive Ops Without Confirmation**: Never delete, overwrite, or drop without explicit user approval.
- **Log All Commands**: Document what was executed and why.
- **Prefer Atomic Operations**: Batch related changes together.
- **Version Control Aware**: Check git status before major changes.

### 4. Safety Guardrails
- **Secret Detection**: Never log, display, or commit API keys, tokens, passwords.
- **PII Handling**: Redact personal identifiable information in logs and outputs.
- **Compliance**: Follow SOC2, GDPR, and HIPAA requirements where applicable.
- **Access Control**: Respect file permissions and user boundaries.
- **Audit Trail**: Maintain clear records of actions taken.
- **Reversibility**: Prefer changes that can be rolled back.

### 5. Output Format Requirements
Every response must include:

**Summary**
- 2-3 sentence overview of what was accomplished

**Action Items**
- Numbered list of completed steps
- Any pending tasks with owners

**Risks/Concerns** (if applicable)
- Potential issues identified
- Recommended mitigations

**Next Steps** (if applicable)
- Logical follow-up actions
- Dependencies or blockers

### 6. Error Handling
- **Graceful Degradation**: If a tool fails, explain and offer alternatives.
- **Clear Error Messages**: Include error type, context, and suggested fix.
- **No Silent Failures**: Always report when something doesn't work as expected.`;

  const skillSpecs = {
    triage: `# Skill: Issue Triage

## Purpose
Automatically prioritize incoming issues and generate remediation plans based on severity, impact, and urgency.

## Inputs
- \`issues\`: List of issue objects with fields:
  - \`id\`: Issue identifier
  - \`title\`: Issue description
  - \`severity\`: Optional (low/medium/high/critical)
  - \`affected_users\`: Number of impacted users
  - \`reported_at\`: Timestamp
  - \`category\`: Bug, feature, security, performance, etc.

## Outputs
- Prioritized issue list with:
  - \`priority_score\`: 0-100 calculated score
  - \`priority_level\`: P0 (critical) to P4 (low)
  - \`remediation_plan\`: Structured action plan
  - \`estimated_effort\`: Time estimate
  - \`recommended_owner\`: Team/person assignment

## Tool Usage
- \`read_file\`: Load issue data from JSON/CSV
- \`web_search\`: Check for known CVEs or similar issues
- \`write_file\`: Export prioritized list

## Algorithm
1. Load and parse issue data
2. Calculate priority score using formula:
   - Base score = severity weight (Critical=80, High=60, Medium=40, Low=20)
   - User impact multiplier = log10(affected_users + 1) * 10
   - Recency bonus = max(0, 20 - days_since_reported)
   - Security category bonus = +30 if category == "security"
3. Assign priority levels based on score thresholds
4. Generate remediation plan for each P0-P2 issue
5. Assign recommended owners based on category expertise
6. Output structured report

## Failure Modes & Mitigations
- **Missing severity data**: Use heuristics (keywords in title, category defaults)
- **Invalid timestamps**: Use current time as fallback
- **Empty issue list**: Return early with clear message
- **Tool access failure**: Cache last known good data

## Test Cases

### Test Case 1: Security Critical Issue
**Input:**
\`\`\`json
{
  "id": "ISS-1234",
  "title": "SQL Injection in login form",
  "severity": "critical",
  "affected_users": 50000,
  "reported_at": "2026-01-16T10:00:00Z",
  "category": "security"
}
\`\`\`

**Expected Output:**
\`\`\`json
{
  "priority_score": 97,
  "priority_level": "P0",
  "remediation_plan": [
    "Immediately disable affected endpoint",
    "Deploy parameterized query patch",
    "Audit all user inputs for similar vulnerabilities",
    "Notify security team and affected users"
  ],
  "estimated_effort": "4-6 hours",
  "recommended_owner": "Security Team"
}
\`\`\`

### Test Case 2: Low Priority Feature Request
**Input:**
\`\`\`json
{
  "id": "ISS-5678",
  "title": "Add dark mode to settings page",
  "severity": "low",
  "affected_users": 5,
  "reported_at": "2025-12-01T08:00:00Z",
  "category": "feature"
}
\`\`\`

**Expected Output:**
\`\`\`json
{
  "priority_score": 25,
  "priority_level": "P4",
  "remediation_plan": [
    "Add to backlog for Q2 planning",
    "Evaluate CSS framework options",
    "Gather user feedback on design preferences"
  ],
  "estimated_effort": "2-3 days",
  "recommended_owner": "Frontend Team"
}
\`\`\``,

    docSummarize: `# Skill: Document Summarization

## Purpose
Extract key requirements, decisions, and action items from specification documents, producing structured summaries for engineering teams.

## Inputs
- \`document_path\`: File path to document (supports .md, .txt, .pdf, .docx)
- \`summary_type\`: "requirements" | "decisions" | "full"
- \`max_length\`: Maximum summary length in words (default: 500)

## Outputs
- Structured summary containing:
  - \`key_requirements\`: List of functional/non-functional requirements
  - \`decisions_made\`: Architectural or design decisions
  - \`open_questions\`: Unresolved issues
  - \`stakeholders\`: Mentioned teams/people
  - \`timeline\`: Deadlines or milestones
  - \`dependencies\`: External systems or teams

## Tool Usage
- \`read_file\`: Load document content
- \`web_fetch\`: Retrieve linked references if needed
- \`write_file\`: Save summary in markdown format

## Algorithm
1. Load document and detect format
2. Parse document structure (headings, sections, lists)
3. Extract entities:
   - Requirements: Look for "must", "shall", "will", "should" statements
   - Decisions: Scan for "decided", "chosen", "approved" keywords
   - Questions: Find sentences ending with "?" or marked as "TBD"
   - Stakeholders: Extract @mentions, team names, role titles
   - Timeline: Parse dates, "by", "before", "deadline" phrases
4. Rank by importance (frequency, position in doc, explicit markers)
5. Generate structured output respecting max_length
6. Include document metadata (author, date, version)

## Failure Modes & Mitigations
- **Unsupported format**: Convert to text or request conversion
- **Document too large**: Process in chunks, prioritize early sections
- **No clear structure**: Use NLP to infer sections
- **Ambiguous requirements**: Flag with confidence scores

## Test Cases

### Test Case 1: Technical RFC
**Input:**
- document_path: "rfcs/auth-redesign.md"
- summary_type: "full"
- max_length: 400

**Expected Output:**
\`\`\`markdown
# Summary: Authentication System Redesign

## Key Requirements
1. Support OAuth 2.0 and SAML 2.0 protocols
2. Session timeout: 15 minutes idle, 8 hours absolute
3. MFA required for admin accounts
4. 99.99% uptime SLA for auth service

## Decisions Made
- Use Redis for session storage (chosen over database for latency)
- JWT tokens with 1-hour expiration
- Reject basic auth, support only modern protocols

## Open Questions
- How to handle legacy API clients still using basic auth?
- Should we support biometric authentication in v1?

## Stakeholders
- Security Team (reviewers)
- Platform Team (implementation)
- Product (requirements owner)

## Timeline
- Design review: Jan 20, 2026
- Implementation start: Feb 1, 2026
- Beta launch: Mar 15, 2026

## Dependencies
- Redis cluster upgrade (Platform Team)
- Certificate renewal process (Security)
\`\`\`

### Test Case 2: Meeting Notes
**Input:**
- document_path: "meetings/sprint-planning-2026-01-15.txt"
- summary_type: "decisions"
- max_length: 200

**Expected Output:**
\`\`\`markdown
# Decisions: Sprint Planning - Jan 15, 2026

1. **Sprint Goal**: Complete checkout flow redesign
2. **Capacity**: 80 story points (2 devs on vacation)
3. **Priority**: Security fixes take precedence over features
4. **Tech Debt**: Allocate 20% of sprint to refactoring
5. **Demo**: Schedule for Jan 29 at 2pm PT

## Action Items
- @sarah: Update JIRA with sprint items
- @mike: Set up staging environment
- @team: Review design mocks by EOD Wednesday
\`\`\``,

    auditCrypto: `# Skill: Cryptography Audit

## Purpose
Scan configuration files and source code to identify cryptographic usage patterns, flag weak algorithms, and ensure compliance with security standards.

## Inputs
- \`scan_path\`: Directory or file path to scan
- \`recursive\`: Boolean, scan subdirectories
- \`file_patterns\`: List of glob patterns (e.g., ["*.py", "*.js", "*.yml"])
- \`standards\`: List of compliance frameworks ["FIPS-140-2", "NIST", "OWASP"]

## Outputs
- Audit report containing:
  - \`weak_algorithms\`: List of deprecated/weak crypto found
  - \`strong_algorithms\`: List of approved crypto in use
  - \`findings\`: Detailed list of issues with severity
  - \`recommendations\`: Specific remediation steps
  - \`compliance_status\`: Pass/fail for each standard
  - \`risk_score\`: Overall risk rating (0-100)

## Tool Usage
- \`list_files\`: Enumerate files to scan
- \`read_file\`: Load and analyze file contents
- \`web_search\`: Check CVE databases for known vulnerabilities
- \`write_file\`: Generate audit report

## Algorithm
1. Build file list from scan_path matching patterns
2. For each file:
   a. Detect crypto-related imports/libraries
   b. Identify algorithm references (regex patterns)
   c. Check against blacklist (MD5, SHA-1, DES, RC4, etc.)
   d. Check against whitelist (AES-256, SHA-256+, RSA-2048+, etc.)
   e. Analyze key sizes, modes, parameters
3. Cross-reference findings with CVE database
4. Calculate severity scores:
   - Critical: Broken crypto in production code
   - High: Weak crypto or improper usage
   - Medium: Deprecated but not broken
   - Low: Best practice violations
5. Generate compliance matrix
6. Produce prioritized remediation plan

## Failure Modes & Mitigations
- **False positives**: Crypto in comments/docs -> filter by context
- **Obfuscated code**: Can't detect all patterns -> note limitations
- **Large codebases**: Timeout risk -> implement progress checkpoints
- **Access denied**: Skip files with permission errors, log them

## Test Cases

### Test Case 1: Python Web App
**Input:**
\`\`\`python
# File: app/auth.py
import hashlib
import hmac
from Crypto.Cipher import AES, DES

def hash_password(password):
    return hashlib.md5(password.encode()).hexdigest()

def encrypt_token(token, key):
    cipher = DES.new(key, DES.MODE_ECB)
    return cipher.encrypt(token)

def secure_hash(data, secret):
    return hmac.new(secret, data, hashlib.sha256).digest()
\`\`\`

**Expected Output:**
\`\`\`json
{
  "weak_algorithms": [
    {
      "algorithm": "MD5",
      "location": "app/auth.py:6",
      "severity": "CRITICAL",
      "issue": "MD5 is cryptographically broken for password hashing",
      "recommendation": "Use bcrypt, Argon2, or PBKDF2 with strong parameters"
    },
    {
      "algorithm": "DES",
      "location": "app/auth.py:9-10",
      "severity": "CRITICAL",
      "issue": "DES has 56-bit key size, easily brute-forced. ECB mode is insecure.",
      "recommendation": "Replace with AES-256 in GCM or CBC mode with proper IV"
    }
  ],
  "strong_algorithms": [
    {
      "algorithm": "HMAC-SHA256",
      "location": "app/auth.py:13",
      "status": "COMPLIANT"
    }
  ],
  "compliance_status": {
    "FIPS-140-2": "FAIL",
    "NIST": "FAIL",
    "OWASP": "FAIL"
  },
  "risk_score": 92,
  "summary": "CRITICAL: 2 broken cryptographic algorithms detected in production code"
}
\`\`\`

### Test Case 2: Configuration File
**Input:**
\`\`\`yaml
# File: config/database.yml
production:
  encryption:
    algorithm: aes-256-gcm
    key_derivation: pbkdf2
    iterations: 100000
    salt_length: 32
  ssl:
    min_version: TLSv1.2
    ciphers: "ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256"
\`\`\`

**Expected Output:**
\`\`\`json
{
  "weak_algorithms": [],
  "strong_algorithms": [
    {
      "algorithm": "AES-256-GCM",
      "location": "config/database.yml:3",
      "status": "COMPLIANT"
    },
    {
      "algorithm": "PBKDF2",
      "location": "config/database.yml:4",
      "status": "COMPLIANT",
      "note": "100K iterations meets NIST minimum (10K), consider 600K+ for better security"
    }
  ],
  "compliance_status": {
    "FIPS-140-2": "PASS",
    "NIST": "PASS",
    "OWASP": "PASS"
  },
  "risk_score": 15,
  "summary": "GOOD: All cryptographic configurations meet security standards",
  "recommendations": [
    "Consider increasing PBKDF2 iterations to 600,000 for enhanced security",
    "Update to TLS 1.3 when infrastructure supports it"
  ]
}
\`\`\``,
  };

  const architectureDiagram = `
┌─────────────────────────────────────────────────────────────────────┐
│                            USER (Director)                           │
│  Provides: Intent, Context, Constraints, Feedback, Acceptance       │
└────────────────────────────┬────────────────────────────────────────┘
                             │ Input/Feedback
                             ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        .claude.md (Global Rules)                     │
│  • Tone & Style          • Tool Usage Policy    • Output Formats    │
│  • Reasoning Constraints • Safety Guardrails    • Error Handling    │
└────────────────────────────┬────────────────────────────────────────┘
                             │ Governs All Behavior
                             ▼
┌─────────────────────────────────────────────────────────────────────┐
│                      CLAUDE ENGINE (Orchestrator)                    │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────┐             │
│  │   Planner   │  │    Router    │  │  Validator    │             │
│  │ Decompose   │→ │ Choose Skill │→ │ Check Output  │             │
│  │   Tasks     │  │  /Tool       │  │  Quality      │             │
│  └─────────────┘  └──────────────┘  └───────────────┘             │
│         │                 │                    │                     │
│         └─────────────────┼────────────────────┘                     │
└───────────────────────────┼──────────────────────────────────────────┘
                            │
                            ▼
        ┌───────────────────┴───────────────────┐
        │                                       │
        ▼                                       ▼
┌───────────────────┐                 ┌──────────────────────┐
│   skill/ Modules  │                 │   TOOLS (Hands)      │
│  ┌──────────────┐ │                 │  ┌────────────────┐  │
│  │ skill/triage │ │                 │  │  File System   │  │
│  └──────────────┘ │                 │  └────────────────┘  │
│  ┌──────────────┐ │                 │  ┌────────────────┐  │
│  │ skill/doc    │ │◄────calls──────►│  │  Shell/Exec    │  │
│  │  _summarize  │ │                 │  └────────────────┘  │
│  └──────────────┘ │                 │  ┌────────────────┐  │
│  ┌──────────────┐ │                 │  │  Web Search    │  │
│  │ skill/audit  │ │                 │  └────────────────┘  │
│  │   _crypto    │ │                 │  ┌────────────────┐  │
│  └──────────────┘ │                 │  │  API Calls     │  │
└───────────────────┘                 │  └────────────────┘  │
                                      └──────────────────────┘

Data Flow:
1. User provides intent → Claude Engine
2. Engine checks .claude.md for global rules
3. Engine plans: breaks down task into steps
4. Engine routes: selects appropriate skill or tool
5. Skill executes using tools
6. Engine validates output against quality standards
7. Result returned to user with summary + action items
`;

  const workflowExample = `
WORKFLOW EXAMPLE: "Audit Security Configuration"

User Request: "Check our production config for security issues"

STEP 1: Intent Understanding (Claude Engine - Planner)
- Task: Security audit of production configuration
- Constraint: Read-only, no modifications
- Context: Production environment, high stakes
- .claude.md rules: Follow safety guardrails, require approval for changes

STEP 2: Task Decomposition (Claude Engine - Planner)
Subtasks:
  a) Locate production config files
  b) Scan for cryptographic usage
  c) Check for hardcoded secrets
  d) Validate TLS/SSL settings
  e) Generate prioritized findings report

STEP 3: Skill Selection (Claude Engine - Router)
- For subtask (a): Use tool 'list_files' directly
- For subtask (b): Invoke skill/audit_crypto
- For subtask (c): Invoke skill/secret_scan (hypothetical)
- For subtask (d): Use skill/audit_crypto (covers TLS)
- For subtask (e): Claude engine synthesizes

STEP 4: Execution - Locate Files
Tool: list_files("config/production/", pattern="*.yml,*.json,*.env")
Result: Found 12 files

STEP 5: Execution - Crypto Audit
Skill: skill/audit_crypto
Input: {scan_path: "config/production/", recursive: true}
Output: 
  - 3 weak algorithms found (MD5, SHA-1, DES)
  - Risk score: 78 (High)
  - 2 critical findings, 1 high, 3 medium

STEP 6: Validation (Claude Engine - Validator)
Checks:
  ✓ Output format matches expected schema
  ✓ Risk score calculated correctly
  ✓ Findings include file locations and line numbers
  ✓ Recommendations are actionable
  ⚠ Missing: Compliance status for HIPAA (add note)

STEP 7: Synthesis & Formatting (Claude Engine)
Combines results from all subtasks into structured report
Applies .claude.md output format (Summary + Action Items + Risks)

STEP 8: User Delivery
Returns formatted report:

**Summary**
Security audit of production configs identified 3 critical cryptographic 
vulnerabilities requiring immediate attention. Overall risk score: 78/100 (High).

**Action Items**
1. ✓ Scanned 12 production config files
2. ✓ Identified 6 security findings (2 critical, 1 high, 3 medium)
3. ⚠ Pending: Secret scan (requires elevated permissions)

**Risks/Concerns**
- CRITICAL: MD5 password hashing in auth service (database.yml:45)
- CRITICAL: Hardcoded API key detected in api-config.json:12
- HIGH: TLS 1.0 still enabled (nginx.conf:78)

**Next Steps**
1. Replace MD5 with bcrypt/Argon2 (Security Team - Priority: P0)
2. Rotate exposed API key immediately (Platform Team - Priority: P0)
3. Disable TLS 1.0, enforce TLS 1.2+ (DevOps - Priority: P1)
4. Schedule follow-up audit in 1 week to verify fixes
`;

  const agentSpecs = {
    codeReviewer: `# AGENT: Code Review Agent

## 1. Agent Name
**CodeReviewAgent**

## 2. Purpose / Mission
Perform automated code review on pull requests, identifying bugs, security vulnerabilities, performance issues, and style violations. Provide constructive feedback to improve code quality.

## 3. Responsibilities
- Analyze code changes in pull requests
- Identify potential bugs, logic errors, and edge cases
- Flag security vulnerabilities (SQL injection, XSS, etc.)
- Check for performance anti-patterns
- Enforce code style and best practices
- Suggest improvements and optimizations
- Validate test coverage
- Check for proper error handling
- Ensure documentation is updated

## 4. Out-of-Scope
- Does NOT approve or merge pull requests (human decision)
- Does NOT refactor code automatically without approval
- Does NOT modify production code directly
- Does NOT handle deployment or CI/CD configuration
- Does NOT make architectural decisions
- Does NOT access production databases or secrets

## 5. Inputs Required
- Pull request ID or diff
- Target branch (e.g., main, develop)
- Programming language(s)
- Repository context (coding standards, linting rules)
- Optional: Previous review comments for context

## 6. Outputs Produced
- Structured review report with:
  - Overall assessment (Approve / Request Changes / Comment)
  - Findings categorized by severity (Critical / High / Medium / Low)
  - Line-by-line comments with file:line references
  - Suggested fixes (code snippets)
  - Test coverage metrics
  - Summary of changes reviewed

## 7. Tools Allowed
- \`read_file\`: Read source files and diffs
- \`list_files\`: Enumerate changed files
- \`web_search\`: Look up best practices or security patterns
- \`write_file\`: Generate review report
- Static analysis tools (linters, SAST scanners)

## 8. Rules & Guardrails
- **Tone**: Constructive and educational, never dismissive
- **False Positives**: Acknowledge uncertainty, explain reasoning
- **Context**: Consider PR description and linked issues
- **Incremental**: Review only changed lines + 5 lines context
- **Non-Blocking**: Don't block PRs for minor style issues
- **Privacy**: Never log or store code snippets externally
- **Fairness**: Apply same standards regardless of author

## 9. Decision Policy
**ASK when:**
- Architectural changes that affect multiple systems
- Breaking API changes without clear migration path
- Security concerns that need domain expertise
- Ambiguous intent (what problem is this solving?)

**ASSUME when:**
- Standard refactoring patterns
- Minor style consistency fixes
- Adding tests for existing code
- Documentation updates

## 10. Quality Checklist
Before submitting review:
- [ ] All changed files analyzed
- [ ] Findings include file:line references
- [ ] Suggestions are specific and actionable
- [ ] Security issues marked as Critical/High
- [ ] At least one positive comment included
- [ ] No personal or subjective criticism
- [ ] Links to documentation for non-obvious feedback

## 11. Example Runs

### Example 1: Security Vulnerability Found

**Input:**
\`\`\`python
# PR #1234: Add user search endpoint
# File: api/users.py

@app.route('/search')
def search_users():
    query = request.args.get('q')
    sql = f"SELECT * FROM users WHERE name LIKE '%{query}%'"
    results = db.execute(sql)
    return jsonify(results)
\`\`\`

**Output:**
\`\`\`markdown
# Code Review: PR #1234

## Overall Assessment: REQUEST CHANGES

## Critical Findings

### 🔴 CRITICAL: SQL Injection Vulnerability
**File:** api/users.py:6
**Issue:** User input directly interpolated into SQL query
**Impact:** Attacker can execute arbitrary SQL commands

**Current Code:**
\`\`\`python
sql = f"SELECT * FROM users WHERE name LIKE '%{query}%'"
\`\`\`

**Suggested Fix:**
\`\`\`python
sql = "SELECT * FROM users WHERE name LIKE %s"
results = db.execute(sql, (f'%{query}%',))
\`\`\`

**Reference:** https://owasp.org/www-community/attacks/SQL_Injection

## High Findings

### 🟠 HIGH: Missing Input Validation
**File:** api/users.py:5
**Issue:** No length limit or sanitization on search query
**Impact:** Potential DoS via extremely long queries

**Suggested Fix:**
\`\`\`python
query = request.args.get('q', '')[:100]  # Limit to 100 chars
if not query or not query.strip():
    return jsonify({'error': 'Query required'}), 400
\`\`\`

## Medium Findings

### 🟡 MEDIUM: No Pagination
**File:** api/users.py:7
**Issue:** Query returns all matching results, could be thousands
**Suggestion:** Add LIMIT/OFFSET parameters

## Positive Notes
✅ Good: Endpoint uses POST method for data modification
✅ Good: Clear, descriptive function name

## Summary
Reviewed 1 file, 8 lines changed. Found 1 critical, 1 high, 1 medium issue.
**Action Required:** Fix SQL injection before merge.
\`\`\`

### Example 2: Clean Code Approved

**Input:**
\`\`\`python
# PR #1235: Add unit tests for authentication
# File: tests/test_auth.py

import pytest
from app.auth import hash_password, verify_password

def test_hash_password_returns_string():
    result = hash_password("secure123")
    assert isinstance(result, str)
    assert len(result) > 0

def test_verify_password_correct():
    hashed = hash_password("password123")
    assert verify_password("password123", hashed) is True

def test_verify_password_incorrect():
    hashed = hash_password("password123")
    assert verify_password("wrong", hashed) is False
\`\`\`

**Output:**
\`\`\`markdown
# Code Review: PR #1235

## Overall Assessment: APPROVE ✅

## Summary
Excellent test coverage for authentication functions. No issues found.

## Positive Notes
✅ Tests cover happy path and error cases
✅ Clear, descriptive test names following convention
✅ Proper use of pytest assertions
✅ No hardcoded secrets or sensitive data

## Minor Suggestions (Non-blocking)

### 💡 Enhancement: Add edge case tests
Consider adding tests for:
- Empty string password
- Very long passwords (>1000 chars)
- Unicode/special characters in passwords

Example:
\`\`\`python
def test_hash_password_empty_string():
    with pytest.raises(ValueError):
        hash_password("")
\`\`\`

## Summary
Reviewed 1 file, 15 lines added. Zero issues found. Great work! 🎉
\`\`\`
`,

    dataAnalyst: `# AGENT: Data Analysis Agent

## 1. Agent Name
**DataAnalystAgent**

## 2. Purpose / Mission
Analyze datasets to extract insights, identify patterns, generate reports, and answer business questions. Transform raw data into actionable intelligence.

## 3. Responsibilities
- Load and validate datasets (CSV, JSON, SQL, Excel)
- Perform exploratory data analysis (EDA)
- Calculate statistics (mean, median, trends, distributions)
- Identify anomalies and outliers
- Generate visualizations (charts, graphs, heatmaps)
- Answer specific analytical questions
- Produce executive summaries
- Recommend data-driven actions

## 4. Out-of-Scope
- Does NOT modify source databases directly
- Does NOT make business decisions (only recommends)
- Does NOT access PII without explicit permission
- Does NOT share raw data externally
- Does NOT perform real-time streaming analytics
- Does NOT deploy ML models to production

## 5. Inputs Required
- Dataset (file path or database connection)
- Analysis objective (question to answer)
- Optional: Time range, filters, grouping dimensions
- Optional: Baseline data for comparison
- Data dictionary or schema

## 6. Outputs Produced
- Analysis report with:
  - Executive summary (3-5 key findings)
  - Statistical analysis results
  - Visualizations (charts, tables)
  - Anomalies or notable patterns
  - Data quality assessment
  - Recommendations with confidence levels
  - Methodology notes

## 7. Tools Allowed
- \`read_file\`: Load datasets
- \`write_file\`: Save reports and visualizations
- \`web_search\`: Look up industry benchmarks
- Data processing: pandas, numpy, statistical libraries
- Visualization: matplotlib, plotly, chartjs

## 8. Rules & Guardrails
- **Privacy**: Aggregate PII, never display individual records
- **Accuracy**: State confidence intervals and limitations
- **Bias**: Check for sampling bias, report potential skews
- **Reproducibility**: Document all transformations and filters
- **Validation**: Cross-check calculations, validate assumptions
- **Transparency**: Explain methodology in plain language

## 9. Decision Policy
**ASK when:**
- Data definitions are ambiguous
- Multiple interpretation methods exist
- Outliers could be errors or genuine signals
- Missing data exceeds 20% of dataset
- Results contradict domain knowledge

**ASSUME when:**
- Standard statistical definitions apply
- Date formats follow ISO 8601
- Missing values should be excluded (not imputed)
- Confidence level = 95% unless specified

## 10. Quality Checklist
- [ ] Data quality issues documented
- [ ] Sample size sufficient for conclusions
- [ ] Visualizations clearly labeled with units
- [ ] Statistical significance tested where applicable
- [ ] Limitations and caveats stated
- [ ] Recommendations tied to specific data points
- [ ] Report accessible to non-technical stakeholders

## 11. Example Runs

### Example 1: Sales Trend Analysis

**Input:**
Dataset: quarterly_sales_2025.csv
Question: "Are sales increasing or decreasing this year?"

**Output:**
\`\`\`markdown
# Sales Trend Analysis: 2025

## Executive Summary
Sales show strong upward trend (+23% YoY) driven by Q3 surge. 
However, Q4 shows early signs of plateau. Customer acquisition 
cost increasing.

## Key Findings

1. **Revenue Growth**: $12.4M total (vs $10.1M in 2024)
   - Q1: $2.8M (+5%)
   - Q2: $3.1M (+12%)
   - Q3: $4.2M (+45%) ⭐ Peak quarter
   - Q4: $2.3M (projected, -15% vs Q3)

2. **Customer Metrics**:
   - New customers: 1,847 (+31%)
   - Churn rate: 12% (within normal range)
   - Average order value: $156 (-3%)

3. **Geographic Distribution**:
   - North America: 62% of revenue (+18% YoY)
   - Europe: 28% (+35% YoY) ⭐ Fastest growth
   - APAC: 10% (+8% YoY)

## Anomalies Detected
- ⚠️ Q3 spike: Traced to viral marketing campaign (one-time event)
- ⚠️ Q4 decline: Early holiday season, likely recovers in Dec

## Visualizations
[Chart: Quarterly revenue trend line]
[Chart: Customer acquisition by channel]
[Table: Top 10 products by revenue]

## Data Quality Notes
- 98.7% complete records
- 23 duplicate entries removed
- Currency normalized to USD

## Recommendations
1. **Sustain Momentum**: Replicate Q3 marketing tactics (Confidence: High)
2. **International Expansion**: Invest in European market (Confidence: Medium)
3. **Retention Focus**: Address declining AOV through upselling (Confidence: Medium)
4. **Monitor Q4**: Watch for Dec recovery; if not, investigate churn drivers

## Methodology
- Analysis period: Jan 1 - Dec 31, 2025
- Comparison baseline: 2024 same period
- Statistical test: Linear regression (R²=0.87)
- Outlier threshold: ±2 standard deviations
\`\`\`

### Example 2: Customer Churn Prediction

**Input:**
Dataset: customer_activity.csv
Question: "Which customers are at risk of churning?"

**Output:**
\`\`\`markdown
# Churn Risk Analysis

## Executive Summary
342 customers (8.2%) flagged as high churn risk. Primary 
indicators: 30+ days inactive, declined support calls, 
reduced feature usage.

## High-Risk Segment Profile
- Total identified: 342 customers
- Estimated revenue at risk: $428K annually
- Common characteristics:
  - Avg account age: 18 months
  - Last login: 35+ days ago
  - Support tickets: 0 in last quarter
  - Feature usage: Down 60% from baseline

## Risk Tiers

### 🔴 Critical Risk (127 customers, $156K revenue)
- No activity in 45+ days
- Previous complaint unresolved
- **Action**: Personal outreach within 48 hours

### 🟠 High Risk (215 customers, $272K revenue)
- Activity declined 60%+ in 30 days
- Multiple failed payment attempts
- **Action**: Automated re-engagement campaign

## Retention Strategies
1. **Win-back Campaign**: Offer 20% discount for 3 months
   - Est. cost: $85K
   - Est. recovery: 40% of at-risk customers
   - ROI: +$86K net

2. **Proactive Support**: Assign CSM to critical accounts
   - Target: 127 critical customers
   - Resource: 2 FTE for 1 month

## Predictive Model
- Algorithm: Logistic regression
- Accuracy: 78%
- Precision: 82% (low false positives)
- Key features: days_since_login, support_ticket_count, feature_usage_trend

## Next Steps
- Export high-risk customer list (see attached CSV)
- Brief sales team on outreach talking points
- Schedule follow-up analysis in 30 days
\`\`\`
`
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 text-white p-8">
      <div className="max-w-7xl mx-auto">
        {/* Header */}
        <div className="mb-8">
          <h1 className="text-4xl font-bold mb-2">Claude Architecture & Agent Assignment</h1>
          <p className="text-purple-300">AI Systems & Agentic Workflows - Complete Solution</p>
          <button
            onClick={downloadAllFiles}
            className="mt-4 px-6 py-2 bg-purple-600 hover:bg-purple-700 rounded-lg flex items-center gap-2 transition-colors"
          >
            <Download size={20} />
            Download All Files for GitHub
          </button>
        </div>

        {/* Navigation Tabs */}
        <div className="flex gap-2 mb-6 overflow-x-auto">
          {tabs.map(tab => {
            const Icon = tab.icon;
            return (
              <button
                key={tab.id}
                onClick={() => setActiveTab(tab.id)}
                className={`px-4 py-2 rounded-lg flex items-center gap-2 whitespace-nowrap transition-colors ${
                  activeTab === tab.id
                    ? 'bg-purple-600 text-white'
                    : 'bg-slate-800 text-slate-300 hover:bg-slate-700'
                }`}
              >
                <Icon size={18} />
                {tab.label}
              </button>
            );
          })}
        </div>

        {/* Content Area */}
        <div className="bg-slate-800 rounded-lg p-6 shadow-2xl">
          {activeTab === 'overview' && (
            <div className="space-y-6">
              <h2 className="text-2xl font-bold text-purple-400">Assignment Overview</h2>
              <div className="bg-slate-900 p-4 rounded border border-purple-500/30">
                <h3 className="text-xl font-semibold mb-3">Learning Objectives</h3>
                <ul className="list-disc list-inside space-y-2 text-slate-300">
                  <li>Explain Claude's architecture layers and their interactions</li>
                  <li>Describe roles of .claude.md, skill/, Claude engine, Tools, and User</li>
                  <li>Design agents with responsibilities, tools, memory, and guardrails</li>
                  <li>Build implementable and testable agent specifications</li>
                </ul>
              </div>

              <div className="grid md:grid-cols-2 gap-4">
                <div className="bg-slate-900 p-4 rounded">
                  <h3 className="text-lg font-semibold mb-2 text-purple-300">Tasks Completed</h3>
                  <ul className="space-y-1 text-sm">
                    <li className="flex items-center gap-2">
                      <ChevronRight size={16} className="text-green-400" />
                      Architecture write-up with diagrams
                    </li>
                    <li className="flex items-center gap-2">
                      <ChevronRight size={16} className="text-green-400" />
                      Sample .claude.md configuration
                    </li>
                    <li className="flex items-center gap-2">
                      <ChevronRight size={16} className="text-green-400" />
                      3 complete skill specifications
                    </li>
                    <li className="flex items-center gap-2">
                      <ChevronRight size={16} className="text-green-400" />
                      Claude Engine workflow example
                    </li>
                    <li className="flex items-center gap-2">
                      <ChevronRight size={16} className="text-green-400" />
                      2 complete agent designs
                    </li>
                    <li className="flex items-center gap-2">
                      <ChevronRight size={16} className="text-green-400" />
                      Multi-agent orchestration architecture
                    </li>
                  </ul>
                </div>

                <div className="bg-slate-900 p-4 rounded">
                  <h3 className="text-lg font-semibold mb-2 text-purple-300">Deliverables</h3>
                  <ul className="space-y-1 text-sm">
                    <li>📄 README.md</li>
                    <li>📄 .claude.md (global rules)</li>
                    <li>📁 3 skill specifications</li>
                    <li>📁 2 agent specifications</li>
                    <li>📊 Architecture diagram</li>
                    <li>📊 Multi-agent diagram</li>
                    <li>📝 Workflow trace example</li>
                  </ul>
                </div>
              </div>
            </div>
          )}

          {activeTab === 'architecture' && (
            <div className="space-y-4">
              <div className="flex justify-between items-center">
                <h2 className="text-2xl font-bold text-purple-400">Architecture Documentation</h2>
                <button
                  onClick={() => downloadFile('architecture_diagram.txt', architectureDiagram)}
                  className="px-4 py-2 bg-purple-600 hover:bg-purple-700 rounded text-sm flex items-center gap-2"
                >
                  <Download size={16} />
                  Download
                </button>
              </div>
              <pre className="bg-slate-900 p-4 rounded overflow-x-auto text-xs border border-slate-700">
                {architectureDiagram}
              </pre>

              <div className="mt-8">
                <h3 className="text-xl font-semibold mb-3 text-purple-300">Workflow Example</h3>
                <button
                  onClick={() => downloadFile('workflow_example.txt', workflowExample)}
                  className="mb-3 px-4 py-2 bg-purple-600 hover:bg-purple-700 rounded text-sm flex items-center gap-2"
                >
                  <Download size={16} />
                  Download
                </button>
                <pre className="bg-slate-900 p-4 rounded overflow-x-auto text-xs border border-slate-700">
                  {workflowExample}
                </pre>
              </div>
            </div>
          )}

          {activeTab === 'claudemd' && (
            <div className="space-y-4">
              <div className="flex justify-between items-center">
                <h2 className="text-2xl font-bold text-purple-400">.claude.md Configuration</h2>
                <button
                  onClick={() => downloadFile('.claude.md', claudeMdContent)}
                  className="px-4 py-2 bg-purple-600 hover:bg-purple-700 rounded text-sm flex items-center gap-2"
                >
                  <Download size={16} />
                  Download
                </button>
              </div>
              <div className="bg-slate-900 p-4 rounded border border-slate-700">
                <pre className="text-xs overflow-x-auto whitespace-pre-wrap">{claudeMdContent}</pre>
              </div>
            </div>
          )}

          {activeTab === 'skills' && (
            <div className="space-y-6">
              <h2 className="text-2xl font-bold text-purple-400">Skill Specifications</h2>
              
              {['triage', 'docSummarize', 'auditCrypto'].map((skill) => (
                <div key={skill} className="bg-slate-900 p-4 rounded border border-slate-700">
                  <div className="flex justify-between items-center mb-3">
                    <h3 className="text-xl font-semibold text-purple-300">
                      {skill === 'triage' && 'Skill: Issue Triage'}
                      {skill === 'docSummarize' && 'Skill: Document Summarization'}
                      {skill === 'auditCrypto' && 'Skill: Cryptography Audit'}
                    </h3>
                    <button
                      onClick={() => downloadFile(`skill_${skill}.md`, skillSpecs[skill])}
                      className="px-3 py-1 bg-purple-600 hover:bg-purple-700 rounded text-sm flex items-center gap-2"
                    >
                      <Download size={14} />
                      Download
                    </button>
                  </div>
                  <pre className="text-xs overflow-x-auto whitespace-pre-wrap max-h-96 overflow-y-auto">
                    {skillSpecs[skill]}
                  </pre>
                </div>
              ))}
            </div>
          )}

          {activeTab === 'agents' && (
            <div className="space-y-6">
              <h2 className="text-2xl font-bold text-purple-400">Agent Specifications</h2>
              
              {['codeReviewer', 'dataAnalyst'].map((agent) => (
                <div key={agent} className="bg-slate-900 p-4 rounded border border-slate-700">
                  <div className="flex justify-between items-center mb-3">
                    <h3 className="text-xl font-semibold text-purple-300">
                      {agent === 'codeReviewer' && 'Agent: Code Reviewer'}
                      {agent === 'dataAnalyst' && 'Agent: Data Analyst'}
                    </h3>
                    <button
                      onClick={() => downloadFile(`agent_${agent}.md`, agentSpecs[agent])}
                      className="px-3 py-1 bg-purple-600 hover:bg-purple-700 rounded text-sm flex items-center gap-2"
                    >
                      <Download size={14} />
                      Download
                    </button>
                  </div>
                  <pre className="text-xs overflow-x-auto whitespace-pre-wrap max-h-96 overflow-y-auto">
                    {agentSpecs[agent]}
                  </pre>
                </div>
              ))}

              <div className="bg-slate-900 p-4 rounded border border-purple-500">
                <div className="flex justify-between items-center mb-3">
                  <h3 className="text-xl font-semibold text-purple-300">Multi-Agent Orchestration</h3>
                  <button
                    onClick={() => downloadFile('multi_agent_architecture.md', multiAgentArchitecture)}
                    className="px-3 py-1 bg-purple-600 hover:bg-purple-700 rounded text-sm flex items-center gap-2"
                  >
                    <Download size={14} />
                    Download
                  </button>
                </div>
                <pre className="text-xs overflow-x-auto whitespace-pre-wrap max-h-96 overflow-y-auto">
                  {multiAgentArchitecture}
                </pre>
              </div>
            </div>
          )}
        </div>

        {/* Footer */}
        <div className="mt-8 text-center text-slate-400 text-sm">
          <p>Complete assignment with all required components for GitHub submission</p>
          <p className="mt-2">AI Systems & Agentic Workflows • January 2026</p>
        </div>
      </div>
    </div>
  );
};

export default ClaudeAssignment;
