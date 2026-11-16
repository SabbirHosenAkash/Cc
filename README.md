# Personal AI Engine — CC

এই repository-তে Personal AI Engine প্রকল্পের মূল specification এবং Google AI Studio-তে ব্যবহারের জন্য আলাদা phase-wise prompt রাখা হয়েছে।

## শুরু করার আগে
- [Google AI Studio Master Execution Prompt](prompts/MASTER_EXECUTION_PROMPT.md)
- [সম্পূর্ণ Master Specification](MASTER_SPECIFICATION.md)

প্রতিটি Google AI Studio session-এ Master Execution Prompt, সর্বশেষ Master Specification এবং নির্দিষ্ট phase prompt আপলোড করবে। সঙ্গে সেই phase-এর জন্য প্রয়োজনীয় সর্বশেষ source ZIP ও handover report দেবে।

## Google AI Studio prompts
- [Phase 1 — Core AI Foundation](prompts/PHASE_1.md)
- [Phase 2 — Voice and Knowledge](prompts/PHASE_2.md)
- [Phase 3 — PRILINA Integration](prompts/PHASE_3.md)
- [Repair Prompt — Bug Fixes and Recovery](prompts/REPAIR.md)

## ব্যবহারের নিয়ম
1. কাজ শুরুর আগে Master Specification সম্পূর্ণ পড়বে।
2. যে phase বাস্তবায়ন করতে হবে, শুধু সেই phase-এর prompt কপি করবে।
3. প্রতিটি phase-এর জন্য প্রয়োজনীয় সর্বশেষ source ZIP এবং specification আপলোড করবে।
4. আগের কাজের functionality অক্ষত রেখে test/build result সত্যভাবে report করতে হবে।
5. কোনো APK বা ZIP তৈরি হয়েছে বলে দাবি করার আগে file ও build output যাচাই করতে হবে।

**Project rule:** Master Specification হলো source of truth। README শুধু navigation ও ব্যবহারবিধি।
