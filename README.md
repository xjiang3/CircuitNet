# CircuitNet 2.0: An Advanced Dataset for Promoting Machine Learning Innovations in Realistic Chip Design Environment

This repository is intended to hosts codes for the review process of CircuitNet 2.0.

## Prerequisites

Dependencies can be installed using pip:

```sh
pip install -r requirements.txt
```

PyTorch is not included in requirement.txt, and you could install it following the instruction on PyTorch homepage [https://pytorch.org/](https://pytorch.org/).

DGL is also not included in requirement.txt, and it is required for net delay prediction only. You could install it following the instruction on DGL homepage [https://www.dgl.ai/pages/start.html](https://www.dgl.ai/pages/start.html).

Our experiments run on Python 3.9 and PyTorch 1.11. Other versions should work but are not tested.

## Congestion, DRC, IR drop prediction

### Data Preparation
Dataset Link: https://drive.google.com/drive/folders/1gdV8cKMFQHwuzOw2qu-ORPA9wyt2lmJc?usp=drive_link

### Example Usage:

**Change the configure in [utils/config.py](utils/configs.py) to fit your file path and adjust hyper-parameter before starting.**

#### Test

##### Congestion

```python
python test.py --task congestion_gpdl --pretrained PRETRAINED_WEIGHTS_PATH
```

##### DRC

```python
python test.py --task drc_routenet --pretrained PRETRAINED_WEIGHTS_PATH --save_path work_dir/drc_routenet/ --plot_roc 
```

##### IR Drop

```python
python test.py --task irdrop_mavi --pretrained PRETRAINED_WEIGHTS_PATH --save_path work_dir/irdrop_mavi/ --plot_roc
```

#### Train

##### Congestion

```python
python train.py --task congestion_gpdl --save_path work_dir/congestion_gpdl/
```

##### DRC

```python
python train.py --task drc_routenet --save_path work_dir/drc_routenet/
```

##### IR Drop

```python
python train.py --task irdrop_mavi --save_path work_dir/irdrop_mavi/
```

## Net Delay prediction (DGL required)

### Data Preparation

Graphs for net delay prediction can be built with the following script:

```python
python build_graph.py --data_path DATA_PATH --save_path ./graph
```
where DATA_PATH is the path to the parent dir of the timing features: nodes, net_edges and pin_positions.

### Train

```python
python train.py --checkpoint CHECKPOINT_NAME
```
where CHECKPOINT_NAME is the name of the dir for saving checkpoint.
### Test

```python
python train.py --checkpoint CHECKPOINT_NAME --test_iter TEST_ITERATION
```
where TEST_ITERATION is the specific iteration for testing, corresponding to the saved checkpoint file name.

## License

This repository is released under the BSD 3-Clause. license as found in the LICENSE file.
