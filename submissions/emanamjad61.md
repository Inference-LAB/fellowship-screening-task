## Name
eman amjad

## Project and Role
docling-pk — Research / Implementation Engineer

## Expected Contribution
As the Research/Implementation Engineer on docling-pk, I'd own the messy middle of the pipeline: the OpenCV preprocessing (deskewing, denoising, adaptive thresholding), the EasyOCR wrapper, and the per-document parser modules for the full v1 set — CNIC old and new format, matric, intermediate, and degree/transcript. My first move wouldn't be writing regex; it would be running EasyOCR on a batch of real phone-camera CNICs to see how the raw output actually degrades — dashes misread as underscores, glare over fields, documents rotated 90 degrees — and building the preprocessing step to correct those before any parsing happens. I'd treat graceful failure as a feature: an unclear field should lower its confidence score and attach a warning, never return a wrong value or crash. Since that confidence-and-warning behavior is exactly what the Lead's `extract()` contract and the Integration Engineer's fixtures depend on, I'd lock it down early and keep each parser small and independently testable.

## Question
The brief has `extract()` return a per-field confidence score. For the OCR-to-parser boundary I'd own, should a field's confidence come straight from EasyOCR's per-token probability, or should it be a composite that also factors in whether the regex/format validation for that field passed? That choice decides whether confidence is computed once in the OCR wrapper or inside each parser module — and it shapes how I structure the whole extraction layer.
