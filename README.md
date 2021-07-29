# END2_Assignment12
This assignment was based on the Transformer architecture, implemented from scratch. We we supposed to execute this implementation for some task of our choice.
So decided to test this implementation out on 
1. **Translation task**, more specifically **German to English** translation on **Multi30k** Dataset. 
2. **Question and Answer task**,  Dataset from **CMU question_answer_pair.txt** dataset. 

The colab files which were developed in assignment 7, were taken and the model was changed from Seq2Seq with attention to the current model of transformer architecture. Discussion of these two follows:
## Translation
Colab file is **Assignment12_transformer from scratch on nmt.ipynb** </br>
The dataset was prepared without using the _torch.legacy.data_. The model required the number of training examples (batch_size) as the first dimension, so that data was adjusted accordingly and model could be trained.</br>
### Key Points
1.It was observed that after some 30 epochs, test PPL was oscillating between 250 and 265, and was not reducing further, even though the training PPL was steadily coming down initially with some evidence of fluctuation as shown in the graph below for 10 epochs.</br>
![image](https://user-images.githubusercontent.com/82941475/127483611-c63a811e-da3d-4a42-af5d-bf8efbcc43d6.png)


2. Here is sample of Training  loss,  training PPL, Test loss, and Test PPL

Epoch|Training  loss|  training PPL| Test loss| Test PPL|
------|--------|----------------|------------|---------|
Epoch: 01 | 5.693 |  296.658 |	 5.672 |  290.694
Epoch: 02 |  5.618 | 275.387 |	 5.682 |   293.603
Epoch: 03 | 5.601 | 270.681 |	5.693 |  296.780
Epoch: 04 |  5.581 | 265.409 |	 5.712 |  302.616
Epoch: 05 |  5.564 | 260.827 |	 5.720 |   304.992
Epoch: 06 |5.551 |  257.415 |	 5.739 |  310.606
Epoch: 07 |  5.540 |  254.624 |	  5.746 |   313.007
Epoch: 08 |  5.532 |  252.670 |	  5.770 |  320.626
Epoch: 09 | 5.526 | 251.224 |	 5.776 |   322.477
Epoch: 10 | 5.557 |  259.073 |	 5.763 |  318.206

3. A closer look at the translated sentences (after 10 epochs) revealed a single word in the whole sentence. Clearly the model was underfitting to the data. A review of the similar work revealed training for 10,000 epochs with a smaller learning rate of the order of 3e-4. It was cleary visible from the oscillating PPL, that the training cycle was stuck somewhere in the local minimum and was not able to come out of that.
## Question and Answer task
Colab file is **Assignment12_transformaerqa.ipynb**
The dataset was taken as it was in the file prepared for assignment 7. The current model required the number of training examples (batch_size) as the first dimension, so that data was adjusted accordingly and model could be trained.</br>
### Key points
The training cycle would run for some time and then would report error (_self index out of range_). So I decided to reduce the number of training examples. The training dataset for this dataset had 88 batches (each batch of 32 size). So I started with 5 batches, no error. I gradually increased number of batches, to train on, up to 30. Training cycle reported training loss and PPL for one epoch and then reported error same error. This needs to be further investigated. It could be some sentence(question or answer) in the dataset, going beyond the listed maxmimum size or some parameter needing re-initialized.
