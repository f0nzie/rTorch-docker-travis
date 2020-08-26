# FIX ERRORS AND WARNINGS


## Better PyTorch installation alternative


## From Docker
Prevents the error caused by previous PyTorch script (after the suffix `-cpu` was removed).
```
# from docker-travis
RUN R -e 'rTorch:::install_conda(package="pytorch=1.6", envname="r-torch", \
    conda="auto", conda_python_version = "3.6", pip=FALSE, channel="pytorch", \
    extra_packages=c("torchvision", "cpuonly", "matplotlib", "pandas"))'
```


## ERRORS


### `CXXABI_1.3.11' not found`
This error is persistent. There are solutions for it but so far none has worked.

```
Import/usr/lib/x86_64-linux-gnu/libstdc++.so.6: version `CXXABI_1.3.11' not found (required by /home/travis/miniconda/envs/r-torch/lib/python3.6/site-packages/torch/lib/libtorch_python.so)
```


### /bin/sh: 1: conda: not found


* Adding `conda install libgcc && \` does not make error `CXXABI_1.3.11' not found` go away
* List files under `anaconda3/lib`:
```
   $ ls -alh ~/anaconda3/lib/libstdc*
lrwxrwxrwx 1 msfz751 msfz751  19 Jul 30 13:58 /home/msfz751/anaconda3/lib/libstdc++.so -> libstdc++.so.6.0.26
lrwxrwxrwx 1 msfz751 msfz751  19 Jul 30 13:58 /home/msfz751/anaconda3/lib/libstdc++.so.6 -> libstdc++.so.6.0.26
-rwxrwxr-x 5 msfz751 msfz751 13M Jun  9  2019 /home/msfz751/anaconda3/lib/libstdc++.so.6.0.26
```



### 3.4. How do I insure that the dynamically linked library will be found?  
https://gcc.gnu.org/onlinedocs/libstdc++/faq.html#faq.how_to_install


### libstdc discovered before Miniconda
https://www.pythonanywhere.com/forums/topic/25376/
*The miniconda installation provides its own libstdc++.so.6, which simlinks to its own libstdc++.so.6.0.26, but the system one located in /usr/lib/x86_64-linux-gnu is discovered ahead of the one in the miniconda installation.*

```
# Linux libs
travis@cb47359a7f13:~$ ls -slh /usr/lib/x86_64-linux-gnu/libstd*
   0 lrwxrwxrwx 1 root root   19 Oct  4  2019 /usr/lib/x86_64-linux-gnu/libstdc++.so.6 -> libstdc++.so.6.0.21
1.5M -rw-r--r-- 1 root root 1.5M Oct  4  2019 /usr/lib/x86_64-linux-gnu/libstdc++.so.6.0.21
```


```
# PyTorch envirnoment libs
travis@cb47359a7f13:~$ ls -alh /home/travis/miniconda/envs/r-torch/lib/libstdc*
lrwxrwxrwx 1 travis travis  19 Aug 25 21:33 /home/travis/miniconda/envs/r-torch/lib/libstdc++.so -> libstdc++.so.6.0.28
lrwxrwxrwx 1 travis travis  19 Aug 25 21:33 /home/travis/miniconda/envs/r-torch/lib/libstdc++.so.6 -> libstdc++.so.6.0.28
-rwxrwxr-x 2 travis travis 13M Aug 22 21:40 /home/travis/miniconda/envs/r-torch/lib/libstdc++.so.6.0.28
```

```
# conda libs
travis@cb47359a7f13:~$ ls -alh ~/miniconda/lib/libstdc*
lrwxrwxrwx 1 travis travis  19 Aug 25 21:30 /home/travis/miniconda/lib/libstdc++.so -> libstdc++.so.6.0.26
lrwxrwxrwx 1 travis travis  19 Aug 25 21:30 /home/travis/miniconda/lib/libstdc++.so.6 -> libstdc++.so.6.0.26
-rwxrwxr-x 2 travis travis 13M Jun  9  2019 /home/travis/miniconda/lib/libstdc++.so.6.0.26
```



