# scENV
单细胞转录组相关分析工具安装流程

------

## Python

### scanpy

```
mamba create -n scanpy conda-forge:scanpy=1.11.5 -y

mamba activate scanpy
mamba install ipykernel -y

# 为了联合使用R
mamba install -c bioconda anndata2ri -y

# 为了聚类
mamba install conda-forge:python-igraph -y
```

```
./miniforge3/bin/conda init

conda activate scanpy
python -m ipykernel install --name scanpy --display-name scanpy
conda deactivate
```

### scvi-tools

```
mamba create -n scvi-tools conda-forge:scvi-tools=1.4.1 conda-forge:scanpy=1.11.5 -y

mamba activate scvi-tools
mamba install ipykernel -y
```

### pertpy

```
mamba create -n pertpy conda-forge:pertpy=1.0.4 conda-forge:scanpy=1.11.5 python=3.13 -y

mamba activate pertpy
mamba install ipykernel -y

# 为了进行差异分析
pip install 'pertpy[de]'
pip install pydeseq2

# 为了用edger
mamba install conda-forge::rpy2 -y

# 为了使用tcoda
mamba install schrodinger::pyqt6 -y
pip install 'pertpy[tcoda]'
```

```
./miniforge3/bin/conda init

conda activate pertpy
python -m ipykernel install --name pertpy --display-name pertpy
conda deactivate
```

### pertpy (VS Code)

```
mamba create -n pertpy conda-forge:scanpy=1.11.5 python=3.13 -y

mamba activate pertpy
pip install scikit-misc
pip install pertpy
pip install pydeseq2
```

### scanpro

```
mamba create -n scanpro conda-forge:scanpy=1.11.5 -y

mamba activate scanpro

# 细胞比例工具
module purge;module load compiler/gcc/9.3.0 #gcc版本不对导致pip连一些基础的东西都装不上
pip install scanpro

mamba install ipykernel -y
```

```
./miniforge3/bin/conda init

conda activate scanpro
python -m ipykernel install --name scanpro --display-name scanpro
conda deactivate
```

### scikit-bio

```
mamba create -n scikit-bio conda-forge:scikit-bio conda-forge:scanpy=1.11.5 -y

mamba activate scikit-bio
mamba install ipykernel -y
```

```
./miniforge3/bin/conda init

conda activate scikit-bio
python -m ipykernel install --name scikit-bio --display-name scikit-bio
conda deactivate
```

### cellphonedb

```
mamba create -n cpdb scanpy=1.11.5 -y

mamba activate cpdb
module purge;module load compiler/gcc/9.3.0
pip install cellphonedb


# 下载数据库，注意要解压后其中的cellphonedb.zip才是真正的数据库，不能直接用cellphonedb-data-5.0.0.zip
# https://github.com/ventolab/cellphonedb-data # v5.0.0
# 存储路径：/work/home/acfrxahp1e/software/cpdb/db/v5/cellphonedb.zip

mamba install ipykernel -y
```

```
./miniforge3/bin/conda init

conda activate cpdb
python -m ipykernel install --name cpdb --display-name cpdb
conda deactivate
```

### cellphonedb (VS Code)

```
mamba create -n cpdb -c tttpob -c bioconda -c conda-forge cellphonedb=5.0.1 scanpy=1.11.5 -y # Windows下似乎python不能3.14只能3.12

# 下载数据库cellphonedb-data-5.0.0.zip，注意要解压后其中的cellphonedb.zip才是真正的数据库，不能直接用cellphonedb-data-5.0.0.zip
# https://github.com/ventolab/cellphonedb-data # v5.0.0
# 存储路径：D:/System/Documents/GitHub/CellphoneDB/notebooks/data_tutorial/db/v5/cellphonedb.zip

mamba install notebook -c conda-forge -y
mamba install ipykernel -y
```

### celltypist

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

```
./miniforge3/bin/conda init

conda activate celltypist
python -m ipykernel install --name celltypist --display-name celltypist
conda deactivate
```
### base (VS Code)
```
mamba install pandas -y
```

------

## R

### Seurat5

```
mamba create -n Seurat5 conda-forge::r-seurat=5.4.0 -y
mamba activate Seurat5
mamba install r-irkernel -y
mamba install bioconda::bioconductor-scran -y

```

```
./miniforge3/bin/conda init

conda activate Seurat5
R -e "IRkernel::installspec(name = 'Seurat5', displayname = 'Seurat5'" 
```

### Clustree

```
mamba create -n Clustree conda-forge::r-seurat=5.4.0 -y
mamba activate Clustree
mamba install r-irkernel -y

mamba install -c conda-forge r-tweenr r-systemfonts r-ggforce r-graphlayouts r-backports r-ggraph r-checkmate r-viridis r-tidygraph -y

R
install.packages("clustree") #下载时选18合肥线比较顺利
```

```
./miniforge3/bin/conda init

conda activate Clustree
R -e "IRkernel::installspec(name = 'Clustree', displayname = 'Clustree'" 
```

### TDEseq

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

```
./miniforge3/bin/conda init

conda activate TDEseq
R
IRkernel::installspec(name='TDEseq', displayname='TDEseq')
quit()
```

### DeepCellSeek (VS Code)

```
mamba create -n DeepCellSeek
mamba activate DeepCellSeek

mamba install conda-forge::r-devtools -y
mamba install conda-forge::r-tidyverse -y
mamba install -c conda-forge radian -y
mamba install r-irkernel -y

R.exe
devtools::install_github("ZhangLab-Kiz/DeepCellSeek")
quit()

# 为了用notebook，试了下，之后也可以删
mamba install notebook -c conda-forge -y
mamba install r-irkernel -y
```

### r-base (VS Code)

```
mamba create -n r-base conda-forge::r-base=4.5.2 -y
mamba activate r-base

# notebook
mamba install notebook -c conda-forge -y
mamba install r-irkernel -y

mamba install r::r-ggvenndiagram -y
mamba install r::r-patchwork -y
mamba install conda-forge::r-tidyverse -y
mamba install conda-forge::r-eulerr -y
mamba install conda-forge::r-gridextra -y
```

### Enrich (VS Code)

```
mamba create -n Enrich conda-forge::r-base=4.5.2 -y
mamba activate Enrich

# notebook
mamba install notebook -c conda-forge -y
mamba install r-irkernel -y

mamba install conda-forge::r-tidyverse -y

R.exe
install.packages("BiocManager")
BiocManager::install("clusterProfiler")
```



------



## Bash

### OrthoFinder

```
mamba create -n of3_env python=3.10 -y
mamba activate of3_env
mamba install bioconda::orthofinder -y

```



## VS Code

### 自动加载mamba环境

```
# 在 PowerShell 中运行以下命令，查看当前用户的配置文件路径：
$PROFILE
# 使用文本编辑器（如 VS Code 或 Notepad）打开配置文件：
code $PROFILE # D:\System\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
# 在配置文件中添加以下内容：
mamba.exe shell hook -s powershell | Out-String | Invoke-Expression

# 保存并关闭配置文件
# 重新启动 PowerShell
```

## Jupyter

```
jupyter kernelspec list # 查看添加了哪些内核
jupyter kernelspec uninstall xxx -y # 删除xxx内核（注意替换xxx）
```