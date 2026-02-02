# TM-AI-01: Retrieval-Augmented Generation (RAG) Application

## Overview
This threat model covers a cloud-native AI application using a
Retrieval-Augmented Generation (RAG) pattern.

The system combines:
- User prompts
- Retrieved contextual data
- Large Language Model (LLM) inference

to generate responses.

## Architecture Pattern
- User-facing application
- Retrieval layer backed by vector search
- External or hosted LLM
- Orchestration logic controlling prompts and tools

## Goals
- Identify AI-specific threat vectors beyond traditional cloud risks
- Model trust boundaries involving prompts, retrieval, and model outputs
- Define security controls for safe and reliable AI system operation

## Out of Scope
- LLM training pipeline security
- Model weight theft
- Hardware-level attacks
