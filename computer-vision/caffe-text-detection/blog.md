# Text Is Not What You See

When you look at a document, you see words. Coherent units. Meaning. A neural network looking at the same document sees: pixels with intensity values arranged in 2D space. To find text, it first has to find the *concept* of text—regions that look like text without understanding what text means.

I started with a question that sounds simple: "Given an image, where is the text?" But as soon as you try to answer it, the question fragments. Text can be oriented any direction. Can be small or large. Can be printed or handwritten. Can be partially occluded. Can be stylized in ways that make it barely recognizable as text.

The approach I took was based on HED-FCN architecture—Holistically-Nested Edge Detection applied to dense prediction. Sounds complicated because it is. But the insight beneath it is elegant: text consists of edges. Letter boundaries, stroke transitions, contrasts. If you can find edges at multiple scales and fuse them, you've found text regions.

Here's where architecture becomes philosophy.

Early edge detection methods treated edges as local information—look at a pixel and its neighbors, compute gradients, threshold. But edges at different scales tell different stories. Small edges catch fine details of letter strokes. Large edges catch the boundaries of text blocks. Neither alone is sufficient.

HED solves this by using a pyramid. Multiple layers of the network operate at different resolutions. Each layer learns to detect edges at its particular scale. Then all these multi-scale edge maps are combined—fused into a single prediction that respects both fine and coarse structure.

The interesting part? This pyramid approach isn't just technically sound. It mirrors how humans might see. We don't look at a document once and see all text. We glance, see text blocks (coarse). We zoom in, see individual characters (fine). We move our eyes across the page, building a model of where text exists.

But the network does it simultaneously, in parallel across scales.

```
Input Image
    ↓
    ├─→ Fine Scale (Small edges, letter details)
    ├─→ Medium Scale (Word-level boundaries)
    └─→ Coarse Scale (Text block regions)
    ↓
Multi-scale Fusion (Combine predictions)
    ↓
Text Region Map (Dense output)
```

The real challenge came with validation. How do you know if you found text correctly? With image classification, you have a score: accuracy. With dense prediction, every pixel is a prediction. Some pixels matter more—if you miss a letter, that's bad. If you incorrectly mark background as text, that's bad, but differently bad.

Measuring success becomes philosophical. Do you care about precision (no false positives) or recall (no false negatives)? With text detection, missing text is usually worse than marking some background. Because missing text means users never see it. Excess detection can be cleaned up in post-processing.

But what I found surprising: deploying text detection is harder than building it. Because in the real world, images aren't clean. Document photos are taken at angles. Under poor lighting. With shadows. With reflections. The algorithm works perfectly on test data—which is curated, aligned, well-lit.

Then you test on real data and it fails in ways you didn't anticipate.

This taught me something about the gap between research and practice. The network learned pattern matching on a specific distribution of images. Deploy it on a different distribution—photos from actual documents—and confidence drops sharply. The network is brittle in ways metrics don't reveal.

What kept me thinking: If the network excels at finding edges and edges indicate text, but edges also indicate many other boundaries—shadows, folds, artifacts—then the network is really solving a different problem. It's finding *candidate regions for text*, not definitively finding text. The final decision—is this really text—might require context the image doesn't contain.

---

*If a network can find text edges with high accuracy but struggle with real-world conditions, is it failing at text detection or succeeding at pattern matching on a narrow domain?*