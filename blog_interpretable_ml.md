# Stop Explaining Black Boxes — Build Models People Can Actually Understand

*A summary of Cynthia Rudin's influential 2019 perspective in Nature Machine Intelligence, and why it still matters.*

---

Machine learning models are making decisions that deeply affect human lives — who gets parole, who qualifies for a loan, whether the air outside is safe to breathe. And yet, most of these models are black boxes. Nobody can look inside them and understand *why* they made a particular prediction.

The dominant response in the ML community has been to develop post hoc explanation methods: train a complex model first, then build a second, simpler model to "explain" the first one. In a landmark 2019 paper, Cynthia Rudin (Duke University) argues that this entire approach is fundamentally misguided — and that for high-stakes decisions, we should be building **inherently interpretable models** instead.

Her argument is not a soft plea. It is a structured, evidence-backed case that the field has been solving the wrong problem.

---

## The core thesis

Rudin's central claim is simple but radical: **there is no necessary trade-off between accuracy and interpretability**, at least not for the structured data problems that dominate high-stakes decision-making. The widespread belief that you *need* a complex model to get good predictions is, in many cases, a myth.

She draws on her own experience in a large-scale project to predict electrical grid failures in New York City. Despite working with messy, heterogeneous data — free-text trouble tickets, century-old cable records, brand-new inspection logs — the performance gap between complex and simple models on any fixed dataset was at most 1%. But the ability to *interpret* the model's outputs and iteratively improve the data processing led to much larger gains. In other words, interpretability didn't hurt accuracy. It improved it.

---

## Why post hoc explanations are dangerous

The paper makes several sharp arguments against the "explain the black box" paradigm.

**Explanations are inherently unfaithful.** If an explanation were perfectly faithful to the original model, it *would be* the original model — and you wouldn't need the black box. Any approximate explanation is therefore wrong in some part of the feature space. An explanation that agrees with the black box 90% of the time is wrong 10% of the time, and you can never know *which* 10%.

**Explanations can use entirely different reasoning.** A post hoc model might match a black box's predictions while relying on completely different features. Rudin illustrates this with the COMPAS recidivism tool: ProPublica built a linear explanation model for COMPAS that depended on race, and then accused COMPAS of racial bias. But since COMPAS appears to be nonlinear, it is entirely possible that it does not depend on race beyond correlations with age and criminal history. The explanation was accurate in mimicking predictions but misleading about the model's internal logic.

**Saliency maps explain almost nothing.** In computer vision, saliency maps show *where* a network is looking — but not *what* it is doing with that information. The saliency maps for classifying an image as "Siberian husky" can look essentially identical to those for "transverse flute." Showing explanations only for the correct class, as is common practice, creates a false sense of confidence.

**Black boxes invite human error.** COMPAS requires over 130 input factors. If data entry errors occur at a rate of just 1%, more than one in every two surveys will contain at least one mistake. These errors can directly determine bail or parole outcomes — a form of procedural unfairness that a simpler model would avoid entirely.

---

## Interpretable models can match black box performance

One of the paper's most compelling contributions is a concrete demonstration. The CORELS algorithm (Certifiably Optimal Rule Lists) produces a model for recidivism prediction that uses just three rules based on age, sex, and number of prior offenses. This model matches the accuracy of COMPAS — which uses 130+ factors and is sold as proprietary software.

Similarly, the RiskSLIM algorithm produces scoring systems — sparse linear models with integer coefficients, much like those that physicians have been designing by hand for decades — that are competitive with black box alternatives. An example scoring system for recidivism uses just five binary features and maps to a clear risk percentage.

These are not toy demonstrations. They are full ML models, optimized over hard combinatorial search spaces, that happen to produce outputs humans can read and verify.

---

## Why black boxes persist anyway

If interpretable models can be just as accurate, why do black boxes dominate? Rudin identifies several structural reasons.

**Profit motives.** Proprietary models generate licensing revenue. An interpretable three-rule model has no obvious business model, while a proprietary 130-factor tool can be sold as a software license. The companies profiting from black boxes are not the ones suffering the consequences when those models fail.

**Training gaps.** Researchers are trained in deep learning but rarely in interpretable ML. Toolkits offer little support for building constrained, interpretable models.

**Computational difficulty.** Interpretable models often require solving hard optimization problems — finding the sparsest model that minimizes error is generally NP-hard. But recent algorithmic advances (branch-and-bound, cutting plane methods, specialized bit-vector libraries) have made these problems tractable for many real-world datasets.

**The myth of "hidden patterns."** Because black boxes are hard to build, people assume they must be uncovering deep, subtle patterns that simpler models would miss. But if a pattern is important enough for a black box to leverage it, an interpretable model flexible enough to capture the same structure can often find it too.

---

## The Rashomon set: why interpretable models often exist

Rudin offers an elegant theoretical intuition for why accurate interpretable models tend to exist. For a given dataset, consider the *Rashomon set*: the set of all models whose accuracy is close to optimal. Because data is finite and noisy, this set is often large, containing models with very different functional forms — random forests, neural networks, linear models — that all perform similarly.

If the Rashomon set is large enough and contains sufficiently diverse models, it is likely to include at least some that are simple enough to be interpretable. The uncertainty in the data doesn't just allow for multiple good models; it almost guarantees that some of them will be transparent.

---

## A policy proposal

Rudin ends with a concrete governance suggestion: **for high-stakes decisions, no black box model should be deployed when an interpretable model with the same level of performance exists.** Organizations selling black box models would bear the burden of proof that no equally accurate transparent alternative is available.

A weaker but still useful version: mandate that any organization deploying a black box must also report the accuracy of interpretable alternatives, letting regulators and the public judge whether the complexity is justified.

---

## Why this still matters

Published in 2019, this paper has only grown more relevant. As ML systems proliferate into healthcare, criminal justice, finance, and climate science, the consequences of opaque decision-making compound. The EU's AI Act, debates around algorithmic accountability, and the growing use of large language models all raise the same fundamental question Rudin posed: when the stakes are high, do we really need a model we can't understand?

Her answer is clear. In most cases, no. The interpretable model exists. We just need to invest the effort to find it.

---

*Reference: Rudin, C. (2019). Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead. Nature Machine Intelligence, 1, 206–215.*
