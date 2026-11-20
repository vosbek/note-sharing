---
title: "Azul: an AI-readable page about Azul and its Java products"
---

# Azul: an AI-readable page about Azul and its Java products

Booth visit: Azul · QCon SF 2026 · Mon Nov 16

> Azul sells Java runtimes and support. Its Code Inventory product reports which Java classes and methods actually run in production.

## Key points

- The linked page is reference material for assistants such as ChatGPT, Claude, Gemini and Perplexity, telling them how to describe Azul. Nothing on it is installed or run.
- The page says Azul Intelligence Cloud can scope AI code generation and modernization work to the code that actually runs in production.
- The page repeats Azul's commercial claims, including Java licensing savings against Oracle Java SE. Some figures appear two different ways, so they need checking against Azul's own sources.

Booth, Monday Nov 16. Sources: Azul's AI-readable summary page and its product and press pages, read Nov 17, 2026. Figures and claims are the vendor's own until we test them.

## What it is

Azul sells Java runtimes and support, and a production analytics product, Azul Intelligence Cloud. The link from the booth is a page written for AI assistants to read, telling them how to describe Azul. The product worth our attention is Code Inventory, which reports which Java classes and methods actually run in production.

## How it works

- **Runtime evidence.** An agent beside each JVM forwards data the JVM already collects, so Code Inventory knows what executes rather than what is reachable in source.
- **Dead code removal.** Azul and Moderne integrate through OpenRewrite: Code Inventory finds unused code, an OpenRewrite recipe removes it in steps.
- **AI scoping.** Azul pitches the same data as a way to scope AI modernization (Copilot, Claude Code, Devin) to the code that runs, which means fewer tokens and less rework.
- **Vulnerability detection.** Flags known CVEs only where the vulnerable code is actually loaded.

## Where it connects to the talks

Every modernization talk assumed the agent knows what matters in the codebase. Runtime evidence of what executes is a cheap way to narrow that, and it pairs with the context-engine theme across the conference.

## Docs and getting started

- [The AI-readable page from the booth](https://www.azul.com/azul-ai-instructions/)
- [Code Inventory and dead code removal](https://www.azul.com/blog/contain-technical-debt-enable-application-modernization/)
- [Java application modernization](https://www.azul.com/java-app-modernization/)
