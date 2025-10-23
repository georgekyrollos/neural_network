# Neural Network Notes — Clean LaTeX Rendering

This README uses **only** `$...$` for inline math and `$$...$$` for display equations so it renders on GitHub and most Markdown viewers.

## Notation

- Layer index: $\ell \in \{1,\dots,L\}$
- Activations: $a^{(\ell)} \in \mathbb{R}^{N_{\ell}}$
- Pre-activations (weighted sums): $z^{(\ell)} \in \mathbb{R}^{N_{\ell}}$
- Biases: $b^{(\ell)} \in \mathbb{R}^{N_{\ell}}$
- Weights: $W^{(\ell)} \in \mathbb{R}^{N_{\ell} \times N_{\ell-1}}$
- Example activation: $\sigma(x) = \frac{1}{1 + e^{-x}}$

## Forward Propagation

For layer $\ell = 1,\dots,L$:

$$
z^{(\ell)} = b^{(\ell)} + W^{(\ell)}\,a^{(\ell-1)},
\qquad
a^{(\ell)} = \sigma\!\big(z^{(\ell)}\big).
$$

Component-wise for neuron $n$ in layer $\ell$:

$$
z^{(\ell)}_{n} = b^{(\ell)}_{n} + \sum_{k=1}^{N_{\ell-1}} W^{(\ell)}_{nk}\,a^{(\ell-1)}_{k}.
$$

## Loss (Squared Error)

For one example with target $y \in \mathbb{R}^{N_{L}}$:

$$
C = \sum_{n=1}^{N_{L}} \big(a^{(L)}_{n} - y_{n}\big)^{2} = \lVert a^{(L)} - y \rVert_{2}^{2}.
$$

## Gradient Descent Updates

Let $\alpha$ be the learning rate. One step of gradient descent:

$$
W^{(\ell)} \leftarrow W^{(\ell)} - \alpha \,\frac{\partial C}{\partial W^{(\ell)}}, 
\qquad
b^{(\ell)} \leftarrow b^{(\ell)} - \alpha \,\frac{\partial C}{\partial b^{(\ell)}}.
$$

> Note: Using $W$ (not $\Omega$) and superscripted layer indices is the standard convention.

## Sigmoid (Example) and Derivative

$$
\sigma(x) = \frac{1}{1 + e^{-x}}, 
\qquad 
\sigma'(x) = \sigma(x)\,\big(1 - \sigma(x)\big).
$$

## Optional: Low-Rank Compression via SVD

Given $W^{(\ell)} \in \mathbb{R}^{m \times n}$ with SVD $W^{(\ell)} = U \Sigma V^{\top}$, a rank-$k$ approximation is:

$$
W^{(\ell)} \approx U_{[:,1\!:\!k]}\,\Sigma_{1\!:\!k,\,1\!:\!k}\,V_{[:,1\!:\!k]}^{\top}.
$$

Multiplying by the factorization reduces cost when $k \ll \min\{m,n\}$:

$$
a\,V^{\top}\Sigma\,U^{\top} :\; \mathcal{O}(nk + k^{2} + mk).
$$

---

### Rendering Checklist (if you still see raw LaTeX)
- Ensure you are viewing this on GitHub (which supports math) or in a Markdown viewer with math enabled.
- Do **not** wrap math inside backticks. Code spans like `` `\frac{1}{2}` `` will not render as math.
- Keep inline math on one line (no newlines inside `$...$`).
- Use ASCII characters only in math (e.g., `\Sigma` not `Σ`, `\ell` not `ℓ`).
- Leave a blank line before and after each `$$` display block.

