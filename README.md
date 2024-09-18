# ArSL-fingerspelling-translation
This model performs hand detection and recognition of Arabic Sign Language Letters and writes the letters to form a word. It's intended to provide us with a basic tool that facilitates communication with the Arabic-speaking deaf community by providing them with an app that doesn't require them to type everything and allows the person on the other end of communication to capture words along with facial expressions to have the full experience of a conversation. 
## I. Dataset
We used the <a href = "https://www.kaggle.com/datasets/muhammadalbrham/rgb-arabic-alphabets-sign-language-dataset">RBG Fingerspelling Dataset</a> on Kaggle containing `250 samples` per class for each letter.  
### Labels
We have a total of 30 letters   
<img src="https://github.com/RanwaKhaled/ArSL-fingerspelling-translation/blob/main/guide.png">
## II. Feature Extraction
We used the `MediaPipe` framework to extract **hand landmarks** from the images and normalise them to feed them to the model without the hand's position influencing the prediction. This provides an efficient way of training the model on a matrix of numbers and focusing on the important features - **20 hands landmarks** - to recognize the gesture.   
<img src="https://github.com/user-attachments/assets/c46fca8d-c699-42fa-b0e8-5c592251df67" width = 700>  
After extraction and normalisation,, the landmarks were saved with their corresponding labels in a `csv` file so we could use it when training the model
## III. Model
Since we were dealing with numbers we created 2 basic Multi-layer Perceptron structures to compare them based on prediction accuracy and out-of-sample accuracy  
### First Network Structure
- Input layer
- 2 hidden layers: 20 nodes in the 1st layer and 10 nodes in the 2nd layer `ReLU`
- 1 Output layer: Softmax function
With `Dropout = 0.2` after the first layer and a `learning rate of 0.001`
**Test Accuracy**: `93%`
However, when using out-of-sample pictures it seemed to confuse some of the more similar gestures if the picture was a bit tilted or when a finger was not fully extended
### Second Network Structure
- Input layer
- 3 hidden layers:
    - 64 nodes in 1st layer
    - 48 nodes in 2nd and 3rd layer
- 1 Ouput layer: Softmax

with `Droput = 0.4` after first layer and `Dropout = 0.2` and the same `learning rate`  
**Test Accuracy**: `96.5%`  
This model generalised better over the out-of-sample pictures than the previous trial, providing a more accurate classification of the signed letter
## IV. Live Prediction
<img src="https://github.com/user-attachments/assets/53cb7019-8688-4966-be30-45130304c5f7">    
The hand is detected and landmarks extracted and normalized, then they are passed to the model and the letter is appended to the word at the bottom of the screen
