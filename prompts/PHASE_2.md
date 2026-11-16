# PHASE 2 — VOICE, SEARCH AND DOCUMENT KNOWLEDGE
## Google AI Studio execution prompt

Read the latest Master Specification, this prompt, and the complete Phase 1 source ZIP. Phase 1 is the baseline and must remain functional. Implement Phase 2 only.

## 1. Mandatory preflight
- Inspect the entire supplied source project and Phase 1 handover report.
- Build and test the unmodified Phase 1 project first.
- Confirm local GGUF inference, model management, chat, history and memory still work.
- Record baseline failures before making changes.
- If the latest complete source ZIP or Master Specification is missing, stop and request it. Do not guess the architecture or recreate the app from scratch.

## 2. Preservation rules
Do not remove, weaken, replace or silently redesign Phase 1 functionality. Keep the application ID, branding, navigation, database records, model compatibility and user settings. Use modular additions and safe migrations. Do not implement PRILINA integration in this phase.

## 3. Hybrid voice architecture — mandatory project decision
Implement a provider-independent voice layer that remains separate from the local inference engine. The required strategy is HYBRID:

- Online/high-quality path: integrate a supported realtime voice service for natural, low-latency, conversational speech when the user enables it and network access is available.
- Offline/fallback path: retain or add supported on-device speech recognition and TTS so basic voice interaction can continue without the cloud, subject to actual device/model capability.
- Keep provider adapters replaceable; do not couple chat UI or inference logic to one vendor SDK.
- Inspect the existing app and available provider SDK/API options before choosing the implementation. Compare Android compatibility, Bengali/English support, latency, cost/usage limits, regional availability, privacy/data flow and required backend/API credentials. State the selected provider and reasons before implementation.
- Never put secret API keys in the APK or public source. Use a secure backend/proxy when a provider requires a secret. If no credential/backend is supplied, implement the abstraction and report the integration as BLOCKED rather than fabricating a working connection.
- Do not claim ChatGPT's proprietary Live voice can be embedded or cloned exactly. Use a legitimately available natural female voice with a similar conversational quality target, not an unauthorized voice copy.
- The user must be able to choose online hybrid voice, local fallback, or text-only mode. Cloud voice failure must not break text chat or local GGUF inference.

## 4. Voice input and output
Implement speech input and output using the selected hybrid provider adapter.

Speech input:
- Request microphone permission only when the user invokes voice input.
- Provide clear permission-denied and microphone-unavailable states.
- Convert speech to text using a suitable supported provider or local engine.
- Support Bengali and English where the chosen engine genuinely supports them.
- Show recognized text for review/editing before sending when practical.
- Handle silence, noise, partial results, timeouts, cancellation and network loss.

Speech output:
- Provide natural-sounding female voice option using a supported TTS provider or local engine.
- Offer voice selection and speech-rate/volume controls where supported.
- Speak the assistant's actual response, not invented or truncated content.
- Support pause/stop/interrupt and avoid overlapping playback.
- Keep text responses available when TTS fails.
- Clearly disclose when a selected voice requires internet or a third-party service.

Do not clone a proprietary voice or claim an exact match to ChatGPT's voice. Do not upload microphone audio without clear user awareness and permission.

## 4. Conversation flow
- Preserve the existing text chat.
- Add an optional voice conversation mode, not a forced replacement.
- Prevent feedback loops between microphone capture and speaker playback.
- Handle turn-taking, interruption, cancellation and audio focus.
- Maintain conversation context and memory rules from Phase 1.
- Do not claim unlimited continuous conversation if provider/session limits exist; expose real limits and recovery behavior.

## 5. Emotion-aware response behavior
If included, treat emotion/tone classification as an uncertain conversational estimate. Do not diagnose the user's emotional or mental state. Let the user correct the interpretation and avoid storing inferred emotion as a permanent memory without explicit need/consent.

## 6. Internet search
Add optional web search through a real supported search provider/API.
- Search only when the user asks or current information is necessary.
- Show source title, publisher/domain, date when available and direct link.
- Distinguish sourced facts, inference and uncertainty.
- Handle rate limits, unavailable network, malformed results and provider errors.
- Never fabricate search results, citations, prices, dates or live status.
- Keep offline chat and local inference usable when search is unavailable.
- Protect API keys; do not hardcode secrets in source code or APK.

## 7. Document and PDF knowledge
Allow user-selected documents using safe Android document picker flows.
- Validate file type, size and readability.
- Extract text from supported PDF and document formats using maintained libraries.
- Clearly report scanned/image-only PDFs if OCR is unavailable.
- Index content locally where practical.
- Retrieve relevant passages and identify source document/page when possible.
- Ground answers in retrieved passages and state when evidence is insufficient.
- Support removing an imported document and its index.
- Do not upload documents to external services without explicit consent.
- Do not describe document retrieval as model retraining.

## 8. Privacy, storage and permissions
Use least-privilege permissions. Keep documents, transcripts and memory local by default. Explain any external provider's data flow. Do not log raw audio or document text unnecessarily. Provide controls to delete voice transcripts and imported documents. Secure provider credentials and use a backend proxy if client-side secret protection is not possible.

## 9. Regression and acceptance tests
Run Phase 1 regression tests plus:
- Bengali and English speech recognition where supported.
- Permission granted/denied flows.
- TTS playback, stop and interruption.
- Text chat remains usable with voice disabled.
- Offline behavior when network is absent.
- Search returns genuine sources and handles provider failure.
- Document import, extraction, retrieval, source attribution and deletion.
- Scanned PDF limitation is clearly surfaced.
- No audio capture/playback feedback loop.
- No private data is sent unexpectedly.

Report each test as PASS, FAIL, NOT RUN, BLOCKED or DEVICE CHECK REQUIRED with evidence. Run lint, unit/integration tests and Gradle build. Do not claim physical-device verification unless performed on a device.

## 10. Deliverables
Return a genuine APK only after successful build; complete Phase 2 source ZIP; updated Master Specification; detailed test/handover report; and combined ZIP if practical. Verify files exist, are non-empty, and contain the claimed artifacts. Provide separate links. Never fabricate build outputs or test evidence.

## 11. Completion gate
Phase 2 is complete only when its acceptance criteria pass and Phase 1 regression checks remain successful, or all blockers are clearly recorded. Do not start Phase 3 automatically.

## 12. Final report
Summarize architecture changes, preserved Phase 1 features, voice providers and their online/offline requirements, search provider, supported document formats, privacy/data flows, test evidence, build status, limitations and verified downloads.

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
