## Name
Abdul Moiz Muhammad

## Project and Role
docling-pk
Research / Implementation Engineer

## Expected Contribution
I'd start with the OCR to regex boundary, since that's where this project will actually break. 
A phone-camera photo of a CNIC is much messier than a clean scanned PDF, and the brief already lists real problems: dashes read as underscores, stamps covering fields, documents rotated 90 degrees. 
So before writing any parser, I'd build the OpenCV preprocessing step (deskew, denoise, adaptive threshold) and test it against messy sample images first. For all four document types in v1 (CNIC old and new format, Matric, Intermediate, Degree/Transcript), I'd make the extraction fail gracefully. 
If a field is unclear, it should lower the confidence score and add a warning, not return a wrong value or crash. 
That confidence and warnings behavior is also what the Lead Engineer's API and the Integration Engineer's tests depend on, so I'll make it right early.

## Question
CNIC and certificate documents often mix English and Urdu script (father's name, address, institution name are often in Nastaliq(calligraphic  style)). EasyOCR is noticeably weaker on Urdu script than on Latin text. For v1, should Urdu-script fields be extracted with lower confidence, transliterated, or marked as unsupported and skipped?