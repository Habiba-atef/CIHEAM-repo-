# Session 1 

## Exe1) How many sequences have been formatted and how does this affect the E-value of BLAST searches?

code:
    makeblastdb -dbtype prot -in uniprot_Atha.fasta

output:

    Adding sequences from FASTA; added 15719 sequences in 0.479077 seconds.

E-value "describes the number of hits one can expect to see by chance when searching a database of a particular size If the number of sequences is high the number of matches you can expect to happen by chance increase so a high E-value

## Exe2) Can you redirect the output to separate files called test.faa.blast and test.fna.blast?

Using the below code we ensure  the outputs of the blastp and blastx savedinto two differents files.
Code:        

    blastp -db uniprot_Atha.fasta -query test.faa -outfmt 6 > test.faa.blast
    blastx -db uniprot_Atha.fasta -query test.fna -outfmt 6 > test.fna.blast
    

## Exe3) What is the default alignment format, can you show an example?
-outfmt 6:prints the blast result as a tabular format — columns with IDs, % identity, alignment lengths, E-values

Code:

    head test.faa.blast
    head test.faa.blast

output:

    AT1G30330.2     sp|Q9ZTX8|ARFF_ARATH    100.000 935     0       0    1935     1       935     0.0     1915
    AT1G30330.2     sp|Q9FGV1|ARFH_ARATH    55.667  900     284     20   1888     1       797     0.0     850
    AT1G30330.2     sp|Q8RYC8|ARFS_ARATH    65.116  430     132     10   1422     1       420     2.97e-174       534
    AT1G30330.2     sp|Q8RYC8|ARFS_ARATH    48.889  135     67      1    776      910     938     1070    5.47e-32        134
    AT1G30330.2     sp|P93022|ARFG_ARATH    64.871  427     132     10   4422     5       421     1.23e-169       524
    AT1G30330.2     sp|P93022|ARFG_ARATH    63.043  92      34      0    797      888     1038    1129    1.71e-30        129
    AT1G30330.2     sp|P93024|ARFE_ARATH    62.078  385     141     3    19       403     48      427     1.67e-157       485
    AT1G30330.2     sp|Q94JM3|ARFB_ARATH    55.710  359     155     4    21       378     57      412     2.72e-128       407
    AT1G30330.2     sp|Q94JM3|ARFB_ARATH    46.154  91      47      2    795      884     732     821     5.79e-18        88.2
    AT1G30330.2     sp|Q8L7G0|ARFA_ARATH    53.930  369     161     6    21       385     18      381     2.53e-125       393



## Exe4) Are there differences in the results retrieved in both searches?
Both compares against protein database but the difference is in the query format 
- blastp compares a protein sequence vs. a protein database.
- blastx translates the nucleotide query in all frames then compares those translations to the protein database.

Code:

    head test.faa.blast
    head test.faa.blast
Output:

    head test.faa.blast
    AT1G30330.2     sp|Q9ZTX8|ARFF_ARATH    100.000 935     0       0    1935     1       935     0.0     1915
    AT1G30330.2     sp|Q9FGV1|ARFH_ARATH    55.667  900     284     20   1888     1       797     0.0     850
    AT1G30330.2     sp|Q8RYC8|ARFS_ARATH    65.116  430     132     10   1422     1       420     2.97e-174       534
    AT1G30330.2     sp|Q8RYC8|ARFS_ARATH    48.889  135     67      1    776      910     938     1070    5.47e-32        134
    AT1G30330.2     sp|P93022|ARFG_ARATH    64.871  427     132     10   4422     5       421     1.23e-169       524
    AT1G30330.2     sp|P93022|ARFG_ARATH    63.043  92      34      0    797      888     1038    1129    1.71e-30        129
    AT1G30330.2     sp|P93024|ARFE_ARATH    62.078  385     141     3    19       403     48      427     1.67e-157       485
    AT1G30330.2     sp|Q94JM3|ARFB_ARATH    55.710  359     155     4    21       378     57      412     2.72e-128       407
    AT1G30330.2     sp|Q94JM3|ARFB_ARATH    46.154  91      47      2    795      884     732     821     5.79e-18        88.2
    AT1G30330.2     sp|Q8L7G0|ARFA_ARATH    53.930  369     161     6    21       385     18      381     2.53e-125       393
    head test.fna.blast
    AT1G30330.2     sp|Q9ZTX8|ARFF_ARATH    100.000 935     0       0  12805    1       935     0.0     1706
    AT1G30330.2     sp|Q9FGV1|ARFH_ARATH    75.584  471     100     4  11392    1       463     0.0     699
    AT1G30330.2     sp|Q9FGV1|ARFH_ARATH    48.198  222     92      8  2020     2664    592     797     1.05e-43        170
    AT1G30330.2     sp|Q8RYC8|ARFS_ARATH    65.116  430     132     10 11266    1       420     2.38e-170       527
    AT1G30330.2     sp|Q8RYC8|ARFS_ARATH    48.889  135     67      1  2326     2730    938     1070    1.48e-31        132
    AT1G30330.2     sp|P93022|ARFG_ARATH    64.871  427     132     10 10       1266    5       421     6.79e-166       518
    AT1G30330.2     sp|P93022|ARFG_ARATH    63.043  92      34      0  2389     2664    1038    1129    3.68e-30        128
    AT1G30330.2     sp|P93024|ARFE_ARATH    62.078  385     141     3  55       1209    48      427     5.22e-154       479
    AT1G30330.2     sp|P93024|ARFE_ARATH    49.635  137     66      1  2284     2685    756     892     5.56e-33        137
    AT1G30330.2     sp|Q94JM3|ARFB_ARATH    55.710  359     155     4  61       1134    57      412     1.37e-122       395


