# Neural Networks: Zero to Hero — Study Implementations

A hands-on deep-learning study repository based on Andrej Karpathy's [Neural Networks: Zero to Hero](https://karpathy.ai/zero-to-hero.html) course. It documents my implementation-first path from automatic differentiation to character-level language models and a decoder-only Transformer.

The notebooks contain my code, derivations, debugging notes, and experiment observations. This is a learning portfolio rather than an original framework or a production-ready GPT implementation.

## Highlights

- Built a small scalar-valued autograd engine with computation-graph visualization, reverse-mode differentiation, neural-network modules, and gradient-descent training.
- Implemented character-level language models over a names dataset, progressing from bigram counts to MLPs, batch normalization, manual backpropagation, and a hierarchical WaveNet-style architecture.
- Built a character-level, decoder-only Transformer in PyTorch: token/position embeddings, masked self-attention, multi-head attention, feed-forward layers, residual connections, layer normalization, dropout, and autoregressive text generation.
- Kept notebooks as an interview-reference trail: design choices, tensor shapes, mathematical intuition, implementation details, and training observations are captured alongside the code.

## Learning path and repository guide

| Module | What is implemented | Key concepts |
| --- | --- | --- |
| [`src/01-autograder/`](src/01-autograder/) | A micrograd-style scalar autograd engine and a small MLP trained from scratch. | Computation graphs, chain rule, backward pass, gradient descent, `torch.nn` comparison |
| [`src/02-makemore/`](src/02-makemore/) | Character-level name generation, from a bigram baseline through MLP and WaveNet-style models. | Maximum likelihood, embeddings, initialization, BatchNorm, activation/gradient diagnostics, manual backpropagation, hierarchical context compression |
| [`src/03-gpt/`](src/03-gpt/) | A progressively built, character-level GPT-style language model. | Tokenization, batching, causal masks, Q/K/V attention, multi-head attention, residual blocks, LayerNorm, dropout, scaling |
| [`src/04-reproduce-gpt2/`](src/04-reproduce-gpt2/) | Placeholder for future work. | Planned: GPT-2 reproduction |

## Notebook roadmap

### 1. Autograd and neural-network foundations

[`01-autograder.ipynb`](src/01-autograder/01-autograder.ipynb) implements a `Value` object that records scalar operations, constructs a computation graph, and propagates gradients with reverse-mode autodiff. It then builds `Neuron`, `Layer`, and `MLP` abstractions before comparing the ideas with PyTorch autograd.

### 2. Makemore: character-level name generation

- [`01-bigram.ipynb`](src/02-makemore/01-bigram.ipynb): count-based and neural bigram language models; likelihood, log-likelihood, and sampling.
- [`02-0-MLP.ipynb`](src/02-makemore/02-0-MLP.ipynb) and [`02-1-MLP-recap.ipynb`](src/02-makemore/02-1-MLP-recap.ipynb): embeddings and multi-layer perceptrons for larger character context.
- [`03-00-Enhanced-MLP.ipynb`](src/02-makemore/03-00-Enhanced-MLP.ipynb) and [`03-01-enhanced-MLP.ipynb`](src/02-makemore/03-01-enhanced-MLP.ipynb): initialization, tanh saturation, BatchNorm, and activation/gradient analysis.
- [`04-backprop-drill.ipynb`](src/02-makemore/04-backprop-drill.ipynb): manual derivatives for the full MLP and a check against PyTorch autograd.
- [`05-wavenet.ipynb`](src/02-makemore/05-wavenet.ipynb): custom layers and a WaveNet-inspired hierarchical architecture for increasing receptive field efficiently.

### 3. GPT: build a decoder-only Transformer

- [`01-bigram.ipynb`](src/03-gpt/01-bigram.ipynb): a PyTorch bigram baseline trained on character-level text.
- [`02-0-self-attention-background.ipynb`](src/03-gpt/02-0-self-attention-background.ipynb) and [`02-1-single-head-self-attention.ipynb`](src/03-gpt/02-1-single-head-self-attention.ipynb): causal masking and single-head self-attention.
- [`03-multi-head-attention.ipynb`](src/03-gpt/03-multi-head-attention.ipynb): multi-head attention and feed-forward layers.
- [`04-block-optimization.ipynb`](src/03-gpt/04-block-optimization.ipynb): Transformer blocks with residual connections and LayerNorm.
- [`05-scale-up.ipynb`](src/03-gpt/05-scale-up.ipynb): a larger GPT-style configuration with stacked blocks and dropout.

## Run the notebooks locally

The included Docker environment provides Python 3.12, PyTorch, JupyterLab, and supporting packages.

```bash
docker build -t zero-to-hero .
docker run --rm -it -p 8888:8888 \
  -v "$PWD/src":/usr/local/app/src \
  zero-to-hero
```

Open the JupyterLab URL printed in the terminal (normally `http://localhost:8888/lab?token=...`). The `src/` directory is mounted into the container, so notebook edits persist locally.

## Tech stack

- Python 3.12
- PyTorch and torchvision
- NumPy, Matplotlib, Pandas, and Seaborn
- JupyterLab
- Docker

CUDA is used automatically when it is available; the notebooks also fall back to CPU. Larger Transformer configurations are considerably more practical on a GPU.

## Attribution

The curriculum, exercise structure, and much of the instructional material are based on Andrej Karpathy's **Neural Networks: Zero to Hero** course. This repository is my personal implementation and notes workspace. See [LICENSE](LICENSE) for this repository's license.