## ERRORS
```
# * checking examples with --run-donttest ... WARNING
# checking a package with encoding  'UTF-8'  in an ASCII locale
#  ERROR
# Running examples in 'rTorch-Ex.R' failed
# The error most likely occurred in:
# > base::assign(".ptime", proc.time(), pos = "CheckExEnv")
# > ### Name: all.torch.Tensor
# > ### Title: all
# > ### Aliases: all.torch.Tensor
# > 
# > ### ** Examples
# > 
# > ## No test: 
# > a <- torch$BoolTensor(list(TRUE, TRUE, TRUE, TRUE))
# Error: Python module torch was not found.

# Error in py_module_import(module, convert = convert) : 
#   ImportError: /usr/lib/x86_64-linux-gnu/libstdc++.so.6: version `CXXABI_1.3.11' not found 
#   (required by /home/travis/miniconda/envs/r-torch/lib/python3.6/site-packages/torch/lib/libtorch_python.so)

# travis@76b57b6c0495:~$ ls miniconda/lib/libstdc*
# miniconda/lib/libstdc++.so  
# miniconda/lib/libstdc++.so.6  
# miniconda/lib/libstdc++.so.6.0.26

# ENV LD_LIBRARY_PATH=/home/travis/R-bin/lib     # confuses search for libstdc++.so.6
# RUN export PATH=/home/travis/R-bin/bin:$PATH   # confuses search for libstdc++.so.6
# TODO: remove these two lines later
# RUN echo $PATH
# RUN cat ~/.Rprofile.site
# RUN export PATH=$HOME/miniconda/bin:$PATH
# # check simple
# RUN cd f0nzie && \
#     R CMD build rTorch  && \
#     R CMD check rTorch_0.0.3.tar.gz
# export LD_LIBRARY_PATH=/home/travis/miniconda/envs/r-torch/lib/ && \
# export PATH="$HOME/miniconda/bin:$PATH" && \
# export PATH=${TRAVIS_HOME}/texlive/bin/x86_64-linux:$PATH && \
```

# install C++
# ===================================
#* option 1
# RUN sudo apt update && \
#     sudo apt-get install gcc-4.9
# -----------------------------------
#* option 2
RUN sudo apt-get update && \
    sudo apt-get install libstdc++6
# ====================================

## WARNINGS

### Warnings when running under R-4.0.0

*   Running tests from Travis local machine

```
docker run --rm --name my-travis-kont -dit my-travis /sbin/init  &&  docker exec -it my-travis-kont bash -l
```

*   Docker container

```
travis@5d00f0364a22:~/f0nzie/rTorch$ Rscript -e 'devtools::test()'
```

*   Output

```
Loading rTorch
loading PyTorch
Testing rTorch
✔ |  OK F W S | Context
✔ |  65       | extract syntax [0.5 s]
✔ |  24       | switch extract style R to Python [0.2 s]
✔ |   4       | generic methods
✔ |  11       | log of number with a base
✔ |   4       | dim on tensor
✔ |  10   2   | tensor arithmetic
────────────────────────────────────────────────────────────────────────────────
test_generics.R:106: warning: length of tensor is the same as numel()
the condition has length > 1 and only the first element will be used