The results show in more or slightly different hits when using blastx vs blastp
    -Alignment coordinates are different
    -Percent identity is often higher in blastx
    -Bit scores differ even when E-values are similar
blastp finds matches based on the actual protein sequence.
blastx can find matches even if the coding sequence contains frameshifts.

Ref:
https://www.ncbi.nlm.nih.gov/books/NBK279684/ 


## Exe5) Can you explain the contents of the output file profile.out?
code:

    psiblast -db uniprot_Atha.fasta -query test.faa -num_iterations 3 -out_ascii_pssm   profile.out

Output:

    Matrix: BLOSUM62
    Gap Penalties: Existence: 11, Extension: 1
    Neighboring words threshold: 11
    Window for multiple hits: 40
    
The file profile.out contains the final PSI-BLAST position-specific scoring matrix (PSSM), showing for each residue position the log-odds substitution scores for all amino acids, their observed weighted frequencies, the information content per position, and the relative contribution of real matches versus pseudocounts, reflecting evolutionary conservation across homologous sequences.

## Exe6) Create a FASTA file with the complete protein sequences of the matches of your protein search with bit score > 200. You might find one-liners useful for this.
- Compute a multiple alignment of these sequences with Clustal Omega. Check the available output formats.
- Build a HMM out of these aligned sequences with hmmbuild
- Scan the HMM against your sequence collection with hmmerscan and write a short report on the     results.

Steps :
### 1.Extract BLAST hits into hits.fasta

    awk '$12 > 200 {print $2}' test.faa.blast | sort -u > hit_ids.txt
    seqkit grep -f hit_ids.txt uniprot_Atha.fasta > hits.fasta
Output

    head hits.fasta
    
    >sp|Q9LQE8|ARFN_ARATH Putative auxin response factor 14 OS=Arabidopsis thaliana           OX=3702 GN=ARF14 PE=3 SV=2
    MESGNVVNTQPELSGIIDGSKSYMYEQLWKLCAGPLCDIPKLGEKVYYFPQGHIELVEAS
    TREELNELQPICDFPSKLQCRVIAIQLKVENNSDETYAEITLMPDTTQVVIPTQNQNQFR
    PLVNSFTKVLTASDTSVHGGFSVPKKHAIECLPPLDMSQPLPTQEILAIDLHGNQWRFRH
    IYRGTAQRHLLTIGWNAFTTSKKLVEGDVIVFVRGETGELRVGIRRAGHQQGNIPSSIVS
    IESMRHGIIASAKHAFDNQCMFIVVYKPRSSQFIVSYDKFLDVVNNKFNVGSRFTMRFEG
    DDFSERRSFGTIIGVSDFSPHWKCSEWRSLEVQWDEFASFPRPNQVSPWDIEHLTPWSNV
    SRSSFLKNKRSREVNEIGSSSSHLLPPTLTQGQEIGQQSMATPMNISLRYRDITEDAMTP
    SRLLMSYPVQPMAKLNYNNVVTPIEENITTNAVASFRLFGVSLATPSVIKDPVEQIGLEI
    SRLTQEKKFGQSQILRSPTEIQSKQFSSTRTCTKVQMQGVTIGRAVDLSVLNGYDQLILE

