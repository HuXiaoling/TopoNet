# TopoLoss
This repository contains the implementation of our work "[Topology-Preserving Deep Image Segmentation](https://proceedings.neurips.cc/paper_files/paper/2019/file/2d95666e2649fcfc6e3af75e09f5adb9-Paper.pdf)", **accepted to NeurIPS 2019**. 

Theoretically speaking, the loss function can be incorporated into any suitable framework.
The function is used in PyTorch. And there are two ways to incorporate this loss function into your framework:  
1) Update the total gradient (e.g. cross entropy gradient + lambda * topo gradient) when backpropagation;  
2) Our loss function is actually defined on critical pixels, and you can conduct your total loss (e.g. cross entropy loss + lambda * topo loss) based on the repository. And do the else as usual.

## Content directory
Data/:                                   data folder

Results/:                                storing results

Code/TDFPython/TDFMain.py:               main python script (run it to start), results are all written in Results folder

Code/TDFPython/PersistencePython.so:     persistence code, wrapped as a static library (most likely you would have to recompile this library by yourself)

Code/cPers/:                             c++ persistence code

Code/cPers/cPers/compile_pers_lib.sh:    script to compile the library

Code/cPers/cPers/PersistencePython.cpp:  root file for the python library

pybind11-stable.zip:                     tools used for compiling c++ code into library (python wrapper)

## PyTorch example
1. To be noted that our method is architecture-agnostic, you could incorporate the topological loss into your own framework to deal with your own datasets. 

2. At present, we only provide example for PyTorch framework. And to be honest, I am not quite sure if it's compatible with other libraries. Anyway, if you do want to apply the proposed method to other framework, feel free to have a try and I'm always welcome for discussion.

3. Here is an example to incorporate the C++ topological loss into deep learning framework based on PyTorch: https://github.com/HuXiaoling/imageSeg-2.5D_topo. The original paper only deals with 2D images, while this repository contains both 2D and 2.5D implementations (backbone may be slightly different). And we also plan to release the code for true 3D implementations (the paper is in preparation).

4. I apologize for the possible confusion. But stay tuned. All of the related repositories are under construction. You can definitely adopt existing repositories regarding your own data. If there are any questions, please feel easy to post them here.

## Update (06/2021)
A more efficient version topoloss is uploaded!！

Now you could simply incorporate the topological loss function into your own backbone (PyTorch).

topoloss.py: offline sample showing how to use topological loss.

topoloss_pytorch.py: function used in pytorch framework (Will be included in pip later)

## Post-processing

Be sure to post-process (remove small connected components) as topoloss may create a few isolated points.

## Citation
Please consider citing our paper if you find it useful.
```
@article{hu2019topology,
  title={Topology-preserving deep image segmentation},
  author={Hu, Xiaoling and Li, Fuxin and Samaras, Dimitris and Chen, Chao},
  journal={Advances in neural information processing systems},
  volume={32},
  year={2019}
}
