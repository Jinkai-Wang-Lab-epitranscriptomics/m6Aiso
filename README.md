
# m6anet

m6aiso is a python tool that based on semi supervised framework to detect m6A modifications from nanopore direct RNA sequencing.

# Table of Contents
- **[Running m6Aiso](#running-m6anet)**<br>
    - **[Installation](#installation)**<br>
    - **[Data prepare](#data-prepare)**<br>
- **[Getting Help](#getting-help)**<br>
- **[Citing](#citing-m6aiso)**<br>
- **[Contributors](#contributors)**<br>
- **[License](#license)**<br>

# Running m6Aiso

## Installation

m6anet requires [Python version 3.7 or higher](https://www.python.org). To install the latest release with PyPI (recommended) run

```sh
$ pip install m6aiso
```

## Data prepare

m6Aiso data prepare requires eventalign.txt from ``nanopolish eventalign``:
```
    nanopolish eventalign 
                            --reads <in.fasta> 
                            --bam <in.bam> 
                            --genome <genome.fa> 
                            --signal-index
                            --scale-events 
                            --summary <summary.txt> | gzip > <out.tsv.gzip>
```

After running nanopolish eventalign, we need to preprocess the segmented raw signal file using 'm6aiso current_signal_abstract_for_m6A_pred'::

```
    python -m m6anet current_signal_abstract_for_m6A_pred 
                            --nanopolish_result <out.tsv.gzip>
                            --number the number of each batchs
                            --out_dir /path/to/output
```

The output files are stored in ``/path/to/output``:


## m6A Prediction

Once `m6aiso current_signal_abstract_for_m6A_pred` finished, we can run `m6aiso molecular_m6A_predication` based on the data prepare output:
```
    python -m m6aiso current_signal_abstract_for_m6A_pred
                            --model_path path/to/output
                            --model_type path/to/output
                            --using_signal_filename
                            --predict_result_filename
                            --max_value_filename
                            --min_value_filename
```

## semi supervised model training

In order to training model based on semi supervised framework, we can run `m6aiso semi_supervised_model_train` based on the data prepare output:
```
    python -m m6aiso semi_supervised_model_train
                            --model_name AttentionNet,Res1dNet,Res2dNet
                            --orginal_pos_filename 
                            --orginal_neg_filename
                            --max_value_filename
                            --min_value_filename
                            --out_dir
```

# Getting help

We appreciate your feedback and questions! You can report any error or suggestion related to m6Aiso as an issue on [github]().

### Contribution

We appreciate contributions on bug fixes and potential new features. Thank you!

# Citing m6Aiso

If you use m6Aiso in your research, please cite
[XXXXXXXXXXXXXXXX]()


# Contributors

This package is developed and maintaned by [ZhiJun Ren](https://github.com/ZJRen9) and [WenBing Guo](https://github.com/GuoWenBing). If you want to contribute, please leave an issue or submit a pull request. Thank you.

# License
m6Anet is licensed under the terms of the MIT license.