### 2.Run Clustal Omega

    clustalo -i high_score_hits.fasta -o aligned_sequences.sto --outfmt=st

Output
    
    head hits.aln
    
        #=GS O23661 DE    Auxin response factor 3 OS=Arabidopsis thaliana OX=3702 GN=ARF3 PE=1 SV=2
    #=GS P93022 DE    Auxin response factor 7 OS=Arabidopsis thaliana OX=3702 GN=ARF7 PE=1 SV=2
    #=GS P93024 DE    Auxin response factor 5 OS=Arabidopsis thaliana OX=3702 GN=ARF5 PE=1 SV=3
    #=GS Q84WU6 DE    Auxin response factor 17 OS=Arabidopsis thaliana OX=3702 GN=ARF17 PE=2 SV=1
    #=GS Q8L7G0 DE    Auxin response factor 1 OS=Arabidopsis thaliana OX=3702 GN=ARF1 PE=1 SV=2
    #=GS Q8RYC8 DE    Auxin response factor 19 OS=Arabidopsis thaliana OX=3702 GN=ARF19 PE=1 SV=2
    #=GS Q93YR9 DE    Auxin response factor 16 OS=Arabidopsis thaliana OX=3702 GN=ARF16 PE=1 SV=1
    #=GS Q94JM3 DE    Auxin response factor 2 OS=Arabidopsis thaliana OX=3702 GN=ARF2 PE=1 SV=2
    #=GS Q9C5W9 DE    Auxin response factor 18 OS=Arabidopsis thaliana OX=3702 GN=ARF18 PE=1 SV=1
    #=GS Q9C7I9 DE    Auxin response factor 20 OS=Arabidopsis thaliana OX=3702 GN=ARF20 PE=2 SV=3
    #=GS Q9C8N7 DE    Auxin response factor 22 OS=Arabidopsis thaliana OX=3702 GN=ARF22 PE=2 SV=2
    #=GS Q9C8N9 DE    Putative auxin response factor 21 OS=Arabidopsis thaliana OX=3702 GN=ARF21 PE=3 SV=2
    #=GS Q9FGV1 DE    Auxin response factor 8 OS=Arabidopsis thaliana OX=3702 GN=ARF8 PE=1 SV=2
    #=GS Q9FX25 DE    Auxin response factor 13 OS=Arabidopsis thaliana OX=3702 GN=ARF13 PE=2 SV=3
    #=GS Q9LQE3 DE    Putative auxin response factor 15 OS=Arabidopsis thaliana OX=3702 GN=ARF15 PE=3 SV=2
    #=GS Q9LQE8 DE    Putative auxin response factor 14 OS=Arabidopsis thaliana OX=3702 GN=ARF14 PE=3 SV=2
    #=GS Q9SKN5 DE    Auxin response factor 10 OS=Arabidopsis thaliana OX=3702 GN=ARF10 PE=2 SV=1
    #=GS Q9XED8 DE    Auxin response factor 9 OS=Arabidopsis thaliana OX=3702 GN=ARF9 PE=1 SV=1
    #=GS Q9XID4 DE    Auxin response factor 12 OS=Arabidopsis thaliana OX=3702 GN=ARF12 PE=2 SV=2
    #=GS Q9ZPY6 DE    Auxin response factor 11 OS=Arabidopsis thaliana OX=3702 GN=ARF11 PE=2 SV=3
    #=GS Q9ZTX8 DE    Auxin response factor 6 OS=Arabidopsis thaliana OX=3702 GN=ARF6 PE=1 SV=2
    #=GS Q9ZTX9 DE    Auxin response factor 4 OS=Arabidopsis thaliana OX=3702 GN=ARF4 PE=1 SV=1
    
    O23661  ---------MGGLIDLNVMETEEDETQTQTPS--------SA--------
    P93022  --------------------------------------------------
    P93024  --------------MMASLSCVEDKMKTSCLVNGGGTITTTTSQSTL---
    Q84WU6  --------------------------------------------------
    Q8L7G0  --------------------------------------------------
    Q8RYC8  --------------------------------------------------
    Q93YR9  --------------------------------------------------
    Q94JM3  ---------------MASSEVS-------MKGNRGGDNFSSSGFSDPKET
    Q9C5W9  -----------------------------MASVEGDDDFGS---------
    Q9C7I9  --------------------------------------------------
    Q9C8N7  --------------------------------------------------
    Q9C8N9  --------------------------------------------------
    Q9FGV1  --------------------------------------------------
    Q9FX25  --------------------------------------------------
    Q9LQE3  --------------------------------------------------


