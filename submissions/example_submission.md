## Name
Muhammad Ali Hassan

## Project and Role
docling-pk — Research / Implementation Engineer

## Expected Contribution
As the Research Engineer on docling-pk, I expect to own the core extraction pipeline — specifically the image preprocessing module using OpenCV and the field extraction logic for CNIC and matric certificate parsers. My prior work includes a document scanner project where I used cv2.adaptiveThreshold() for handling uneven lighting in phone-camera images, which is directly relevant to the preprocessing challenge here. I plan to start the design document section by running EasyOCR on real CNIC images in Week 1 to understand the actual OCR output before writing any regex — rather than assuming the output format.

## Question
The project brief mentions that CNIC formats differ between the old green and new blue versions. Are both in scope for v1, and if so, should the parser detect the version automatically from the image, or will the caller pass the version as a parameter? The design choice affects whether I build one parser with conditional logic or two separate parsers.
