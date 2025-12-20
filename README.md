# scENV
单细胞转录组相关分析工具安装流程
## scanpy

```
mamba create -n scanpy conda-forge:scanpy=1.11.5 -y

mamba activate scanpy
mamba install ipykernel -y

# 为了联合使用R
mamba install -c bioconda anndata2ri -y

# 为了聚类
mamba install conda-forge:python-igraph -y
```

## scvi-tools

```
mamba create -n scvi-tools conda-forge:scvi-tools=1.4.1 conda-forge:scanpy=1.11.5 -y

mamba activate scvi-tools
mamba install ipykernel -y
```

## pertpy

```
mamba create -n pertpy conda-forge:pertpy=1.0.4 conda-forge:scanpy=1.11.5 python=3.13 -y

mamba activate pertpy
mamba install ipykernel -y

# 为了进行差异分析
pip install 'pertpy[de]'

# 为了用edger
mamba install conda-forge::rpy2 -y

# 为了使用tcoda
mamba install schrodinger::pyqt6 -y
pip install 'pertpy[tcoda]'


```

## TDEseq

```
mamba create -n TDEseq r::r-devtools -y

mamba activate TDEseq
mamba install r::r-coneproj -y
mamba install r::r-matrix -y

R
library(devtools)
install_github("Efdix/TDEseq", force=TRUE)

mamba install r-irkernel -y
```

## sc_tools

```
mamba create -n sc_tools conda-forge:scanpy=1.11.5 -y

mamba activate sc_tools

# 细胞比例工具
module purge;module load compiler/gcc/9.3.0 #gcc版本不对导致pip连一些基础的东西都装不上
pip install scanpro

mamba install ipykernel -y
```

## scikit-bio

```
mamba create -n scikit-bio conda-forge:scikit-bio conda-forge:scanpy=1.11.5 -y

mamba activate scikit-bio
mamba install ipykernel -y
```

## cellphonedb

```
mamba create -n cpdb scanpy=1.11.5 -y

mamba activate cpdb
module purge;module load compiler/gcc/9.3.0
pip install cellphonedb

# 下载数据库
# https://github.com/ventolab/cellphonedb-data # v5.0.0
# 存储路径：/work/home/acfrxahp1e/software/cpdb


```

## celltypist

```
mamba create -n celltypist -c bioconda -c conda-forge celltypist scanpy=1.11.5 -y
mamba activate celltypist

# 下载数据库，其实也可以手动下，默认存储在家目录下
python
import celltypist
from celltypist import models
models.download_models()

mamba install ipykernel -y
```

## Jupyter Notebook

```
./miniforge3/bin/conda init

conda activate pertpy
python -m ipykernel install --name pertpy --display-name pertpy
conda deactivate

conda activate omicverse
python -m ipykernel install --name omicverse --display-name omicverse
conda deactivate

conda activate scanpy
python -m ipykernel install --name scanpy --display-name scanpy
conda deactivate

conda activate sc_tools
python -m ipykernel install --name sc_tools --display-name sc_tools
conda deactivate

conda activate scikit-bio
python -m ipykernel install --name scikit-bio --display-name scikit-bio
conda deactivate

conda activate celltypist
python -m ipykernel install --name celltypist --display-name celltypist
conda deactivate

conda activate TDEseq
R
IRkernel::installspec(name='TDEseq', displayname='TDEseq')
quit()
n
conda deactivate

conda activate Seurat5
R
IRkernel::installspec(name='Seurat5', displayname='Seurat5')
quit()
n
conda deactivate
```

