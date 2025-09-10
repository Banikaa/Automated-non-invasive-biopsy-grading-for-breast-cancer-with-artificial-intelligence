# Automated-non-invasive-biopsy-grading-for-breast-cancer-with-artificial-intelligence
Lancaster University CS dissertation


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
