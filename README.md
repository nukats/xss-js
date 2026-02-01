# SKILL: Reverse Engineering & Vulnerability Research

| field        | value                                  |
|--------------|----------------------------------------|
| skill_id     | re-vuln-research                       |
| category     | Reverse Engineering, Vulnerability R&D |
| difficulty   | Advanced                               |
| timebox      | 2–8 hours per target                   |
| focus        | Native, firmware, and app binaries     |

## Purpose

Systematically reverse engineer binaries and components to discover and validate security vulnerabilities, focusing on memory‑safety issues, logic bugs, and exploit‑relevant behaviors. [web:1][web:7]

## Prerequisites

- Strong OS fundamentals (process, memory, syscalls, file formats).
- Proficiency in at least C/C++ and one scripting language (Python preferred).
- Familiarity with exploitation primitives (stack/heap, info‑leaks, ROP, gadgets, chains). [web:5][web:8]

## Required Skills

- Static analysis: disassembly, decompilation, control‑flow and data‑flow reasoning. [web:1][web:7]
- Dynamic analysis: debugging, tracing, instrumentation, coverage‑guided exploration.
- Protocol and file‑format reverse engineering.
- Fuzzing design and triage workflow.
- Vulnerability pattern recognition (UAF, OOB, TOCTOU, race conditions, authZ logic bugs).
- Report writing with PoC and exploitability assessment. [web:3][web:5]

## Tooling Baseline

- Disassemblers/decompilers: IDA / Ghidra / Binary Ninja.
- Debuggers: gdb/lldb, WinDbg, rr, debugger plugins.
- Instrumentation: Frida, DynamoRIO, Intel PIN, sanitizers.
- Fuzzers: AFL++, libFuzzer, honggfuzz, custom harnesses.
- Supplementary: radare2, binwalk/firmware‑mod‑kit (for firmware), network/file analyzers. [web:1][web:6]

## Workflow

1. Scoping and Recon
   - Identify target binary, environment, and threat model.
   - Collect all available inputs (samples, configs, PCAPs, firmware images, symbols, communication and network stack, ie. Network/Web Interfaces and communication protocols). [web:1][web:3]

2. Triage and Surface Mapping
   - Classify binary type, architecture, protections (RELRO, NX, PIE, canaries).
   - Map entry points: exported APIs, IPC, RPC, network handlers, parsers, syscalls.
   - Document trust boundaries and untrusted inputs.

3. Static Reverse Engineering
   - Load into disassembler and normalize: rename functions, annotate types, group subsystems.
   - Recover high‑level logic and data structures for input parsing and privileged operations.
   - Identify suspicious patterns and sinks (memcpy‑like calls, deserialization, crypto misuse). [web:1][web:7]

4. Dynamic Analysis
   - Set up a controlled environment (VM, container, emulator, or hardware lab).
   - Attach debugger, collect traces, and observe behavior for representative inputs.
   - Use hooks/instrumentation to monitor critical functions and state transitions.

5. Fuzzing and Input Generation
   - Design harnesses around parsers, protocol handlers, and complex state machines.
   - Run coverage‑guided fuzzing at scale; refine dictionaries and corpus. [web:3][web:6]
   - Minimize and deduplicate crashes; persist and tag interesting inputs.

6. Crash Triage and Root Cause
   - Reproduce crashes under debugger with sanitizers if possible.
   - Localize root cause, characterize bug class, and evaluate exploitability (control of PC, heap feng‑shui feasibility, sandbox/mitigation impact). [web:5][web:8]

7. Vulnerability Documentation
   - Write structured notes:
     - Affected components, version, configuration.
     - Detailed root cause analysis and control‑flow/data‑flow explanation.
     - Reliable repro steps and minimal PoC.
     - Impact assessment, constraints, and potential mitigations. [web:3][web:9]

8. Hardening & Knowledge Capture
   - Extract recurring anti‑patterns and add them to internal checklists.
   - Propose code‑level fixes, tests, and fuzzing harnesses for regression prevention.
   - Update SKILL.md with new techniques or tools as they prove effective. [web:3][web:6]

## Deliverables

- Annotated project (IDA/Ghidra/BN database or equivalent).
- Textual analysis report with vulnerability details and PoCs.
- Fuzzing artifacts (harness code, corpus, crash samples, logs).
- Recommendations for remediation and long‑term hardening.

## Quality Criteria

- All crashes and suspicious behaviors are triaged with clear root cause or explicitly marked unknown.
- Analysis is reproducible from notes, artifacts, and environment description.
- Findings are prioritized by realistic exploitability and impact, not just presence of a crash. [web:5][web:8]

## Safety & Ethics

- Only test on authorized targets and environments.
- Minimize collateral impact; isolate testing infrastructure.
- Follow coordinated disclosure and relevant program policies. [web:3][web:9]
