# Comandos de la Practica 02
## Equipo SARS
### Integrante 1: Diana Balmaseda
### Integrante 2: Gabriel Loya
### Integrante 3: Luis Tenorio

## Parte I.
01. mkdir sars_p02
02. cd sars_p02
    nano comandos_p02.md

## Parte II.
| Plataforma/compañía          | Longitud de lecturas (pb)  | # lecturas x corridas  | Tiempo   | Costo x 10^6 bases  | Error (%)   | Química                    |
| ------------------------------------ |:-------------------------------:| ------------------:| -----------:| ----------------------------:| --------------:| ---------------------------:|
| Primera generación  |     |   |   |    |    |     |
| Sanger/Life Technologies    | 800                                | 1                    | 2 hrs      | 2400                           | 0.3             | Dideoxy terminator   |
| Segunda generación           |                                       |                       |               |                                    |                   |                                   |   
| 454 GS FLX+/Roche	| 700	| 1×10^6	| 24/48 hrs |	10	| 1	| Pyrosequencing |
| GS Junior/Roche	| 500	| 1×10^5	| 18 hrs |	9	|	|	Pyrosequencing |
| HiSeq/Illumina |	2x150 |	5×10^9 | 27/240 hrs |	0.1	| 0.8	| Reversible terminators |
| MiSeq/Illumina | 2x300 |	3×10^8	| 27 hrs |	0.13	| 0.8 |	Reversible terminators|
| SOLiD/Life Technologies | 50	| 1×10^9	| 14 días | 0.13	| 0.01	| Ligation |
| Retrovolocity/BGI |	50	| 1×10^9	| 14 días	| 0.01	| 0.01	| Nanoball/ligation |
| Ion Proton/Life Technologies | 200	| 6×10^7 |	2–5 hrs |	1 |	1.7	|	Proton detection |
| Ion PGM/Life Technologies |	200	| 5×10^6 | 	2–5 hrs |	1 |	1.7	| Proton detection |
| Tercera generación              |                                       |                       |               |                                    |                   |                                   |						
| SMRT/Pac Bio |	>10,000	| 1×10^6 | 1–2 hrs |	2	 | 12.9 |	Real-time SMS |
| Heliscope/Helicos| 35 |	7×10^9	| 8 días |	0.01	| 0.2 |	Real-time SMS |
| Nanopore/Oxford Nanopore Technologies |	>5000	| 6×10^4 |	48/72 hrs |	<1	| 34 |	Real-time SMS |
| Electron microscopy/ZS| 	7200 | 	|	14 h | 	<0.01 |   | Real-time SMS |

## Parte III.
01. 
  * En el artículo [@myco2017] en la sección "Availability of data and materials" podemos encontrar la liga a las secuencias del *Mycoplasma genitalium*. 
  * **Mover los archivos** 
      mv ERR486827_1.fastq.gz ~/still.luis-ciencias.unam.mx/sars_p02/data/raw_data
      mv ERR486827_2.fastq.gz ~/still.luis-ciencias.unam.mx/sars_p02/data/raw_data
  * **Ligas simbólicas**
      ln -s ~/still.luis-ciencias.unam.mx/sars_p02/data/raw_data/ERR486827_2.fastq.gz 
      ln -s ~/still.luis-ciencias.unam.mx/sars_p02/data/raw_data/ERR486827_1.fastq.gz 
  * **fastq a fasta**
      gunzip -c ERR486827_1.fastq.gz | awk '/^@ERR/{gsub(/^@/,">",$1);print;getline;print}' > ERR486827_1.fasta
      gunzip -c ERR486827_2.fastq.gz | awk '/^@ERR/{gsub(/^@/,">",$1);print;getline;print}' > ERR486827_2.fasta

02.
* En el 1 tenemos 398824 (grep ERR -c ERR486827_1.fasta) y en el 2 tenemos 398824 (grep ERR -c ERR486827_2.fasta) por lo que sí tenemos la misma cantidad de secuencias.
* El siguiente código se usó para aislar las secuencias sin headers (awk '/^>ERR/{getline;print}' ERR486827_2.fasta  > ERR486827_2_aux.fasta) luego se aplicó ( awk '{print length($0)}' ERR486827_2_aux.fasta > length_2.txt) para obtener la longitud de cada secuencia y finalmente (awk '{ total += $1; count++ } END { print "Promedio: "  total/count}' length_2.txt >> length_2.txt) para obtener el promedio. 

03. 
* Alineamiento:
`AGCATGTTAGATTA   GATAGCTGTGCTA...`

      `TTAGAT AAAGGATA CTG`
* Alineamiento empezando en posición 6 (empezando de 0) y cadena de CIGAR 6M1D1M3I4M1D3M

04.
* three_prime_UTR: 1
* stem_loop: 5
* gene: 11
* CDS: 13
* region: 2
* five_prime_UTR: 1


## Parte IV.
01. cd sars_p02 | mkdir bin

## Parte V.

01. cd sars_p02

    wget 'https://sra-downloadb.be-md.ncbi.nlm.nih.gov/sos1/sra-pub-run-1/SRR253106/SRR253106.3'
    
    [Link a la base de datos SRA](https://www.ncbi.nlm.nih.gov/sra/?term=SRR253106.3)
    
    mv SRR253106.3 data/raw_data
    
02. *Instrument:*  454 GS 20 (Life Sciences)

    *Strategy:* WGS
    
    *Source:* GENOMIC
    
    *Selection:* RANDOM
    
    *Layout:* SINGLE
    
 03. Teniedo que: 
* El genoma de Geobacter lovleyi SZ mide **3917761** bp
* En el archivo fastq hay **614406** lecturas single end
* La longitud de las lecturas es de **107.35** pb en promedio

 La cobertura del genoma = (# de lecturas * longitud de lecturas / tamaño del genoma) es de: 
 
    **16.84
 04.

    

## Referencias
* https://www.intechopen.com/books/next-generation-sequencing-advances-applications-and-challenges/next-generation-sequencing-an-overview-of-the-history-tools-and-omic-applications

* https://www.ncbi.nlm.nih.gov/nuccore/CP001089.1
---
references:
  - id: myco2017
    title: *Mycoplasma genitalium*: whole genome sequence analysis, recombination and population structure
    author:
      - family: Fookes
        given: María C
      - family: Harris 
        given: Simon
      - family: Parmar 
        given: Surendra
      - family: Unemo 
        given: Magnus
      - family: Jensen
        given: Jørgen S.
      - family: Thomson 
        given: Nicholas R.
    container-title: BMC genimics 
    volume: 18
    URL: "https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5745988/#MOESM1"
    DOI: 10.1186/s12864-017-4399-6
    type: article-journal
    issued:
      year: 2017
      month: 12
---