test_generics.R:106: warning: length of tensor is the same as numel()
the condition has length > 1 and only the first element will be used
────────────────────────────────────────────────────────────────────────────────
✔ |   4       | tensor equal ==
✔ |  14       | tensors not equal != [0.8 s]
✔ |   9       | tensor comparison [0.6 s]
✔ |   2       | tensor multiplication
✔ |   5       | Matrix product of two tensors, matmul()
✔ |   2     1 | PyTorch version
────────────────────────────────────────────────────────────────────────────────
test_info.R:22: skip: (unknown)
Reason: On Travis
────────────────────────────────────────────────────────────────────────────────
✔ |   6       | matrix like tensor operations
✔ |   0       | numpy logical operations
✔ |  13       | AND logical operations
✔ |  11       | OR logical operations
✔ |   3       | extract parts of a Python object 1
✔ |   7       | extract parts of a Python object 2
✔ |   7       | print R values from within Python
✔ |   8       | R and Python share variables
✔ |  17       | read, write tensors by index
✔ |  10       | test function tensor_dim [0.2 s]
✔ |   6       | reshape tensor
✔ |   2       | test slicing with chunk() and select_index()
✔ |   8       | split tensor with function chunk()
✔ |   6       | tensor extraction of 3D tensor with index_select()
✔ |  25       | tensor extraction of 4D tensor with index_select() [0.3 s]
✔ |   2       | function narrow() extracts part of a tensor
✔ |   5   6   | _select
────────────────────────────────────────────────────────────────────────────────
test_torch_core.R:23: warning: masked_select
the condition has length > 1 and only the first element will be used

test_torch_core.R:23: warning: masked_select
the condition has length > 1 and only the first element will be used

test_torch_core.R:52: warning: index_select
the condition has length > 1 and only the first element will be used

test_torch_core.R:52: warning: index_select
the condition has length > 1 and only the first element will be used

test_torch_core.R:63: warning: index_select
the condition has length > 1 and only the first element will be used

test_torch_core.R:63: warning: index_select
the condition has length > 1 and only the first element will be used
────────────────────────────────────────────────────────────────────────────────
✔ |   6   12   | cat, split
────────────────────────────────────────────────────────────────────────────────
test_torch_core.R:91: warning: cat
the condition has length > 1 and only the first element will be used

test_torch_core.R:91: warning: cat
the condition has length > 1 and only the first element will be used

test_torch_core.R:102: warning: cat
the condition has length > 1 and only the first element will be used

test_torch_core.R:102: warning: cat
the condition has length > 1 and only the first element will be used

test_torch_core.R:127: warning: split
the condition has length > 1 and only the first element will be used

test_torch_core.R:127: warning: split
the condition has length > 1 and only the first element will be used

test_torch_core.R:132: warning: split
the condition has length > 1 and only the first element will be used

test_torch_core.R:132: warning: split
the condition has length > 1 and only the first element will be used

test_torch_core.R:142: warning: split
the condition has length > 1 and only the first element will be used

test_torch_core.R:142: warning: split
the condition has length > 1 and only the first element will be used

test_torch_core.R:149: warning: split
the condition has length > 1 and only the first element will be used

test_torch_core.R:149: warning: split
the condition has length > 1 and only the first element will be used
────────────────────────────────────────────────────────────────────────────────
✔ |   7   8   | squeeze, take, narrow
────────────────────────────────────────────────────────────────────────────────
test_torch_core.R:178: warning: take
the condition has length > 1 and only the first element will be used

test_torch_core.R:178: warning: take
the condition has length > 1 and only the first element will be used

test_torch_core.R:196: warning: narrow
the condition has length > 1 and only the first element will be used

test_torch_core.R:196: warning: narrow
the condition has length > 1 and only the first element will be used

test_torch_core.R:202: warning: narrow
the condition has length > 1 and only the first element will be used

test_torch_core.R:202: warning: narrow
the condition has length > 1 and only the first element will be used

test_torch_core.R:211: warning: narrow
the condition has length > 1 and only the first element will be used

test_torch_core.R:211: warning: narrow
the condition has length > 1 and only the first element will be used
────────────────────────────────────────────────────────────────────────────────
✔ |   8       | transpose
✔ |   4       | permute
✔ |  25       | basic tests

══ Results ═════════════════════════════════════════════════════════════════════
Duration: 4.5 s

OK:       340
Failed:   0
Warnings: 28
Skipped:  1
```

## Test results

### rTorch v0.0.3.9003, R-3.6.3, python=3.6, pytorch=-1.1

* All tests from `Rscript -e 'devtools::test(cran=TRUE, run_dont_test=TRUE)'` passed
