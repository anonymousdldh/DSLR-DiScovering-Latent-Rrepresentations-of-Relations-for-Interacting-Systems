# DiScovering Latent Rrepresentations of Relations for Interacting Systems

This work is now reviewed on ICML 2021. 

This repo contains the code for **DiScovering Latent Rrepresentations of Relations for Interacting Systems**. We generated our code based on https://github.com/MilesCranmer/symbolic_deep_learning. 

## Requirements
* python 3.7
* pytorch-geometric (https://pytorch-geometric.readthedocs.io/en/latest/notes/installation.html)
* jax (https://github.com/google/jax#installation)

## Data generation
### Physically simulated data
We performed expriments with physics data with 7 combinations of 3 relations (spring, r_1, none). The list of datasets is as following, and can be seen in *src/datasets_list.py*:

```
spring_None
spring_r1
r1_None
spring_r1_None
spring4
spring100
spring100_r1100
```

The details of each are explained in the experiment section in our paper. To generate the data:

```
python data_generator.py --sim [name of data]
```

For example, to generate *spring_None*, execute ```python data_generator.py --sim spring_None``` The generated data is in *data* directory.

### CMU mocap data
We have prepared the CMU mocap data for our model in advance that can be found in *data* directory. Details of CMU mocap data is on http://mocap.cs.cmu.edu/.

## Train
To train the model with physics data:

```
python -m trainer.train --train_name [any name] --seed [seed] --dataset [data to use]
```

For example, to train the model with *spring_None* data, execute ```python -m trainer.train --train_name train0 --seed 0 --dataset spring_None```

To train the model with CMU mocap data:

```
python -m trainer.train --train_name [any name] --seed [seed] --dataset cmu_walking --connection-value --sparsity-prior 0.91 --batch-size 4 --epochs 2000 --gpu 1 --msg-dim 3 --n-relation-STD 1
```

The model will be saved in *models* directory.

## Test
To test the model:

```
python -m tester.test
```

The given arguments must be same as training. The results will be saved in *results* directory.

