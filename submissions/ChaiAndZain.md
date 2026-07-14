## Name
Zain Ul Abideen

## Project and Role
docling-pk - Lead Engineer

## Expected Contribution
My main focus will be designing a clean public api contract for the `extract()` function.  I want to build a solid `DocumentResult` dataclass schema that can handle real world edge cases like missing or obscured fields gracefully. this way the research engineers OCR modules can plug right in without friction, and external devs get a smooth experience using the Typer CLI and PyPI package. 

## Question
Why we are not using some more advance OCR model like baidu OCR, Deekseek OCR or GLM ocr?? if size is the issue then some smaller model could be finetuned that could efficintly run on a cpu. 