# PHASE 3 — SECURE PRILINA INTEGRATION
## Google AI Studio execution prompt

Read the latest Master Specification, the complete latest Personal AI Engine source ZIP, its handover report, and the complete current PRILINA source ZIP. Implement Phase 3 only. PRILINA and the Personal AI Engine remain separate applications unless the user explicitly approves a different architecture.

## 1. Preflight — inspect both projects
- Inventory both complete projects and identify package IDs, SDK levels, languages, architectures, storage, networking, background execution and existing assistant/action flows.
- Build and test both projects before changes when possible.
- Map PRILINA's current chat, voice, command, automation, permission and settings flows.
- Identify the Personal AI Engine's supported request/response interface.
- Record baseline failures and create a feature-preservation checklist for both apps.
- If either complete source project is missing, stop and request it. Never invent unseen APIs or reconstruct either project from assumptions.

## 2. Non-negotiable preservation
- Keep PRILINA's existing features, UI, branding, voice behavior, commands, automations and data.
- Keep the Personal AI Engine's local inference, model manager, chat, memory, voice and knowledge features.
- Do not merge the projects into one app or replace PRILINA's existing agent.
- Make the smallest modular changes needed for communication.
- Do not remove a feature because it is difficult to integrate; report incompatibility and propose a safe adapter.

## 3. Choose and document the communication method
Evaluate Android-supported options such as bound service/AIDL, explicit intents with signature-level permissions, or a loopback-only local HTTP interface. Choose based on the actual project architecture, minimum SDK, reliability and security.

Requirements:
- Do not bind a service or HTTP listener to all network interfaces.
- Never expose an unauthenticated API to the public internet or local network.
- Authenticate/authorize the calling application using platform-supported identity/permission mechanisms where possible.
- Validate all request fields, payload sizes and message types.
- Use request IDs, timeouts, cancellation and bounded queues.
- Define versioned API contract and compatibility behavior.
- Avoid leaking conversation data, memories, model paths or secrets in logs.
- Handle engine unavailable, app process stopped, permission denied, timeout, malformed response and user cancellation.
- Ask before sharing user data between the two apps if the existing consent model does not clearly cover it.

## 4. API contract
Document:
- Request/response schema and version.
- Supported operations (at minimum submit user message and receive assistant response).
- Optional conversation/session identifier.
- Whether memory context is used and how user consent applies.
- Streaming vs complete-response behavior.
- Cancellation semantics.
- Error codes and retry policy.
- Authentication/authorization.
- Data retention and deletion expectations.

Do not expose arbitrary shell, file-system, device-control or unrestricted automation operations through the AI endpoint. PRILINA remains responsible for validating and executing its own actions under its existing permission and safety model.

## 5. User experience
- Preserve PRILINA's current chat and voice interface.
- Add a clear option to use the Personal AI Engine where appropriate.
- Indicate connection state and which engine is responding.
- Provide fallback to existing PRILINA behavior when the engine is unavailable, if safe and consistent with existing design.
- Prevent duplicate replies and loops.
- Preserve conversation continuity only according to the documented consent and session rules.
- Do not silently route private conversations to a remote service.

## 6. Reliability and security testing
Test:
- Successful request/response between the two installed apps.
- Unauthorized caller rejection.
- Malformed/oversized payload rejection.
- Timeout and cancellation.
- Engine app not installed, stopped or unavailable.
- Reconnect and repeated requests.
- Process death and lifecycle transitions.
- No duplicate messages or feedback loops.
- No regression in PRILINA voice, chat, commands and automations.
- No regression in Personal AI Engine model loading, chat, memory, voice and documents.
- Data is not transmitted outside the intended local channel.

Run unit/integration/security checks, lint and Gradle builds for both apps. Physical-device tests must be identified separately from emulator or mocked tests.

## 7. Deliverables
Provide, separately and only if actually produced:
- Personal AI Engine APK and complete source ZIP.
- Updated PRILINA APK and complete source ZIP, if PRILINA was modified.
- Updated Master Specification.
- Versioned API contract document.
- Integration and security test report.
- Combined deliverables ZIP if practical.

Verify each artifact exists and is non-empty. Verify APKs are genuine build outputs and source ZIPs are complete. Never fabricate APKs, test evidence or download links. Clearly identify debug/release builds and any signing limitations.

## 8. Completion gate
Do not declare integration complete until end-to-end communication and regression/security checks pass, or blockers are explicitly documented. Do not publish, release or distribute either app without the user's explicit instruction.

## 9. Final handover
Report both project architectures, exact files changed, preserved features, API/security decisions, tests and evidence, build results, known limitations, device checks still needed, and verified artifact links.