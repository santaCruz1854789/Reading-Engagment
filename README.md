# Reading Engagement

A browser-based tool that passively estimates whether a user is engaged while
reading an e-book (.epub), without asking for any input. It combines two signals:

- **Video:** blink rate, long eye closures and head movement, computed in the
  browser from the webcam with MediaPipe Face Landmarker.
- **Touch/interaction:** time spent per page and number of "previous page" presses.

At the end of a session the tool gives a verdict (engaged / not engaged).

## Current status

- `EPubReader.html` – the main application. One page with the e-book reader and, in the
  background, the webcam analysis (the camera preview is hidden). It counts the words on each
  page, logs page times and turn directions, and on **End Session** shows the measures, the four
  votes and the engaged / not engaged verdict. Verdicts are saved in the browser
  (localStorage); when the last page of the book is reached, the book-level ratio
  (engaged sessions / sessions needed to finish) is shown. The **Show measured values** button
  displays the live values. If the camera is unavailable, only the reading signals are used.
- `FaceDetection.html` – the standalone webcam module used to calibrate the thresholds
  (eye aspect ratio, blinks per minute, long closures, head movement).
- `report/` – the project report (LaTeX, ACM sigconf).

Status: the reader, word counting and fusion were tested in a browser. The merged page has not
been tested with a live face on a second reader, and the thresholds are hand-set starting points
validated only on the author.

## How to run

1. Install an editor such as Visual Studio Code, plus the **Live Server** extension
   (a local server is required; opening the files directly with `file://` will not work).
2. Open the project folder in VS Code, right-click `EPubReader.html`
   and choose **Open with Live Server**.
3. Allow camera access when the browser asks.
4. The book `epubs/RomeoJuliet.epub` is included; to read another book, change `BOOK_PATH`
   at the top of the script in `EPubReader.html`.

## Model

The `face_landmarker.task` model is in `app/shared/models/`. It comes from
Google's MediaPipe Face Landmarker guide.

## Privacy

All processing happens locally in the browser. No video is recorded or sent anywhere.
