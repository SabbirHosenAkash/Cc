PERSONAL AI ENGINE

MASTER PROJECT SPECIFICATION

Version: 1.3
Project Type: Android Personal AI Assistant
Development Strategy: Local-first, modular, future server-ready
Primary Integration Target: PRILINA Autonomous AI Agent

---

1. PROJECT VISION

Build a powerful personal AI application that initially runs directly on an Android phone, using local AI models wherever practical.

The application must act as the user's personal intelligence engine.

It should support natural conversations, long-term memory, personalized responses, voice interaction, document knowledge retrieval, internet search and future integration with PRILINA.

The application and PRILINA must remain separate projects.

The Personal AI Engine will provide intelligence. PRILINA will remain responsible for its existing assistant, automation and action-related capabilities.

Do not merge the two applications prematurely.

2. CORE DEVELOPMENT PRINCIPLES

1. Preserve all existing working functionality.
2. Use modular architecture.
3. Prefer offline/local processing when practical.
4. Avoid unnecessary dependencies.
5. Keep the application lightweight and responsive.
6. Design the architecture so that it can migrate to a server in the future.
7. Do not remove existing features without explicit approval.
8. Never claim a feature works without testing it.
9. Fix discovered bugs before moving to the next phase.
10. Keep the Master Specification updated after every phase.

3. TARGET DEVICE AND PERFORMANCE

Initial target environment:

- Android smartphone; verify the actual device model, Android version, ABI, available RAM and free storage from supplied project/device evidence.
- Design initially for a phone with approximately 8 GB physical RAM, but do not assume all RAM is available to the app.
- Do not assume 256 GB storage; treat storage capacity as unknown until verified.
- Local GGUF model support.
- Offline operation for supported features.

Performance requirements:

- Use appropriately quantized models.
- Avoid loading multiple large models simultaneously.
- Provide model selection and model management.
- Monitor memory consumption where possible.
- Provide practical performance settings.
- Handle insufficient memory gracefully.
- Avoid freezing or crashing during inference.
- Provide clear loading, generating, completed and error states.

Do not promise that every large model will run on the target phone.

Measure actual performance and document model limitations.

4. AI ENGINE AND MODEL ARCHITECTURE

Use a modular AI engine.

Preferred initial inference technology: llama.cpp with GGUF model support, provided it is compatible with the Android project and target device.

The architecture should not be restricted to one specific model.

Plan for future support of compatible model families, including:

- Qwen
- Llama
- Mistral
- Gemma
- Other compatible GGUF models

Required capabilities:

- Load and unload models.
- Display model information.
- Select an active model.
- Handle model loading errors.
- Handle unsupported model files.
- Provide generation progress.
- Support configurable context and generation settings.
- Stop generation when requested.
- Handle long responses safely.

Keep the inference engine separate from the chat interface.

5. CHAT AND CONVERSATION SYSTEM

Create a clean, modern chat interface.

Required features:

- Send and receive messages.
- Display AI responses clearly.
- Conversation history.
- Create new conversations.
- Rename and delete conversations.
- Preserve conversations after app restart.
- Copy messages.
- Support long responses.
- Show generation status.
- Stop ongoing generation.
- Handle errors without losing existing messages.

The chat experience should feel smooth and natural.

6. LONG-TERM MEMORY

The AI must have a persistent memory system.

Memory categories should include:

- User preferences.
- Important information explicitly shared by the user.
- Conversation context.
- Ongoing projects.
- Frequently used instructions.
- Useful facts learned from user feedback.

Required controls:

- View saved memories.
- Edit memories.
- Delete memories.
- Clear selected memory categories.
- Control what information is retained.

Do not store sensitive information unnecessarily.

Memory retrieval must be relevant to the current conversation.

The AI must not pretend to remember information that it cannot retrieve.

7. PERSONALIZATION AND LEARNING FOUNDATION

The system should improve its responses based on user feedback.

Required foundation:

- Positive and negative feedback.
- Response preference tracking.
- Learning from user corrections.
- Improved retrieval of relevant memories.
- Personalized response behavior.

Important distinction:

Memory and feedback-based personalization are not the same as training model weights.

Do not claim the model has been retrained merely because memory has been updated.

Future versions may support LoRA or other fine-tuning methods, potentially using external hardware.

8. PHASE 2 CAPABILITIES

The following features are planned for Phase 2.

8.1 Voice Interaction

Support speech input and spoken responses.

Requirements:

- Speech-to-text.
- Text-to-speech.
- Natural conversation flow.
- Bengali and English support where available.
- Voice selection.
- Adjustable speech settings.
- Ability to interrupt speech.
- Proper handling of microphone and audio permissions.

