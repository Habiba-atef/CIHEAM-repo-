Exercise 1: 

1.1 Note that there are 2 FASTQ files with the same name but different numeric suffix, why?
SAMEA2569438.chr10_1.fastq.gz → Read 1 (forward)
SAMEA2569438.chr10_2.fastq.gz → Read 2 (reverse)

1.2 Check first SAMEA2569438.chr10_1.fastq.gz and then SAMEA2569438.chr10_2.fastq.gz, can you spot * the
difference? Do you recognize the typical FASTQ format of these files?
Yes , Line 1: Header (starts with @) , Line 2: DNA Sequence , Line 3: Separator (+) and Line 4: Quality String (This indicates the error rate)

Code:

    fastqc /home/habiba/variant_calling/*.fastq.gz -o quality_check/
    zcat SAMEA2569438.chr10_1.fastq.gz | head
    zcat SAMEA2569438.chr10_1.fastq.gz | tail

Output 

		zcat SAMEA2569438.chr10_1.fastq.gz | head
	  @ERR605441.15/1
	  ATCTTCTTGTTATTGCAACACATGACATGATATGCTATATGTATGCTAAGCTCTTGAACATTAATGAACATAATTCCTATGCT
	  +
	  FHHHHHJJJJJJJJJJJJJHIIJJIJIIJIJIJJJJJJIJJJIJJJIIJIJJJJJJIJIIJJIJJJIJIIJHHHHHHFFFFFF
	  @ERR605441.63/1
	  CTTCCTATTTGATCTTTATTGATTATGTGCATATGCGTTCCTTCATATCCATATGTATGCACATCTTGAGGGGGAGCTTATTC
	  +
	  FHHHHHIJJJIJJJIJJIJJJJJIIJG?FGHHIIIIFGHIJJIIJG@HIIIIHHGJIJJJIJJIIJJJJJIEHDADDDDDDEE
	  @ERR605441.82/1
	  TGGTTTTATTAGGGTTTTTCCTCATTTTGCGTGCCAGCGTGTAGAATCCGTCGTTTCGGAAGATCGCGGTCGCGGGGAAAAGA
	  
	  zcat SAMEA2569438.chr10_1.fastq.gz | tail
	  +
	  FGFBDHGGHEGGIIIIIEGH?)18BECDHIGHFH=FAFGIHGGGIIJJIJFFHEFFECCCCACDCDDBDBDDDEDDACA:@DD
	  @ERR605445.1921895/1
	  CTTTTAGTGTAGTTGAAATAACGGAATTGGAACTTGTTTGGTCAAGTAGGGGAAACTCAATCAAACTCATAACTGTCTTAATG
	  +
	  FHGHHGDDBFGHHGIFEECHIGGIIJEGGIIIJBFHIIIJEGHEHGG<F:A8@FGIJ@DCEEFHGFDF@DEEEEECCC3;@>A
	  @ERR605445.1921928/1
	  CAAAATCAAAAAGATGGACAATCCAATTTCTCGATTCAATAGAAGCCCAAAGAGGTGCATATGGTACCCAAATAAGGATAGGA
	  +
	  DDDDD?EBEEEDF?AC+1??CEDDEIDFEIIIII@DDEDDBBBBBDII9C>A;@CEDIAC>>A377@7;A(;(6>>AAAAA>>


1.3 Are read starts and ends similar in terms of error rate?
    No , the output at the end of the reads Symbols and numbers indicating high error rate 
    Read starts → high quality (low error rate)
    Read ends → lower quality (higher error rate)
		
 problem
 
 	zcat | head SAMEA2569438.chr10_1.fastq.gz

The prevous code didnt work so i ammended the order to unzip the file stream before sending it to head & Run the command 


--------------------------------------------------------------------------------------------------------------------------------------------------------------------


2.1 Compare the different file sizes for each of the alignment files generated in the previous section (formats SAM, BAM and CRAM).

Codes used 

	zcat Oryza_sativa.IRGSP-1.0.dna.toplevel.chr10.fa.gz > data/reference.fna
	samtools faidx /data/reference.fna
	samtools faidx data/reference.fna
	zcat /home/habiba/variant_calling/Oryza_sativa.IRGSP-1.0.48.chr10.gtf.gz > ./data/annotation.gtf
	bwa index /data/reference.fna
To generate required files 
Bam:

	bwa mem reference.fna /home/vep/variant_data/SAMEA2569438.chr10_1.fastq.gz 		/home/vep/variant_data/SAMEA2569438.chr10_2.fastq.gz | samtools view -b -o SAMEA2569438.chr10.bam
Sam

	 bwa mem data/reference.fna SAMEA2569438.chr10_1.fastq.gz SAMEA2569438.chr10_2.fastq.gz > SAMEA2569438.chr10.sam
Cram

	 bwa mem reference.fna /home/vep/variant_data/SAMEA2569438.chr10_1.fastq.gz /home/vep/variant_data/SAMEA2569438.chr10_2.fastq.gz |samtools view -C -T reference.fna > SAMEA2569438.chr10.cram
	 

	ls -lh SAMEA2569438.chr10.sam SAMEA2569438.chr10.bam SAMEA2569438.chr10.cram

	
Output

	-rw-r--r-- 1 habiba habiba 31M Jan 20 22:03 SAMEA2569438.chr10.bam
	-rw-r--r-- 1 habiba habiba 17M Jan 20 22:06 SAMEA2569438.chr10.cram
	-rw-r--r-- 1 habiba habiba 91M Jan 20 22:12 SAMEA2569438.chr10.sam

Observed file sizes
SAM: 91MB
BAM: 31MB
CRAM: 17MB

The SAM file is the largest because it stores alignment information in plain text f
The BAM file is substantially smaller than the SAM file because it is a binary which make it more storage-efficient than SAM files.

The CRAM file is the smallest because it uses reference-based compression, storing only the differences between the reads and the reference genome rather than the full alignment information. This results in the highest compression ratio but requires access to the same reference genome to decode the file.

Problems 

on trying to generate the sam format using 

	bwa mem reference.fna ./home/habiba/variant_calling/SAMEA2569438.chr10_1.fastq.gz ./home/habiba/variant_calling/SAMEA2569438.chr10_2.fastq.gz | samtools view -o SAMEA2569438.chr10.bam
I got error 

	[E::bwa_idx_load_from_disk] fail to locate the index files
	[main_samview] fail to read the header from "-".
I used the below prompt in gemini to fix the error :
	
	identify the following error msg and propose a the needed amendment to generate the sam formt : 			[E::bwa_idx_load_from_disk] fail to locate the index files
	[main_samview] fail to read the header from "-".



-----------------------------------------------------------------------------------------------------------------------------------------------------------------



Exe3 3.1 Using samtools mpileup estimate the percentage of chr10 with depth > 100.

Code :

	samtools mpileup -a -r 10 -f data/reference.fna SAMEA2569438.chr10.sorted.bam | awk '{if($4 > 100) count++} END {print (count/NR)*100 "%"}'

Output:
0.223253% indicating a  low coverage 


-------------------------------------------------------------------------------------------------------------------------------------------------------------------

Exe4 

	
