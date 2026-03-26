# Agent Team Builder

A meta-agent system for Claude Code that creates specialized AI agents through deep domain research and multi-lens quality review. Unlike template-based agent generators, this system researches the target domain before designing agents -- producing agents with real expertise, not generic instructions.

## Why this exists

Most agent builders generate agents from templates or brief prompts. The result is generic agents that lack domain depth. Agent Team Builder takes a different approach:

- **Researches before designing.** The architect agent runs 10-15 web searches, reads 8-10 sources, and extracts domain-specific competencies before writing a single line of the agent definition.
- **Reconnaissance before asking.** A quick domain scan happens before user questions, so the system asks informed, domain-specific questions instead of generic ones.
- **Reviews before shipping.** A dedicated reviewer agent evaluates every proposal through 7 independent lenses, catching overlap, missing interfaces, unrealistic workflows, and problem-solution misfit.
- **Creates agents that ask before acting.** Every agent produced includes a domain-specific clarification step -- they never start working blind.

## How it works

Two agents collaborate in a structured pipeline:

```
User request
    |
    v
[agent-architect]
    |-- STEP 0: Reads existing agent ecosystem
    |-- STEP 1: Quick domain reconnaissance (2-3 searches)
    |-- STEP 2: Asks informed, domain-specific questions
    |-- STEP 3: Deep research (10-15 sources per domain)
    |-- STEP 4: Extracts competencies from sources
    |-- STEP 5: Designs agent(s) with full spec
    |-- STEP 6: Sends proposal to reviewer
    |           |
    |           v
    |   [team-builder]
    |       |-- Reads ecosystem + researches real-world domain workflows
    |       |-- Evaluates through 7 lenses
    |       |-- Returns structured feedback
    |           |
    |           v
    |-- STEP 7: Incorporates feedback, creates files
    |-- STEP 8: Delivers summary
    v
Agent files in ~/.claude/agents/
```

### Single and batch mode

Create one agent or an entire coordinated team in a single session:

- **Single mode:** "Create a technical writing agent"
- **Batch mode:** "Build me a team of 3 agents for my sales proposal workflow"

In batch mode, the system cross-checks between new agents, builds a responsibility table, maps inter-agent interfaces, and validates that the division into N agents (vs N-1 or N+1) is justified.

### The 7 review lenses

Every proposal is evaluated through:

| Lens | What it checks |
|------|---------------|
| 1. Overlap | Competency conflicts with existing agents (and between new agents in batch) |
| 2. Interfaces | Connection quality, handoff clarity, missing implicit interfaces |
| 3. Skill granularity | Whether skills are truly atomic and reusable |
| 4. Ecosystem balance | Domain bias, solo vs team ratio, user cognitive load |
| 5. Problem-solution fit | Whether agents address the user's actual pain points and workflow |
| 6. Workflow realism | Whether agent orchestration mirrors real-world domain workflows |
| 7. Structural quality | Format compliance, tool references, checklist verifiability |

### What makes the output different

Every agent created by this system includes:

- An identity statement (who the agent is, not what it does)
- 3-5 core philosophy principles
- A strict-order process with tool-specific instructions
- A domain-specific clarification step (asks before acting)
- A verifiable quality checklist
- Clear boundaries (what the agent does NOT do)
- 2-4 optional atomic skills

## Installation

Copy both agents to your Claude Code agents directory:

```bash
git clone https://github.com/klausners/agent-team-builder.git
cp agent-team-builder/agents/*.md ~/.claude/agents/
```

## Usage

In Claude Code, ask to create an agent or a team:

```
"Build me an agent for technical writing"
"I need a data engineering specialist agent"
"Create 3 agents to cover my content marketing workflow"
"Design a team that helps me build sales proposals"
```

Claude Code will automatically set up the architect + reviewer team and run the full pipeline.

## Requirements

- Claude Code with Opus model access
- Internet access (for domain research via WebSearch/WebFetch)

## Comparison with other approaches

| Feature | Agent Team Builder | AutoAgent | Meta-Agent | Strands Agent Builder |
|---------|-------------------|-----------|------------|----------------------|
| Domain research before design | 10-15 sources | No | No | No |
| Reconnaissance before questions | Yes | No | No | No |
| Independent quality review | 7 lenses | No | Optimization loop | No |
| Batch/team creation | Yes, coordinated | Yes | Yes (FSM) | No |
| Real-world workflow validation | Yes | No | No | No |
| Created agents ask before acting | Yes, domain-specific | No | No | No |
| Platform | Claude Code | Python/API | Python/API | CLI |

## Structure

```
agents/
  agent-architect.md   # Researches domains, designs agents (single or batch)
  team-builder.md      # Reviews proposals through 7 lenses, validates workflow realism
```

## License

MIT
