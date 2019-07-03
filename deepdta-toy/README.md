# DeepDTA: using your own train/test datasets

Here is the modified version of DeepDTA that enables the use of your own training and/or test datasets.

## Data folder

These are two sample datasets that I used as an example. DTC is used as training set and mytest folder contains three example files that your test data should be formatted as.

*   **DTC:** is a subset of data collected from (https://drugtargetcommons.fimm.fi/) that only contains pKd binding affinity values.
    *   since training data values are pKd, predicted values will be pKd as well. You can also change the training set according to your needs. 
    *    for that uncomment line 552 in 'run_experiments.py' file.
    ```py
        #prepare_new_data(FLAGS.test_path, test=False) #Uncomment this if you also have a new training data
    ```
*   **mytest:** 
    *   Y.tab: tab-seperated binding affinity file (drugs x proteins matrix). This can be 0's if one wants to predict binding affinity values for the unknown data.
    *    ligands.tab: each line contains tab-seperated ligand ID and corresponding SMILES.
    *    proteins.fasta: fasta file for each protein in the dataset. 


## Requirements

You'll need to install following in order to run the codes.

*  [Python 3.4 <=](https://www.python.org/downloads/)
*  [Keras 2.x](https://pypi.org/project/Keras/)
*  [Tensorflow 1.x](https://www.tensorflow.org/install/)
*  numpy
*  matplotlib

You have to place "data" folder under "source" directory. 

# Usage
```
python run_experiments.py --num_windows 32 \
                          --seq_window_lengths 8 12 \
                          --smi_window_lengths 4 8 \
                          --batch_size 256 \
                          --num_epoch 100 \
                          --max_seq_len 1000 \
                          --max_smi_len 100 \
                          --dataset_path 'data/DTC/' \
                          --test_path 'data/mytest/' \
                          --problem_type 1 \
                          --isLog 0 \
                          --log_dir 'logs/'


```