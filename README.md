# Neural Networks Lab Notebooks

A collection of 23 deep learning and machine learning projects—each one an exploration of how neural networks solve real-world problems. From real-time object detection to generative models, these projects show both the theory and the practice, with actual code, results, and honest reflections on what worked and what didn't.

## Overview

This repo is structured around a simple question: *how do you actually build machine learning systems that work?* Not theoretically, but practically. You'll find projects that span foundational neural networks (MNIST, basic CNNs) through state-of-the-art techniques (StyleGAN2, multi-task learning). Each one includes the complete workflow—data preparation, architecture decisions, training results, visualizations, and candid thoughts on tradeoffs and limitations.

## What's Inside

### Computer Vision (10 projects)
**Real problems that touch images:** detecting objects, finding faces, understanding geometry, and pushing pixels into different artistic styles.

- **YOLO Object Detection** — Single network, multiple boxes, 45-65 FPS on GPU. The speed vs accuracy tradeoff made practical.
- **MTCNN Face Detection** — Three cascaded networks that detect faces and extract 68 landmarks. Multi-task learning at work.
- **HED Edge Detection** — Holistically-nested predictions in Caffe. Finding edges where humans see contours.
- **FCN Text Detection** — Fully convolutional approach to locating text regions. Works because the network learns to ignore everything except text.
- **Fruit Classification (Quick Draw)** — Taking sketches from Quick Draw and training a CNN that actually recognizes them.
- **Facial Expression Recognition** — 7 emotions from pixels. The hard part: why are angry and disgusted so similar to the network?
- **3D Multi-view Reconstruction** — Taking multiple camera views and reconstructing 3D geometry. Structure from motion the Open3D way.
- **Photo-to-Cartoon Stylization (Toonify)** — StyleGAN2 adapted for turning photos into cartoon art. Generative models doing something creative.
- **HED Tutorial (BSDS)** — Deep dive into edge detection on Berkeley segmentation benchmarks.
- **Caffe Text Detection Setup** — The infrastructure: CUDA, Caffe, compiling everything from scratch for GPU acceleration.

### Deep Learning (5 projects)
**Building and understanding neural networks from the ground up.**

- **MNIST CNN** — The hello world of deep learning, but with 99.36% accuracy and visualizations showing what the network actually learns.
- **Breast Cancer Neural Network** — Implementing backpropagation from scratch. Teaches you what frameworks hide.
- **Number Addition (TensorFlow)** — Regression networks predicting the sum of two numbers. Simple problem, but shows the pipeline.
- **VGG-LSTM Video Analysis** — Combining CNNs for spatial features with LSTMs for temporal patterns. How networks understand video.
- **VGG-Face GRU Emotion** — Transfer learning with VGG face embeddings feeding into a GRU. Standing on the shoulders of pre-trained models.

### Natural Language Processing (1 project)
- **GPT-2 Investigation** — What is a large language model? How does it generate text? What are the implications?

### Time Series & Classical ML (2 projects)
- **Holt-Winters Forecasting** — Exponential smoothing with trend and seasonality. Classical ML that often works better than people expect.
- **SVM Iris Classification** — Support vector machines with multiple kernels. Understanding how kernel methods separate data.

### Incomplete / Setup Projects (5 projects)
Documentation and setup guides for infrastructure and dependencies.

## What You'll Actually Find

Each project is more than code. You get the visualizations from actual training runs—loss curves, confusion matrices, decision boundaries. You see what the network learned and where it struggles. There are over 17 extracted images showing real results, not diagrams.

The documentation goes deeper than typical READMEs. Each project has a technical breakdown covering methodology and architecture, plus a longer narrative piece exploring the "why"—not just the what. You'll see reflections on tradeoffs made, limitations discovered, and what I'd change if doing it again.

Most projects target GPU acceleration (CUDA 8.0), with model exports for deployment (TensorFlow Lite for mobile, Protocol Buffers for Android). The code works across multiple frameworks: TensorFlow, Keras, PyTorch concepts, Caffe, scikit-learn.

## Technologies Used

**Deep Learning:** TensorFlow (1.7.0 and 1.15.3), Keras, PyTorch, Caffe, TFLearn

**Vision Libraries:** OpenCV, Open3D, YOLO, MTCNN, HED edge detection framework

**Compute:** CUDA 8.0, GPU training, batch processing with learning rate scheduling

**Data & Visualization:** NumPy, Pandas, Matplotlib, Seaborn, scikit-learn

**Deployment:** TensorFlow Lite (mobile), Protocol Buffers (Android), model freezing and export

## Key Results

Some numbers from the projects:

| Project | Result | What It Shows |
|---------|--------|---------------|
| MNIST CNN | 99.36% accuracy | The network learns digit patterns almost perfectly |
| Facial Expression CNN | 73.89% accuracy | Emotions are harder to classify than basic objects |
| Breast Cancer Network | Implemented from scratch | You understand what frameworks hide |
| YOLO Detection | 45-65 FPS on GPU | Real-time speed actually possible |
| SVM Iris | Linear & RBF kernels | Different decision boundaries for different kernels |

## 🛠️ Repository Structure

