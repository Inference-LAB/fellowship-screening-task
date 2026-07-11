## Name
Muhammad Maaz

## Project and Role
llm-eval-kit - Research/Implementation Engineer

## Expected Contribution
I expect to build out the four criterion implementations - factual_grounding, relevance, refusal_check, and completeness - using sentence-transformers embeddings and cosine similarity, along with the singleton model-loading pattern that keeps evaluate() calls fast. I've worked directly with this kind of problem before: I built a Self-Reflective RAG system where an [IsSup] classifier checks whether a generated response is actually supported by retrieved context, which is functionally close to what factual_grounding needs to do here. I'm also comfortable with the failure modes this role has to guard against - for example, getting refusal_check to correctly separate a genuine refusal from a response that merely contains cautionary language, since a naive keyword match would misfire on cases like "I cannot stress enough how important this is."

## Question
The brief says the embedding model should load once per session via a singleton so evaluate() stays fast, rather than reloading per call. If llm-eval-kit is ever wrapped behind a web API (say, a Flask service evaluating responses concurrently) rather than used purely from the CLI, does that singleton need explicit thread-safety guarantees, or is v1 scoped strictly for single-threaded/CLI use? I ask because I ran into a very similar per-call-vs-shared-resource bug with a database connection pool in a past project, and the fix ended up shaping the whole architecture.
