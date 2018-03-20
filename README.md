# SeqMatchSeq

- [Machine Comprehension Using Match-LSTM and Answer Pointer](https://arxiv.org/abs/1608.07905) by Shuohang Wang, Jing Jiang

# Machine Comprehension Using Match-LSTM and Answer Pointer

### Requirements
- [Torch7](https://github.com/torch/torch7)
- [nn](https://github.com/torch/nn)
- [nngraph](https://github.com/torch/nngraph)
- [optim](https://github.com/torch/optim)
- [parallel](https://github.com/clementfarabet/lua---parallel)
- Python 2.7
- Python Packages: [NLTK](http://www.nltk.org/install.html), collections, json, argparse
- [NLTK Data](http://www.nltk.org/data.html): punkt
- Multiple-cores CPU

### Datasets
- [Stanford Question Answering Dataset (SQuAD)](https://rajpurkar.github.io/SQuAD-explorer/)
- [GloVe: Global Vectors for Word Representation](http://nlp.stanford.edu/data/glove.840B.300d.zip)

### Usage
```
sh preprocess.sh squad
cd main
th mainDt.lua 
```

`sh preprocess.sh squad` will download the datasets and preprocess the SQuAD corpus into the files 
(train.txt dev.txt) under the path "data/squad/sequence" with the format:

>sequence1(Doument) \t sequence2(Question) \t sequence of the positions where the answer appear 
in Document (e.g. 3 4 5 6)  \n

`mainDt.lua` will first initialize the preprossed data and word embeddings into a Torch format and 
then run the alogrithm. As this code is run through multiple CPU cores, the initial parameters are
written in the file "main/init.lua". 

- `opt.num_processes`: 5. The number of threads used.
- `opt.batch_size`   : 6. Batch size for each thread. (Then the mini_batch would be 5*6 .)
- `opt.model`        : boundaryMPtr / sequenceMPtr 

## Docker
You may try to use Docker for running the code.
- [Docker Install](https://github.com/codalab/codalab-worksheets/wiki/Installing-Docker)
- [Image](https://hub.docker.com/r/shuohang/seqmatchseq/): docker pull shuohang/seqmatchseq:1.0

After installation, just run the following codes (/PATH/SeqMatchSeq need to change):
```
docker run -it -v /PATH/SeqMatchSeq:/opt --rm -w /opt      shuohang/seqmatchseq:1.0 /bin/bash -c "sh preprocess.sh squad"
docker run -it -v /PATH/SeqMatchSeq:/opt --rm -w /opt/main shuohang/seqmatchseq:1.0 /bin/bash -c "th mainDt.lua"
```

# Copyright
Copyright 2015 Singapore Management University (SMU). All Rights Reserved.
