# HISTORY
Command history in the Travis local docker machine.

* From newest to oldest:
```
    1  conda
    2  conda activate r-torch    # needs to activate conda first
    3  conda init bash
    4  exit
    5  conda activate r-torch
    6  python
```    

```
    1  Rscript -e 'devtools::check()'
    2  ls
    3  cd ..
    4  R CMD check --as-cran rTorch_0.0.3.tar.gz
    5  ls
    6  R CMD check rTorch_0.0.3.tar.gz
    7  ls
    8  R CMD check rTorch
    9  R CMD check --as-cran rTorch
   10  cd rTorch
   11  R CMD check rTorch
   12  Rscript -e 'devtools::test()'
   13  R
   14  Rscript -e 'devtools::test()'
```   

```    
    2  ls /usr/lib/x86_64-linux-gnu
    3  ls /usr/lib/x86_64-linux-gnu/libstd*
    4  ls -slh /usr/lib/x86_64-linux-gnu/libstd*
    5  ls /home/travis/miniconda/envs/r-torch/lib/libstdc*
    6  ls -alh/home/travis/miniconda/envs/r-torch/lib/libstdc*
    7  ls -alh /home/travis/miniconda/envs/r-torch/lib/libstdc*
    8  ls -alh ~/miniconda/lib/libstdc*
    9  nano /home/travis/miniconda/envs/r-torch/lib/libstdc++.so
   10  nano /home/travis/miniconda/envs/r-torch/lib/libstdc++.so.6.0.28
   11  sudo rm /usr/lib/x86_64-linux-gnu/libstdc++.so.6    # remove link to libstdc++.so.6 in ther Linux installation
   12  Rscript -e 'devtools::check()'                      # cannot find libstdc++.so.6 installed by Anaconda
   13  export LD_LIBRARY_PATH=/home/travis/miniconda/envs/r-torch/lib/   # indicate where to find the libraries
   14  Rscript -e 'devtools::check()'                      # run the tests
   15  cd f0nzie/rTorch                                    # change to package folder
   16  Rscript -e 'devtools::check()'                      # all tests pass now
```   


```
    1  echo $LD_LIBRARY_PATH
    2  unset LD_LIBRARY_PATH
    3  echo $LD_LIBRARY_PATH
    4  export home/travis/miniconda/envs/r-torch/lib/
    5  echo $LD_LIBRARY_PATH
    6  Rscript -e 'devtools::check()'
    7  cd f0nzie/rTorch
    8  Rscript -e 'devtools::check()'
    9  rm  ~/miniconda/lib/libstdc++.so
   10  rm  ~/miniconda/lib/libstdc++.so.6
   11  Rscript -e 'devtools::check()'
   12  ls /usr/local/lib64
   13  ls /usr/local/lib
   14  ls /usr/local/lib/R
   15  echo $LD_LIBRARY_PATH
   16  unset LD_LIBRARY_PATH
   17  export LD_LIBRARY_PATH=/home/travis/miniconda/envs/r-torch/lib/
   18  echo $LD_LIBRARY_PATH
   19  Rscript -e 'devtools::check()'
   20  ls /home/travis/miniconda/envs/r-torch/lib/
   21  ls /home/travis/miniconda/envs/r-torch/lib/libstdc*
```   


```
    1  ls ~/miniconda/lib
    2  ls ~/miniconda/lib/libstd*
    3  ls ~/miniconda/lib/libstdc*
    4  ls -alh ~/miniconda/lib/libstdc*
    5  rm  ~/miniconda/lib/libstdc++.so.6.0.21
    6  Rscript -e 'devtools::check()'
    7  pwd
    8  cd f0ncho/rTorch
    9  cd f0nzie/rTorch
   10  Rscript -e 'devtools::check()'
   11  ls -alh ~/miniconda/env/r-torch/lib/libstdc*
   12  ls -alh ~/miniconda/envs/r-torch/lib/libstdc*
   13  rm  ~/miniconda/lib/libstdc++.so
   14  rm  ~/miniconda/lib/libstdc++.so.6
   15  Rscript -e 'devtools::check()'
```   




```

    2  ls miniconda/lib
    3  ls miniconda/lib/libstdc
    4  ls miniconda/lib/libstdc*
    5  pwd
    6  cd f0nzie/rTorch
    7  Rscript -e 'devtools::check()'
    8  echo $LD_LIBRARY_PATH
   10  echo $LD_LIBRARY_PATH
   11  Rscript -e 'devtools::check()'
   12  echo $LD_LIBRARY_PATH
   13  ls miniconda/lib/libstdc*
   14  ls /home/travis/miniconda/lib/libstdc*
   15  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/travis/miniconda/lib/
   16  echo $LD_LIBRARY_PATH
   17  Rscript -e 'devtools::check()'
   18  unset $LD_LIBRARY_PATH
   19  unset LD_LIBRARY_PATH
   20  echo $LD_LIBRARY_PATH
   21  LD_LIBRARY_PATH=/home/travis/R-bin/lib:
   22  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/travis/miniconda/lib/
   23  echo $LD_LIBRARY_PATH
   24  Rscript -e 'devtools::check()'
   25  Rscript -e 'devtools::test()'
   26  unset LD_LIBRARY_PATH
   27  LD_LIBRARY_PATH=/home/travis/R-bin/lib
   28  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/travis/miniconda/lib/
   29  Rscript -e 'devtools::check()'
   30  history
```



```
    2  ls miniconda/lib
    3  ls miniconda/lib/libstdc
    4  ls miniconda/lib/libstdc*
    5  pwd
    6  cd f0nzie/rTorch
    7  Rscript -e 'devtools::check()'
    8  echo $LD_LIBRARY_PATH
   10  echo $LD_LIBRARY_PATH
   11  Rscript -e 'devtools::check()'
   12  echo $LD_LIBRARY_PATH
   13  ls miniconda/lib/libstdc*
   14  ls /home/travis/miniconda/lib/libstdc*
   15  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/travis/miniconda/lib/
   16  echo $LD_LIBRARY_PATH
   17  Rscript -e 'devtools::check()'
   19  unset LD_LIBRARY_PATH
   20  echo $LD_LIBRARY_PATH
   21  LD_LIBRARY_PATH=/home/travis/R-bin/lib:
   22  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/travis/miniconda/lib/
   23  echo $LD_LIBRARY_PATH
   24  Rscript -e 'devtools::check()'
   25  Rscript -e 'devtools::test()'
   26  unset LD_LIBRARY_PATH
   27  LD_LIBRARY_PATH=/home/travis/R-bin/lib
   28  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/travis/miniconda/lib/
   29  Rscript -e 'devtools::check()'
   32  cd ..
   33  cd miniconda
   34  ls
   35  cd lib
   36  ls libstd*
   37  mv libstdc++.so libstdc++.so.bkp
   38  mv libstdc++.so.6 libstdc++.so.6.bkp
   39  Rscript -e 'devtools::check()'
   40  cd ../../f0nzie/rTorch
   41  Rscript -e 'devtools::check()'
   42  echo $LD_LIBRARY_PATH
   43  cd ../../miniconda/lib
   44  ls libstd*
   45  ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6 libstdc++.so.6
   cd ~/f0nzie/rTorch
   Rscript -e 'devtools::check()'
   48  rm /usr/lib/x86_64-linux-gnu/libstdc++.so.6
   49  sudo rm /usr/lib/x86_64-linux-gnu/libstdc++.so.6
   50  pwd
   51  cd miniconda/lib
   52  ls libstd*
   53  ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6 libstdc++.so.6
```

