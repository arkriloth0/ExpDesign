<p align="center">
  <i>Dr. Sina Beier</i>
</p>

This guide aims to help you design better experiments. Well-designed experiments lead to high-quality data analysis and robust, meaningful results.

This guide is written with biological - mostly high-throughput sequencing-based - experiments in mind, but the general concepts apply to many types of experiments. It should cover all major issues you would encounter during experiment design, but if you have further questions don't hesitate to let us know.

## Table of contents
### Before you begin
1. [Where to start](#start)
2. [Having a well-defined research question is important](#hypothesis)
3. [Ethical considerations](#ethics)
### Replicates and Controls
4. [Different types of replicates](#rep_type)
5. [What are good biological replicates?](#rep_biol)
6. [How many replicates do you need?](#rep_number)
7. [Different types of controls](#control_type)
### Sequencing 
8. [What is the best sequencing depth for my experiment?](#seq_depth)
9. [DNA/RNA concentration needed and how to deal with issues](#concentration)
### Confounders, Batch Effects and Bias
10. [Confounding factors and how to deal with them](#confounder)
11. [How to avoid and deal with batch effects](#batch)
### Good Experiment Design
12. [Do I need to run another set of controls for each experiment?](#control_pub)
13. [Quasi-Experimental Design](#quasi)
14. [Pilot experiments provide insights into how to get the best results](#pilot)
15. [Human bias](#bias)
16. [Metadata](#metadata)
17. [Examples for good vs bad experiment design](#examples)
### Final remarks
18. [Can’t I just use AI to plan my experiment?](#ai)
19. [Final remarks](#final)
20. [References](#ref)

<figure>
<p align="center"><img src="https://github.com/BioinfSina/GuidesAndDocs/blob/main/Pictures/expPlan.svg" alt="Flow of experiment design"></p>
<figcaption><p align="center"><i>Experiment design goes from an idea or hypothesis through an iterative process of improving an experiment design by including, for example, literature research, expert advice, creating preliminary experiment plans, conducting pilot experiments and getting ethical approval until finally converging into a plan for the final experiment.</i></p></figcaption></figure>


## Where to start
<a id="start"></a>
When designing an experiment, the first step is to define your [hypothesis](#hypothesis) or biological question. Based on that you can identify the methods used to answer your question. These choices then lead to further choices about how the experiment might be designed.
With a hypothesis in mind, you should already start talking to collaborators and facilities that might be involved in the process, so they can help you make sensible choices about methodology and experimental design. For non-standard experiments, you likely need a [pilot experiment](#pilot) to test and practice different processes and to design the experiment to best answer your question.
A successful pilot experiment helps you make informed decisions on necessary changes as well as deciding the [number](#rep_number) and [types](#rep_type) of replicates and [controls](#control_type) necessary for the main experiment. You can identify issues like [batch effects](#batch) and [confounding factors](#confounder) and will need to adapt your design or analysis to appropriately deal with them. Once you are conducting your main experiment you will also need to collect appropriate [metadata](#metadata) to aid future analysis and reproducibility.
In this guide, we will talk about each step of experiment planning. It is, however, a general guide and each experiment will be different. This is not a substitute for consulting with us (<a href="mailto:bioinformatics@gurdon.cam.ac.uk">bioinformatics'at'gurdon.cam.ac.uk</a>) and other facilities to ensure the best results.


<a id="hypothesis"></a>
## Having a well-defined research question is important

With a vague goal in mind and abundant measurements and observations, you could try and get as much out of a single experiment as humanly possible. But would this approach really allow you to answer any questions properly?

In experiments, we can either follow a hypothesis-driven design or a more observational, hypothesis-free design.
Hypothesis-driven design involves a research question, which is testable and allows you to design a well-defined and reproducible experiment to answer this specific question properly.
For example, if the hypothesis is that stem cells will proliferate more under condition 1 than under condition 2 you would grow them under both conditions and monitor proliferation. If the hypothesis is correct all (or at least a significant number) samples from condition 1 will be more proliferative than any of the samples under condition 2.
Having a good hypothesis is the optimal situation, but especially in sequencing-based experiments, people often take a more investigative approach, utilising a hypothesis-free design. This approach may seek to observe development, disease or the effect of a treatment over time, in multiple genetic backgrounds or environments, without a clear idea of what is expected. The nature of -omics experiments means that you can get a good overview of, for instance, how the expression of every gene changes and this can be useful for discovering new knowledge about your biological system of interest. 
There might not be a defined hypothesis that you are testing, but you should take into account as much prior knowledge as possible to define the parameters of your experiment. You should also expect to do further experiments to more specifically answer hypotheses generated by your initial experiment. A good hypothesis-free design should still have a primary focus and a clear end goal for your experiment.

A well-defined research question enables you to define the most appropriate experimental design required to answer that question including which time points are needed for sampling, what concentrations of a drug or nutrient should be used, how long treatment will need to last to have the expected effect and many more details that help to achieve the best results possible. [Pilot experiments](#pilot) can then help to optimise those values and decisions.

<a id="ethics"></a>
## Ethical considerations

Good experiment design includes considering the ethical implications of your experiment. <i>In vivo</i> experiments can be done in a live animal model or donated human embryos. This comes with considerations of the ethical use of these resources. They also apply to synthetic embryos created from stem cells, as we do not have separate guidelines for them yet. In this case, detailed experiment design is even more important to make sure you have exactly as many replicates as necessary for good results and also avoid any unnecessary use of the resources. It might even be necessary to do [pilot experiments](#pilot) for better estimation of variance and calculation of statistical power, which is often required for ethical approval.
Ethical considerations can limit the extent of your experiment, including number of replicates, strength of dosage (in life animals) or length of observation. For example, there are clear limits on how long embryos can be grown or at what point you will have to humanely sacrifice an animal if it's health is declining too rapidly.
Getting the necessary approval is often a back and forth conversation with the approving body and involves discussing the feasibility of an experiment within ethical constraints. To speed up this process it is helpful to start with a well-thought-through design and decisions informed by pilot experiments, legal guidelines, statistical power analysis and relevant publications.
Guidance on these matters is given by the Animal Welfare & Ethical Review Body (AWERB) [[1]](#1) and your departmental or institutional Research Ethics Committee. The AWERB will also have to approve you with a project licence for any experiments involving live animals. You should expect to adhere to the three Rs - **Replacement** (replace methods requiring life animals with other experimental techniques where possible), **Reduction** (reduce the number of animals included to the minimum which achieves the aim of the research) and **Refinement** (adapt experimental procedures to induce minimal suffering in the animals involved). 

<a id="rep_type"></a>
## Different types of replicates

We usually have two different types of replicates, technical and biological replicates.

<figure>
<p align="center"><img src="https://github.com/BioinfSina/GuidesAndDocs/blob/main/Pictures/replicate_types.svg" alt="Biological and Technical Replicates in comparison"></p>
<figcaption><p align="center"><i>Comparison of the design and process of handling biological and technical replicates in a high-throughput sequencing-based experiment.</i></p></figcaption></figure>


Technical replicates are achieved by either sequencing the exact same sample multiple times or by splitting a sample into multiple (sub)samples. Those samples will then be separately processed through the same pipeline. This is done to ensure reproducible results and a consistent process. If you plan to include them based on worries about inconsistencies in the process it might be beneficial to do a [pilot study](#pilot) to make sure the potential variability and any necessary additional training, equipment maintenance or adaptation of the main experiment has been identified.
It is tempting to exclude technical replicates - which can be done for well-established protocols - but it is better to adapt analysis or repeat an experiment if the technical replicates showed issues than to unknowingly publish irreproducible (and potentially wrong) results. For novel protocols or ones you have not personally conducted before it is always a good idea to include technical replicates even if a [pilot experiment](#pilot) has been conducted beforehand, as it can help to exclude or identify technical issues as a source of variation.

[Biological replicates](#rep_biol) are samples taken from multiple closely related sources that underwent the same treatment in the experiment. In an animal experiment that would mean sampling from multiple animals in the same treatment group. For cell lines, it could mean using cells from different passages or fully independent cultures. For organoids, it involves generating them from different batches of stem cells or tissue samples or even deriving stem cells from completely different donors. This ensures accounting for individual variation. Biological replicates need to be chosen so the variation between replicates does not overpower the variation you wish to measure. While technical replication is usually not necessary, biological replication is essential.


<a id="rep_biol"></a>
## What are good biological replicates?

Good biological replicates are based on being as biologically close to each other - at least in respect to measures which are important for your experiment - as possible without being the same. In an experiment on a cell line this can, for example, mean aliquoting your cells into 12 tubes, then treating half with a drug and half with just buffer. For a mouse experiment, that would mean using replicates with the same genetic background, the same age, from the same litters. There can be known variation in a group of replicates, for example including male and female mice or multiple genetic backgrounds, but in an optimal situation, those subgroups would be both equally distributed and have enough replicates amongst themselves to identify any effect based on their differences (a [confounding factor](#confounder)). So a good example is using 5 male and 5 female mice in one group, while a bad grouping would include 2 male and 8 female mice.
In the bad example, any effect only seen in male mice will not be able to be statistically distinguishable from the average. Another option would be to perform the experiment only on male or only on female mice, which can give better results but at the same time limit generalisability and potentially selection of enough individual mice at the same age or from the same litter might not be achievable.

When studying human disease, it is often not possible to assign the treatment group randomly. If the group of interest is patients with a given medical condition, they might tend to have differing backgrounds and lifestyles from the general population. These factors would then be confounded with the medical condition. It is helpful to go with a [quasi-experimental design](#quasi) in those cases.

Another common problem is to define a biological replicate regarding cell lines. One solution could be using multiple separate freezer stocks, which can be expensive or not feasible. The common solution for biological replicates in <i>in vitro</i> experiments is to maintain separate cultures of the same cells. However, the less variation you have between your replicates, the better you can determine detailed causal relationships or study smaller effect sizes.


<a id="rep_number"></a>
## How many replicates do you need?

With sequencing-based experiments we expect an absolute minimum of three biological replicates per sample group. With two or fewer replicates it is harder to accurately access variability and estimate error for calculation of standard error and standard deviation. If one of the samples is invalid or cannot be used for any reason you would end up with no replication and no statistical power.
That's why you should not collect fewer than three biological replicates per condition. With three replicates, you have the chance to spot outliers and swapped samples - two samples agreeing on a measurement and one disagreeing would indicate that the third one is an outlier. It is rarely possible to decide if a single outlier has biological significance or not, hence it is generally better to include more than three replicates. The more replicates we have the more accurately we can determine the mean and standard error of our measurements. With only two replicates we will not get a good estimate and we are less likely to be able to distinguish even moderate differences in expression between conditions. 
While in practice, three biological replicates are generally sufficient to detect outliers and to find significant differences between your conditions, they are often not actually enough to find all the real differences (false negatives) and exclude erroneous results (false positives). But how many do we need?

<figure>
<p align="center"><img src="https://github.com/BioinfSina/GuidesAndDocs/blob/main/Pictures/outliers.svg" alt="Influence of outliers on your results"></p>
<figcaption><p align="center"><i>Left: PCA plot of an experiment group with three samples, one of them an outlier. Right: Box plot of mean (horizontal line) and variance (grey box) of this group with the outlier included and removed from the calculation, showing the strong influence of a single outlier in small groups.</i></p></figcaption></figure>


Schurch et al. (2016) [[2]](#2) discuss the necessary number of replicates to achieve good results in bulk RNA-seq experiments. They see increases in true positives and decreases in false negatives until up to 40 replicates per group! Using appropriate analysis tools and fold change thresholds, they suggest that 12 replicates per group are enough for high-quality results in bulk RNA-sReq.
12 replicates sounds like a lot, but we strongly suggest including at least 6 replicates to generate useful results in most situations. You need to consider that potentially not all of your replicates will pass sequencing and pre-processing quality control and some could be outliers. Outliers can be caused by unexpected biological variation like a rare genetic variant, contamination or experimental error. If they are singular occurrences it can be necessary to exclude them, however, if there are multiple outliers in a group it would be better to look into finding the exact cause and consider they might be showing valid variations.

Statistical power analysis gives you a mathematically supported number of replicates required to work with the expected variation. While it is a statistically sound tool, it is based on estimates for variation and effect size [[3]](#3), [[4]](#4). It can be difficult to define these estimates appropriately without [pilot experiments](#pilot). Hence, we suggest going with a number of replicates known to work for technically and biologically similar experimental designs instead of doing a power analysis with questionable input estimates.

Cell lines generally show less variability than for instance tissue samples from genetically divergent humans. While we advise having at least 6 replicates per group as a general guideline, when working in a very controlled system like a cell line derived from the same individual this can be reduced down to the minimal three [[5]](#5). Generally speaking, higher variability requires more replicates to capture effects of the same size. Smaller effect sizes also require more replicates to be detected than larger effect sizes.
Using an appropriate number of biological replicates is crucial for ensuring the reliability and reproducibility of results. It allows you to capture variability, increase statistical power and confidence in findings, identify outliers and improve data quality - achieving robust and trustworthy results. It can be difficult to decide what number of replicates is appropriate, which is why we would suggest for you to aim for six replicates if you are in doubt and consult with us for further discussions.


<a id="control_type"></a>
## Different types of controls

The most commonly used control types are positive and negative controls. Positive controls receive a treatment which is known to elicit the measured effect, while negative controls are usually untreated and should not show the studied effect at all. Negative controls act as a point of reference, allowing us to measure the size and direction of effects in our treatment groups. Positive controls can tell us whether the experiment has worked. If the positive control fails to show the expected result, something went wrong with the experiment. If the positive control succeeded, but the treatment group shows no effect, we can be confident there really is no effect.

To define appropriate controls it’s important to know the potential for variability in the experiment. Higher variability will require more replicates to capture the full range of outcomes reliably and distinguish true biological variability from accidental outliers based on issues with the experiment or environmental influences. Controls should be spread over all batches to generate a baseline which doesn’t suffer a batch effect. Optimally control samples are chosen randomly, but can also be blocked to include the same diversity as the treatment groups to avoid known [batch effects](#batch).
A simple example of this is how an allergy scratch test would be controlled by just scratching the skin without added substance for a negative control and a scratch with added histamine for a known reaction as a positive control to establish a baseline of reactivity for the patient.
For a bulk RNA-seq experiment, you might use a treatment with a well-known outcome as a positive control, for example treating with a cytokine and expecting upregulation of genes known to be triggered by this cytokine. This is only relevant if you are expecting and hoping to measure activation of the same pathway through other means in your treatment group.
Another form of control are mock treatment controls. In humans this could be a placebo instead of no treatment. In a cell line or model organism-based experiment this involves comparable handling of the controls and treatment groups, but without applying the treatment itself in the control e.g., using mock injections with PBS [[6]](#6).
Preferably division into treatment and controls should be done without prior knowledge at the start of the experiment to avoid bias, for example choosing ‘stronger’ individuals for a treatment group to avoid having dropouts. 
Optimally control groups have just as many individuals as treatment groups. In [quasi-experimental design](#quasi), control groups tend to be bigger than treatment groups to capture general population diversity.

<a id="seq_depth"></a>
## What is the best sequencing depth for my experiment?

It can be difficult to decide on the proper sequencing depth for an experiment. Standard experiment designs can be compared to existing advice on sequencing depth - but it has to be kept in mind that advice on ‘reads per sample’ is usually only applicable to human or mouse genomes or ones with similar size and structure.

Some examples are:

* 20,000 read pairs per cell as a minimum in single-cell RNA-seq for 10x Genomics sequencing [[7]](#7), but more for RNA-rich (e.g. tissues like spleen and thymus) samples or dependent on the questions asked, generally around 60,000 reads per cell for typical samples [[8]](#8)
* 25,000 read pairs per spot for Visium FFPE v1
* 25-50 M reads per sample for bulk RNA-seq depending on the complexity of the sample
* Calculate based on coverage for whole genome sequencing (Coverage = read length * number of reads / genome size). 30-100x whole genome coverage is commonly used for calling variants based on Illumina short reads.

The final answer depends on your needs, the protocols and technology you are using, the organism sequenced, the type of analysis you plan to do and financial constraints. Aim to have close to the numbers suggested, but don’t add a full sequencing run if you would achieve 90% of those numbers without it.
It is worth taking the complexity of the sample into account. A cell line is less complex than for example a tissue. 

If you are interested in a gene expressed at low level in a rare cell type within a tissue sample you would need more reads to detect it than a lowly expressed gene in a cell line. If you plan to look at specific celltypes and have information on their expected frequency in the sample, aim to have at least 100 cells of the least abundant celltype of interest per sample and calculate the necessary total of cells per sample based on that frequency. Increased sequencing depth is required for more complex samples.

For example, if you have a human bulk RNA-seq experiment with 5 treatment samples and 5 control samples, and you know that a good sequencing depth for a human bulk RNA-seq is about 30M reads per sample because of the diverse transcriptome you would need to 30 M reads * 10 samples = 300 M reads in total. This amounts to nearly a full lane of sequencing on an Illumina NovaSeq 6000 using v1.5 chemistry (based on 350-450M reads per lane).

<a id="concentration"></a>
## DNA/RNA concentration needed and how to deal with issues 

The DNA/RNA concentration needed as input for sequencing library preparation depends on the library protocol used, the requirements requested by the sequencing provider and what you want to achieve with your data. In most cases, you can expect to need at least 150 ng of total RNA/DNA to achieve good results, but it can vary between 50 ng and 1 µg per sample. Low input or ultralow input libraries are available and can reduce the input requirements down to 200pg of RNA, however, it will then be even more important to achieve high input quality by avoiding degradation.

Concentration can be measured with different methods, the most commonly used being NanoDrop, QuBit or Tapestation machines, or qPCR.

* **NanoDrop** is a simple spectrometry-based method that provides information on DNA, RNA, or protein concentration, as well as sample purity. It is quick, cheap, and easy to use, but it tends to overestimate DNA concentration.
* **QuBit** is based on fluorometry, measuring DNA or RNA concentration in a sample using their binding to a fluorescent dye. It is less affected by contaminants and generates more reliable measurements, especially at very low concentrations.
* Agilent **TapeStation** systems are based on electrophoresis. They analyse multiple samples in parallel and also generate a qualitative measurement, but are less reliable than a QuBit measurement.
* Quantitative PCR (**qPCR**) is the most accurate but most expensive and time-consuming method for DNA quantification. Rarely used for large-scale sequencing preparation.
 
Some sequencing providers require fluorometry-based readings to ensure the input requirements for their promised throughput results are met.

If you cannot achieve the optimal concentration for sequencing, there are a few options:

* **Dilution:** If samples have widely differing input concentrations, they should be diluted to a more unified concentration to ensure comparable results in multiplexed sequencing.
* **Improving Extraction Protocol:** If concentrations are generally too low, try to improve the extraction protocol. Pilot experiments are useful, especially if extracting from a tissue type or organism new to you.
* **Increasing Input:** Possibly increase the mass of the input material.
* **PCR Cycles:** If it is not possible to increase the extracted DNA or RNA, increasing the number of PCR cycles in library preparation is an option, but this must be documented to be able to troubleshoot the resulting batch effects in the analysis process. Preferably all samples within an experiment should be subject to the same number of PCR cycles.

<a id="confounder"></a>
## Confounding factors and how to deal with them

Confounding factors include batch effects but are more generally any factors influencing the outcome of an experiment. They are connected both to the causal independent variable (e.g. treatment), and the dependent variable, which is the measured effect (e.g. gene expression levels). However, confounding factors are different from the independent variable. They are correlated with the independent variable and causally related to the dependent variable. This can make it hard or even impossible to distinguish the effect from being caused by the (observed or changed) independent variable or the correlated confounding factor. 

Confounding factors can be mitigated by using techniques like randomisation, where you don’t know what the confounding factors are, and blocking where you do. If that is not possible they can only be potentially discussed if they are part of the collected metadata.
If possible you would **restrict** your treatment and control group to only subjects with the same value for a confounding factor. For example, only using male or female participants in studies where sex-related diseases or hormones can be confounding. However, this may restrict the generalisability of your experiment.

<a id="random"></a>
**Randomisation** is a way to reduce the impact of a known confounding factor. Individuals are randomly assigned to the treatment and control groups - which should lead to the confounding factors affecting both groups in the same way.

<a id="block"></a>

A more direct method is **blocking**, where you allocate the same number of individuals affected by the same value of the confounding factor into all control and treatment groups, for example having age-matched controls or comparable numbers of male and female subjects to account for sex differences.

<figure>
<p align="center"><img src="https://github.com/BioinfSina/GuidesAndDocs/blob/main/Pictures/blocking.svg" alt="Comparison of a mouse experiment with and without blocking for sex differences."></p>
<figcaption><p align="center"><i>Comparison of male (light blue) and female (light pink) mice distributed to treatment (red) and control (yellow) groups with and without blocking for a batch effect caused by the sex of the mice.</i></p></figcaption></figure>


Blocking and randomisation control for confounding variables, restriction avoids them and collecting abundant [metadata](#metadata) helps deal with them during analysis - especially for factors that were unknown during experiment design.


<a id="batch"></a>
## How to avoid and deal with batch effects

Optimally, all samples in your experiment are treated in exactly the same way, by the same person under fixed conditions at the same time. In reality, it's rarely like that, which introduces batch effects. Batch effects are a subset of [confounding factors](#confounder) caused by technical factors like using multiple reagent batches or changing personnel.
Methods to avoid and deal with batch effects by adapting the experiment design are [randomisation](#random) and [blocking](#block).
Some batch effects cannot be avoided. For example, if you are conducting a longitudinal study to investigate the progression of a disease over several years, collecting blood samples from patients at multiple time points: baseline, 1 year, 2 years, and 5 years. The technology and equipment used for sample processing and analysis evolve, leading to differences in the data generated at each time point. Even if you can keep the equipment the same, it will have been maintained multiple times throughout the experiment, and reagents will come from different batches, as they do not keep long enough. In this scenario, batch effects are introduced by the changes in technology, reagents, and equipment over the years and you cannot avoid the effect caused by these changes.
Other batch effects can be mitigated by controlling how they affect the results through experiment design. Having to sequence samples over multiple runs could introduce a batch effect per run, but if you ensure running an equal number of samples from each experimental group on each run as well as including each treatment group in each run (blocking), this might still introduce a measurable batch effect for the runs, but it will not obscure your results when comparing the treatment groups. Alternatively, all samples could be sequenced at lower depths on each of the runs, resulting in multiple technical replicates per sample, which are merged for analysis.

Batch effects that can not be avoided through those methods or were unknown until data analysis uncovered them can sometimes be algorithmically controlled or corrected for during analysis  [[9]](#9). This usually requires the availability of unaffected controls or samples to correct for the batch effect. Methods not based on using information from unaffected samples as a baseline are available but can potentially introduce another bias or only change the bias from the batch effect to be less noticeable. They could obscure actual biological variation by overcorrection. Hence, if it is not possible to avoid or correct the batch effect during experiment design, it might be advisable to leave it in and discuss it using the appropriate metadata for reference, taking known biological effects into account.

Dealing with batch effects that couldn’t be avoided in the analysis is often done through specific toolkits, for example, Harmony [[10]](#10) (for scRNA-seq or spatial transcriptomics) and ComBat [[11]](#11) for bulk RNA-seq.


<a id="control_pub"></a>
## Do I need to run another set of controls for each experiment?

It can be tempting to reuse controls from a previous experiment or published data. However, this approach has multiple problems. Even with controls from a comparable previous experiment in the same lab, there will still be a significant potential for a [batch effect](#batch) from the control being processed at a different time, with a different batch of reagents, by a different person. Published data will have all these confounding factors, plus potentially different genotypes, different experimental protocols, different library preparation kits and different sequencing machines. Therefore, it is never advisable to forego controls in your current experiment.

<a id="quasi"></a>
## Quasi-Experimental Design

If the treatment group is impossible to [randomise](#random) - for example, patients with a specific disease - you can utilise a quasi-experimental design to define [control groups](#control_type) in a way that allows controlling for [confounding factors](#confounder).
There can be inherent confounding factors, like risk factors of a studied disease. For example, a study group with lung cancer would include a larger number of smokers than expected in the general population. Even if a similar number of smokers can be added to the control group, healthy smokers have an increased risk of having undiagnosed lung cancer or precancerous lesions based on this risk factor.
The quasi-experimental design relies either on carefully matched controls or covering the expected diversity of a relevant group or the general population through large control groups. Matching controls can include age, sex, gender, ethnicity, environment, genetics (family members), disease status for a set of related diseases, risk factors and more depending on your patient group. Finding an appropriate control group can be difficult and will usually come with some compromise. Hence, healthy control groups are often much larger than the patient group to cover the general population diversity without matching each patient.

<a id="pilot"></a>
## Pilot experiments provide insights into how to get the best results

Pilot experiments are small-scale studies conducted before the main experiment. They are crucial for refining and improving the design of your main study.
A pilot experiment can be used to assess the feasibility of the experiment, test and practice the procedures, and generate example data for analysis. They help determine the amount of expected variation and thus ensure the number and type of replicates and controls collected are appropriate. They can be used to determine what is an appropriate sequencing depth and to determine the number of cells you need to collect for a scRNA-seq experiment so you can analyse a rare cell population.
 
While having a preliminary experiment seems not cost or time effective, conducting pilot experiments can save you time and money in the long run by optimising the experiment design and ensuring you have the right training and analysis tools available before starting a larger experiment. This way, you maximise the outcomes of the main experiment without risking a loss of time and resources.

The general way to design a pilot experiment involves reducing your number of samples to a ‘minimal example’. However, for a single-cell RNA-seq experiment, you could aim to sequence a large number of cells at high depth, to determine the optimal number of cells and [sequencing depth](#seq_depth) on the full set of samples in the main experiment.


<a id="bias"></a>
## Human bias

Bias is ever present in our world and experimental designs. Just like asking someone suggestive questions can ensure getting the answer you want, bias can also influence experiments. Biased experiments lead to biased results which cannot be replicated.
It sounds convenient if a pilot experiment showed you the expected results for 4 out of 6 genetic backgrounds to omit the unexpected ones in the main experiment and get a cleaner result. This is a valid choice and can make publication easier, but a less biased solution would be to discuss the [pilot experiment](#pilot) results in the publication and argue why you have been focussing on the selected backgrounds. Otherwise, an experiment might give the implication that it is generalisable even though biased selection is only making it seem so.

There can also be subconscious biases. For example, choosing a cell line you have previously worked with over one that is objectively more appropriate because you have more experience with it. Similarly, when working with multiple cell lines or technologies in the same experiment, ones you have more experience with can give you better results than ones you are working with for the first time. To avoid biased choices and results, additional training and pilot experiments are helpful.
Subconscious bias is also well known to be present in experiments with human participants, leading to placebo or nocebo effect in patients or biased treatment by researchers or health care personnel. This is why we introduce blinding - either of the researchers and care personnel, the patients or optimally both. In human experiments, this generally involves blinding knowledge about treatment and placebo groups for patients and researchers or the disease status of the volunteers for researchers.
Blinding can also be used in molecular biology - for example having someone interpret Western Blotting or immuno-staining results who doesn't know the assignment of samples to groups to avoid biased interpretation of band or staining intensities.
It is important to talk through experiment design with colleagues who can point out subconscious biases to you. 

<a id="metadata"></a>
## Metadata

Metadata provides context for your data and ensures reproducibility. There are standardised rules for metadata necessary to publish and upload data in the appropriate databases [[12]](#12), but it is also very important to collect as much metadata as possible for better analysis.
Metadata can help identify [confounding factors](#confounder) during analysis and underpin the biological validity of your results.
It is important to document metadata consistently and through standardised measures. However, it can also be helpful to keep general notes and observations during an experiment as metadata.
Types and examples of metadata include sample-associated metadata (sampling time, genetic background, age, disease status), preparation metadata (sampling protocol, RNA extraction, number of PCR cycles, RIN numbers, library prep), experimental metadata (observations and changes, behaviour) and analysis metadata (analysis workflow, software versions, necessary curation steps, exclusion of outliers).

<a id="examples"></a>
## Examples for good vs bad experiment design

### Bulk RNASeq mouse experiment

**Objective:** Investigate the effect of a new injectable drug on gene expression in mice

#### Design
**Treatment Group:** Mice injected with the drug  
**Mock Treatment [Control](#control_type):** Mice injected with PBS  
**Negative Control:** Healthy mice not injected with either   

#### Challenges	
**Known [Batch Effect](#batch):** Experiment requires two days of RNA extraction and multiple sequencing runs

**[Confounding Factor](#confounder):** Age of the mice

#### Good Experimental Design:

* [Randomisation](#random): Randomly assign mice to each group at the start of the experiment to minimise selection bias
* [Replication](#rep_number): Include six biological replicates for each group 
* [Blocking](#block): Distribute equal numbers of samples from each group on both extraction days and all sequencing runs
* Blinding: Animal facility staff are blinded to the group assignments to reduce chances of [biased](#bias) treatment
* Control for [Confounding Factors](#confounder): Use age- and sex-matched mice for all groups to control for variability

Sequence each sample to a [depth](#seq_depth) of 25-30 million reads to enable differential expression analysis of known mouse genes.


#### Issues to avoid (bad design):

* Lack of Randomisation: Selecting mice perceived as stronger or healthier for the treatment group
* No Replication: Use only two mice per group, making the results unreliable and statistically invalid for analysis
* Ignoring Batch Effects: Each group has RNA extraction on a separate day and is sequenced on a separate run
* No Blinding: Staff know the group assignments, potentially causing biased behaviour.
* Confounding Factors: Use younger mice for the treatment group and older ones as a negative control, all male mice are in the mock treatment group

### Working with patients - [Quasi-experimental design](#quasi)

**Objective:** Evaluate the impact of a new medication on the methylation patterns in patients with lung cancer.

#### Design:
**Intervention Group:** Patients with lung cancer who receive the new medication  
**Standard Care Group:** Patients with lung cancer who receive the current standard of care  
**Control Group:** Healthy individuals  

#### Challenges:
**Smoking as a Confounding Factor:**  
Issue: Smokers are more prevalent in lung cancer patients than in the general population. If the control group has fewer smokers than the intervention groups, it could skew the results. Cancer is more likely to develop later in life.   
Solution: Ensure all groups have a similar proportion of smokers to control for this variable and have the same age range.

**Risk of Pre-Cancerous Lesions or Undiagnosed Lung Cancer in Smokers:**   
Issue: Smokers in the control group might have pre-cancerous lesions or undiagnosed lung cancer  
Solution: Detailed health checks for the control group to remove individuals at risk

A larger control group is necessary to take into account potentially having to remove participants from the control if they develop lung cancer, keeping enough participants for statistically relevant results.
[Sequencing depth](#seq_depth) is highly dependent on your financial constraints, as sequencing required for methylation analysis tends to be more expensive. It could be advisable to do targeted sequencing of selected regions of interest.

<a id="ai"></a>
## Can’t I just use AI to plan my experiment?

AI can assist you with planning steps like workflows for data analysis but usually gives very generalised advice. While it is helpful to get started or identify known issues with a design or workflow you are planning to use, it is no match for human professionals. If you struggle with experiment design, talk to your colleagues and friendly core facility staff before haggling with a large language model that might or might not give you advice appropriate for your specific needs. If you have used AI in planning please cross-check your results with human experts to avoid disappointment.

<a id="final"></a>
## Final remarks

A lot of information on experiment design is based on a perfect world where your resources are unlimited and your choices only affected by your aim to optimise the experiment. We have aimed in this guide to give realistic and feasible advice. Realistically, there will be decisions made based on funding availability, time restrictions, practicality and availability of equipment and expert knowledge. In those cases, discussing with experts how to achieve the best design under given constraints is especially important.
Contact us (<a href="mailto:bioinformatics@gurdon.cam.ac.uk">bioinformatics'at'gurdon.cam.ac.uk</a>) if you would like to discuss your experiment at any stage of the process - the earlier, the better.

<a id="ref"></a>
## References

<a id="1">[1]</a>
‘Animal Welfare & Ethical Review Body’. 6 February 2015. https://www.ubs.admin.cam.ac.uk/animal-welfare-ethical-review-body.

<a id="2">[2]</a>
Schurch, Nicholas J., Pietá Schofield, Marek Gierliński, Christian Cole, Alexander Sherstnev, Vijender Singh, Nicola Wrobel, et al. ‘How Many Biological Replicates Are Needed in an RNA-Seq Experiment and Which Differential Expression Tool Should You Use?’ RNA 22, no. 6 (June 2016): 839. https://doi.org/10.1261/rna.053959.115.

<a id="3">[3]</a>
Peterson, Sarah J., and Sharon Foley. ‘Clinician’s Guide to Understanding Effect Size, Alpha Level, Power, and Sample Size’. Nutrition in Clinical Practice 36, no. 3 (2021): 598–605. https://doi.org/10.1002/ncp.10674.

<a id="4">[4]</a>
Steidl, Robert J, and Len Thomas. ‘Power Analysis and Experimental Design’. In Design and Analysis of Ecological Experiments, edited by Samuel M Scheiner and Jessica Gurevitch, Second Edition., 14–36. Oxford University PressNew York, NY, 2001. https://doi.org/10.1093/oso/9780195131871.003.0002.

<a id="5">[5]</a>
Broman, Karl W. ‘Experimental Design and Sample Size Determination’. https://www.biostat.wisc.edu/~kbroman/talks/acuc_ho.pdf.

<a id="6">[6]</a>
Conn, Vicki S., and Tamara Coon Sells. ‘Compared to What?’ Western Journal of Nursing Research 42, no. 9 (1 September 2020): 772–73. https://doi.org/10.1177/0193945916650392.

<a id="7">[7]</a>
10X Genomics. ‘What Is the Recommended Sequencing Depth for Single Cell 3’ and 5’ Gene Expression Libraries?’ Accessed 17 March 2025. https://kb.10xgenomics.com/hc/en-us/articles/115002022743-What-is-the-recommended-sequencing-depth-for-Single-Cell-3-and-5-Gene-Expression-libraries.

<a id="8">[8]</a>
Settles, Dr Matthew L. ‘Single-Cell Transcriptomics’, https://ucdavis-bioinformatics-training.github.io/2017-June-RNA-Seq-Workshop/friday/scRNAseq.pdf.

<a id="9">[9]</a>
Yu, Ying, Yuanbang Mai, Yuanting Zheng, and Leming Shi. ‘Assessing and Mitigating Batch Effects in Large-Scale Omics Studies’. Genome Biology 25, no. 1 (3 October 2024): 254. https://doi.org/10.1186/s13059-024-03401-9.

<a id="10">[10]</a>
Korsunsky, Ilya, Nghia Millard, Jean Fan, Kamil Slowikowski, Fan Zhang, Kevin Wei, Yuriy Baglaenko, Michael Brenner, Po-ru Loh, and Soumya Raychaudhuri. ‘Fast, Sensitive and Accurate Integration of Single-Cell Data with Harmony’. Nature Methods 16, no. 12 (December 2019): 1289–96. https://doi.org/10.1038/s41592-019-0619-0.

<a id="11">[11]</a>
Zhang, Yuqing, Giovanni Parmigiani, and W Evan Johnson. ‘ComBat-Seq: Batch Effect Adjustment for RNA-Seq Count Data’. NAR Genomics and Bioinformatics 2, no. 3 (1 September 2020): lqaa078. https://doi.org/10.1093/nargab/lqaa078.

<a id="12">[12]</a>
National Microbiome Data Collaborative. ‘Introduction to Metadata and Ontologies’. Accessed 17 March 2025. https://microbiomedata.org/introduction-to-metadata-and-ontologies/.

