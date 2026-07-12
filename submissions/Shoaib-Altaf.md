## Name
Muhammad Shoaib Altaf

## Project and Role
inference-audit — Research Engineer

## Expected Contribution
I'd focus on the five check modules, particularly check_near_duplicates and check_language_contamination, where I can bring direct experience: my person re-identification project (EfficientNet-B0 with triplet loss, evaluated via t-SNE) required reasoning carefully about embedding similarity thresholds and what counts as "the same" versus "merely similar" — the exact judgment call near-duplicate detection with MinHash+LSH demands. Separately, I've been building toward Roman Urdu NLP work, so I understand firsthand why character 3-gram fingerprints are the right call over word tokens here — Roman Urdu's lack of standardized spelling makes token-based matching unreliable. I'd also want to own getting the langdetect determinism right (DetectorFactory.seed = 0) early, since debugging a "flaky" contamination check after the fact wastes far more time than fixing the seed on day one.

## Question
Character 3-gram MinHash will catch lexical near-duplicates well, but Roman Urdu commonly has multiple valid spellings for the same word (e.g. "kya" / "kiya" / "kia"). Is there a planned normalization pass before fingerprinting to catch these as duplicates, or is that intentionally out of scope for v1, with only exact/near-exact spelling matches counted?
