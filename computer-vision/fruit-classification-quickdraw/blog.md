# Teaching a Network to Remember What It Never Drew

The Quick Draw dataset is unusual. Millions of sketches drawn by humans, often in under 20 seconds. Rough, unfinished, stylized. People drawing "apple" produce radically different images. Sometimes it's a filled circle. Sometimes it's a circle with stem and leaf. Sometimes it's barely recognizable.

This is the opposite of curated datasets. ImageNet and MNIST have careful, controlled images. Quick Draw is chaos refined to training data.

The question I started with: can a network learn to classify fruit from sketches so variable that even humans sometimes can't guess what's intended?

What surprised me: it could. Better than I expected. But the failures were more interesting than the successes.

The network trained on simple sketches, often missing details. When you show it a complete, detailed drawing, it sometimes struggles. When you show it a sketch in an unusual orientation or drawn in an unexpected style, it hesitates. But within the training distribution—rough sketches in the style the data encompasses—it's confident.

This revealed something about representation. The network learned the *essence* of fruit, in the style humans sketch rapidly. It learned: apples are usually roughly circular with a simple stem. Bananas are curved. Grapes are clustered circles.

But these essences are learned from data. Show the network an apple drawn in a style outside the training data—photorealistic, or super-minimalist, or abstract—and it's lost.

Here's what kept me thinking: humans have a richer concept of "apple." We know apples roll. We know they taste a certain way. We know they grow on trees. We know their history. We know Newton's apple fundamentally changed physics.

A network trained only on sketches knows none of that. It knows: the set of pixel patterns that humans labeled "apple" when drawing quickly.

```
Training Distribution              Deployment Distribution
(Quick Draw sketches)             (How people actually use it)
- Rough drawings                  - Varied drawing styles
- Fast execution                  - Different skill levels
- Hand-drawn digital              - Different intents
```

The interesting challenge came when deploying to a real application. Users don't draw in the Quick Draw style. They draw naturally. Some are careful, some are messy. Some understand perspective, some don't.

So the network I trained on Quick Draw doesn't work perfectly on real-world user inputs. It works *okay*. Usually right. But the confidence scores are misleading. The network is equally confident in cases where it's wrong and right.

What I learned: the gap between "works on test data" and "works in production" is huge. Test data is sampled from the same distribution as training. Production data often isn't.

Deploying machine learning means confronting this gap. You build on clean data. You deploy to messy reality. The network was trained on one truth. It deploys to different truths.

But here's the philosophy: is that a failure of the network or a failure of expectations? We asked it to generalize from quick sketches to all possible fruit drawings. That's a lot to ask of 20 seconds of user drawing.

What if instead we reframe: the network is specialized. It works well for quick sketch classification. If you want to classify realistic fruit images, use a different model. If you want to classify high-art fruit drawings, again, different model.

Specialization isn't failure. It's honesty.

---

*If a network learns to classify fruit from rough sketches but struggles with polished drawings, did it fail to learn fruit or succeed at learning sketches?*