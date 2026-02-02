# TM-AI-02: Agentic AI with Tool Execution

## Overview
This threat model covers an agentic AI system where a Large Language Model
can select and invoke tools that perform real-world actions.

Unlike RAG systems, agentic systems introduce:
- autonomous planning
- tool invocation
- stateful execution
- side effects

This significantly increases security risk.

## Architecture Pattern
- User-facing application
- Agent orchestrator controlling planning and execution
- LLM used for reasoning and decision support
- Tools executed only via policy-guarded interfaces

## Primary Risks
- Unauthorized actions triggered by model output
- Privilege escalation via tools
- Confused-deputy attacks
- Prompt and context manipulation leading to real-world impact

## Out of Scope
- Model training security
- Autonomous self-modifying agents
- Hardware-level attacks
