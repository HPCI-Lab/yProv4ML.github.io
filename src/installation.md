
# Installation

Install from the repository:

```bash
git clone https://github.com/HPCI-Lab/yProvML.git
cd yProvML

pip install -r requirements.txt
pip install .

# Or use apple extra if on a Mac
pip install .[apple]

# or install for specific arch
pip install .[nvidia] # or .[amd]
```

or simply:

```bash
pip install --no-cache-dir git+https://github.com/HPCI-Lab/yProvML
```

To install a specific branch of the library: 

```bash
git clone https://github.com/HPCI-Lab/yProvML.git
cd yProvML

git switch development # or any other branch

pip install -r requirements.txt
pip install .
```


[Home](README.md) | [Next](setup.md)