8.2 Natural Female Voice and Hybrid Voice Architecture

Provide a natural, pleasant female voice option with conversational pacing, expressive prosody and low-latency turn-taking.

Use a hybrid architecture: a supported cloud/realtime voice service may provide the highest-quality natural conversation when the user enables internet-based voice; a local/on-device speech input and TTS fallback should remain available where technically supported. Keep the voice provider behind a replaceable interface so the app is not locked to one vendor.

Before selecting a provider, inspect the current app architecture, supported SDK/API access, pricing/usage limits, regional availability, data handling, latency and Android compatibility. Present the concrete provider choice and any required API key/backend before implementation. Never hardcode secrets in the APK. If credentials or a backend are unavailable, implement only the provider-independent interface and clearly mark the provider connection as blocked; do not fake live voice.

Do not claim that ChatGPT's proprietary Live voice can be directly embedded or exactly cloned. Match the desired natural, warm female conversational quality using a legitimately available voice. Keep text chat and local AI usable when cloud voice is unavailable.

8.3 Emotion-Aware Conversation

Allow the AI to interpret conversational tone and respond appropriately.

Examples:

- Happy conversation.
- Sad conversation.
- Frustration.
- Serious discussion.
- Casual conversation.

Emotion detection must be treated as an estimate, not a guaranteed understanding of the user's actual feelings.

8.4 Internet Search

Provide optional internet search.

Requirements:

- Search when current information is needed.
- Present useful source links.
- Distinguish verified information from uncertainty.
- Continue supporting offline functionality when internet is unavailable.
- Do not invent search results or citations.

8.5 Document and PDF Knowledge

Allow users to upload supported documents and PDF files.

Required features:

- Import documents.
- Extract readable text.
- Index document content.
- Search relevant passages.
- Answer questions using uploaded knowledge.
- Identify the relevant document when possible.
- Preserve privacy.

Document retrieval is not equivalent to model retraining.

9. PHASE 3: PRILINA INTEGRATION

PRILINA must remain a separate application.

The Personal AI Engine should expose a secure local communication interface so PRILINA can request AI responses.

Possible integration methods:

- Local HTTP API.
- Android IPC or another suitable native communication method.

Choose the safest practical approach after inspecting both projects.

Requirements:

1. Inspect the actual PRILINA source code before modifying it.
2. Understand its existing architecture.
3. Define a clear API contract.
4. Preserve existing PRILINA features.
5. Avoid unnecessary changes.
6. Secure the local communication channel.
7. Restrict access to trusted applications where practical.
8. Handle unavailable AI services gracefully.
9. Provide useful error messages.
10. Test integration end to end.

Do not expose an unauthenticated local API to the public internet.

10. FUTURE EXPANSION AND SERVER MIGRATION

Design the system so future expansion is practical.

Possible future capabilities:

- Remote AI model hosting.
- Cloud inference.
- Multiple model providers.
- Additional voice engines.
- Advanced memory retrieval.
- More document formats.
- Additional integrations.
- More powerful personalization.
- Optional synchronization.

Do not implement expensive future features prematurely.

Keep the architecture modular so future additions do not require rewriting the entire application.

Important Android limitation:

Changes to native code, dependencies, Android permissions, manifests or bundled native libraries will generally require a new APK.

Do not promise that every future feature can be installed without rebuilding the application.

11. PRIVACY AND SECURITY

- Keep personal data private.
- Prefer local storage for local-first features.
- Do not transmit private documents without user permission.
- Request only necessary permissions.
- Protect stored credentials and tokens.
- Validate imported files.
- Avoid unsafe file operations.
- Restrict local API access.
- Provide memory deletion controls.
- Clearly identify features that require internet access.

12. THREE-PHASE DEVELOPMENT PLAN

PHASE 1 — CORE AI FOUNDATION

Implement:

- Android application foundation.
- Local GGUF inference.
- Model manager.
- Chat interface.
- Conversation history.
- Persistent memory.
- Memory management controls.
- Feedback and personalization foundation.
- Performance and error handling.

Phase 1 acceptance criteria:

- App installs successfully.
- A supported local model loads.
- User can send a message.
- Model returns a usable response.
- Generation can be stopped.
- Conversations persist after restart.
- Memory can be saved and retrieved.
- Errors are handled properly.
- Tests and build checks pass.

PHASE 2 — VOICE AND KNOWLEDGE

Implement:

- Speech input.
- Natural female voice option.
- Spoken responses.
- Bengali and English support where available.
- Emotion-aware response behavior.
- Internet search with sources.
- Document and PDF ingestion.
- Knowledge retrieval.