### 3.Build a HMM out of these aligned sequences with hmmbuild

    hmmbuild mymodel.hmm hits.aln
    hmmsearch --tblout exe6_report.txt ARF_profile.hmm uniprot_Atha.fasta

Output

    # hmmbuild :: profile HMM construction from multiple sequence alignments
    # HMMER 3.4 (Aug 2023); http://hmmer.org/
    # Copyright (C) 2023 Howard Hughes Medical Institute.
    # Freely distributed under the BSD open source license.
    # - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    # input alignment file:             hits.aln
    # output HMM file:                  mymodel.hmm
    # - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    
    # idx name                  nseq  alen  mlen eff_nseq re/pos description
    #---- -------------------- ----- ----- ----- -------- ------ -----------
    1     hits                    22  1361   670     1.43  0.590
    
    # CPU time: 0.32u 0.00s 00:00:00.32 Elapsed: 00:00:00.32

HMM Profile built from high-scoring BLAST hit alignments was used to search the *Arabidopsis thaliana* proteome (15,719 proteins) and it recognized the identified 74 significant family members, including top matches to known Auxin Response Factors (ARFs) and more distant B3 domain-containing relatives. This shows that HMMs are more sensitive than single-sequence BLAST searches for detecting complete protein families.


## EX7) Produce a table with:
i) domains defined by the boundaries of matched entries from the Protein Data Bank and Pfam and 
ii) similar sequences in AlphaFoldDB.

Claude suggested choosing the examples based on coverage of the entire protein not only the the lowest E value. hence     choosing the best match (4LDU) which was in regions (PF06507 and 6L5K) ensuring that table include the full length of     the protein.

Output:

| Category | Database Source | Hit ID / Accession | Description / Function | Boundaries / Identity |
| :--- | :--- | :--- | :--- | :--- |
| **i) Domains** | **PDB** (via HHPred) | **4LDU_A** | Auxin Response Factor 5 (DNA Binding) | Residues **16 – 363** |
| | **Pfam** (via HHPred) | **PF02362** (B3) | B3 DNA Binding Domain | Residues **129 – 208** |
| | **Pfam** (via HHPred) | **PF06507** (ARF_AD) | ARF Ancillary Domain | Residues **278 – 357** |
| | **PDB** (via HHPred) | **6L5K_A** | Auxin Response Factor 5 (PB1 / Oligomerization) | Residues **793 – 888** |
| | **Pfam** (via HHPred) | **PF02309** (AUX_IAA) | AUX/IAA Family (PB1 domain) | Residues **795 – 854** |
| **ii) Similar Seqs** | **AlphaFoldDB** | **Q9ZTX8** | Auxin Response Factor 6 (*Arabidopsis thaliana*) | **100% Identity** |
| | **AlphaFoldDB** | **Q6H6V4** | Auxin Response Factor 6 (*Oryza sativa*) | **63.0% Identity** |
| | **AlphaFoldDB** | **Q653U3** | Auxin Response Factor 17 (*Oryza sativa*) | **62.6% Identity** |


## EX8) search for functional annotations for protein AT1G30330.2 with help from eggNOG-mapper. Make sure you set one-to-one orthologues only. What are the GO terms and eggNOG orthology groups of this protein?

As eggNOG-mapper wasnt efficient in the search so Unioprot was used instead of it.
the unitprot resulted in :
1-Gene Ontology :Molecular Function: DNA-binding transcription factor activity and DNA binding.
2-Biological Process: Auxin-activated signaling pathway, response to auxin and flower development.
3-Cellular Component: Nucleus
eggNOG Orthology Group: The protein belongs to the eggNOG group ENOG502QSCZ at the Eukaryota taxonomic level.

## EX9) Summarization 
using the GO-web browser 

### 1)Searching for: GO IDs GO:0009414, GO:0035618, GO:0016491.
-GO:0016491 : oxidoreductase activity (Category: Molecular Function, marked with an F)
-GO:0035618 : root hair (Category: Cellular Component, marked with a C)
-GO:0009414 : response to water deprivation (Category: Biological Process, marked with a P)

