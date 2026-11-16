# REPAIR — BUG FIX, REGRESSION AND RECOVERY
## Google AI Studio execution prompt

Do not start a new phase or add unrelated features. Read the latest Master Specification, latest test/handover report and inspect the complete current source project. Fix the reported issue with the smallest safe change.

## 1. Reproduce before fixing
- Restate the exact observed problem and expected behavior.
- Identify device/Android version, app version, model/provider, logs and reproduction steps when available.
- Inspect the relevant source path and surrounding architecture.
- Run the failing test or reproduce the failure before editing when possible.
- Separate pre-existing failures from newly introduced regressions.
- If the necessary source files/logs are missing, request them rather than guessing.

## 2. Safe repair rules
- Preserve all existing working features and user data.
- Do not rewrite the app or replace working modules with demo code.
- Do not remove dependencies or permissions without verifying impact.
- Prefer minimal, maintainable, backward-compatible fixes.
- Add a regression test for the bug when practical.
- Protect database contents and provide safe migrations.
- Do not add secrets, insecure endpoints or unnecessary permissions.
- Do not claim a root cause unless evidence supports it.

## 3. Verify the repair
Run the relevant unit/integration test, full regression suite where available, lint/static checks and Gradle build. Test adjacent flows that could be affected. For runtime/device-specific behavior, clearly state whether it was tested on a physical device, emulator, or not tested.

Mark every check PASS, FAIL, NOT RUN, BLOCKED or DEVICE CHECK REQUIRED. Include commands, concise outputs and logs relevant to the result. Do not fabricate test results.

## 4. Deliverables
Return:
- Complete repaired source ZIP.
- Genuine APK only if the build succeeds.
- Updated Master Specification and progress record.
- Repair report describing root cause (or uncertainty), exact files changed, tests and known limitations.
- Combined ZIP if practical.

Verify every file exists, is non-empty and contains what its name claims. Provide separate links. Never create placeholder APKs or pretend a blocked build succeeded.

## 5. Final response
State what failed, evidence-based cause, exact repair, regression tests, build status, unresolved issues and verified artifacts. Do not move to the next phase until the user approves.

## Mandatory File Explorer handover after every repair
Keep the complete repaired project in the active Google AI Studio workspace/File Explorer so it can be used in the next session/phase. Build the APK from this exact repaired project. If the environment supports writing build outputs into File Explorer, place the genuine verified APK there under one stable current filename (for example, `PRILINA-latest.apk`). Replace/remove the old APK only after the new APK has built successfully and passed file verification; never delete the previous known-good APK before that point. Keep a complete repaired source ZIP separately when supported. Report exact workspace paths, filenames, file sizes, build variant, tests, and whether File Explorer replacement actually succeeded. If the environment cannot place files there or cannot build, state the precise blocker and do not claim completion or fabricate artifacts. Source repair, successful build, APK placement/replacement, and physical-device testing must be reported as separate statuses.
