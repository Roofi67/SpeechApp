# Android Speech and Text-to-Speech Integration App

## Overview

This Android application combines speech recognition and text-to-speech (TTS) functionalities to offer a comprehensive user interaction interface. Below is a detailed explanation of the various components and how they work together.

### Project Structure Overview

#### 1. AndroidManifest.xml
- **Permissions**: 
  - The app declares the `RECORD_AUDIO` permission, which is essential for accessing the microphone to capture audio for speech recognition.
- **Application and Activity Setup**: 
  - Defines the main activity (`MainActivity`) as the entry point of the app through the intent filter specifying this activity as the "MAIN" action and "LAUNCHER" category.

#### 2. activity_main.xml (Layout File)
- **User Interface Elements**:
  - `TextView` (`textTv`): Displays the results of the speech recognition.
  - `Button` (`speakBtn`): Initiates the speech recognition process.
  - `EditText` (`inputText`): Enables manual text entry for TTS.
  - `Button` (`readTextBtn`): Activates the TTS functionality to vocalize the text entered in the EditText.

#### 3. MainActivity.java
### 1. Text-to-Speech (TTS) Initialization and Usage:
- **Initialization**: A `TextToSpeech` object (`mTTS`) is initialized in the `onCreate` method. The initialization process involves creating a new `TextToSpeech` instance and setting a listener (`OnInitListener`) to check if the initialization is successful. If successful, it sets the language to the default system language.

- **Setting Language**: After initialization, the language is set with `mTTS.setLanguage(Locale.getDefault())`. This method returns a status that indicates whether the language data is missing, not supported, or successfully set.

- **Speak Out Text**: The method `speakOut(String text)` is used to speak the text. It is called when the "Read Text" button (`mReadTextBtn`) is clicked. This method uses `mTTS.speak(text, TextToSpeech.QUEUE_FLUSH, null, null)` to speak the text, where `TextToSpeech.QUEUE_FLUSH` clears the current speech queue and starts the new speech immediately.

- **Shutdown**: In the `onDestroy` method, the TTS engine is properly shutdown using `mTTS.stop()` and `mTTS.shutdown()` to release resources when the activity is destroyed.

### 2. Speech Recognition:
- **Prompt Speech Input**: The method `promptSpeechInput()` creates and starts an intent for speech recognition. It uses `RecognizerIntent.ACTION_RECOGNIZE_SPEECH` to start the speech recognition service. The intent is configured to use a free-form language model (`RecognizerIntent.LANGUAGE_MODEL_FREE_FORM`) and set to the default locale. A prompt message "Say something..." is also set to guide the user.

- **Handling Speech Input Results**: The `onActivityResult` method handles the result of the speech recognition activity. It checks if the result is OK and if data is present. If so, it retrieves the spoken words from the intent data, which returns as an `ArrayList<String>`. The first item from this list (assuming it's the most confident result) is then displayed on a `TextView` (`mTextTv`).

- **Error Handling**: If the device does not support speech input, a `Toast` notification informs the user that the feature is not supported.


### Build Configuration (`build.gradle`)


- **Dependencies**:
  - **AppCompat and Material Design**: Ensures backward compatibility and modern UI designs are supported.
    - `implementation("androidx.appcompat:appcompat:1.6.1")`
    - `implementation("com.google.android.material:material:1.2.1")`


### Overall Functionality

The app is designed to be interactive and user-friendly, ideal for users who may benefit from speech-to-text for easier data entry and text-to-speech for accessibility. It leverages Android's built-in capabilities for both functionalities to provide a seamless experience where users can either speak to the app or have the app speak back to them. The layout and manifest setups ensure a clean interface and the necessary permissions for proper function.




