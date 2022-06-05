# x86-high-freq-cache-timing-leakage
x86 Dataset contains an implementation of unprotected AES-128 on the X86 platforms. This dataset includes the high-frequency cache timing traces of 16 cachelines corresponding to the 4 T-tables(Te0 to Te3) during the execution of AES-128. Each high-frequency cache timing trace is collected using the concurrent cache monitor introduced in the paper *A Cross-Platform Cache Timing Attack Framework via Deep Learning* published on 2022 Design, Automation & Test in Europe Conference & Exhibition (DATE). 

The last round key bytes (2<sub>nd</sub>, 6<sub>th</sub>, 10<sub>th</sub>, 14<sub>th</sub>) corresponde to the first Table(Te0) is 29,174,167,48; 

x86 dataset is packaged into a .h5 file (dataset.h5), where the structure is described below:

1. **training dataset**: dataset to train the attack model
   - traces: 80k high-frequency cache timing traces of first T-table cacheline (index 0);
   - ciphertext: 80k corresponding ciphertext;
   - label_kc: the label of 14<sub>th</sub> byte of last round key that is computed through: inv_s_box(ciphertext[14] xor kc)//16 == 0(index of monitored cacheline)
   - labels: the label of all key candidates in the training dataset;     
2. **attack dataset**: dataset to test the attack model
   - traces: 20k high-frequency cache timing traces of first T-table cacheline (index 0);
   - ciphertext: 20k corresponding ciphertext;
   - labels: the label of all key candidates in the training dataset: for candidate kg, the label is computed as inv_s_box(ciphertext[14] xor kg)//16 == 0(index of monitored cacheline);                                                        

