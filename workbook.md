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

