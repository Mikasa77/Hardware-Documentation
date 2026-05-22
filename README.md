# Hardware Documentation

AI-consumable hardware reference documentation. Every claim in this repository reflects something observed or confirmed on physical hardware — not vendor datasheets taken on faith.

This repository documents hardware for my own projects. It is published in case others find it useful, but comes with no guarantees of accuracy, completeness, or fitness for any purpose. Use at your own risk.

## Purpose

This repository exists to give AI coding agents accurate, verified hardware context at the start of a project. Paste the relevant document into agent context before writing any hardware-specific code.

## Structure

```
Hardware Documentation/
└── ESP32-P4/
    └── JC8012P4A1C/
        └── JC8012P4A1C.md    # Guition 10.1" ESP32-P4 board — full hardware reference
```

## Conventions

- **Confirmed** — observed on physical hardware (boot log, runtime probe, oscilloscope, etc.)
- **From vendor** — sourced from vendor demo sdkconfig, BSP, or schematic; not independently verified
- **TBD** — not yet determined; treat as unknown
- All GPIO numbers are ESP32-P4 GPIO numbers unless stated otherwise
- IDF version in use is noted per-document; API calls are version-specific

## How to use

Find the document for your target board and paste it into context. The document is self-contained: it includes pin assignments, confirmed sdkconfig settings, required IDF patches, known issues, and working code patterns. No other context is needed to start a project targeting that board.

## Boards

| Board | SoC | Doc |
|---|---|---|
| Guition JC8012P4A1C | ESP32-P4 + ESP32-C6 | [ESP32-P4/JC8012P4A1C/](ESP32-P4/JC8012P4A1C/) |