### 2)The GO ID and the functional category corresponding to photosynthesis: GO:0015979 
Functional Category: Biological Process.


### 3)What are the immediate parent(s) and children of the photosynthesis GO term?
Immediate Parent: metabolic process (GO:0008152).
Immediate Children:
   photosynthesis, light reaction (GO:0019684) 
   photosynthesis, dark reaction (GO:0019685) 
   regulation of photosynthesis (GO:0010109)
   photosystem (GO:0009521)
   negative regulation of photosynthesis	(GO:1905156)
   positive regulation of photosynthesis (GO:1905157)
   photosynthetic membrane (GO:0034357)

### 4)Search for the GO annotation terms of the following protein A0A068LKP4,A0A097PR28, A0A059Q6N8? What do you observe?

I)A0A068LKP4:
Name: RPW8 domain-containing protein
Organism (Taxon): Arabidopsis thaliana (Thale cress)

II)A0A097PR28:
Name: General transcription factor IIH subunit 2
Organism (Taxon): Prunus persica (Peach)

III)A0A059Q6N8:
Name: Photosystem II reaction center protein M
Organism (Taxon): Zea mays subsp. mays (Corn/Maize)

All the three proteins from Viridiplantae but belong to 3 different species (Arabidopsis, Peach, and Maize) and perform different functions (Defense/Resistance, Transcription, and Photosynthesis)

### 5)How many gene products are involved in leaf development? Give the GO ID corresponding to this term.
The results show 21,805 annotations to 21,009 distinct gene products.
Leaf development: GO:0048366

### 6)How many proteins of Arabidopsis thaliana, Prunus perisca and Zea mays are assigned to the leaf development GO term. Tip : Zea mays. Taxonomy ID=4577
   Arabidopsis thaliana: 638 annotations
   Prunus perisca: 59 annotations
   Zea mays: 178 annotations

### 7)Check the total number of BP annotations and proteins supported by the experimental evidence codes in both Arabidopsis thaliana and Prunus persica. (see the evidence codes) Tip : check the ‘Statistics’ box.
   Arabidopsis thaliana: 423 annotations to 332 distinct gene products
   Prunus perisca: No matching annotations have been found

### Summary table
| Question | Result |
| :--- | :--- |
| **1. GO Terms** | **GO:0009414**: Response to water deprivation (Biological Process)<br>**GO:0035618**: Root hair (Cellular Component)<br>**GO:0016491**: Oxidoreductase activity (Molecular Function) |
| **2. Photosynthesis** | **GO ID:** GO:0015979<br>**Category:** Biological Process |
| **3. Relationships** | **Parent:** Metabolic process<br>**Children:** Light reaction, Dark reaction, Regulation of photosynthesis, photosystem, negative regulation of photosynthesis, positive regulation of photosynthesis, photosynthetic membrane |
| **4. Protein Observation** | The proteins belong to three different organisms (*Arabidopsis*, *Prunus*, *Zea mays*) and perform different functions (Resistance, Transcription, Photosynthesis), showing that GO terms are universal across species. |
| **5. Leaf Development** | **GO ID:** GO:0048366<br>**Total Count:** ~21,805 Annotations (Global) |
| **6. Organism Counts** | **Arabidopsis:** 638 annotations<br>**Zea mays:** 178 annotations<br>**Prunus persica:** 59 annotations |
| **7. Experimental Evidence** | **Arabidopsis:** 423 annotations (well-studied model organism)<br>**Prunus persica:** 0 annotations (lacks experimental verification) |
## EX10: Choose from the options [here](https://eead-csic-compbio.github.io/bioinformatica_estructural/#c%C3%B3mo-obtener-y-usar-modelos-de-alphafold-y-algoritmos-similares) and model the structure of one of the sequences obtained in Exe5. Save a screen capture of your model and a table with associated quality scores.
I used the protein I found in Exe5: REM13 (Uniprot ID: P0CAP5) and i choosed to work with alphafold, the 3D form I got is:

<img width="464" height="284" alt="image" src="https://github.com/user-attachments/assets/2157c689-82e9-41c7-b6ca-630e19b5ff47" />

| pLDDT Value | Description |
| :--- | :--- |
| **pLDDT > 90** | Very high confidence (Dark Blue) |
| **90 > pLDDT > 70** | High confidence (Light Blue) |
| **70 > pLDDT > 50** | Low confidence (Yellow) |
| **pLDDT < 50** | Very low confidence (Orange) |

