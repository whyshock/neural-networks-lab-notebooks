# Boundaries in Feature Space

Support vector machines are elegant. Deceptively simple. Find the line (or plane, or hyperplane) that best separates two classes. Position it to have maximum margin—the largest gap between any point and the line.

This is geometric thinking applied to classification. Not neural networks. Not probabilistic models. Just geometry.

Now add kernels. Instead of finding a line in the original feature space, apply a transformation. Map the data to a higher-dimensional space where it becomes linearly separable. Then find the line there.

The trick: you don't have to explicitly compute the transformation. A kernel function computes distances in the transformed space directly. It's elegant mathematics at work.

```
Input Space             Kernel Transform        Feature Space
(possibly nonlinear)    (implicit mapping)      (linearly separable)
  ●   ■                 ───────────────→        ●  ●  ●
    ●       ■                                   ■  ■  ■
  ●     ■     ■                                 ───────── 
(hard to separate)     (magic happens)      (easy to separate)
```

When I applied SVM to Iris classification, something shifted in how I thought about learning. SVMs don't learn features. They work with given features. They learn boundaries.

This is fundamentally different from neural networks that learn features automatically. With SVM, you choose features. The algorithm finds boundaries in that feature space.

For Iris—a small dataset with four features (sepal length, width, petal length, width)—you can understand what's happening. Visualize it. See where the decision boundary cuts the space.

You can ask: "why is this flower classified as this species?" And trace it back to geometry. "Because in feature space, it's closer to the decision boundary of that class."

With neural networks, asking why is harder. The network transforms features internally in ways you can't easily trace.

But here's the trap with SVM: simplicity can be deceptive. An SVM finds boundaries, yes. But are they the *right* boundaries? For toy datasets like Iris—28 samples total, well-structured—SVM works beautifully.

For real-world problems with thousands of complex features, SVM has to choose: use all features (high dimensionality, risk of overfitting) or select features (requires domain knowledge, risk of losing signal).

Neural networks sidestep this by learning which features matter. For Iris, humans already know: petal length and width are most informative. The human feature engineering is done. SVM thrives in such environments.

Kernel selection is where I had to make choices. Linear kernel assumes linearly separable data—usually not true. RBF kernel (Radial Basis Function) is more flexible. It can learn nonlinear boundaries. Polynomial kernels are somewhere in between.

But more flexible kernels overfit more easily. The boundary that perfectly separates training data might fail on test data.

```
Kernel Choice
├─ Linear: Simple, interpretable, often underfits
├─ RBF: Flexible, can overfit, hard to interpret
└─ Polynomial: Middle ground, controls complexity
```

Visualizing decision boundaries—creating meshgrids, evaluating SVM on grid points—showed something profound. The contours of the decision function tell a story. Linear kernels produce straight lines. RBF kernels produce curved, locally-adaptive boundaries.

Which is "more correct?" Neither. It depends on the true underlying distribution. Iris happens to have somewhat separable classes with nonlinear features, so RBF performs better.

But that's empirical success, not understanding.

What I found most interesting: support vectors—the points closest to the decision boundary. These points define the boundary. All other points are irrelevant. An SVM could delete all non-support points and produce identical boundaries.

This is different from neural networks, where every training point affects learning. In SVM, most points are irrelevant noise. Only the boundary cases matter.

This has beautiful implications. If you have a dataset with some outliers or errors, SVM might ignore them. Only the boundary points shape decisions. But it also means: you can't easily diagnose what features the SVM learned from all your data. Only the boundary points are informative.

What kept me thinking: SVM was dominant before deep learning. Now it's almost forgotten in some circles. But for certain problems—especially with limited data—it outperforms neural networks.

The switch from SVM to neural networks was a shift from "find optimal boundaries" to "learn optimal features." Different paradigms. Neither universally better.

---

*If SVM finds optimal boundaries in feature space and neural networks learn optimal features, which solves the harder problem?*