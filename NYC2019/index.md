# Welcome to RadCamp 2019 - The New York City Edition

Part I - Wet lab (3RAD protocol)  
September 14-15, 2019

Part II - Bioinformatics (ipyrad)  
October 12-13, 2019  

Schermerhorn Extension Building Room 1010  
Columbia University  
New York City  

# Summary
This two-part workshop is designed to guide participants through a full RADseq pilot
study.

**Part** I of the workshop is an interactive 2-day wet-lab workshop where attendees will be
guided through a RADseq DNA library preparation ([3RAD]( https://www.biorxiv.org/content/10.1101/205799v4)). 
Participants will have the option of bringing 10-20 of their own extracted DNA samples that can be 
used in the workshop to develop pilot data for their research. In addition to demonstrating and generating 
3RAD libraries, we will introduce RADseq methods, explain common pitfalls and focus on ways to increase 
data quality and reduce missing data while reducing costs compared to other protocols. At the end of the 
first weekend the libraries will be pooled and sent for paired-end Illumina sequencing to generate
~1M reads per sample. The best part is that the sequencing cost will be completely subsidized
(free!). One month later we will meet again to analyze these data.

In **Part II** of this workshop, we will introduce RADseq assembly, phylogenetic and
population genetic methods, high performance computing, basic unix command line and python
programming, and jupyter notebooks to promote reproducible science. We will introduce ipyrad,
a unified and self-contained RAD-seq assembly and analysis framework, which emphasizes
simplicity, performance, and reproducibility. We will proceed through all the steps necessary to
assemble the RAD-seq data generated in Part I of the workshop. We will introduce both the
command line interface, as this is typically used in high performance computing settings, and the
ipython/jupyter notebook API, which allows researchers to generate documented and easily
reproducible workflows. Additionally, we will mentor participants in using the ipyrad.analysis
API which provides a powerful, simple, and reproducible interface to several widely used
methods for inferring phylogenetic relationships, population structure, and admixture.
Participants can give a short research talk on October 12.

This workshop is intended as a bootcamp for early career students, post-docs, or faculty
to learn best practices that they can then help to disseminate to the broader community. The
opportunity to learn while generating and analyzing real data is a bonus that we hope will
accelerate the learning process, particularly for early stage students who can use the pilot data for
their thesis research. This was made possible through generous funding from the Society for the
Study of Evolution, the Society of Systematic Biologists, Columbia University, and The City
College of New York.

# Organisers, Instructors, and Facilitators

  - Deren Eaton (Columbia)
  - Isaac Overcast (CCNY)
  - Sandra Hoffberg (Columbia)
  - Natalia Bayona Vasquez (University of Georgia)
  - Laura Bertola (CCNY)

# Registration

Registration for each weekend will be separate and preference will be given to participants who
can commit to attending both weekends. The workshop will be limited to ~30 participants per
weekend. This workshop is geared toward practicing field biologists without RADseq data for
their system and with little or no computational experience. We encourage all scientists to submit
their application. We especially welcome women and under-represented minorities and early
stage students, or early-career faculty with the potential to pass on skills to large groups. Note
that you will be responsible for your own lodging, transportation, and meals. We will provide coffee 
and snacks during breaks. Please only apply to the workshop if you acknowledge that if accepted, 
you will commit logistically and economically to attend. A registration fee ($15 per weekend) 
will be due upon acceptance. Nobody will be turned away for lack of funding - if you would like 
to request a fee waiver, contact the organizers.

# Wet Lab (3RAD) Schedule

Times            | Saturday 9/14 | Sunday 9/15 |
-----            | ------ | ------- |
8:30-9:00       | Check-in and refreshments | Check-in and refreshments |
9:00-12:30      | [Lecture](Part_I_Files/RADcamp2019_slides.pdf) | Library amplification |
12:30-13:30 | Lunch | Lunch |
13:30-17:00 | Digestion and Ligation | [Library amplification and QC](Part_I_Files/gel_images_of_complete_libraries.pdf) |
17:00-19:00 | Free evening        | Networking dinner |

## 3RAD resources
* [i7 and inner barcodes used during workshop](Part_I_Files/sample_tags.pdf)
* [Find the i5/i7 index sequence from the name](Part_I_Files/Sample_tags_populator_2019.xlsx)
* [Inner barcode sequences in ipyrad format](Part_I_Files/plate_inner_barcodes.txt)
* [BadDNA order form with index sequences](Part_I_Files/BadDNA_Oligo_Order_Form_current.xlsx)
* [Full 3RAD protocol for plates](Part_I_Files/3RAD_Molecular_ID_Protocol.docx)
* [Library pooling guide](Part_I_Files/Library_Pooling_Guide_with_directions_June2016.xlsx)
* [Adapter Info](Part_I_Files/3RAD_iTru_adapter_TaggiMatrix.xlsx)
* [How to resuspend adapters](Part_I_Files/Adapter_Mixed_Plate_Instructions.docx)
* [How to resuspend primers - i7 and i5](Part_I_Files/Primer_Plate_Instructions_1.25nmole.docx)
* [Index diversity calculator](Part_I_Files/Index_diversity_calculator_June2016.xlsx)
* [Homemade speedbeads](Part_I_Files/Speedbead_Protocol_June2016.docx)


# Bioinformatics (ipyrad) Schedule

Times            | Saturday 10/12 | Sunday 10/13 |
-----            | ------ | ------- |
8:30-9:00       | Check-in and refreshments | Check-in and refreshments |
9:00-12:30      | [Introductions, data QC, and ipyrad CLI Part 1](RADCamp-PartII-Day1-AM.md) | [ipyrad API and analysis tools](RADCamp-PartII-Day2-AM.md) |
12:30-14:00 | Lunch | Lunch |
14:00-17:00 |[ipyrad CLI Part 2 & 3RAD Assembly](RADCamp-PartII-Day1-PM.md) |  [Small group analysis of real data](RADCamp-PartII-Day2-PM.md) |
17:00-19:00 | Networking Dinner | Social |

## Additional ipyrad analysis cookbooks

* [Tetrad - A Quartet-based species tree method](https://nbviewer.jupyter.org/github/dereneaton/ipyrad/blob/master/tests/cookbook-tetrad.ipynb)
* [Phylogenetic inference: RAxML](06_RAxML_API.md)
* [Clustering analysis: PCA](04_PCA_API.md)
* [Clustering analysis: STRUCTURE](05_STRUCTURE_API.md)
* [BPP - Bayesian inference under a multi-species coalescent model](https://nbviewer.jupyter.org/github/dereneaton/ipyrad/blob/master/tests/cookbook-bpp-species-delimitation.ipynb)
* [Bucky - Phylogenetic concordance analysis](https://nbviewer.jupyter.org/github/dereneaton/ipyrad/blob/master/tests/cookbook-bucky.ipynb)
* [ABBA-BABA - Admixture analysis](https://nbviewer.jupyter.org/github/dereneaton/ipyrad/blob/master/tests/cookbook-abba-baba.ipynb)
* [Demographic analysis ([momi2](07_momi2_API.md))

## RADCamp NYC 2019 co-sponsored by:

![SSE](images/SSE.png)
![SSB](images/SSB.png)  
![CUNY Graduate Center](images/GC-logo.png)
![Columbia E3B](images/E3B-logo.jpg)

# RADCamp NYC 2019 Part I Group Photo
![jpg](RADCampNYC-2019-PartI.jpg)


# RADCamp NYC 2019 Part II Group Photo
Don't forget to get a sweet group photo!

## Acknowledgements
RADcamp NYC 2019 Part I materials are prepared by Sandra Hoffberg, Natalia Bayona Vasquez, and Travis Glenn. Many things we reference can be found on [badDNA.uga.edu](https://baddna.uga.edu). We borrowed supplies from the Rubenstein, Duik-Wasser, and Hickerson labs at Columbia and CCNY.
RADCamp NYC 2019 Part II materials are largely based on materials from the [RADCamp AF-Biota workshop](https://radcamp.github.io/AF-Biota/) which were created by Isaac Overcast, Mariana Vasconcellos, and Laura Bertola.
