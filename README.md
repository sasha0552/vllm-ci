# vllm-ci

CI scripts designed to build a Pascal-compatible version of vLLM.

## Installation

### vLLM

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

Note that `vllm` is an alias for `python3 -m vllm.entrypoints.openai.api_server`.

### Triton

To install the patched `triton` separately, for use in other applications:

```sh
# Install triton
pip3 install --extra-index-url https://sasha0552.github.io/vllm-ci/ triton
```

Note that you may need to install triton with `--force-reinstall` if triton has already been installed.
