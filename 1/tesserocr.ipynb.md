[[BRIEF 1]]
This shows you how to use TesseractOCR so you can see how well your algorithm performs.

Never used before, looks fairly straightforward, Things to note: 

- `image_to_text`: This function from `tesserocr` performs OCR on the image and returns the extracted text.
- `psm=6`: Page Segmentation Mode (PSM) specifies how Tesseract interprets the image layout. Mode 6 assumes a "single uniform block of text."
- `oem=1`: OCR Engine Mode (OEM) specifies which OCR engine to use. Mode 1 uses the "LSTM only" (a modern, machine-learning-based engine).

Preprocessing seems very important..

