# PointNet: *Deep Learning on Point Sets for 3D Classification*

## Installation
### Linux
Install poetry:
```shell
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python -
```
Install pyenv and install python 3.7.9
```shell
sudo apt install pyenv
pyenv install 3.7.9
```
Inside the repo folder install the python environment
```shell
pyenv local 3.7.9
poetry install
```
### Windows PowerShell
Install poetry:
```ps
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py -UseBasicParsing).Content | python -
```
Download and install Python 3.7.9 from the [Official Site](https://www.python.org/downloads/release/python-379/)

Inside the repo folder install the python environment
```ps
poetry install
```
### UB CCR
There is no preconfiguration or installation needed. Just copy the folder into CCR using scp
```shell
scp -r pointnet {username}@transfer.ccr.buffalo.edu:
```
## Usage
### Linux/Windows
Activate the environment
```shell
poetry shell
```
To train a model to classify point clouds sampled from 3D shapes:
```shell
python train.py
```
Log files and network parameters will be saved to `log` folder in default. Point clouds of <a href="http://modelnet.cs.princeton.edu/" target="_blank">ModelNet40</a> models in HDF5 files are already present in the `data` folder. Each point cloud contains 2048 points uniformly sampled from a shape surface. Each cloud is zero-mean and normalized into an unit sphere. There are also text files in `data/modelnet40_ply_hdf5_2048` specifying the ids of shapes in h5 files.

To see HELP for the training script:
```shell
python train.py -h
```
We can use TensorBoard to view the network architecture and monitor the training progress.
```shell
tensorboard --logdir log
```
After the above training, we can evaluate the model and output some visualizations of the error cases.
```shell
python evaluate.py --visu
```
Point clouds that are wrongly classified will be saved to `dump` folder in default. We visualize the point cloud by rendering it into three-view images.

### UB CCR
A slurm script is provided which runs the training. To schedule your job on CCR just run
```shell
sbatch slurm.sh
```

## Citation
    @article{qi2016pointnet,
      title={PointNet: Deep Learning on Point Sets for 3D Classification and Segmentation},
      author={Qi, Charles R and Su, Hao and Mo, Kaichun and Guibas, Leonidas J},
      journal={arXiv preprint arXiv:1612.00593},
      year={2016}
    }
