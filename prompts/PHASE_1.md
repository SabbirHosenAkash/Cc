# PHASE 1 — CORE AI FOUNDATION
## Google AI Studio execution prompt

You are the senior Android architect and implementation engineer for this project. Read the complete `MASTER_SPECIFICATION.md` before doing anything. The Master Specification is authoritative. This file defines the Phase 1 execution procedure.

## 1. Mission and scope
Implement Phase 1 only: a stable Android Personal AI Engine with local GGUF inference, model management, chat, persistent conversation history, persistent memory, feedback/personalization foundation, and robust performance/error handling.

Do not implement Phase 2 voice/search/document features or Phase 3 PRILINA integration in this phase. Do not remove or redesign unrelated working features already present in the supplied project.

## 2. Inspect before editing — mandatory
1. Inventory every file and module in the supplied source ZIP/repository.
2. Identify language, UI framework, min/target SDK, Gradle/AGP/Kotlin versions, architecture, database, navigation, permissions, native libraries, build variants and current build status.
3. Read existing code paths for chat, model loading, inference, storage and settings before changing them.
4. Build the untouched project first when possible. Record baseline errors separately from errors introduced by your changes.
5. Create a concise architecture map and an existing-feature preservation checklist.
6. If the source ZIP is missing, incomplete, corrupt, or not actually accessible, stop and request it. Do not fabricate a replacement project or pretend to have inspected source.

## 3. Preserve existing work
- Keep all currently working screens, flows, settings, assets, branding, package/application ID, signing configuration and features unless a change is essential and approved.
- Prefer minimal, backward-compatible changes.
- Do not replace the entire app with a new demo or template.
- Do not delete files or dependencies merely because they appear unused; verify references first.
- Keep a change log listing each modified/added/deleted file and the reason.
- Never overwrite user data during migrations. Provide safe database migrations and fallback behavior.

## 4. Local inference architecture
Use llama.cpp with GGUF where compatible with the supplied Android project. First inspect the existing llama.cpp integration; reuse and repair it rather than adding a duplicate engine.

Create or preserve a model-independent inference interface so the UI does not depend on Qwen-specific code. Support compatible GGUF models from Qwen, Llama, Mistral, Gemma and other families, subject to tokenizer/template/runtime compatibility.

Required behavior:
- Import/select a local GGUF file using Android's Storage Access Framework; do not require broad storage permission without need.
- Validate file access, readability, extension and basic metadata. Do not assume extension alone proves a valid model.
- Show model name/path or user-friendly location, file size, supported status, load state and useful errors.
- Load and unload models safely; prevent duplicate concurrent loads.
- Show clear states: idle, validating, loading, ready, generating, stopping, completed and failed.
- Stream tokens or partial output if supported by the current engine.
- Stop generation promptly when requested and release resources safely.
- Handle invalid model, unsupported architecture, missing tokenizer/template, out-of-memory, native crash and cancellation without leaving the UI stuck.
- Keep model loading/inference off the main/UI thread.
- Do not claim every GGUF file is supported. Report tested model, quantization, context size, runtime version and device results.
- Avoid downloading model weights automatically or sending model files to a server.

## 5. Memory and performance
The initial target described in the Master Specification is an Android phone with approximately 8 GB physical RAM. Verify the actual device model, Android version, ABI, available RAM and free storage where possible; do not assume a 256 GB storage capacity or that all physical RAM is available to the app.

Implement practical controls where technically supported:
- Model/context/generation settings with safe defaults.
- A conservative memory/performance profile and an optional higher-performance profile.
- Clear warning before selecting settings likely to exceed available memory.
- Monitor available memory using supported Android APIs.
- Release model/context/native resources on unload and relevant lifecycle events.
- Avoid loading multiple large models simultaneously.
- Handle backgrounding, activity recreation and process death safely.
- Explain that storage cannot simply replace RAM for active inference. Memory mapping/offloading may reduce pressure in some configurations but is not equivalent to RAM and must be measured.

Do not invent a RAM slider that does not control real engine parameters. Label unsupported controls as unavailable rather than decorative.

## 6. Chat and conversation history
Implement or preserve:
- Send/receive text messages.
- Distinct user and assistant message presentation.
- Streaming/generation status and stop button.
- New conversation, rename, delete and conversation list.
- Persistent history after app restart.
- Copy message and sensible long-message rendering.
- Error handling that preserves the user's message and existing history.
- Prevent duplicate submissions and overlapping generation unless explicitly supported.
- Empty, loading, error and no-model-selected states.
- Clear distinction between a model response and system/application errors.

Persist data using the project's existing database/storage approach unless there is a strong technical reason to migrate. If a migration is needed, explain it and preserve existing records.

## 7. Persistent memory and personalization foundation
Build a transparent, user-controllable memory layer separate from raw chat history and separate from model-weight training.