Phase 2 acceptance criteria:

- Phase 1 functionality remains working.
- Voice input and output are tested.
- Internet search reports genuine sources.
- Uploaded documents can be retrieved.
- Offline features remain usable where supported.
- Tests and build checks pass.

PHASE 3 — PRILINA INTEGRATION

Implement:

- Secure communication interface.
- PRILINA integration.
- Request and response handling.
- Error and connection handling.
- Privacy protections.
- Modular expansion foundation.
- Final regression testing.

Phase 3 acceptance criteria:

- Existing PRILINA features remain intact.
- PRILINA can communicate with the Personal AI Engine.
- Requests and responses work correctly.
- Disconnection and failure states are handled.
- Security checks are performed.
- Final builds and tests pass.

13. TESTING AND QUALITY CONTROL

At the end of every phase:

1. Inspect the complete project.
2. Review the current implementation.
3. Run relevant unit tests.
4. Run integration tests where available.
5. Run lint and static checks.
6. Run the Android Gradle build.
7. Fix failures.
8. Rerun failed checks.
9. Check for regressions in earlier features.
10. Record actual results in the handover report.

Do not report a test as passed unless it was actually executed successfully.

Clearly distinguish:

- Tested successfully.
- Not tested.
- Failed.
- Blocked.
- Requires physical-device verification.

14. MANDATORY DELIVERABLES AFTER EVERY PHASE

Return these deliverables separately:

1. Installable APK
   
   - Must be a genuine successful build output.
   - Clearly identify debug or release build.
   - Never provide a renamed placeholder as an APK.

2. Complete Source Code ZIP
   
   - Include all required project source files.
   - Include Gradle wrapper and configuration.
   - Include resources and tests.
   - Keep the project usable for the next development phase.

3. Updated Master Specification
   
   - Preserve all stable requirements.
   - Update progress and implementation status.
   - Record known issues and limitations.
   - Record the next phase.

4. Testing and Handover Report
   
   - List implemented features.
   - List tests actually executed.
   - Record build results.
   - Record known bugs.
   - Record remaining device checks.

5. Combined ZIP
   
   - Provide one combined archive when practical.
   - Do not replace the separate deliverables with the combined archive.

Suggested folder structure:

deliverables/

- phase-1/
- phase-2/
- phase-3/

Suggested filenames:

- PersonalAI_Phase1.apk
- PersonalAI_Phase1_Source.zip
- PersonalAI_Master_Specification_v1.2.md
- PersonalAI_Phase1_Report.txt
- PersonalAI_Phase1_Deliverables.zip

Use corresponding names for Phase 2 and Phase 3.

Before providing links:

- Verify that each file exists.
- Verify that each file is non-empty.
- Verify that the APK is a real build output.
- Verify that the source ZIP contains the complete project.
- Provide separate direct download links.
- Never claim an unavailable file was created.

15. LIVING PROJECT PROGRESS RECORD

This specification must be updated after every phase.

Maintain the following information:

- Current project version.
- Current phase.
- Completed features.
- Partially completed features.
- Unimplemented features.
- Bugs discovered.
- Bugs fixed.
- Tests executed.
- Exact test outcomes.
- Build results.
- Known limitations.
- Device verification status.
- Next recommended task.

Do not erase historical progress.

Preserve stable requirements while updating implementation status.

If a phase is incomplete, clearly record the blockers.

Do not move to the next phase while critical blockers remain unresolved.

16. HOW TO USE THIS MASTER FILE

This is the project's main source of truth. The separate `prompts/MASTER_EXECUTION_PROMPT.md` explains exactly how Google AI Studio must consume this specification and execute one selected phase. It does not replace this specification.

At the beginning of Phase 1, upload:

- This Master Specification.
- The required project source ZIP, if one is being used as the starting project.

At the beginning of Phase 2, upload:

- The latest updated Master Specification.
- The latest complete Phase 1 Source ZIP.

At the beginning of Phase 3, upload:

- The latest updated Master Specification.
- The latest complete Personal AI Source ZIP.
- The current PRILINA Source ZIP.

Do not assume Google AI Studio remembers earlier conversations or uploaded files.

Always use the latest versions.

17. FINAL PROJECT RULE

The goal is not merely to create an application that looks complete.

The goal is to create a stable, useful, extensible Personal AI Engine that works reliably on the target device and can later integrate with PRILINA.

Correctness, stability, privacy, performance, and verified functionality are more important than adding features quickly.

END OF MASTER SPECIFICATION
