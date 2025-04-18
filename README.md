this is an api based text to voice converter

1️⃣ Create a speech object

let speech = new SpeechSynthesisUtterance();
This creates a new speech request.

SpeechSynthesisUtterance() is a built-in constructor that holds:

The text to speak

The voice to use

The pitch, rate, and volume (you can control those too)

2️⃣ Define an array to hold voices

let voices = [];
When the browser loads the available voices (which is asynchronous), we store them here.

3️⃣ Get the voice selector dropdown

let voiceSelect = document.querySelector("select");
This gets the <select> element from the HTML page (the dropdown where users pick a voice).

4️⃣ Load available voices when the browser finishes loading them

window.speechSynthesis.onvoiceschanged = () => {
    voices = window.speechSynthesis.getVoices(); // Load voices
    speech.voice = voices[0]; // Set default voice

    // Populate the dropdown with voice names
    voices.forEach((voice, i) =>
        voiceSelect.options[i] = new Option(voice.name, i)
    );
};
🔍 Explanation:
onvoiceschanged runs only when voices are available (important because they may not be ready on page load).

getVoices() returns an array of all installed voices in the browser.

We save the list to voices[].

We set the default voice to the first one: voices[0].

Then we loop through each voice and create <option> elements for the dropdown:

new Option(voice.name, i)
This creates:

<option value="0">Google US English</option>
<option value="1">Microsoft Zira</option>
...
5️⃣ Change voice when the user selects a new one

voiceSelect.addEventListener("change", () => {
    speech.voice = voices[voiceSelect.value];
});
🔍 What’s happening:
When the user picks a voice from the dropdown,

We get the selected <option>'s value → which is the voice index.

Then we assign that voice to the speech.voice property.

6️⃣ Speak the text when the button is clicked

document.querySelector("button").addEventListener("click", () => {
    speech.text = document.querySelector("textarea").value;
    window.speechSynthesis.speak(speech);
});

🔍 Explanation:
Grabs the text the user typed into the <textarea>.

Assigns that text to speech.text.

Then calls speechSynthesis.speak(speech) to read it aloud using the selected voice.
