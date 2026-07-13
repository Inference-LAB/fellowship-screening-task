# Engineering Fellowship Screening

**Full Name:** Muhammad Fahad Faryad

**Project Applied For:** Pakistani Document Intelligence Library (docling-pk)

**Role Applied For:** Lead Engineer

## Expected Contribution
As the Lead Engineer, I expect to architect the library's foundational framework, designing a clean and intuitive public `extract()` API contract and a robust `DocumentResult` dataclass schema during Week 1. I will focus on building a structured, developer-friendly codebase, establishing the Typer CLI, writing comprehensive documentation, and structuring the PyPI packaging process. My goal is to ensure that the public API contract handles partial extractions and edge-case errors elegantly, allowing the Research and Integration modules to plug in without architectural friction.

## Project Question
When designing the public `extract()` API contract to handle partial results where certain critical document fields are obscured or fail validation, should the library throw a custom exception, or return a partial `DocumentResult` populated with specific warnings and a reduced overall confidence score?
