# What Edges Reveal When You Stop Looking for Objects

Edge detection feels like it should be simple. Look at where pixels change intensity sharply. Those are edges. Mark them. Done.

Except the world doesn't work that way.

When you look at an image, you see objects because your brain groups edges into coherent structures. But edge detection—if you just compute intensity gradients—gives you a noisy map of all transitions. Shadows create edges. Textures create edges.. Noise creates edges. Most of what you detect isn't the structural edges that matter.

HED—Holistically-Nested Edge Detection—thinks differently. Instead of computing edges at one scale and calling it truth, it computes edges at many scales. Small-scale edges catch fine details. Large-scale edges catch major boundaries. All these scales are combined—fused—into a final edge map that respects structure at all levels.

The word "holistically" matters. It means: don't just look at local neighborhoods. Look at nested hierarchies of context. An edge at fine scale makes sense only if it fits the structure of coarser scales.

```
Image
    ├─ Scale 1: Find fine edges (texture, writing)
    ├─ Scale 2: Find medium edges (objects, boundaries)
    └─ Scale 3: Find coarse edges (scene structure)
    ↓
Fuse scales: Where do all levels agree?
    ↓
Output: Edges that matter
```

Here's what I found when I trained HED on the BSDS dataset—a collection of photographs with human-annotated edges. Humans agree on major edges: object boundaries, shape contours. Humans disagree on texture, fine details. So the dataset reflects this—strong consensus on important structure, ambiguity elsewhere.

HED learns to respect this ambiguity. It produces confidence maps, not binary edges. Some edges are confident. Some are tentative.

But the real insight came when I tried to use the output. Edge detection is rarely an end goal. It's a step toward something else—object detection, segmentation, 3D reconstruction. So how good does your edge map need to be?

If it's perfect, 100% detection, that's not actually useful. Because perfection means detecting every edge, including noise and texture. What you actually want: edges that structure perception.

A human looking at an image doesn't detect every intensity transition. They detect edges that *mean something*. A shadow edge might be ignored if it's clearly just shadow. A texture edge might be filtered away. But a real object boundary is always captured.

HED can't access semantic understanding directly. It can't know "this is shadow, ignore it." It can only learn from data. And the data tells it: humans annotate these edges, not those edges.

What I found fascinating: improving raw edge detection accuracy sometimes made the output useless. More false positives meant more confusing outputs. The goal wasn't accuracy on every edge. It was accuracy on *meaningful* edges.

This forced a conversation about what "accuracy" means. In classification, it's simple: percent correct. In edge detection, it's ambiguous. Precision? Recall? The boundary between them?

And fundamental question: Is edge detection actually solving an objective problem, or is it solving a human perception problem? Those aren't the same thing.

From a physics perspective, an edge is where there's an intensity discontinuity. Simple. But from a perception perspective, edges are where boundaries between objects exist. More complex. The two would agree if the world were simple. It isn't.

What kept me thinking: HED performs remarkably well on BSDS because it learned from human annotations. But deploy it on photos of real-world scenes—not BSDS—and something shifts. The network is answering: "which edges would humans mark on BSDS photographs?" Not: "which edges are structurally important in this scene?"

It's specialized to the training distribution, and doesn't know it.

---

*If a network learns edge detection from human annotations, is it learning to detect edges or learning to predict what humans would find important?*