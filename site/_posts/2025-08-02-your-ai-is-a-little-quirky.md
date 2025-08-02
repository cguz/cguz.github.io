---
title: "Your AI is a Little Quirky. And it’s not a bug—it’s a feature that makes them brilliant."
date: 2025-08-02
categories: [Artificial Intelligence, AI Research]
tags: [LLMs, Transformers, Bayesian Reasoning, Prompt Engineering, Chain-of-Thought, AI Theory, Order Sensitivity]
excerpt: "Your AI is a Little Quirky. And it’s not a bug—it’s a feature that makes them brilliant."
---

We feed ChatGPT (LLMs) information, and they process it with cold, hard logic, like a digital Sherlock Holmes piecing together clues. 

For a long time, the leading theory was that LLMs were behaving like "Bayesian" reasoners—a fancy term for an ideal thinker who constantly updates their beliefs as new evidence comes in. It’s the gold standard of rational thought.

Then, a new paper, “LLMs are Bayesian, In Expectation, Not in Realization”, threw a wrench in the works. They discovered something unsettling: LLMs have a weird quirk. If you give them a set of facts in one order, they might give you a slightly different answer than if you give them the exact same facts in a different order.

For a true Bayesian reasoner, this is a cardinal sin. The order of the clues shouldn't matter. 

Finding a muddy footprint and then a dropped glove should lead a detective to the same conclusion as finding the glove and then the footprint. 

![alt text](/assets/images/gloves.png)

This discovery sent a shiver through the AI community. Was the incredible reasoning power of LLMs just a clever illusion? Were they fundamentally flawed?

No, they’re not flawed. They’re just not playing by our old rules.

# The paradox of the shuffled clues

The problem researchers found is a violation of something called the "martingale property." At its heart, it’s a test of consistency. If you’re learning about a topic—say, trying to predict whether a coin is fair by observing a series of flips (Heads, Tails, Heads) — your best guess should only depend on the tally of heads and tails, not the order in which they appeared. But LLMs failed this test. Shuffling the in-context examples in a prompt could subtly change their final prediction. This was a direct contradiction of the popular "LLMs are Bayesian" theory.

So, how can they be so smart and so flawed at the same time?

The authors resolve this paradox with a beautifully simple insight: Transformers, the architecture behind LLMs, were never designed to ignore order. In fact, they’re built to obsess over it. Every word you feed into a transformer gets a "positional encoding" — think of it as a seat number in a theater. 

The model knows that "dog bites man" is fundamentally different from "man bites dog" precisely because it tracks the position of each word. This architectural feature, essential for understanding language, is what causes the "quirk."

The paper proves that LLMs aren't trying to be perfect Bayesian reasoners in every single instance. Instead, they are optimized to be brilliant on average, across all possible orderings of the data. They are "Bayesian in expectation."

It's a trade-off. They sacrifice perfect, rigid consistency for incredible efficiency and a deep understanding of sequential information. This quirk isn't a bug; it's a core feature of their intelligence.

# From deep theory to your keyboard

This discovery isn't just for academics. It has profound, practical implications for how we use and build AI systems. The paper hands us a new user manual for getting the best out of our AI assistants.

Here are two game-changing takeaways:

- Since we know LLMs are sensitive to order, we can exploit that. If you need a highly reliable or calibrated answer for a critical task, don't just ask once. Ask the same prompt a few times, but shuffle the examples or facts you provide. By averaging the AI's responses, you cancel out the positional quirks and get a much more stable and trustworthy result. The paper shows this simple trick can dramatically reduce the variance in predictions.

- You've probably heard of "chain-of-thought" (CoT) prompting, where you ask the model to "think step-by-step." This makes it much smarter at complex reasoning but comes at a literal cost—every "thinking" token costs money and time. So, how much thought is enough? Too little, and the answer is wrong. Too much, and you're wasting money. For the first time, this paper provides a closed-form formula to calculate the optimal chain-of-thought length. It balances the benefit of more reasoning against the cost, telling you exactly how many steps are "just right." For businesses using LLMs at scale, this could save millions.

# A new kind of intelligence

This research fundamentally reframes our understanding of LLMs. We’ve been trying to fit these new minds into old boxes, expecting them to behave like the idealized logicians from our textbooks. But they don't. They are something new.

They show us that intelligence doesn't have to be perfectly rigid or consistent to be powerful. Their brand of reasoning—messy, a little quirky, but stunningly effective on average—might be a more efficient path to cognition.

So the next time your AI seems a little inconsistent, don't worry that it's broken. It's just being itself: a new kind of thinker that’s brilliant, not in spite of its quirks, but because of them. And we’re just beginning to understand the profound implications of that.

---

*Read the full paper [LLMs are Bayesian, In Expectation, Not in Realization](https://arxiv.org/pdf/2507.11768).*
*Working on space AI systems or have thoughts on autonomous space operations? I'd love to hear about your experiences and ideas. Feel free to reach out at [cguzwork@cguz.org](mailto:cguzwork@cguz.org).*
