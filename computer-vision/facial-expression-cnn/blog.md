# What Emotions Look Like When You're Not Looking at Them

Facial expressions feel objective. Happy looks like smile. Sad looks like frown. Angry looks like wrinkles and tension. But what does a neural network see when it looks at a face?

I started with data—thousands of images labeled with seven emotional categories: angry, disgust, fear, happy, neutral, sad, surprise. Clean labels. Clear intent. A solved problem, or so I thought.

The first thing that broke my assumptions came from preprocessing. Your face in an image is surrounded by other faces, or background, or ambiguity. So the first step is: find the face. Extract just the face region. Align it to a canonical size—256x256 pixels usually. This sounds straightforward until you realize: this preprocessing step is already making decisions about what emotion is.

When you extract just the face and lose the body language, the context, the environment—you're telling the network "emotion lives here in these pixels." But we know emotion is contextual. A raised eyebrow means different things depending on what happened before it.

The network doesn't know that. It sees: a grid of pixels. Emotional features if you ask it to find them. Or just patterns if you don't.

So here's the real question I grappled with: Is a network learning to recognize emotions, or learning to recognize *the faces* that typically express emotions? There's a subtle difference, but it matters when accuracy hits a ceiling around 65-70% on test data.

The architecture I built was classical: convolutional blocks to extract features from the image, then dense layers to map those features to emotion categories. This works. The network learns to identify certain pixel patterns that correlate with certain emotional labels.

But accuracy is not the same as understanding. A network that's 70% accurate at emotion recognition is wrong 30% of the time. More interestingly, it's *confidently wrong* 30% of the time. It doesn't admit uncertainty.

When you deploy this to a phone as an Android app, something shifts in your thinking. You're not just training. You're making a system. A system that will look at someone's face and declare their emotions. That carries weight. That has implications.

The final challenge—converting the trained model to a mobile format—forced a conversation between different constraints. The Keras model works on a desktop. Converting it to work on Android requires changing precision, reshaping tensors, rethinking performance. And in doing so, you realize: what I trained isn't the final product. The final product is what survives the journey to constraints.

```
Raw Image
    ↓
Face Detection & Alignment
    ↓
Preprocessing (Normalize, resize)
    ↓
Conv Blocks (Feature extraction)
    ↓
Flattening
    ↓
Dense Layers (Emotion classification)
    ↓
7 Emotion Labels (with confidence scores)
```

But here's what stays with me: Facial expression work assumes emotions are expressions. But what if emotions are mostly internal? What if expressions are just social signals—the performance of emotion rather than the feeling itself? Then a network trained on expressions is learning a social code, not emotional truth.

When you build a system that reads emotions, you're betting that external signs correlate strongly enough with internal states to be useful. And maybe they do. For many purposes. But the failures are worth interrogating. The 30% error rate isn't just a number. It's 30% of people being misread by a machine that doesn't know it's guessing.

---

*If a network can learn to classify facial expressions with 70% accuracy, is it understanding emotions or just identifying surface patterns that correlate with emotion labels?*