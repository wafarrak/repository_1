# repository_1

Code used to download data: scp /Users/waleed/Downloads/GSE53890_RAW.tar wafarrak@opuntia.rcdc.uh.edu:/project/stuckert/wafarrak

To download the relevant fastq files, I navigated to the SRA site, looked up the run number SRR28168644 on the ENA browser and used wget to download the files (forward and reverse reads) using its url:

(wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR281/044/SRR28168644/SRR28168644_1.fastq.gz)

In order to trim the sequences, you can use Trimmomatic: 

java -jar trimmomatic-0.39.jar PE -threads 5 \
-baseout SRR28168640.TRIM.fastq \
SRR28168640_1.fastq.gz SRR28168640_2.fastq.gz \
LEADING:3 TRAILING:3 \
ILLUMINACLIP:/project/stuckert/wafarrak/adap-PE.fa:2:30:10:8:TRUE \
MINLEN:25

Next use trinity (compute node) : Trinity \
--SS_lib_type RF \
--no_version_check \
--seqType fq \
--output trinity/ \
--max_memory 15G \
--left SRR28168640.TRIM_1P.fastq.gz \
--right SRR28168640.TRIM_2P.fastq.gz \
--CPU 5 \
--inchworm_cpu 5 \
--full_cleanup \
--no_bowtie
