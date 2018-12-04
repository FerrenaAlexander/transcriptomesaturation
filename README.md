# transcriptomesaturation
"Transcriptome saturation" (aka, "coverage") is a sensitivty metric that 
attempts to estimate the breadth of capture of unique transcripts by 
RNA-seq. It is particularly of interest when considering rare/relatively 
lowly expressed transcripts; experimental protocols may bias against 
capture of these in favor of very highly expressed transcripts, which 
may be of lesser interest. For example, reverse transcription or PCR 
amplification of rare transcripts may be disfavored due to their 
relatively low level in the reaction compared to highly abundant RNA 
species.

[Zieganhan et al 
2017](https://www.sciencedirect.com/science/article/pii/S1097276517300497) 
and [Wu et al 
2014](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4022966/) both 
estimate transcriptome saturation and inspired this analysis. However, 
both papers use a strategy at the raw fastq level. First, they normalize 
across "conditions" (in each case, they are comparing various scRNA-seq 
library prep/sequencing protocols); they do this by first selecting a 
baselin of 1 million reads). From there, they systematically downsample 
further (ie 0-100% of 1 million, ostensibly in discrete intervals); each 
downsampling is then processed via the same alignment/quantification 
pipeline. This seems computationally heavy, so with Dr. Jason Chan's 
guidance I have set out to try to accomplish a similar estimation, but 
instead downsampling at the gene expression matrix level (post 
alignment); thus, we can estimate a similar metric but with higher speed 
and efficiency.
