## Name
Muneeb Ahmed Khan

## Project and Role
docling-pk — Research/Implementation Engineer

## Expected Contribution
I want to own the part of docling-pk that actually gets tested against reality: the OpenCV preprocessing pipeline and the OCR wrapper that has to make sense of a photo someone took on their phone in bad light with the CNIC held at an angle. This is not something for me. My IEEE paper was on a pose-aware biometric security framework, so I have already spent real time thinking about how to extract reliable information from visual input that does not seem right. I also worked on object detection under nighttime and adverse weather conditions using YOLOv8n with a ConvLSTM layer for temporal consistency, which is a similar thing: build something that holds up when the input is messy instead of clean lab data. I would bring that same mindset to docling-pk, testing against real scanned CNICs and certificates early, not synthetic clean samples, and building the deskewing, denoising and thresholding logic around what actually goes wrong in practice, stamps covering fields, rotated images, dashes read as underscores, rather than what goes wrong in theory.

## Question
When a scan comes in with more than one problem at once, say it is rotated and has a stamp partially covering the CNIC number, does the pipeline correct these in a fixed sequence, or is there flexibility to reorder preprocessing steps depending on what the image actually needs?