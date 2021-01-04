# bert-model
BERT, is a new method of pre-training language representations which obtains state-of-the-art results on a wide array of Natural Language Processing (NLP) tasks.
We have shown that the standard BERT recipe (including model architecture and training objective) is effective on a wide range of model sizes, beyond BERT-Base and BERT-Large. The smaller BERT models are intended for environments with restricted computational resources. They can be fine-tuned in the same manner as the original BERT models. 
For each task, we selected the best fine-tuning hyperparameters from the lists below, and trained for 4 epochs:

    batch sizes: 8, 16, 32, 64, 128
    learning rates: 3e-4, 1e-4, 5e-5, 3e-5
If you use these models, please cite the following paper:
@article{turc2019,
  title={Well-Read Students Learn Better: On the Importance of Pre-training Compact Models},
  author={Turc, Iulia and Chang, Ming-Wei and Lee, Kenton and Toutanova, Kristina},
  journal={arXiv preprint arXiv:1908.08962v2 },
  year={2019}
}
This is a release of several new models which were the result of an improvement the pre-processing code.

In the original pre-processing code, we randomly select WordPiece tokens to mask. For example:

Input Text: the man jumped up , put his basket on phil ##am ##mon ' s head Original Masked Input: [MASK] man [MASK] up , put his [MASK] on phil [MASK] ##mon ' s head

The new technique is called Whole Word Masking. In this case, we always mask all of the the tokens corresponding to a word at once. The overall masking rate remains the same.

Whole Word Masked Input: the man [MASK] up , put his basket on [MASK] [MASK] [MASK] ' s head

The training is identical -- we still predict each masked WordPiece token independently. The improvement comes from the fact that the original prediction task was too 'easy' for words that had been split into multiple WordPieces.

This can be enabled during data generation by passing the flag --do_whole_word_mask=True to create_pretraining_data.py.

Pre-trained models with Whole Word Masking are linked below. The data and training were otherwise identical, and the models have identical structure and vocab to the original models. We only include BERT-Large models. When using these models, please make it clear in the paper that you are using the Whole Word Masking variant of BERT-Large.


    BERT-Large, Uncased (Whole Word Masking): 24-layer, 1024-hidden, 16-heads, 340M parameters

    BERT-Large, Cased (Whole Word Masking): 24-layer, 1024-hidden, 16-heads, 340M parameters

