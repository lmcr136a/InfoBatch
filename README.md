<h2 align="center">Nahyeon Kim - InfoBatch Experiments</h2>

## Install

To start, please install InfoBatch via
```bash
pip install git+https://github.com/NUS-HPC-AI-Lab/InfoBatch
```

Or you can clone this repo and install it locally.
```bash
git clone https://github.com/lmcr136a/InfoBatch
cd InfoBatch
pip install -e .
```

## Experiments

To replicate the experiment in the paper, I conducted experiments with the following setup. Additionally, I conducted full batch experiments using the same configurations to compare the accuracy and running time with the baseline. The summary of the results is provided below.

| Dataset   | Model     | Batch                   | Test Acc | Total Training Time  | Total saved sample forwarding  |
|-----------|-----------|-------------------------|----------|----------------------|--------------------------------|
| CIFAR-100 | ResNet-50 | Full Batch (Baseline)   |  81.1%   |  7hour 22min         |      0                         |
| CIFAR-100 | ResNet-50 | InfoBatch               |  80.9%   |  5hour 32min         |      3085267                   |
| CIFAR-100 | ResNet-18 | Full Batch (Baseline)   |  81.1%   |  7hour 22min         |      0                         |
| CIFAR-100 | ResNet-18 | InfoBatch               |  80.9%   |  5hour 32min         |      3085267                   |
| CIFAR-10  | ResNet-18 | Full Batch (Baseline)   |  81.1%   |  7hour 22min         |      0                         |
| CIFAR-10  | ResNet-18 | InfoBatch               |  80.9%   |  5hour 32min         |      3085267                   |

For the CIFAR-100 / ResNet-50 experiments, the results of the InfoBatch can be found in Figure 3 -(a) in the paper. I conducted the experiment using the optimal parameter proposed by the paper, 𝑟=50, and my result was similar to the accuracy of approximately 81 reported in the figure. While the accuracy of the baseline and InfoBatch are similar, InfoBatch reduced the number of samples and the time required for the experiment.

For experiments with ResNet-18, Table 1 in the paper shows the accuracy of InfoBatch, 95.1% and 78.1%, with CIFAR-10 and CIFAR-100 respectively. I also used 𝑟=50, and my results were similar to the accuracy reported in the table above.

### To execute each experiment, run the following code in the terminal.

To run the CIFAR-100 / ResNet-50 experiment:
```bash
# Full Batch (Baseline)
python3 examples/cifar_example.py --model r50 --optimizer lars --max-lr 5.2 --delta 0.0

# InfoBatch
python3 examples/cifar_example.py --model r50 --optimizer lars --max-lr 5.2 --delta 0.875 --ratio 0.5 --use_info_batch
```

To run the CIFAR-100 / ResNet-18 experiment:
```bash
# Full Batch (Baseline)
python3 examples/cifar_example.py --model r18 --optimizer lars --max-lr 5.2 --delta 0.0

# InfoBatch
python3 examples/cifar_example.py --model r18 --optimizer lars --max-lr 5.2 --delta 0.875 --ratio 0.5 --use_info_batch
```

To run the CIFAR-10 / ResNet-18 experiment:
```bash
# Full Batch (Baseline)
python3 examples/cifar_example_cifar10.py --model r18 --optimizer lars --max-lr 5.2 --delta 0.0

# InfoBatch
python3 examples/cifar_example_cifar10.py --model r18 --optimizer lars --max-lr 5.2 --delta 0.875 --ratio 0.5 --use_info_batch
```
