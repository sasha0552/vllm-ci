# vllm-ci

CI scripts designed to build a Pascal-compatible version of vLLM and Triton.

## Installation

### [vllm](https://github.com/vllm-project/vllm)

*Note: this repository holds "nightly" builds of `vLLM`, which may have the same `vLLM` version between releases in this repository, but have different source code. Despite the fact that they are "nightly", they are generally stable.*

*Note: the `vllm` command is an alias for the `python3 -m vllm.entrypoints.openai.api_server` command.*

*Note: kernels for all GPUs except Pascal have been excluded to reduce build time and wheel size. You can still use the new GPUs using tensor parallelism with Ray (and using two instances of `vLLM`, one of which will use upstream `vLLM`). Complain in [issues](https://github.com/sasha0552/vllm-ci/issues) if it disrupts your workflow.*

To install the patched `vLLM` (the patched `triton` will be installed automatically):
```sh
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate

# Install vLLM
pip3 install --extra-index-url https://sasha0552.github.io/vllm-ci/ vllm

# Launch vLLM
vllm --help
```

To update a patched `vLLM` between same `vLLM` release versions (e.g. `0.5.0` (commit `000000`) -> `0.5.0` (commit `ffffff`))
```sh
# Activate virtual environment
source venv/bin/activate

# Update vLLM
pip3 install --force-reinstall --extra-index-url https://sasha0552.github.io/vllm-ci/ --no-cache-dir --no-deps --upgrade vllm
```

### [aphrodite-engine](https://github.com/PygmalionAI/aphrodite-engine)

To install `aphrodite-engine` with the patched `triton`:
```sh
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate

# Install aphrodite-engine
pip3 install --extra-index-url https://sasha0552.github.io/vllm-ci/ --extra-index-url https://downloads.pygmalion.chat/whl aphrodite-engine

# Launch aphrodite-engine
aphrodite --help
```

In other words, add `--extra-index-url https://sasha0552.github.io/vllm-ci/` to the original installation command.

### [triton](https://github.com/triton-lang/triton)

To install the patched `triton` separately, for use in other applications (for example, Stable Diffusion WebUIs):

*Note that this will install `triton==2.3.0` (for `torch==2.3.0`)! If you need other versions of `triton`, check out my other repo - [triton-ci](https://github.com/sasha0552/triton-ci). I plan to publish it on PyPI as soon as the [file size limit increase request](https://github.com/pypi/support/issues/4295) is approved.*

Install application that published on PyPI and depends on `triton`:
```sh
# Install triton
pip3 install --extra-index-url https://sasha0552.github.io/vllm-ci/ <PACKAGE NAME>
```

Install `triton` before installing application:
```sh
# Install triton
pip3 install --extra-index-url https://sasha0552.github.io/vllm-ci/ triton
```

If application is already installed:
```sh
# Install triton
pip3 install --index-url https://sasha0552.github.io/vllm-ci/ --force-reinstall --no-deps triton
```

*Don't forget to activate the virtual environment (if necessary) before performing actions!*
