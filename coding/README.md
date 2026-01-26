
Session 1 exercises

Exe1) How many sequences have been formatted and how does this affect the E-value of BLAST searches?

code:
    makeblastdb -dbtype prot -in uniprot_Atha.fasta

output:

    Adding sequences from FASTA; added 15719 sequences in 0.479077 seconds.

According to [1], E-value "describes the number of hits one can expect to see by chance when searching a database of a particular size", therefore ...
References


Exe2) Can you redirect the output to separate files called test.faa.blast and test.fna.blast?
Code:        

    blastp -db uniprot_Atha.fasta -query test.faa -outfmt 6 > test.faa.blast
    blastx -db uniprot_Atha.fasta -query test.fna -outfmt 6 > test.fna.blast

output:

Exe3) What is the default alignment format, can you show an example?
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



Exe4) Are there differences in the results retrieved in both searches?
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


Exe5) Can you explain the contents of the output file profile.out?
code:

    psiblast -db uniprot_Atha.fasta -query test.faa -num_iterations 3 -out_ascii_pssm   profile.out

Output:

    Matrix: BLOSUM62
    Gap Penalties: Existence: 11, Extension: 1
    Neighboring words threshold: 11
    Window for multiple hits: 40
    
The file profile.out contains the final PSI-BLAST position-specific scoring matrix (PSSM), showing for each residue position the log-odds substitution scores for all amino acids, their observed weighted frequencies, the information content per position, and the relative contribution of real matches versus pseudocounts, reflecting evolutionary conservation across homologous sequences.

Exe6 
- Create a FASTA file with the complete protein sequences of the matches of your protein search     with bit score > 200. You might find one-liners useful for this.
- Compute a multiple alignment of these sequences with Clustal Omega. Check the available         output formats.
- Build a HMM out of these aligned sequences with hmmbuild
- Scan the HMM against your sequence collection with hmmerscan and write a short report on the     results.

Steps :
1.Extract BLAST hits into hits.fasta

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

2.Run Clustal Omega

    clustalo -i hits.fasta -o hits.aln

Output
    
    head hits.aln
    
    >sp|Q9LQE8|ARFN_ARATH Putative auxin response factor 14 OS=Arabidopsis thaliana          OX=3702 GN=ARF14 PE=3 SV=2
    ------------------------------------------------------ME--SG
    NVVNTQP-ELSGIIDGSKSYMYEQLWKLCAGPLCDIPKLGEKVYYFPQGHIELVEASTRE
    ELN-ELQPICDFPSKLQCRVIAIQLKVENNSDETYAEITLMPDTTQVVIPTQN-------
    -------QNQFRPLVNSFTKVLTASDTSVHGGFSVPKKHAIECLPPLDMSQPLPTQEILA
    IDLHGNQWRFRHIYRGTAQRHLLTI--GWNAFTTSKKLVEGDVIVFVRGETGELRVGIRR
    AGHQQGNIPSSI----------------VSIE--------------------------SM
    RHGIIASAKHAFDNQCMFIVVYKP--RSSQFIVSYDKFLDVVNN-KFNVGSRFTMRFEGD
    DFSE-RRSFGTIIGVSDF-SPHWKCSEWRSLEVQWDEFASFPRPNQVSPWDIEHLTPWSN
    VSRSSFL---KNKRSREVNEIGSSS----------------------------SHLLPPT

3.Build a HMM out of these aligned sequences with hmmbuild

    hmmbuild mymodel.hmm hits.aln

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

4.


