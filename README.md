# ID-verification
Define a model for ID verification system to ensure that the user is a student &amp; from that institute where he/she applied for sign in on the platform.
To accurately detect the text on a student’s ID and identify fraudulent IDs, it is imperative to train a model that would learn the patterns within an ID. I used the Verifai SDK for Python to perform this task, the features of which include:
•	Detect ID documents in JPEG images (in a privacy guaranteed way)
•	Give you information about the detected document
•	Position in the image
•	Type of document
•	The zones on the document
•	Get a cropped out image from the provided image
•	Get crops from all individual zones
•	Apply masks to the ID document image

I.	Subfields Detection

A pre-trained model subsequently trained on several documents to learn patterns of valid documents and detect key features within the student ID has been used. This model learns to focus on specific regions of the student ID that are deemed to be markers of a valid ID. The subfields model learns to detect holograms and logos as well as to recognize if the positions of certain text fields (for example, name, student registration no and date of birth) associated with the ID type are unusual. 

II.	Data Extraction

After the provided document has passed the initial validity checks, Optical Character Recognition (OCR) is used to read information within the document. OCR converts the image of text into raw text that can be processed and stored in the system. Instead of extracting text from the entire document, only information from specific fields identified in the Subfield Detection process is extracted.
Using OCR and various text processing techniques, personal details and student ID information (student ID number, issuance and expiration dates, etc.) can be extracted, thereby eliminating the need for manual entry. 

III.	Manual Intervention
Combining the insights from the previous steps, it is possible to determine if the provided document is a valid, authentic ID. Cases that are considered high risk or are found to share similar characteristics with previously-seen fraudulent users are marked for manual review. Similarly, cases that cannot be categorized with an appropriate degree of confidence are also reviewed manually. In the case of manual intervention, the operations team validates and classifies them. Our manual review process not only examines users that have indicators of fraud but also ensures that our system is not discriminating against any segment of users.


Labeling large amounts of images for object detection is a mundane and time-consuming task. Alternatively, I tried to implement a human-in-the-loop system using pseudo-labeling. Instead of labeling each document from scratch, the annotators only need to fine-tune the labels or predictions made by the current model. This makes the annotation process faster and less prone to mistakes and has the added benefit of acting as a feedback loop for us to learn more about model bias and limitations. The model learns from manual classification, and over time can spot patterns and closely mirror the manual results. This is accomplished by semi-automated retraining of the model including the newer data and manually curated data. This process allows for a continuous improvement flow as the model is adapted based on learning taken from real production data.

