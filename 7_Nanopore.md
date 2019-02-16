# Tutorial: Nanopore Analysis Pipeline

## Introduction

### Lesson plan

This is a bit of a bonus lesson. Nanopore is an experimental, new sequencing technique that I (Sabeel) just happen to work on. This lesson/tutorial is an attempt to familiarize you with nanopore.

### What's Nanopore?

Nanopore sequencing is a new and developing technique in bioinformatics that you can read about [here](https://nanoporetech.com/applications/dna-nanopore-sequencing) from one of the leading companies in the field, Oxford Nanopore. If you're not interested in the details, here's a summary: Nanopore uses super small holes to run DNA through, measures current changes to determine which base pair is at that position, and reports it as output.

### So... why?

Nanopore sequencing is getting a bunch of attention because it allows for longer reads. A lot longer. In the sample fastq files we've provided before, you'll notice that each read (or each "entry") was around 200 base pairs long. Nanopore reads have been frequently observed around 10,000 base pairs, and even up to 100,000 base pairs in extreme circumstances.

### No really... why?

Longer reads intuitively seem like a good thing, but why exactly is that? Remember that alignment is, essentially, finding overlaps in reads to fit them together. And, the longer the reads, the easier alignment is. For example, try to assemble the following message using reads of size 3 and reads of size 6:
```
[at!],[u a],[ re],[gre],[You],[ ar],[eat],[e g]
```

```
[great!],[re gre],[You ar]
```

Again, the longer the reads, the easier (and, as you'll have found, the faster) the alignment.

## Software

This tutorial will require the following softwares. They are all already installed. *DO NOT INSTALL THEM AGAIN!*

Click each of the links to understand what they do. This step is critical to understanding the rest of the tutorial.

##### Aside: It's totally possible to complete this tutorial (and most of our lessons) without reading about the softwares. This isn't a good idea. Not only will reading the documentation familiarize you with a particular software, it will familiarize you with (1) the idea behind softwares similar to it and, much more importantly, (2) how to parse documentation effectively so you don't waste your time. Don't underestimate how much time you'll spend reading documentation--if you're a bioinformatician, it's practically your job.

### Canu

[Canu Assembler](https://canu.readthedocs.io/en/latest/) 

Canu is a packaged correction, trimming, and assembly program that is forked from the Celera assembler codebase. What does all of this mean? Read the documentation (and ask us!) until you understand.

### Prokka

[Prokka](https://github.com/tseemann/prokka)

Prokka is a gene annotation program. What does this mean? Read the documentation (and ask us!) until you understand.

### Barrnap

[Barrnap](https://github.com/tseemann/barrnap)

Barrnap is an rRNA prediction software used by Prokka. What does this mean? Read the documentation (and ask us!) until you understand.


## Dataset
The nanopore dataset is from an isolate from a sample taken from a local saline lake at [South Bay Salt Works](https://en.wikipedia.org/wiki/South_Bay_Salt_Works). We're not directly going to be working with it because alignment is so computationally intensive, but click the spoiler arrow below to get a glimpse at what the data looks like:

<details>
  <summary>Click me, then scroll horizontally!</summary>
  
  ```
  @4e750b7b-3e4b-4b04-a35d-6d6718930b5a runid=9c207653f919de83e5e0c7e8e98fe2e51e7429bd read=6 ch=232 start_time=2018-02-28T18:56:07Z
TTATCTTGCTTCGTTCAGTTCAGTAATTTGGGTGTTTAACCGTTTTTCGCATTTTATCGTGGAAACGCTTTCGCGTTTTTCGTGCCGCTTCATCGCGCTCTAGTGCCGCAACTATTCCGCTAAGCGGTGATTCTCAAATGAAGGAGCTTGAGAACGATCCGGCCAGTGCCAATTTCTCAGCCTCTTTCGGTGCACGACCATGGGGCCAAAACGGCTGTGCAGGCTATACCTGCCATGTTGGCAGTGATGATTACGCAACCATTAGCATTAATCGCTCGATCTGGGTTTATCGCGACCTTGGTTGCCATCAGCGGTGAGCTCTTTCGAGGTATTGCTGGCGTCGGTGGCGGGGCAACGTTTGCCGCGCTGATTGTACTCTCTGCACTGGATATGCCGGTCGCGCGGGTCTGGTAATCTCAATTGAACCGTTTAATCGATATGGGCCGCTTACCGCAATTAACGTTAGCGGCTCAATGTGACTGCTGATACGCTCACCTCGCACGTTTAACCGGTGGCCAAGATAAGGCTATCTTCGAGCACCACGGTAGTGAAACAAGACCTGCAAACGCTTAATGCCGCGGGTGCCACCGTTTATAAAATGCCACGCATTGGCGTGTGGCATTTTTTATGTCTATGATCACCCATCAATTCGCTGACTCAACCCCTTATAACTTGTAAAGAATTTATGTCAGCGATTACACTCTGCCGCATTGTTAACGCAGGCTCGATCACCGCCCTACACGGGAACATTTATGAATTATTGAACCAAACACTTCAGGTACGCAGCGGCGTGTAGACTTGTACCCCGCCAAGACAACTTATCTGTGTATGACGTCCGTACTCACCAGATACCACCGCGAACAGCTGCGTATTATTGGTTTGTGGCACCTGTCATGACCAGCTAAGTAACCCTGACAATATGGATGCTTGAACCACTGGCGTTGCCTAGAGTGACAGCATGTGTGGAGCCAAGAACCGGCCATTGCAAGTCGTCGCTTATCGCCAGCTTTCTCGCCTTTCGAAGGTGAAAGCTGGGCGCAAAATAATCTCGACATGATATATATGGAAGATGATGTGCGTAAATGGGCGGAAACCGGTCAAGATATCGAAGAAGTTAAAGTGCTGGATACCAAATGGTGTGGCGCTGCAAAGAAGGCGACTTGACGTGACCGTGATTAAAGATTTGCCAGTGAAAGGCTCAAGCCAGGTAATCAAACAGGTACCGTGATCCGTGGCATTAACCTGACCGATGATCCTACCCATGTGCAGGAGTAGAGTAAACGGCCAAACGTTGTTTGTGATCGCTTCTTCTGCCGCCCGCAAGTAATTGGCAGCCTTAGTCGCCCTTTATTTAAACCTGGTTCTTTCTTTTTTGTTGTATTATAACGACCAGTTATTGATGCTGTTGGCGGTATTTGGGAGCAGTGCCGCCTTATTGCCTCATGGCCTTATTTTGGCTCACTCGCACCCATCTGATCAGACCATCATTTTTAGAAGACCAGCGCCATCCAATGGAAACAGCGCTCATTTGCCGCTTTGTTTGTATTGTTTGCTTGTATTCAGTACACCTACACGGGAGTGAATGTCGATGGGTCAGCGCTGGTAAATATACGCATCATCGCCATTATCGCCGGCGGTGTTTGTTTGGTCCCTTGGGTTGGCGTGACTGCCGGCGTTGTCTCAGGTGTTCACCGCTATCTTATCGATATTGATGGGTAACCTCACAAACCTGTTTTGATCGCCAATTATTATTGCTGGGTGCCTGTCGGCACTGATTCATTATCGCGCGGATAAACAGCATTAATGCACGCTGGCATTTTGTGGTATGCTCTGCGAATCGCTGATAAATGCTGCTTATCCTTTTTGCTTGCCCGCGATCAAACGCTCGCCCAACATTGTTGCG
+
%#&(%+(#&-.&,-;+-'5(&&$'%$((+0/',(11'3,8G8;AJA<3?@1@@>4135?<;,9>/0-+--*/.357DE@8:;4371.14*236634)+2.1.3<77A221;;::DI>A56211)-)'021<FBDABGG0-.0-+&'%&%(%.)/=89=93:00((/1$5//,BH1+9<0/5<@:AF98*43(,'(*-47D<4.-+</;FC5:BC7/..*1+=>7:?A?B?/,497F>8>2=416>:<<;:8@(1&0+'0=:42)%)&4(;(4238:65616-/>?DH>;;=<?:;7(,0160812AD<2)(('5-45???6BF1-*)(%*%-)$+%'--2F?6@45?8093,8123809)$*5/4/0-/(:3.05:>8@8900'+)21:9)1'8AAG90*+**.4..40D01;F380351822=EGI:0<+2.875797:2A=;61,,(,?A<?AC@C;>=0>2+*+-934.<,,**+/:;3801,+.3@>=>;?DC<78(,+6<J0E:H<HE69763,,./64++00/6433)/87B><>56),*&,3),-*+04)15678?GIE8'+>.@3=@@;..+.*2/0;448/5F201CEGH<:=G:50424=6?223*(*/248AIHH046/430*--03:4:F739@;7?57-1:31<>6032HC1/C5+8++D/006C)%6)<?7//3-2*,-+),,,0-059:>9C10%/&$,,&%')++;G@@9787.+/.$+46).0081---,**(</)-&+'//.@>:@G64*,,400672/52+-73)&'',))'+)+((40893;,CA/*,339389*7+*4E9:3500+,09;;C@6C;%/+.09727+/2?;AC/1@(,,.35/)112B>;262(60;3FJG563433;375)/%%(()-4$()**%))%490-388;A847@E754,/*.4FFIEECCJD@<@'5)'&'&&),EC6ACA621.,.35+315.*/668=<<:*9,%-729:AEFE<0>//0856D7895@F67A@E=BJ77*.+..824=5*/67E88440=4.%/*,,566:?8;5663365/38B2D236CBDCB==<;;C<01@<6/00@01H:>:89@CEEDD?4<3)2+)3E9G;(8)/?@889'B(@EH//6=564<899CB;C>1),6.9095341.((-/08>D=G965G8K1--<A2)/1/0835;,3-22>,0(64-B113;,,'2700)1,,33:968::63:6EB@6F0@.8121/3,-2/4784/(05,,624354:+))*.-&+-,,--/7144F3B@9F74?.),--,/--&'&-2@==AE?:F1277628,*=*80//,1%,&&*>=??C62>4(/96=A/2&%.54E@8JI/3CG<H/B5F/**3124GE?>/<<85H62,90462421.;/:04@;<==8&72.*/&(2+4./<@1>00906B?=04.74C4I<>IIH3C97:.554--)3999;933::E6<=>::32+1303),*0//*12-.46AGCF<<;:7A:8@)7(4235;;2E8,-?8115<3;?JH7>95H74@/),&'$0(+B2/*1(,$*('*,,-3=0),,:8>9?:B;=?<?+)($*/06,2(*)('.0837034671215?E=2D235GHG;D89CA+9:/-/>->@2B5)3-;=6809.//B:=<@5,'0'+)?-,+<;<6<777DG=99?14>;<DFGFGH>>>;=B::<AE6);:;D46*/0:.94;;6GC/05688AE;/:0/<:+:--(1.5*/.5EBCD@5@</<778>C=3@300:2323*ACAHF;85,3(/+8+.-222,+.-,.,9EI8.*0.-06=BDA@:?//D@A<<10)'(,%(%+/,+2-23B69CGC-,*&&$.-2.0.,01==C:+:@<-78+/'4+65(-*$%$
@a8347097-bc23-4340-9a2b-b25505800041 runid=9c207653f919de83e5e0c7e8e98fe2e51e7429bd read=44 ch=56 start_time=2018-02-28T18:56:14Z
TTGGACGCTTCCGTTCCGGTTCGAGATGCAGGTGTTTGCCGTTTTCGCATTTATCGTGAAACGCTTTCCGCGTTTCGTGCGCCCGCTTCACTCGCAGCATGGTTTCCACTGCGGGCCTTGTCAGGCTGACCACTTGCCGATGTGGGCGTCAGGTTACGCCCAGCTGCAACGCTTTGTGCATCCGGGGCGGTTAACGTGGCAGAAAAAAACGGCCGCAAGTGCGGCCTGCGTTTCAGGTTGGCAAAGGGGTATGCCACCTAGAACAGCGCATCAGCTTGTCTTTCCAGCAGACCATTGACCTGCACAATGGATTGGCGGTTCCCCGCAGGGCCTTCGTAACCCTGGCGGCAAGTGACCAATCATCTTGCCGCTTTTCGGGCTCGGCGTCGCGATACTGCGCAACCCTGGGCGGGGCTGTCGGCGATGACCTGGTCGATCATCGTTTCAATGGCTCCCCGTGTCGGTACGACTATAGCGGGGCCTTTCATACTCGATGATCGCATCGGCGCTTGCGCATTCCGCCGATGCCACAGCGCCTGGAAGACCTGCTTGGCTGCTTTTGCCGTTGATGGTGTCGTCGACACGCCTTTGAACCAGCTCGCCCAGCTGCGGCCGAGACCGGGCTGTCGGCGATGCTCAGGCTTTCACGGTTGAAGGCGCCTTGATAAGCTCGCCCTGCACCAGTTGGCCGCCTGCGCCCAGCATCGCCACCGCACGTGATGGATATCCCCTCGAAATATTCCGGCCATGTCGCGGCTGGCGGAAAGCACAGATGCATCACGACCGATC
+
'%--/;20)*(0+79B,&'2*()&*)6,-(.6/059+&)2-=G=,:;<4?IG/?>270.C=647;E:7'+*)1;/,2+.12:;*)31.30201-4*255*8/.;6420-,/&/?7=3@100A&(*8../=0()&(#+1211&.,0/-29A9>04-%/'))%'4,-%-.76,-.<2/858:=8>7@>3-)==E>A:--(4+((15@EHG8@6-03+.1345:0,,6,((005GH;-<-1-*':9C,100.)55-2,$'/-(),'('),$.*+,(+*0--14>H.5:4,65<-BC9;>:62)&&'$&**167(.+)>9:@>56543-2(,+21>;E;*.**0-($(.--.8)0%&&0/23@6;142640:1023CB:9=:5898-D;:<<<><=9.44&64/<.@:5.1CF5.??<<><;=8C:C:978C<FFG<96503,-/ABGED@HB@>;7E:8058@>A6/3%&+/.(**.17';.++,17.-#%$*+/-/134=<:CB<6312++:**+@=.318--560(.)/6221153;G>C9?4325333(9*8.8.--8?=/)*466@4.0./.589@C3/)-3;9;,-5+1/:02++,2=./-((1281-2-:,;87)0-12,4:CE=6;43*87<BB/4328@9,$%5/6F2+)(,.&1&&()++,)'/3?:72/,-/38;=6?,8,604<<433*93-%0168IE68-5*$))*,;=CB:922*+01462836?E;=D;D*61>E<B@CDEF>A:8:::01+/,'*$$$&$-%(-.8+)0(/&,&&$
@4588b58c-6c76-46c7-92ec-8448da26a2be runid=9c207653f919de83e5e0c7e8e98fe2e51e7429bd read=88 ch=317 start_time=2018-02-28T18:56:12Z
GGAGGCCATGCTGGATCATAAAGTGAGCTCCACACCGTCGTGATGACATTAACAAATATAAGCAGTTGTTTACCAATAACACGGATAAGCATTACCCTCGAAAGATGTGATTGATTTGAATCTTTGATGGCATTATCAGGCGGATTGCTCATACAGAGCATTAAAATTGATGGCGGATAAATATCGTATTTTCTCAAACCCAAGATCCTGAAATTAATCAGAGGTTGCGCACAAGTCCGGGATGATCTAATCATCGGAACAGAGACGTTCGGATTACCCGAATCGAATTAGATAACGTCTTGTGTTTCGGGAGCATTAGATGTGCGATATAGTGAAATTAATGATGCGATGGTTAGCCGCCGTTGAGGGCAATTCGTAGTTGGCAGAAAGAGCCTGTACCACAATCTGTCTTGGATGCCATGAGCTTGTCTTCACTCAGTTTTGGCCCAGTTACATCATTCCCAAACCGATGGATGCCGTTTACTGCCAGGTAGCACGTGCAAGTAGCGCTTGCAGCCAAGTCAAAACCAGCGTAGCCAGTATTAGCGAACAACTATATGTTTAAAGAAAACATGCTATTAAAGAAAACATGTTGAGTAGAAAACAGTGTCTTACCATAAAAAAACCGCCGATGTGGTTTTGTTAATATTCACTGTCGTCAAACTCAATACCCAACTCTTCCATGATCCGACGTGCCTCAACAGAATGCTATCAGGTTTATCCTTACGGATGTCGTCATCGGTTGGCAGAGAGGCTGCCGGTATAGGCATGTAAAATGCCTCCACGTAACTTTACTGTTGGTCGCATGACGCAGGTTAGCGAACCTGACGGCGGGTGCGCTCATCAGTAAAATTTTAATACTTTAAGTGGGATAAGGACGGTGATCTTCTTTACCTGCTCTTTCTTTTACCATGTTCGGCATACGGATTAATGTAATCATGGTTCCACCGCCATGTCTCACCTATCTTGATTATGGAATACAGAATGATGCTGCGGAGATTTTAGCTATATTAACCGCCACATACAAAGGTGTTTGAATAGAAGTGTTGACGTCCTAAAAGTACAGAGGTAAGTGGTGATGACGACTGGATCACAGCCAAATCGTGCCAGCGCAACAAGAGCAAGGATGAACCATGACGGGTAAAAAACCGACACCATTGCCGTTCGAACAGGAATTGGCACTGACCGCAACATCATGCGGTTATTGCCGCCTTTGTATTTATCAGCCAACTATCGTTTTCCTGCTTTTGGCGGCGTTCCCACTTATGATTATGCCCGTGGGGCAATCAACTCGAGCTCAGTTAGAGCAAGCGTTAACGGAACTGGAAGCGGAGCCGGTGCCGTGGTGACCAACTGTGGATAGCAGCCATTAACTTGGTGTTGTCTTTACTGGATGCAGGGGATCACATTGTTACTGCCCTGATTATTATGGTGGTACCTATCGCTTGTTGAGTCACGCGCCAAACGAGGATTTGGGTCAGTTTTGTCGATCAATCCTGATCGCAGGCGTTAACCGCTGCGCTGGCAAAACAGCCAGAGAACTGGTGTTGGTTAAGAGTACCCTCTAATCCGCTATTGCGTGGTGTGTGCTTTGCCTAAAATCATAAGGCCCGCAAATTATGGGGGGCATGGGTGGTGGTCGATAACACCTTTTATCACCAGCGCTCCAACAGCCGTTTCACTGGGTTACGGACATCATCGTGCATTCACTACTAGAATTTAGCTGGTCCTCTGATATTGTCGGTGGCGCTGTAGTGGCAGACGCCTGAATTGGCTGCAACATTAGCGTGGTGGGAGCCAGCTGCTTGGGCGCAACAGGCAGCACTTAGCGATAGTTATATGACATTGCGAGGGTTGCGTACTTTGGGCGCTCGGGTTAAACAGCATCAATAGAAATGCGCAAGCGGTATTGGCCTATTTGCAAACGGTCCTGCGGTGCGGCAACTCTATTATCGGTTTGGCGACACATCCAGGCCATGACATTTGCCGCCCGTCGGCAGTTTGGATTTGGTGGTATGCTCGGCCTCGGGCTGGACCTGGACTCCGCTGGAATCTTACGTTTAAATGACTTATCATAAACTGCGCTTAGCAGGAATCCTCAATTGCGTGAAATCTGGTCACCTAAATCCGAAGATCAGCGGAAACCACATCGTGACGGCA
+
,)'$&)*(((),,5213&&030-.*'))-;-&+.05,,,+)'%'%*),1/33.46)-.047*0/,2<-.2*')&4+.+1)*-.559&-'+'*(,2<834+44--11/%*'2++&&(-0)85)89')#.'*)'3),.82.0-)1*?-'(*,,-))))+'*00..31+*+-.0.3*1333,;2.*01(($-'(0059/A690).+*07@1.*.6412A4?@10(1/8E57,0.022+334+@AD9740-)3</2'(*&.0555*&*)458?8*,/:=9<.(&'6>;'))4+(&/(*'./A9A2%/./>1/'3+((+5A5:-567772,(*&,%,/%-1-15783:=?.14//3/6-(,8245E1>.(%,+-0*2.7)(-')41*-2/09>8-/08C<9,29,,,EICD?<;>:=:;;<'==()*%24>423=092,.5=6@4FIB5812-%,(=.0345<>D@D=4<,556789G<A06;-3F9.+)(&$$+)++./.-/.($(+'-)030,?+**.13314*331<<-;<5*8.2(27/1%*&6(*%(',;24:01352=290).>/+3>C?19:+,+*.'6:1(,2///-42=61(&++-05;B-,5<(3.22+)3107@@HHG@=CAD0//*2%&*9<C.A3E,2.+4470239<@;:00?,++1+41-66+27275-:)-*))*9?55&2/0,.(,&,)'%/,3/0421-3/6?@H8945152,/1A<=2:<;@AB9E,=3>+.*)((*')398:6+/559996<535-/<GH93(1)+,/&*#%',&'*,*4679HBEC3))$%*(+'0'8,<-&$$)-96@?@@0*+,,**.-/+.5===F6;>7D=;8CA.3.;95@F9:<'@2B?@86),,12471.--,062<A2/;=;?B957G;42GF?4;B=D8?47.33497<4A4;:<?:;9.A)%%)$/*4@?2//27DAE;AA?<69>/:@C<D::9G7<<A;B=6@:;<?<511/0443241&)/321%%+23A<<@=?=F48:3430*42:-/;./3HB-*+/+(-3./2AB<;318.--:CE5597>50407)4-+/-73,/3125:1=??@><624'(''/1209*5/=33.00=?>:C.,/)1;C'+-EACHGE66888*61-1?G@E:7;AC@==7%'(,472@94-0:E--++).*600144=66,,/3<79:?=C?F4>8B&,.).:/1.,.5,-*4<9--,+(.-:7B@A@BA6AI?76<678IH54/&.&(+2<2A>136;176+,54753A6)*)1--4596<0@5:911.55>+(.+)&+$&)-++-/=5552<;?<;>01))*2.-,>E:8=-A@+6-9.,-/026/2,01>56&;956@D2B0E-,2*;0;*7;69<BE?477;EAE99,6>B/;;--/,1=5=F,6327:/.987<&2:44)0,--7++/5;?<86;51:0+*-.11402&185:)-'&)*%9+'&(+B<)'6?>,030**/34>607)*,0/(0,4A@D6H.B.C/:;<><<@-.%.50.+-35?01/,32/4>;2+1(8-A6'(%*&%,/>;25/6:7@>,-.,@./1'5(,*)/+.)*(('$)&(0FF600&&))42<D*-=99(:/,.,6?>5.<:=::261*0*016?@><=:56?=GG@3:;0?64)2*2,C.3%<2))--5CC>664-5-3,%13;35:;;DGC4:8<6CH:/2678>.*)(6-+(&'.0622),..5:>4=@;6@.341>1./143+1/1-.)/<947;-/1<5<3>0013467173/0589C8753*'&//,/4/0+-(762:/03;?7;727$-%()&*(0,*+*256.089???12=45-+7=*CF056:2?2FC2@<><=C90*.:?45-)**235C8B9**9A40*3/4./89=?;.=...8>0%2B4-93@D=(>5CA04DA=?)+/*0-.--,/10A/34.58I8;8:=<>9::1=0&'028',/29<FG('0,)5:*/8:3B;/=AG>80):12549(8=@211/,.)*&.4/?BCCBE7B616*++////01/&+)&&')%''+*'*-1,--%&1.53)%%*'%0+.,)2)*&-).*.*,*1)'%$)&$$%$%/,+,/.1)85*,+(),204-((,((++++(,(-(&**((%+--')$&(*%'
  ```
</details>


## Assembly
Canu can be used directly on the data without any preprocessing. The only additional information needed is an estimate of the genome size of the sample. For saline isolates, we can safely estimate 3,000,000 base pairs based on previous data. 

So, if we were running Canu **WHICH WE ARE NOT!**, we could simply run the following command to assemble our data:

```
canu -nanopore_raw -p test -d nanopore *[input fastq files]* genomeSize=3000000 gnuplotTested=true
```

A quick description of all flags and parameters: 
-nanopore_raw - specifies data is Oxford Nanopore with no data preprocessing
-p - specifies prefix for output files, use “test” as default
-d - specifies directory to run test and output files in, use “nanopore” as default
genomeSize - estimated genome size of isolate
gnuplotTested - setting to true will skip gnuplot testing; gnuplot is not needed for this pipeline

Running this command will output various files into the nanopore directory.


## Assembly Visualization
There's a GUI program called [Bandage](https://rrwick.github.io/Bandage/) that allows you to visualize assemblies. We're not going to  over using Bandage, but if you opened of the files in the test_canu directory using Bandage, you would see the folliwng: O

<br /><img src="https://github.com/sabeelmansuri/bowman_archive/blob/master/Bandage.png" width="300"><br />

This suggests that one of our assembled pieces ("contigs") appears to be a whole circular chromosome!

This happens to be Contig 1. We extract only this sequence from the contigs file to examine further. Note that the first contig takes up the first 38,673 lines of the file, so use `head`:

```
head -n38673 test.contigs.fasta >> contig1.fasta 
```

## Your turn!
This is where you come in! There is a directory on our cluster that has the data you would expect if you completed all of the actions above. Specifically, Canu output plus the head command above. It is located at:

```
~/../smansuri/nanopore
```

Take a quick look at all of the files inside.

We can now blast this contig using NCBI’s nucleotide BLAST database (linked [here](https://blast.ncbi.nlm.nih.gov/Blast.cgi)) with all default options. Do this using Biopython, just like we did before. What is the top hit? 

<details>
  <summary>Answer</summary>
  
  ```
Hit: Halomonas sp. hl-4 genome assembly, chromosome: I  
Organism: Halomonas sp. hl-4  
Phylogeny: Bacteria/Proteobacteria/Gammaproteobacteria/Oceanospirillales/Halomonadaceae/Halomonas  
Max score: 65370  
Query cover: 72%  
E value: 0.0  
Ident: 87%  
```
</details>


It appears this chromosome is the genome of an organism in the genus *Halomonas*. Google *Halomonas*. Sanity check: Does it make sense that we'd find *Halomonas* at South Bay Saltworks?

So, we've identified (generally) which organism this genetic data comes from! We may now be interested in the gene annotation of this genome.


## Gene Annotation
Prokka will take care of gene annotation, the only required input is the contig1.fasta file.

```
prokka --outdir circular --prefix test_prokka ~/../smansuri/nanopore/contig1.fasta
```

The newly created circular directory contains various files with data on the gene annotation. Take a look inside test_prokka.txt for a quick summary of the annotation.


## Summary
The analysis above has taken Oxford Nanopore sequenced data, assmebled contigs, identified the closest matching
organism, and annotated its genome.

## Credits
Adapted from my [Bowman Lab Tutorial](https://www.polarmicrobes.org/tutorial-nanopore-analysis-pipeline/)