```
neural-networks-lab-notebooks/
├── computer-vision/
│   ├── yolo-object-detection/
│   ├── mtcnn-face-detection/
│   ├── hed-edge-detection/
│   ├── text-detection-fcn/
│   ├── fruit-classification-quickdraw/
│   ├── facial-expression-cnn/
│   ├── multiview-3d-reconstruction/
│   ├── toonify-cartoonization/
│   ├── hed-tutorial/
│   └── caffe-text-detection-setup/
├── deep-learning/
│   ├── mnist-cnn/
│   ├── breast-cancer-neural-network/
│   ├── number-addition-tensorflow/
│   ├── vgg-lstm-video-analysis/
│   └── vgg-face-gru-emotion/
├── nlp/
│   └── gpt2-investigation/
├── time-series/
│   └── holt-winters-forecasting/
├── classical-ml/
│   └── svm-iris-classification/
└── README.md (this file)
```

## Getting Started

Most projects run in Google Colab, which handles GPU acceleration. If you want to run locally:

**Requirements:**
- Python 3.6+
- 8GB+ RAM (GPU recommended, but can run CPU-only)
- CUDA 8.0+ if using GPU

**Install:**
```bash
git clone https://github.com/yourusername/neural-networks-lab-notebooks.git
cd neural-networks-lab-notebooks

python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

pip install tensorflow keras torch numpy pandas matplotlib seaborn scikit-learn opencv-python open3d
```

Each project folder has its own specific requirements documented in the README.

## How to Explore

Each project directory has:
- **notebook.ipynb** — The actual code with outputs and visualizations
- **README.md** — Technical breakdown (350+ lines) with architecture and results  
- **blog.md** — Longer narrative exploring the thinking process, tradeoffs, and reflections (1000-1500 words)
- **images/** — Extracted visualizations from the notebook runs

Start with the notebook to see the code in action. Read the README for methodology and findings. The blog piece is where you'll find honest reflection on what worked, what didn't, and what surprised me.

## Project Highlights

**YOLO Object Detection**
The speed is real—45-65 FPS on GPU with sufficient accuracy for practical use. The architecture sacrifices some precision for speed, but the tradeoff is conscious and justified.

**MTCNN Face Detection**
What's interesting isn't just that it detects faces, but how the cascade improves efficiency. Each stage becomes more precise because the crude stages already eliminated most negatives. It's an elegant approach to handling the imbalance problem.

**StyleGAN2 (Toonify)**
Generative models are powerful because they learn the distribution of a style, then interpolate in learned space. The pipeline—detect faces, align, project to latent space, style transfer—shows how complex vision tasks decompose into simpler ones.

**Backpropagation from Scratch**
You realize what neural network libraries do for you: managing gradients, organizing the computation graph, handling numerical stability. Implementing it yourself teaches you where numerical precision matters.

**Holt-Winters Forecasting**
Sometimes the classical approach works better than expected. This project explores why decomposing time series into trend and seasonality is useful, and when that assumption breaks down.

## What Gets Visualized

Training curves showing how loss decreases (or doesn't). Confusion matrices revealing which classes the network confuses. Decision boundaries showing how the network carves up the input space. Edge detection outputs on test images. 3D reconstructions. Generative model outputs. Real results from actual training runs, not idealized plots.

## What You Learn

Going through these projects, you develop intuition about:

- When to use CNNs vs RNNs vs attention-based architectures, and why those choices matter
- How transfer learning actually works (you're not training from scratch, you're adapting)
- Where the real bottlenecks are in practice (data preprocessing, not just training)
- Why metrics matter: accuracy isn't everything, confusion matrices tell the story
- How hyperparameters interact (learning rate, batch size, regularization aren't independent)
- The gap between test accuracy and real-world performance
- How to evaluate models honestly, including where they fail

## Key Insights

**Data preparation beats architecture tweaking.** You can spend hours optimizing layers, but if your data is noisy or imbalanced, you're fighting an uphill battle. Normalization, augmentation, handling class imbalance—these matter more than people realize.

**Metrics hide information.** A 95% accuracy sounds great until you look at the confusion matrix and realize the network fails on one specific class consistently. Or it's confident when wrong.

**Different frameworks solve the same problems differently.** TensorFlow, Keras, PyTorch—they're all solving backpropagation, but they emphasize different things. Understanding one deeply helps you learn others faster.

**GPU acceleration is practical.** Training times drop from hours to minutes. It changes how you experiment. You can iterate faster, try more ideas, afford to be thorough.

**Classical ML still works.** Holt-Winters for time series, SVM for classification—these aren't obsolete. They're simpler, more interpretable, and often more efficient than throwing a neural network at everything.

## How Projects Progress

Start with MNIST and SVM if you're new to this—they're foundational and you understand them completely. Move to the CNN projects to see how architecture choices play out. Then explore combinations like VGG-LSTM that merge spatial and temporal learning. The generative models and reconstruction projects are where it gets genuinely complex.

## Documentation Philosophy

Each project README covers the problem, approach, and results. But the blogs go deeper—they show the thinking, the false starts, what surprised you, what you'd change. Technical writing that's honest beats clever writing every time. If something didn't work, that's interesting. If you made a design choice and regret it, say so.

## Questions?

See the individual project README and blog files for detailed explanations. Each one documents the approach, assumptions, and tradeoffs. If you're wondering why a particular choice was made, there's probably a section explaining it.

## Credits

Built with Google Colab for GPU computing, various open-source datasets (MNIST, ImageNet, Berkeley Segmentation), and a lot of trial and error.

---

**23 projects** | **17+ visualizations** | **50+ pages of documentation** | **15,000+ lines of code**

Last updated: March 26, 2026
