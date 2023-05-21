This project aims to improve the generalization ability of DAM for medical image classification tasks. 
To improve the benchmark performance reported in the MedMNIST paper. For fair comparison, we used the same network structure as in the MedMNIST paper i.e. Resnet-18(28).

## Techniques Used to reduce Overfitting datasets provided:
1. Data Augmentation Techniques Used
2. Controlling Overfitting
3. Data Imbalance Handling
4. Hyper-parameter Tuning
5. Co-training


## Result Comparison with Baseline Estimate:
|     Datasets     |      Ours    |  Baseline |
| ---------------- | ------------ | --------- |
|   BreastMNIST    |   **0.925**  |   0.901   |
|  PneomoniaMNIST  |   **0.973**  |   0.944   |
|    ChestMNIST    |     0.727    | **0.768** |
|   NoduleMNIST3D  |   **0.926**  |   0.915   |
|  AdrenalMNIST3D  |   **0.868**  |   0.827   |
|   VesselMNIST3D  |   **0.965**  |   0.874   |
|  SynapseMNIST3D  |   **0.862**  |   0.820   |




## Result Analysis
### BreastMNIST
There were around 546 train images with 73% of data belonging to one class. Hence, we performed sampling of training data with sampling rate = 0.5. Given the dataset was small, we tried with smaller batch sizes of [16, 32] and found batch size= 32 to be optimal. As we were using StepLR and ReduceLROnPlateau, so we started with a high learning rate of 0.01 as it helped in converging faster for initial epochs. We tried with weight decay of 2e-03 and 1e-05 and found the later to be performing better. We also experimented with introducing dropout in the FC layer. However, we found the architecture with the dropout layers to be performing the best. We performed co-training for 30 epochs to improve test AUC from 0.901 to 0.925. The model could be found at saved models/aucm trained model breastmnist.pth.


### PneumoniaMNIST
There were around 4708 train images with 74% of data belonging to one class. Hence, we performed sampling of training data with sampling rate = 0.5. Given the dataset was small, we tried with smaller batch sizes of [16, 32] and found batch size= 32 to be optimal. As we were using StepLR and ReduceLROnPlateau, so we started with a high learning rate of 0.01 as it helped in converging faster for initial epochs. We tried with weight decay of 2e-03 and 1e-05 and found the later to be performing better. We also experimented with introducing dropout in the FC layer. However, we found the architecture with the dropout layers to be performing the best. We performed co-training for 30 epochs o improve test AUC from 0.944 to 0.973. The model could be found at saved models/aucm trained model pneumoniamnist.pth.


### ChestMNIST
There were around 78,468 train images. As there were 14 classes with class imbalance, we performed sampling of training data with sampling rate = 0.5. Given the dataset was quite large than any of other datasets, we tried with batch sizes of [256, 512, 1024] and found batch size = 512 to be optimal. We used StepLR and ReduceLROnPlateau. Given the data was much complex than any other datasets, we started with a relatively small learning rate of 0.05 as it helped in learning the complex decision boundary for multiple classes. We tried with weight decay of 1e-03 and 1e-05 and found the later to be performing better. We also experimented with introducing dropout in the FC layer. We used CompisitionalAUCLoss as the loss function as the problem is a multi-class problem. We found the architecture without the dropout layers to be performing the best. We performed co-training for 20 epochs to get a test AUC of 0.727. The model could be found at saved models/chestmnist compositionalauc 512bs 0.05 SLR RLRP 7275.pth. However, we couldn’t improve the model AUC from what was mentioned in the paper due to time constraints. We believe we could get a better model if we could do some more hyperparameter tuning as the data is really large and being multiclass, its a complex task. Also the traditional AUCMLoss didn’t do better due to which we had to go to CompositionalAUCLoss after going through the LibAUC code base.


### NoduleMNIST3D
There were around 1100 train images with 74% of data belonging to one class. Hence, we performed sampling of training data with sampling rate = 0.5. Given the dataset was small, we tried with smaller batch sizes of [16, 32, 64] and found batch size= 32 to be optimal. As we were using StepLR and ReduceLROnPlateau, so we started with a high learning rate of 0.1 as it helped in converging faster for initial epochs. We tried with weight decay of 1e-03 and 1e-05 and found the later to be performing better. We also experimented with introducing dropout in the FC layer. However, we found the architecture without the dropout layers to be performing the best. We performed co-training for 20 epochs to get a test AUC of 0.9263. The model could be found at saved models/nodule3d resnet3d pesg 0.1 SLR RLRP noDP 9263.pth. Hence, we improved the model AUC from 0.915 to 0.9263.


### AdrenalMNIST3D
There were around 1200 train images with 78% of data belonging to one class. Hence, we performed sampling of training data with sampling rate = 0.5. Given the dataset was small, we tried with smaller batch sizes of [16, 32, 64] and found batch size= 32 to be optimal. As we were using StepLR and ReduceLROnPlateau, so we started with a high learning rate of 0.1 as it helped in converging faster for initial epochs. We tried with weight decay of 1e-03 and 1e-05 and found the later to be performing better. We also experimented with introducing dropout in the FC layer. However, we found the architecture without the dropout layers to be performing the best. We performed co-training for 20 epochs to get a test AUC of 0.8676. The model could be found at saved models/adrenal3d resnet3d pesg 0.1 SLR RLRP noDP 8676.pth. Hence, we improved the model AUC from 0.827 to 0.8676.


### VesselMNIST3D
There were around 1300 train images with ∼89% of data belonging to one class. Hence, we performed sampling of training data with sampling rate = 0.5. Given the dataset was small, we tried with smaller batch sizes of [16, 32, 64] and found batch size= 32 to be optimal. As we were using StepLR and ReduceLROnPlateau, so we started with a high learning rate of 0.1 as it helped in converging faster for initial epochs. We tried with weight decay of 1e-03 and 1e-05 and found the later to be performing better. We also experimented with introducing dropout in the FC layer. We performed co-training for 20 epochs to get a test AUC of 0.9652. The model could be found at saved models/vessel3d resnet3d pesg 0.1 SLR RLRP 9652.pth. Hence, we improved the model AUC from 0.874 to 0.9652.


### SynapseMNIST3D
There were around 1200 train images with ∼77% of data belonging to one class. Hence, we performed sampling of training data with sampling rate = 0.5. Given the dataset was small, we tried with smaller batch sizes of [16, 32, 64] and found batch size= 16 to be optimal. Even though we were using StepLR and ReduceLROnPlateau, we started with a learning rate of 0.05 as it balanced the convergence as well as gave a overall better validation AUC. We tried with weight decay of 1e-03 and 1e-05 and found the later to be performing better. We also experimented with introducing dropout in the FC layer. However, we found the architecture without the dropout layers to be performing the best.We performed co-training for 30 epochs to get a test AUC of 0.8623. The model could be found at saved models/synapse3d resnet3d pesg 0.05 SLR RLRP 16batchsize 8632.pth. Hence, we improved the model AUC from 0.820 to 0.8623.


## For more details refer to complete report:
https://github.com/Anushkagarg05/DeepAUCMaximization/blob/main/Report.pdf

## Saved models and evaluation notebooks:
https://drive.google.com/file/d/16f8j8NTjo1vTPfcFCiq2j9J13b8SDMu9/view?usp=sharing

## Certificate
https://drive.google.com/file/d/1haSqPPdEes5p_S0g7D-u0Mq-YiCEggwx/view?usp=share_link
