S5 Assignment
-------------

This assignment objective was to achieve test accuracy as 99.4% consistently in the last 4-5 epochs, with less than 10k params & under 15 epochs. It was said, to mention it in 4 steps(or models). 4 jupyter files are placed and the 4 steps are explained below along with their Receptive field.


1_Setup_&_Basic_Skeleton
-----------------------------
    Target
    ======
    1) Setting up a basic skeleton of the model
    2) Setting transforms, dataloads & training & test loops
    3) Set it as working code.

    Results
    ======
    1) Parameters: 2,02,724
    2) Best Train Accuracy: 99.49
    3) Best Test Accuracy: 99.14
    
    Analysis
    1. Huge model with overload of params
    2. Can see the model is overfitting
    3. Training is working fine & can see consistent increase in the training accuracy as we progress through epochs
    4. Will need to make the model lighter in the next step.
    

                    K	P	S	    jin	    nin     nout   RF   jout
            INPUT				    1		   28	    1	   1
            CONV	3	0	1	    1	    28	    26	    3	   1
            CONV	3	0	1	    1	    26	    24	    5	   1
            CONV	3	0	1	    1	    24	    22	    7	   1
            MAX	    2	0	2	    1	    22	    11	    8	   2
            CONV	1	0	1	    2	    11	    11	    8	   2
            CONV	3	0	1	    2	    11	    9	    12	   2
            CONV	3	0	1	    2	    9	    7	    16	   2
            CONV	5	0	1	    2	    7	    3	    24	   2

    

2_Lighter_model_&_batch_norm
---------------------------------
    Target
    ======
    1) Make the model lighter (by reducing the channels)
    2) Adding batch norm to the model to increase the model efficiency

    Results
    ======
    1) Parameters: 11,364
    2) Best Train Accuracy: 99.76
    3) Best Test Accuracy: 99.30

    Analysis
    ========
    1) Before applying Batch norm - Made the model lighter by reducing channels but accuracy was dropped for 
       both the train & test due to less number of parameters. And also can see no overfitting. 
       The train_acc = 98.89 & test_acc = 98.91, gap seems to be less between them.
    2) After adding Batch norm – Could see a significant increase in both the accuracies test & train. 
       This tells how much powerful batch norm is & now it has accentuated the features by uplifting them.
       The train_acc = 99.76 & test_acc = 99.30. Seems to be large gap between train & test accuracy which states 
       the model is overfitting & in the next steps we can use regularization to penalize.
       
 
            K	P	S	    jin	    nin     nout   RF   jout
    INPUT				    1		   28	    1	   1
    CONV	3	0	1	    1	    28	    26	    3	   1
    CONV	3	0	1	    1	    26	    24	    5	   1
    CONV	3	0	1	    1	    24	    22	    7	   1
    MAX	    2	0	2	    1	    22	    11	    8	   2
    CONV	1	0	1	    2	    11	    11	    8	   2
    CONV	3	0	1	    2	    11	    9	    12	   2
    CONV	3	0	1	    2	    9	    7	    16	   2
    CONV	5	0	1	    2	    7	    3	    24	   2
    

3_Regularization_GAP_&_Max_Pool
-------------------------------------
    Target
    ======
    1) Adding regularization – Dropout
    2) Adding GAP to reduce the 11k params to under 10k
    3) To increase the model capacity add layer after GAP
    4) Perform maxpooling at RF = 5
    
    Results
    =======
    1) Parameters: 9924
    2) Best Train Accuracy: 98.95
    3) Best Test Accuracy: 99.20

    Analysis
    ========
    1)	Started with randomly placing of dropouts, but the test accuracy didn’t flinch much, 
        so later added dropout to all the layers, noticing the significant difference in accuracies
        (test was getting better)
    2)	Following added GAP to reduce the no. of params in the model, reduced approx. to 8k params, 
        where the accuracy was drawn down but the gap between test & 
        train accuracy was less but test accuracy was far from the expected one 
        (Both train & test were closed to 98%).
    3)	To increase the params, added a layer after gap to increase the efficiency of the model. 
    4)	Since MNIST finds the edges at the RF of 5, rearranged the max pooling operation which
        led an accuracy about train = 98.90 & test = 99.20. (Model not OVERFITTING)
    5)	Now we want to push 99.20 (test acc) towards our goal 99.4.
    6)	Can see image samples being tilted at few degrees, can implement image augmentation to tackle such images.
    
                    K	P	S	jin	nin 	nout	RF	jout
            INPUT				1		28	1	1
            CONV	3	0	1	1	28	26	3	1
            CONV	3	0	1	1	26	24	5	1
            MAX	2	0	2	1	24	12	6	2
            CONV	3	0	1	2	12	10	10	2
            CONV	1	0	1	2	10	10	10	2
            CONV	3	0	1	2	10	8	14	2
            CONV	3	0	1	2	8	6	18	2
            CONV	3	0	1	2	6	4	22	2
            GAP	4	0	1	2	4	1	28	2
            CONV	1	0	1	2	1	1	28	2




4_Image_augmentation_LR
----------------------------
    Target
    ======
    1) Add rotation in between the range of 5 to 7deg
    2) Change or tweak learning rate
    3) Add LR Scheduler
    
    Results
    =======
    1) Parameters: 9924
    2) Best Train Accuracy: 99.06
    3) Best Test Accuracy: 99.45

    Analysis
    1)	Started with 5deg rotation following on to 6 & 7, checking how it would change the train & test accuracies, 
        6deg fitted well & yielded an accuracy closer to our expected one. The train = 98.84 & test = 99.34. 
        since test data had few of these images which had their rotation w.r.t train dataset.
    2)	Tweaking learning rate with LR scheduler – played around with different learning rates & used LR scheduler, 
        by tweaking the step size was giving good results & was effective at every 5th epoch (step size) reducing the LR by 10th.
        
        
                    K	P	S	jin	nin 	nout	RF	jout
            INPUT				1		28	1	1
            CONV	3	0	1	1	28	26	3	1
            CONV	3	0	1	1	26	24	5	1
            MAX	2	0	2	1	24	12	6	2
            CONV	3	0	1	2	12	10	10	2
            CONV	1	0	1	2	10	10	10	2
            CONV	3	0	1	2	10	8	14	2
            CONV	3	0	1	2	8	6	18	2
            CONV	3	0	1	2	6	4	22	2
            GAP	4	0	1	2	4	1	28	2
            CONV	1	0	1	2	1	1	28	2




