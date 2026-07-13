## Name

Fatima Naveed

## Project and Role

llm-eval-kit - Research / Implementation Engineer

## Expected Contribution

As the Research Engineer on this project, I'd be responsible for building the four scoring checks: factual_grounding, relevance, refusal_check and completeness that turn "is this LLM response good?" into something measurable instead of just eyeballing it. I understand relevance and factual_grounding both work by converting text into embeddings and comparing them using cosine similarity; the closer the numbers, the more similar the meaning. Refusal_check and completeness work differently; refusal_check is closer to pattern matching and completeness is about checking whether the response actually covers what the prompt was asking for not just how similar the wording sounds. Before writing scoring logic for any of these I'd want to test them against a handful of real prompt/response pairs first so I actually see how the scores behave instead of assuming.

## Question

The brief mentions the embedding model should load once per session, not once per evaluate() call, to avoid slowing things down. Is this something I'm expected to design myself inside the Evaluator class or is there a specific pattern used for this?
