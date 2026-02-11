# Machine_Learning
README
# [Project Name: e.g., Image Classifier Model]

This repository contains a machine learning model trained using [Google Teachable Machine](https://teachablemachine.withgoogle.com/). The model is designed to recognize and classify [Images/Sounds/Poses] into specific categories.

## 🚀 Model Link
You can access and test the live model here: 
[https://teachablemachine.withgoogle.com/models/d2UdUo16q_/](https://teachablemachine.withgoogle.com/models/d2UdUo16q_/)

## 📊 Classes
The model has been trained to identify the following classes:
* **[Class 1 Name]**: Description of what this class represents.
* **[Class 2 Name]**: Description of what this class represents.
* **[Class 3 Name]**: (Add more if applicable)
* <img width="369" height="749" alt="Screenshot 2026-02-11 113835" src="https://github.com/user-attachments/assets/fb17c07b-03f7-4340-a2d4-244ec83e6a16" />
<img width="493" height="760" alt="Screenshot 2026-02-11 113907" src="https://github.com/user-attachments/assets/7697e08b-4e0f-4fb4-83bc-0245162c1464" />
<img width="395" height="764" alt="Screenshot 2026-02-11 113931" src="https://github.com/user-attachments/assets/0f5dafe4-13d6-4a67-87cc-66e06013e7d6" />




## 🛠️ How it was built
- **Tool:** Teachable Machine by Google
- **Model Type:** [e.g., Image Classification / Pose / Audio]
- **Framework:** TensorFlow.js

## 💻 Usage

### Integrating with JavaScript
You can use this model in your own web projects using the following snippet:

```javascript
<div>Teachable Machine Model</div>
<button type="button" onclick="init()">Start</button>
<div id="webcam-container"></div>
<div id="label-container"></div>

<script src="[https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@1.3.1/dist/tf.min.js](https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@1.3.1/dist/tf.min.js)"></script>
<script src="[https://cdn.jsdelivr.net/npm/@teachablemachine/image@0.8/dist/teachablemachine-image.min.js](https://cdn.jsdelivr.net/npm/@teachablemachine/image@0.8/dist/teachablemachine-image.min.js)"></script>
<script type="text/javascript">
    const URL = "[https://teachablemachine.withgoogle.com/models/d2UdUo16q_/](https://teachablemachine.withgoogle.com/models/d2UdUo16q_/)";

    let model, webcam, labelContainer, maxPredictions;

    async function init() {
        const modelURL = URL + "model.json";
        const metadataURL = URL + "metadata.json";

        model = await tmImage.load(modelURL, metadataURL);
        maxPredictions = model.getTotalClasses();

        // Convenience function to setup a webcam
        const flip = true; 
        webcam = new tmImage.Webcam(200, 200, flip); 
        await webcam.setup(); 
        await webcam.play();
        window.requestAnimationFrame(loop);

        document.getElementById("webcam-container").appendChild(webcam.canvas);
        labelContainer = document.getElementById("label-container");
        for (let i = 0; i < maxPredictions; i++) {
            labelContainer.appendChild(document.createElement("div"));
        }
    }

    async function loop() {
        webcam.update(); 
        await predict();
        window.requestAnimationFrame(loop);
    }

    async function predict() {
        const prediction = await model.predict(webcam.canvas);
        for (let i = 0; i < maxPredictions; i++) {
            const classPrediction =
                prediction[i].className + ": " + prediction[i].probability.toFixed(2);
            labelContainer.childNodes[i].innerHTML = classPrediction;
        }
    }
</script>
