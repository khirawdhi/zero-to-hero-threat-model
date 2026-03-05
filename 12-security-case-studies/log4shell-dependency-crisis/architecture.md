# Architecture

The vulnerability appeared in applications using the Log4j library within their software stack.

A simplified vulnerable architecture:

User
   ↓
Web Application
   ↓
Logging Library (Log4j)
   ↓
JNDI Lookup
   ↓
External Server
   ↓
Malicious Code Execution

## Components

| Component | Description |
|---|---|
| User | External actor interacting with the application |
| Web Application | Application processing user input |
| Logging Library | Log4j logging component |
| JNDI Lookup | Mechanism allowing external resource loading |
| External Server | Attacker-controlled server hosting malicious payload |

## Trust Boundaries

| Boundary | Description |
|---|---|
| User Input Boundary | External input entering application |
| Application Boundary | Application processing user requests |
| External Resource Boundary | External server interaction |
