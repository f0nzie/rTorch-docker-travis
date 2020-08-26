
## Better PyTorch installation alternative


## From Docker
Prevents the error caused by previous PyTorch script (after the suffix `-cpu` was removed).
```
# from docker-travis
RUN R -e 'rTorch:::install_conda(package="pytorch=1.6", envname="r-torch", \
    conda="auto", conda_python_version = "3.6", pip=FALSE, channel="pytorch", \
    extra_packages=c("torchvision", "cpuonly", "matplotlib", "pandas"))'
```    


## Errors


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