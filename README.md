# Automated-non-invasive-biopsy-grading-for-breast-cancer-with-artificial-intelligence
Lancaster University CS dissertation


Abstract:

One in eight women will develop some form breast cancer during their lifetime in the
UK. Due to the advancements mammography technology, the mortality of this disease was
reduced by 42% present since 1998. This project aims to research ways of implementing
an automated non-invasive biopsy grading software using deep learning in order to further
advance the technology in this area of study. This should help the patients by further
reducing the mortality rate. Designing an efficient and accurate state-of-the-art software
would serve as an aid for the physicians giving them extra information, in the end increasing
the overall diagnosis accuracy and consultation time. This thesis will analyse the literature
regarding past implementations of deep learning models for breast cancer classification and
segmentation methods. Four models have been used for researching optimisation strategies
for the task at hand, using the new mammogram dataset VinDr-Mammo. This paper will
cover the behaviour of these models when trained, and based on the results, modify the
dataset to optimise and enhance the results. The dataset suffered different modifications
during the research process of this thesis, starting with the base dataset, going into the
dataset where the patient studies are randomised, then looking into modifying the images
so that just the breast tissue will show, eliminating any empty of extra figures from the
mammograms and ending with different merging techniques dictated by the past results.
The main hypothesis found during the tests was that the images may have been artificially
annotated, setting the same, higher BI-RADS score for the images within the same study
that have the same laterality. This was confirmed in the end, when changing the predictions
according to this hypothesis outputted by the best performing model (DenseNet121 trained
on the randomised and cropped dataset). This rose the accuracy of the model from 74.8%
to 75.5%, but almost doubling the sensitive of all the classes except the overpopulated one
(BI-RADS 1).


The BI-RADS score is an acronym for Breast Imaging Reporting and Database System
score and is a scoring system that radiologists use to describe a mammogram reading, from
healty breast tissue to clear findings of high risk for cancer. For this
project, the 5-point UK scale was used, as it offers a more accurate description of the
type and severity of the cancer.
<img width="648" height="278" alt="birads" src="https://github.com/user-attachments/assets/a8c02725-9beb-46a7-87a7-2ea98c7bcb9a" />

Dataset:
The dataset used was the VinDr-Mammo breast cancer dataset. The images were split into training/validation/test, making sure the class ditribution between the threee training stages and the BIRADS scores contributed proportional procentages in each training stage. The split was 80/10/10. 
The dataset contains cases where one case is 4 images, 2 per breast, from different viewpoints.

*Note: the dataset was highlly unbalanced, from 20.000 images, 13.000 were BIRADS 1, and only 140 were BIRADS 5.

Data augumentation:
Several data augumentation techniques were used. Firstly, the usual random Noise, rotation, translation and other standard pytorch augumentation methods were used. Moreover, the images were reduced to where only teh ROI was visible. Combining images into a single one based on case(all 4 images per person combined) or based on laterality (right breast images combined). 


Results:
In the table below are the results. This was an ongoing process, modifying the loss functions and the dataset to detect the bottlenecks. 
<img width="743" height="222" alt="results" src="https://github.com/user-attachments/assets/07f16ec2-427e-4c1b-b3a2-f36b958e8bed" />

In the end, my hypothesis was that the data was not accurate. After testing, for all cases, both breast had the exact same score, even with very aggressive ones, which is not always the case. Sometimes, the cancer is more visible in one breast or in one viewpoits. This prompred me to test my hypothesis, which was to apply the same thinking to my results.

Below are the confusion matrices showing before and after applying my hypothesis on the best model ran. For this type of application, it is important to keep in mind
the trade-off between precision and recall. It is better to give false positives and those cancer prediction to be trully false, than it is to give a false diagnosis when there
is actually cancer there. For this reason, this change was very beneficial, as it increased the recall in every class except the overly-populated BIRADS 1, while barely decreasing the precision.

Before and after difference:
\begin{itemize}
  \item : Class 0: Precision +0.0394, Recall -0.0314
  \item :Class 1: Precision -0.0207, Recall +0.1314
  \item :  Class 2: Precision -0.0137, Recall +0.0376
  \item :Class 3: Precision -0.0099, Recall +0.0455
  \item :Class 4: Precision -0.0277, Recall +0.0652
\end{itemize}

<img width="366" height="405" alt="Screenshot 2025-09-10 at 17 41 36" src="https://github.com/user-attachments/assets/6b42428c-1c16-4486-8bce-27194bab8a66" />

This table shows, that the bottleneck in this research was the dataset. When the cancer was visible in only 1 breast and the other was healty, it would categorise both of them equall to the biggest score per case,
adding confusion to a model that already has to deal with extremely small and fine details.




