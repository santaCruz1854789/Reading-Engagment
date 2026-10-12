# Reading Engagement

A browser-based tool that passively estimates whether a user is engaged while
reading an e-book (.epub), without asking for any input. It combines two signals:

- **Video:** blink rate, long eye closures and head movement, computed in the
  browser from the webcam with MediaPipe Face Landmarker.
- **Touch/interaction:** time spent per page and number of "previous page" presses.

At the end of a session the tool gives a verdict (engaged / not engaged).

## Current status

The two modules are separate prototypes:

- `FaceDetection.html` – webcam module (eye aspect ratio, blinks per minute,
  long closures, head movement).
- `EPubReader.html` – epub reader that logs page times and page-turn directions.

Merging them into one page and the final fusion rule are planned next steps.

## How to run

1. Install an editor such as Visual Studio Code, plus the **Live Server** extension
   (a local server is required; opening the files directly with `file://` will not work).
2. Open the project folder in VS Code, right-click the HTML file you want
   and choose **Open with Live Server**.
3. Allow camera access when the browser asks (for `FaceDetection.html`).
4. For `EPubReader.html`, [use the file picker / place a .epub in the `epubs/` folder].
   A book is already included in the repository.

## Model

The `face_landmarker.task` model is in `app/shared/models/`. It comes from
Google's MediaPipe Face Landmarker guide.

## Privacy

All processing happens locally in the browser. No video is recorded or sent anywhere.
