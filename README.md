# Metabarcoding-pipeline

### 1rst: Folders
The first step is create the folder for the project and the subfolders that we need.
```console
mkdir project_A
cd project_A

mkdir rawdata
mkdir scripts
mkdit logs
mkdir output
```

#### 2nd: Cleanning
The second step is cleaning the adapters from the sequences (cutadapt) </br>
```console
sbatch scripts/cutadapt.sh
```
##### Script Adapters:
SMART, Chaetoceros:</br>
PRIMER_F="GCAGTTAAAAAGCTCGTAGT" # EK-565F</br>
PRIMER_R="TTTAAGTTTCAGCCTTGCG" # 18S-EUK-1134R-UnonMet</br>

PRIMER_F="CCAGCASCYGCGGTAATTCC" # TAReuk454FWD1 </br>
PRIMER_R="ACTTTCGTTCTTGATYRATGA" # TAReukREV3_modi </br>

##### Input:
Folder: rawdata/ </br>
Files:</br>
- XX_R[1|2]*.fastq --> The raw data from the secuencer:

##### Output:
Folder: output/cutadapt </br>
Files: </br>
- XX__trimmed_R[1|2].fastq --> same # of the input, seq. without adapter. </br>
- seqkit_stats_trimmed.tsv --> stats of the input files. </br>
- seqkit_stats_untrimmed.tsv --> stats of the output files. </br>

#### 3rd: DADA2
The next step is for filtering, denoising and merge.
```console
sbatch scripts/01_all.sh
```
##### Script:
Change lines: L8-11: the project name (project_A) and the version if needed
- path_principal<- "/home/ntimoneda/ntimoneda/projects/project_A"
- path     <- "/home/ntimoneda/ntimoneda/projects/project_A/cutadapt"
- output   <- "/home/ntimoneda/ntimoneda/projects/project_A/output"
- name.run <- "v1"

Change lines: L28-30: parameters for filtering
- truncLen=c(280,270) --> Lenght to truncate low quality, forward & reverse, see in the graphs step 0.
- maxEE=c(4,6) --> Maximum number of expectation errors, in the denoising (forward and reverse).

Change lines: L69: parameters for dereplication
- minOverlap=10 --> number of overlap. Overlap = (truncLen_fwd + truncLen_rev) - Amplicon_expected
##### Input:
Folder: output/cutadapt</br>
Files: output step 2
##### Output:
Folder: output/filtered
Files: </br>
- XX_[F|R]_filt.fastq --> same # of the input, seq. filtered. </br>
- errors_name.run_[fwd|rev].pdf --> plots about errors learned. </br>
- v1_seqtab.rds --> the sequences. </br>
- v1_track_analysis.v3.tsv --> stats of the output. </br>

#### 4rth: Chimeras (DADA2)


••••••••

```console
```
##### Script:
##### Input:
##### Output:







