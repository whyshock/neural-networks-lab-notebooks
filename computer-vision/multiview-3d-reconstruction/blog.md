# When Fragments Become a Coherent World

Three-dimensional reconstruction from multiple photographs seems like physics. Light reflects, hits camera sensors, creates images. If you have multiple images from multiple angles, you can infer 3D structure.

The mathematics is elegant. Epipolar geometry gives constraints. Feature matching across images gives correspondences. Triangulation converts 2D points into 3D positions.

But the practice is messier.

Real images have noise. Features don't match perfectly. Cameras have lens distortion. Perspective shifts aren't purely geometric—objects move, lighting changes, occlusion happens.

Multi-view reconstruction forces you to ask: what are we actually reconstructing?

Geometry, yes. The 3D positions of surfaces. But also invisible things: lighting assumptions, material properties, occlusion relationships. Choose different assumptions and you get different 3D models from the same images.

```
Multi-view Images
    ├─ Find features in each image
    ├─ Match features across images
    ├─ Triangulate to 3D positions
    ├─ Fuse into coherent structure
    └─ Refine and verify
    ↓
Output: 3D Model
```

The Redwood dataset made this concrete. Real scans with ground truth. So I could measure: how close is my reconstruction to ground truth?

The answer: not very, if you're not careful. The algorithm works in principle. In practice, errors compound. Feature matching errors propagate to triangulation errors, which propagate to fusion errors, which propagate to final geometry errors.

You could spend months tuning parameters, fixing failure cases, smoothing artifacts.

But here's what I found interesting: point clouds (raw 3D points) are easier to compute than meshes (connected surfaces). Point clouds are just locations. Meshes require additional structure—which points connect to which.

So computation progression is: 2D features → 3D points → point cloud → mesh.

Each step adds assumptions. Points alone are ambiguous about surfaces. Meshes assume surfaces exist. Choose wrong and downstream fails.

What kept me thinking: humans reconstruct 3D from photos naturally. We see two angles of an object and instantly know its shape. This seems effortless. But what we're actually doing is inference with massive prior knowledge.

We know objects are usually rigid. We know physics (gravity, support). We recognize objects and use knowledge about their typical shapes. Our brains are loaded with assumptions.

Algorithms assume less. They compute from geometry alone. This is pure, but fragile.

Combining geometry with learned shape priors could be powerful. Networks that learn typical shapes and refine reconstructions based on likelihood. But this is a different approach—not pure geometry.

---

*If humans reconstruct 3D from photos using prior knowledge, and algorithms reconstruct using only geometry, who's actually solving the harder problem?*