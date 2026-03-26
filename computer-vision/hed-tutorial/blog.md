# Following a Tutorial Until You Understand Why

Tutorials exist in a strange space. They're invaluable for learning—guided, step-by-step, with someone else having already solved the hard problems. But they're also educational quicksand. You can follow along perfectly and understand nothing.

I took the HED tutorial and used it to probe that edge. The tutorial shows: here's HED, here's BSDS dataset, here's how to run inference, here's the output. Beautiful edge maps. Elegant results.

But following a tutorial is different from understanding a paper.

So I asked: why does HED work? Not what does it do—I could see that in the output. But *why*—what's the insight that makes multi-scale edge detection work?

The answer forced me back to the core problem: edge detection is ambiguous at single scales. Noise looks like detail looks like real texture. But across multiple scales, the signal clarifies. Noise is random across scales. Real edges persist.

That insight—persistence across scales—is the real nugget. The rest is implementation.

```
Multi-scale Processing
    ├─ Coarse scale: Major edges, low noise
    ├─ Medium scale: Object boundaries
    └─ Fine scale: Detailed structure, high noise
    ↓
Combination rule: Where do scales agree?
    ↓
Output: Robust edges
```

But here's where the tutorial ends and thinking begins. In the implementation, agreement across scales is handled by learning. The network learns which features at which scales are important. It's not an explicit "do scales agree?" check. It's learned weights that implicitly capture this.

This is the difference between understanding the motivation and understanding the implementation. The motivation is elegant. The implementation is learned, opaque.

And this gap matters because it means: you could explain why HED works conceptually to someone in 5 minutes. But explain what the network actually does internally? That's hard. The network has learned something that correlates with multi-scale edge detection, but you can't point to the exact mechanism.

When I tried variations—changing architecture, removing layers, adjusting training—I was experimenting without fully understanding. I had intuition from the tutorial's conceptual explanation, but not from understanding the learned model itself.

This taught me something about the difficulty of reasoning about learned systems. You can understand the motivation. You can measure the output. But the mapping between them—what the network actually learned—is hidden.

Running the tutorial on BSDS gave beautiful results. The network detects edges the way humans have annotated them. That's success. But is the success because the architecture is good, or because BSDS is familiar to the network's learned representations?

Test on different images and the edges became less certain. Confidence scores dropped. The network was hedging its bets.

This is where I had to push beyond the tutorial. Understand not just the method, but its limitations. Understand when it fails and why. Understand that following a tutorial gives you a tool, but using that tool requires understanding what it's for.

What kept me thinking: tutorials are designed for reproducibility. Here's what we did, do this and you'll get our results. But reproducibility isn't understanding. You can reproduce perfect results and still not know why they work.

And that's pedagogically important. The goal isn't to reproduce research. It's to build intuition so you can do novel research. The tutorial teaches what. Understanding teaches why.

---

*If following a tutorial produces perfect results but you don't understand the mechanism, have you learned the technology or just learned to copy?*