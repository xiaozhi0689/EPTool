# EPTool: A New Enhancing PSSM Tool forProtein Secondary Structure Prediction

Recently, a deep learning based enhancing PSSM method (Bagging MSA Learning (Y Guo, et al.)) has been proposed, and its effectiveness has been empirically proved. Program EPTool is the implementation of Bagging MSA Learning, which provides a complete training and evaluation workflow for the enhancing PSSM model. It is capable for handling different input dataset and various computing algorithms to train the enhancing model, then eventually improve the PSSM quality for those proteins with insufficient homologous sequences. In addition, EPTool equips several convenient applications, such as PSSM features calculator, and PSSM features visualization. In this paper, we propose designed EPTool, and briefly introduce its functionalities and applications. The detail accessible instructions is also provided. 

# EPTool Userguide

## preparation
Download Uniref50 fasta format database from https://www.uniprot.org/downloads to `./db/uniref50.fasta`

Donwload HMMER3.2.1 from http://hmmer.org/download.html and install the HMMER following the Userguide.pdf.

## Requirements:
cuda 10.2

python 3.6

pytorch 1.4.0

smile `pip install smile`

## Function
### Run jackhmmer
```
python run_hmmer.py --csv_path ./csv_example/sample.csv --aln_path ./aln_example/sample.aln --db_path ./db/uniref50.fasta --core_num 4
csv_path 
```
#### Parameters
*csv_path* - input protein sequences file path.

*aln_path* - output MSA file path

*db_path* - database file path

*core_num* - cpu core number

### Calculate PSSM
```
python calculate_pssm.py --aln_path ./aln_example/sample.aln --save_path ./feat_example/sample.pssm --method 1 
```
#### Parameters
*aln_path* - MSA file path

*save_path* - save pssm feature file path

*method* - PSSM calculation method num, `0`, `1` or `2`, Usually using `1`.

*ss_path*(optional) - secondary structure label file path, see `./ss_example/sample.ss` for an example.

### Unsupervised model training example
```
python train.py --aln_dpath='./aln_example' --train_fname='sample.aln' --valid_fname='sample.aln' --model_path=./try01 2>&1 | tee try01.log
```
See comments for all hyper-parameters in `train.py`

This part of the manual will be completed upon acceptance of the EPTool paper.

See `./aln_example/sample.aln` for an example of input MSA file.

### Generate enhanced feature
```
python generate_new_feat.py --eval_feat_path='./feat_example/sample2.feat' --save_fpath='./feat_example/new.feat' --model_path='./try01' --epoch=1
```
See comments for all hyper-parameters in `generate_new_feat.py`

This part of the manual will be completed upon acceptance of the EPTool paper.

See `./feat_example/sample2.feat` for an example of input feat file.

### Generate PSSM Grayscale
```
python grayscale.py --pssm_path ./feat_example/sample.pssm
```


