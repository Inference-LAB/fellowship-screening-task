## Name
Abdullah Abid

## Project and Role
**PROJECT:** docling-pk

**ROLE:** Integration/Evaluation Engineer

## Expected Contribution
As Integration/Evaluation Engineer on docling-pk, I would build and own the project's quality safety net: a curated fixture bank of real Pakistani CNIC and certificate images — including old and new CNIC formats, matric and intermediate certificates, each paired with a manually verified, known-correct expected JSON output covering fields like name, CNIC number, name and dates. I would try my best to include all edge cases such as rotated scans, blurred and varying image quality, since these are the conditions the Research Engineer's OCR pipeline must handle robustly. Using this fixture bank, I would write a pytest suite achieving 90%+ coverage, build an accuracy benchmark that measures how often extract() matches ground truth across document types, and verify the packaged library installs and runs correctly via PyPI before release.

## Question
 - For the testing purpose, we would need the samples of the CNIC and other certificates. I researched on the internet and found the dataset for the Pakistani CNIC's but there is no data/sample available for the Ceritificates. Do you have any source for these certificates?

    Pakistani CNIC's: [Link of Pakistani CNIC's dataset](https://universe.roboflow.com/gift-university-qazvo/cnic-card-detection/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true)

- As my role is QA role, it means that I'm expected to help debug why accuracy is low, that spills into CV territory. Is my responsibility also involves to debug the root cause of low accuracy (which could involve digging into OpenCV preprocessing or OCR/regex logic, the Research Engineer's domain)? Or is my responsibility limited to identifying an reporting where accuracy drops?