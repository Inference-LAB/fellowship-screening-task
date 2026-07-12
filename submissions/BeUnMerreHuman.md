## Name
Muneeb Ur Rehman

## Project and Role
docling-pk
Research / Implementation Engineer

## Expected Contribution
I'd start with the OCR to regex boundary, since that's where this project will actually break. 
A phone-camera photo of a CNIC is much messier than a clean scanned PDF, and the brief already lists real problems: dashes read as underscores, stamps covering fields, documents rotated 90 degrees. 
So before writing any parser, I'd build the OpenCV preprocessing step (deskew, denoise, adaptive threshold) and test it against messy sample images first. For all four document types in v1 (CNIC old and new format, Matric, Intermediate, Degree/Transcript), I'd make the extraction fail gracefully. 
If a field is unclear, it should lower the confidence score and add a warning, not return a wrong value or crash. 
The initial preprocesing steps are correct, then we would need 2 open source OCR models,one for English like PaddleOCR and one for urdu like UTRNet, then use regex to clean up and correct some mistakes the OCR are known to make and then display the result
That confidence and warnings behavior is also what the Lead Engineer's API and the Integration Engineer's tests depend on, so I'll make it right early.

## Question
This problem is already solved using latest open source OCR models like Deepseek-OCR, anyone can import and use them, given they have a GPU, and most companies can usually afford one, then whats the purpose of this library and why are we not using newer transformers based frameworks that achieve way better accuracy compared to EasyOCR

So are we making a library that wraps multiple Transformer models into a clean, reliable, and optimized pipeline so a user can just call it and get the answer because i created a similar library msyself on pypi named `muneeb_nlp` that combines all the basic preprocessing for NLP into a single function call