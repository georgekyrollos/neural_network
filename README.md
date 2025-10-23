# Neural Network

This README uses GitHub‑compatible MathJax. Inline math like $a^{(\ell)}$ and display blocks using `$$ ... $$` will render on GitHub.

## Notation

- Layer index: $\ell \in \{1,\dots,L\}$.
- Activations: $a^{(\ell)} \in \mathbb{R}^{N_\ell}$.
- Pre‑activations (weighted sums): $z^{(\ell)} \in \mathbb{R}^{N_\ell}$.
- Biases: $b^{(\ell)} \in \mathbb{R}^{N_\ell}$.
- Weights: $W^{(\ell)} \in \mathbb{R}^{N_\ell \times N_{\ell-1}}$.
- Activation function (example sigmoid): $\sigma(x) = \frac{1}{1 + e^{-x}}$.

## Forward Propagation

For layer $\ell = 1, \dots, L$:
$$
z^{(\ell)} \;=\; b^{(\ell)} \;+\; W^{(\ell)}\, a^{(\ell-1)},
\qquad
a^{(\ell)} \;=\; \sigma\!\big(z^{(\ell)}\big).
$$

Component‑wise for neuron $n$ in layer $\ell$:
$$
z^{(\ell)}_{n} \;=\; b^{(\ell)}_{n} \;+\; \sum_{k=1}^{N_{\ell-1}} W^{(\ell)}_{nk}\, a^{(\ell-1)}_{k}.
$$

## Loss (Squared Error Example)

For a single example with target $y \in \mathbb{R}^{N_L}$:
$$
C \;=\; \sum_{n=1}^{N_L} \big(a^{(L)}_{n} - y_n\big)^2 \;=\; \| a^{(L)} - y \|_2^2.
$$

## Gradient Descent Update

Let $\alpha$ be the learning rate. One step of gradient descent:
$$
W^{(\ell)} \leftarrow W^{(\ell)} \;-\; \alpha \,\frac{\partial C}{\partial W^{(\ell)}},
\qquad
b^{(\ell)} \leftarrow b^{(\ell)} \;-\; \alpha \,\frac{\partial C}{\partial b^{(\ell)}}.
$$

(Backprop gives the exact partial derivatives; notation here is kept conventional with $W$, *not* $\Omega$.)

## Sigmoid and Its Derivative (Example)

$$
\sigma(x) \;=\; \frac{1}{1 + e^{-x}}, 
\qquad
\sigma'(x) \;=\; \sigma(x)\,\big(1 - \sigma(x)\big).
$$

## (Optional) Low‑Rank Compression via SVD

Given $W^{(\ell)} \in \mathbb{R}^{m\times n}$ with SVD $W^{(\ell)} = U\Sigma V^{\!\top}$, a rank‑$k$ approximation is
$$
W^{(\ell)} \approx U_{[:,1:k]}\,\Sigma_{1:k,1:k}\,V_{[:,1:k]}^{\!\top}.
$$

Multiplying $a$ by the compressed factorization can reduce cost:
$$
a\,V^{\!\top}\Sigma U^{\!\top}:\; O(nk + k^2 + mk)\quad \text{when } k \ll \min\{m,n\}.
$$

---

### Tips

- Use inline math `$...$` for short expressions and `$$...$$` for display equations.
- Avoid HTML like `<sub>...</sub>`; prefer LaTeX: `a_{k}`, `W^{(\ell)}`.
- If pasting equations into Jupyter Markdown, `$$...$$` also renders nicely.