Required:
- Store only useful information that is appropriate to retain.
- Support memory categories described in the Master Specification.
- Retrieve only relevant memories for a conversation.
- Provide a memory screen or equivalent controls to inspect, edit and delete stored memories.
- Allow the user to disable memory and clear selected/all memory.
- Avoid storing credentials, secrets or sensitive data unnecessarily.
- Do not silently infer or save uncertain personal facts.
- Provide feedback controls (helpful/not helpful or equivalent) and store preference signals where appropriate.
- Apply feedback through retrieval/prompt personalization, not by claiming the model has been retrained.

Document the memory schema, retention behavior, retrieval strategy and migration plan.

## 8. Privacy and security
- Keep inference local for the local-model path.
- Do not upload conversations, memories or model files.
- Use least-privilege Android permissions.
- Use safe file handling and validate imported paths/content.
- Do not log private message bodies or secrets.
- Protect any stored tokens if the project has them.
- Make data deletion behavior clear.
- Do not introduce a network service or public endpoint in Phase 1.

## 9. Testing — evidence required
Run and report, where available:
1. Baseline and final Gradle build.
2. Unit tests for model state, persistence, memory and relevant logic.
3. Integration tests for model selection/loading and chat flow.
4. Lint/static analysis.
5. Regression checks for every existing feature identified during inspection.
6. APK installation/build validation where tooling permits.
7. Device testing only if an actual device/emulator is available.

At minimum, verify:
- A known compatible GGUF model loads.
- A simple prompt returns a coherent answer.
- A second prompt works without restarting the app.
- Stop generation works.
- Invalid model produces a recoverable error.
- Chat history survives app restart.
- Memory can be saved, retrieved, edited and deleted.
- No-model and low-memory states do not freeze the app.

For every test mark exactly one: PASS (executed successfully), FAIL, NOT RUN, BLOCKED, or DEVICE CHECK REQUIRED. Include command, result and relevant logs. Never mark an unexecuted test as passed.

## 10. Build and deliverables
After fixing failures, create:
- A genuine installable APK, clearly labelled debug or release, only if Gradle build succeeds.
- Complete source ZIP containing the whole buildable project, Gradle wrapper/configuration, resources and tests. Exclude machine-specific caches and secrets.
- Updated Master Specification with actual implementation status and known limitations.
- Phase 1 test and handover report.
- Combined deliverables ZIP if practical.

Verify every file exists and is non-empty. Verify the APK is the actual build output and the source ZIP contains the complete project. Provide separate download links. If a build or export is blocked by the environment, state that precisely and provide the available source/report; never fabricate APKs, test logs, screenshots or links.

## 11. Completion gate
Do not declare Phase 1 complete until all acceptance criteria in the Master Specification are met or each remaining blocker is explicitly documented and accepted. Do not begin Phase 2 automatically.

## 12. Final response format
Report:
- What was inspected.
- What changed and why.
- Existing features preserved.
- Implemented features.
- Tests actually run and exact outcomes.
- Build status and APK type.
- Known issues/blockers.
- Device verification still required.
- Separate verified artifact links.
- Updated current phase and next recommended step.

Be truthful, conservative and evidence-driven. A polished UI is not proof of working inference. A successful build is not proof that every runtime feature works.

## Mandatory File Explorer APK Replacement and Project Handover

The user's required delivery location is the active Google AI Studio project's own File Explorer/workspace file tree—not a download link as the primary delivery method. At the end of every completed phase, repair, or code update:

1. Keep the complete, updated, buildable project in the active workspace/File Explorer, preserving the full project structure and all files needed for the next phase.
2. Build the APK from that exact updated project. Do not use a stale APK, placeholder, renamed ZIP, or APK from an earlier build.
3. When the environment permits writing/copying build outputs into the File Explorer, place the verified APK there beside or inside a clearly named deliverables folder. Use one stable filename for the current APK (for example, `PRILINA-latest.apk`) and make the latest verified build easy to identify.
4. Replace the previous APK in the File Explorer with the new APK only AFTER the new APK has been built successfully and verified as a genuine, non-empty APK. Remove/overwrite the old APK so there is only one file presented as the current APK; do not leave multiple ambiguous files named latest/current. Never delete the previous known-good APK before the replacement is verified. If the new build fails, keep the previous APK but clearly mark it as OLD / NOT CURRENT and report the build failure; do not pretend it was replaced.
5. Keep a complete source archive as a separate deliverable when archive creation is supported, but the live, complete project must remain in the workspace for the next phase. Do not replace the project tree with only an APK or ZIP.
6. Verify and report the actual workspace/File Explorer paths and filenames, file sizes, APK package/application identity where available, build variant (debug/release), build result, and tests. Confirm that the APK shown in File Explorer is the exact output of the latest successful build.
7. If Google AI Studio's current environment does not expose a writable File Explorer, cannot copy build outputs there, or cannot run the Android build, do not claim success or invent a file. State the precise limitation, preserve the complete source project, and provide the closest genuinely supported artifact/export route available in that environment. Ask for a user action only when the environment requires it.
8. Do not finish the phase/update until the workspace contents and handover status have been checked. Clearly distinguish: (a) source updated, (b) build succeeded, (c) APK copied/replaced in File Explorer, and (d) physical-device installation tested. These are separate statuses.
