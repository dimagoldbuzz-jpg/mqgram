# CLAUDE.md — MQGram

This file provides guidance to AI assistants when working with code in this repository.

**MQGram** is a privacy-enhanced Telegram iOS client with anti-delete, ghost mode, device spoofing, voice morphing, and send delay features.

## Build
The app is built using Bazel. See `BUILD.md` for full compilation instructions.

## Code Style Guidelines
- **Naming**: PascalCase for types, camelCase for variables/methods
- **Imports**: Group and sort imports at the top of files
- **Error Handling**: Properly handle errors with appropriate redaction of sensitive data
- **Formatting**: Use standard Swift/Objective-C formatting and spacing
- **Types**: Prefer strong typing and explicit type annotations where needed
- **Documentation**: Document public APIs with comments

## Project Structure
- Core launch and application extensions code is in `Telegram/` directory
- Most code is organized into libraries in `submodules/`
- MQGram-specific settings: `submodules/SettingsUI/Sources/MQGramSettingsController.swift`
- Anti-delete logic: `submodules/TelegramCore/Sources/AntiDelete/`
- External code is located in `third-party/`
- No tests are used at the moment

## MQGram Custom Modules
- **AntiDelete** — intercepts message deletions and stores originals locally
- **GhostMode** — suppresses read receipts, typing, and online indicators
- **DeviceSpoof** — masks device metadata sent to Telegram servers
- **VoiceMorpher** — real-time voice effects for voice messages
- **SendDelay** — configurable send delay with undo capability
- **EditHistory** — tracks and displays message edit history