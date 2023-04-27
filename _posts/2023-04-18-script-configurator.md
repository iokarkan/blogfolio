---
layout: post
title: "\"Poor Man's Configurator\": An unorthodox way to config your scripts by A. Karpathy"
tags: python development
---

As an AI language mod- (kidding) Python script-kiddie, I know how managing configurations can become quite complicated when dealing with large projects. Hell, even exploratory tuning of small scripts (that you 100% wrote yourself without overnight assistance from AI elves) doesn't take too long to bloat. While looking into all the craze that I have missed during these hectic months, a time when we were running out of exotic animals to name our AI models, I stumbled upon a clever way to simplify configuration management - authored by none other than [Andrej Karpathy](https://karpathy.ai/), Sr. Director of Tesla Motors. 

I briefly present and describe the usage of configurator.py and compare it with other methods like Python's argparse and using a config class. Readers are invited to let me know of other hacky setups that they've come to prefer.

## nanoGPT's Configuration Scheme

Around three months ago, at the time of writing, Dr. Karpathy went educationally viral with his from-scratch implementation of [`nanoGPT`](https://github.com/karpathy/nanoGPT), a pure-PyTorch (+numpy) implementation of the Deep Learning Transformer decoder model architecture from the seminal paper [Attention Is All You Need](https://arxiv.org/abs/1706.03762) by a(mostly) Google team.

[`configurator.py`](https://github.com/karpathy/nanoGPT/blob/master/configurator.py) is a lightweight solution that abstracts the configuration set-up process for a main file, such as the LLM evaluation script `sample.py`, or the training script `train.py` of the repository. The key benefit of using configurator.py is that it simplifies the configuration process and allows easy overriding of variables through command-line arguments or configuration files.

```python
"""
Poor Man's Configurator. Probably a terrible idea. Example usage:
$ python train.py config/override_file.py --batch_size=32
this will first run config/override_file.py, then override batch_size to 32

The code in this file will be run as follows from e.g. train.py:
>>> exec(open('configurator.py').read())

So it's not a Python module, it's just shuttling this code away from train.py
The code in this script then overrides the globals()

I know people are not going to love this, I just really dislike configuration
complexity and having to prepend config. to every single variable. If someone
comes up with a better simple Python solution I am all ears.
"""
import sys
from ast import literal_eval

for arg in sys.argv[1:]:
    if '=' not in arg:
        # assume it's the name of a config file
        assert not arg.startswith('--')
        config_file = arg
        print(f"Overriding config with {config_file}:")
        with open(config_file) as f:
            print(f.read())
        exec(open(config_file).read())
    else:
        # assume it's a --key=value argument
        assert arg.startswith('--')
        key, val = arg.split('=')
        key = key[2:]
        if key in globals():
            try:
                # attempt to eval it it (e.g. if bool, number, or etc)
                attempt = literal_eval(val)
            except (SyntaxError, ValueError):
                # if that goes wrong, just use the string
                attempt = val
            # ensure the types match ok
            assert type(attempt) == type(globals()[key])
            # cross fingers
            print(f"Overriding: {key} = {attempt}")
            globals()[key] = attempt
        else:
            raise ValueError(f"Unknown config key: {key}")
```

Implementation is simple. Within the main script files, for example `sample.py`, we encounter the following one-liner:

```python
exec(open('configurator.py').read()) # overrides from command line or config file
```

Thus, a command will have to look something like this:
```python
python train.py config/train_shakespeare_char.py \
    --device=cpu --compile=False --eval_iters=20 \
    --log_interval=1 --block_size=64 --batch_size=12 \
    --n_layer=4 --n_head=4 --n_embd=128 --max_iters=2000 \
    --lr_decay_iters=2000 --dropout=0.0
```

Importantly, it distinguishes between configuration files and \--key=value arguments. Thus, it's easier to manage and override configurations. There's no need to define every argument explicitly like in argparse or a configuration dictionary/class. The key feature of this configuration, in my opinion, is that it combines multi-level modularity in the parameters declared (script-level < config-level < command-level). It allows for easy overriding of variables through command-line arguments or configuration files, providing un-cluttered distributed flexibility.

Much like having an imported `Config` python Class, we achive less clutter in the main file, making it easier to understand and maintain. The added benefit is that one does not instead have to prepend the `config` instance name before calling an 
attribute, let alone defining new attributes in the first place. You can override any global variable already defined before the `exec` line.

Here's a side-by-side comparison of the three:

### Argparse - within script

```python
# sample.py
import argparse
parser = argparse.ArgumentParser(description="Training script")
parser.add_argument("--device", type=str, default="cpu", help="Device to use for training")
parser.add_argument("--compile", type=bool, default=False, help="Whether to compile the model")
args = parser.parse_args()
device = args.device
compile = args.compile
```
### Config Class

```python
# config.py
class Config:
    def __init__(self):
        self.device = "cpu"
        self.compile = False
```
```python
# sample.py
from config import Config
config = Config()
config.device = "cuda"
config.compile = True
```

### Configurator
```python
# configurator.py - a file you never have to touch
```
```python
# config.py
device = 'cuda'
compile = True
```
```python
# sample.py
device = 'cpu'
compile = False
exec(open('configurator.py').read()) # overrides from command line or config file
```

I hope I'm not so totally blind-sided by my admiration of Karpathy that I end up failing to notice some glaring flaw or not playing fair game, and I do believe that it's his humble nature that leads him to concede the possibility of it being a "terrible idea". But I do indeed find it the cleanest solution for such a level of overridability, at least in these non production-grade situations. Alas, it's these little original gems that one finds in cutting-edge demos that make it worth debating over even the most basic of habits!