\# Full Name

Muhammad Zulqarnain Umar



\# Project \& Role Applied For

llm-eval-kit, Research/Implementation Engineer



\# Contribution

I've built retrieval and reasoning layers that depend on embedding based similarity

and LLM output scoring, most directly a RAG pipeline with a Claude Haiku/Sonnet

routing layer for SOC alert triage, and a compliance system with a citation

verifier that checks whether generated claims are actually grounded in retrieved

source text. That's essentially the same problem factual\_grounding and relevance

need to solve here, just in a different domain. I'd want to own the four criterion

implementations end to end, with particular attention to the singleton model

loading pattern. I've hit the reload model every call performance trap before,

and know it needs to be solved at the module level, not patched later. I'd also

push hard on the refusal\_check false positive problem (e.g. "I cannot stress

enough" not being flagged), since I've seen naive keyword based refusal detectors

fail on exactly this kind of phrasing in production LLM outputs.



\# Question

The completeness criterion checks sentence level coverage of prompt aspects in

the response. For prompts with multiple sub questions, is aspect extraction

meant to be handled via sentence embeddings against decomposed prompt clauses,

or is there a lighter weight heuristic planned for v1 before a more robust

aspect decomposition method is introduced later?

