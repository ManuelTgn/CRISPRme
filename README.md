# CRISPRme
[![install with bioconda](https://img.shields.io/badge/install%20with-bioconda-brightgreen.svg?style=flat)](http://bioconda.github.io/recipes/crispritz/README.html)

CRISPRme is a web based tool dedicated to perform predictive analysis and result assessement on CRISPR/Cas experiments with a user-friendly GUI and the precise scope of searching individual variant in VCF dateset.

With this aim in mind we created a simple package that takes care of any step, from downloading the necessary data, to execute a complete search and present to the user an exhaustive result report with images and tabulated targets to navigate with the included web-based GUI.

The software is composed of two principal function:

- complete-search, function to perform a search starting from scratch input data, like a reference genome, a set of VCF data and list of sgRNAs targets.
- targets-integration, function to perform the integration of results targets with a gencode proximity file to identify genes near targets and collect only the top scoring targets in term of CFD score.
- web-interface, function to start the web-interface accessible locally from a web browser

# CRISPRme Installation and Usage
The two fastest way to use CRISPRitz is through the installation of Docker or Conda.
Here we summarize the steps to install CRISPRitz with Docker and Conda.

## Installation (Phase 1)
**Conda installation (Linux and MacOS):**
- Open a terminal window
- Paste this command into the terminal (Linux):
    ```
    curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh --output Miniconda3-latest-Linux-x86_64.sh
    ```
- Paste this command into the terminal (MacOS):
    ```
    curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh --output Miniconda3-latest-MacOSX-x86_64.sh
    ```
- If the file is correctly downloaded you now need to execute it to complete the installation, so paste this command into the terminal:
    - Linux
    ```
    bash Miniconda3-latest-Linux-x86_64.sh
    ```
    - MacOS
    ```    
    bash Miniconda3-latest-MacOSX-x86_64.sh
    ```
- Press ENTER when requested and yes when an answer is requested, in this way you allow conda to set all the directories in your HOME path for an easy use
- After the complete installation you will receive this message “Thank you for installing Miniconda3!” to certify the correct installation.
- Now you need to close the terminal window you are using and open a new one, to allow the system to start conda.
- In the new terminal window you should see something like this:
    ```
    (base) user@nameofPC:~$
    ```
    If you read the "(base)" like this, conda is loaded correctly and you can start using it.
- Now you need to set the channels to allow conda to access different repositories and set the default version of python to version 3.8, so paste these commands into the terminal you just opened:
    ```
    conda config --add channels defaults
    conda config --add channels bioconda
    conda config --add channels conda-forge
    conda install python=3.8
    ```
- Now, you can install CRISPRme by typing the command:
    ```
    conda create -n crisprme python=3.8 crisprme -y
    conda activate crisprme
    ```
- To test your installation, type the command:
    ```
    crisprme.py
    ```
- After the execution of the command you should see a list of CRISPRitz tools.

Now the software is installed and ready to be used.

**Docker installation:  
Note: if you are using MasOS or Windows, you just need to download the installer file
and follow the on screen instructions.  
https://docs.docker.com/docker-for-windows/install/ (Windows)  
https://docs.docker.com/docker-for-mac/install/ (MacOS)**

**Ubuntu installation guide:**
- Open a terminal window
- Paste this command to update the index repository:
    ```
    sudo apt-get update
    ```
- Paste this command to allow package installation over HTTPS:
    ```
    sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
    ```
- Paste this command to add the docker key:
    ```
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```
- Paste this command to set the correct version of docker for your system:
    ```
    sudo add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    Stable"
    ```
- Paste this command to update the index repository another time, to make sure everything is ready and set to install docker:
    ```
    sudo apt-get update
    ```
- Then paste this command to finally install docker:
    ```
    sudo apt-get install docker-ce docker-ce-cli containerd.io
    ```
- Paste this last command to check if the installation is complete and functional:
    ```
    sudo docker run hello-world
    ```
- If this message is printed, everything is perfectly installed
![docker hello world](https://user-images.githubusercontent.com/40895152/63214349-769e3880-c117-11e9-8ee2-d754096b3aca.png)
- Now, we need to do some more steps to complete the settings. Paste this command to create a user group for docker user:
    ```
    sudo groupadd docker
    ```
- Paste this command to add your current user to the created group:
    ```
    sudo usermod -aG docker $USER
    ```
- Now you need to restart your machine or the virtual environment, to re-evaluate the user groups.
- One last command to test if the group is well configured. Paste this command:
    ```
    docker run hello-world
    ```
- If the previous “hello from docker” message is printed, everything is perfectly set.

## Post installation test (Phase <a name="phase2">2</a>):
- Download and untar this package:
    ```
    conda install gdown -y
    gdown https://drive.google.com/uc?id=11wn9pg6AWzDYZ7V_LjBIjGvgx95bnVJ1
    tar -xvf crisprme_test.tar.gz
    ```
- Then move into the directory
    ```
    cd crisprme_test/
    ```
- Write this command to execute the script if you installed with Conda:
    ```
    bash crisprme_auto_test_conda.sh
    ```
- Write this command to execute the script if you want to use Docker (the script will automatically download the necessary docker image):
    ```
    bash crisprme_auto_test_docker.sh
    ```
- You will see the processing starting, first with the download of all the necessary data and then with the analysis, depending on the system hardware and internet connection this may take very different time

After downloading and untaring the package, you will have a ready to use CRISPRme directory, remember DO NOT change any name of folders in the directory to avoid losing data or force the recreation of indexing and dictionaries.
Here a more detailed explanation of the folder structure:
![Folder_structure](https://github.com/pinellolab/CRISPRme/blob/main/folder_structure.png)
- Genomes: folder containing all the genomes in fasta format, each genome has to be saved into a specific folder and the name of the folder will be used to identify the genome itself and all the correlated data (VCF and samplesID).
  - hg19: folder containing fasta files of human genome 19.
  - hg38: folder containing fasta file of human genome 38.
- VCFs: folder containing all the VCFs datasets, each dataset has to be saved into a specific folder and the name must contain the genome release correlated to the variant data.
  - hg38_HGDP: folder containing vcf files of HGDP set correlated with hg38.
  - hg38_1000G: folder containing vcf files of 1000G set correlated with hg38.
- samplesIDs: folder containing all the samplesID files, one for each VCF dataset, the name of the file must contain the identifier of a VCF dataset and the samplesID suffix.
  - hg38_HGDP.samplesID.txt: tabulated file with header to identify samples for HGDP dataset.
  - hg38_1000G.samplesID.txt: tabulated file with header to identify samples for 1000G dataset.
- Annotations: folder containing all the annotation bed files, there is no restriction on the name for this file.
  - gencode_encode.hg38.bed: bed file containing all the pregenerated annotations from gencode and encode datasets.
- PAMs: folder containing all the PAM text files, one for each PAM, the name of the file must contain the name of the Cas protein as last field (field separator character “-”).
  - 20bp-NGG-spCas9.txt: text file containing the single line PAM, in the name is contained the position of the crRNA (the first 20bps), the position of the PAM sequence (the following 3 nucleotides, NGG) and the Cas protein (spCas9).


## Usage (Phase 3):
**<a name="Complete-Search">3.1</a> CRISPRme Complete-Search function**  
This function perform a complete search from scratch producing all the results and post-analysis data.
Input:
- Directory containing a genome in fasta format, need to be separated into single
chromosome files.
- Text file containing path to VCF directories [OPTIONAL]
- Text file with a list of guide (1 to N)
- Text file with a single PAM sequence
- Bed file with annotation, containing a list of genetic regions with a function associated
- Text file containing a list of path to samplesID file (1 to N) equal to the number of VCF dataset used [OPTIONAL]
- Bed file extracted from Gencode data to find gene proximity of targets
- Maximal number of allowed bulges of any kind to compute in the index genome
- Threshold of mismatches allowed
- Size of DNA bulges allowed
- Size of RNA bulges allowed
- Merge range, necessary to reduce the inflation of targets due to bulges, it's the window of bp necessary to merge one target into another maintaining the highest scoring one
- Output directory, in which all the data will be produced
- Number of threads to use in computation
Output:
- bestMerge targets file, containing all the highest scoring targets, in terms of CFD and targets with the lowest combination of mismatches and bulges (with preference to lowest mismatches count), each genomic position is represent by one target
- altMerge targets file, containing all the discarded targets from the bestMerge file, each genomic position can be represented by more than target
- Parameters data file, containing all the parameters used in the search
- Count and distribution files, containing all the data count file useful in the web-tool representation to generate main tables and view
- Integrated results and database, containing all the tabulated data with genes proximity analysis and database representation to rapid querying on the web-tool GUI
- Directory with raw targets, containing the un-processed results from the search, useful to recover any possible target found during the search
- Directory with images, containing all the images generated to be used with the web-tool

Example call:
- Conda
    ```
    crisprme.py complete-search --genome Genomes/hg38/ --vcf list_vcf.txt/ --guide sg1617.txt --pam PAMs/20bp-NGG-spCas9.txt --annotation Annotations/gencode_encode.hg38.bed --samplesID list_samplesID.txt --gene_annotation Gencode/gencode.protein_coding.bed --bMax 2 --mm 6 --bDNA 2 --bRNA 2 --merge 3 --output Results/sg1617/ --thread 4
    ```
- Docker
    ```
    docker run -v ${PWD}:/DATA -w /DATA -i scancellieri/crisprme crisprme.py complete-search --genome Genomes/hg38/ --vcf list_vcf.txt/ --guide sg1617.txt --pam PAMs/20bp-NGG-spCas9.txt --annotation Annotations/gencode_encode.hg38.bed --samplesID list_samplesID.txt --gene_annotation Gencode/gencode.protein_coding.bed --bMax 2 --mm 6 --bDNA 2 --bRNA 2 --merge 3 --output Results/sg1617/ --thread 4
    ```

**<a name="Targets-Integration">3.2</a> CRISPRme Targets-Integration function**  
This function produces the integrated data starting from a Merge file (best/alt).
Input:
- Best/Alt merge targets file, containing the processed targets
- Genome version, the name of the genome used in the search, such as hg38,hg19,mm10 and so on
- Bed file extracted from Gencode data to find gene proximity of targets
- Bed file containing empirical verified OT, like via GUIDE-seq, CIRCLE-seq and other sequencing protocols
- Directory of VCF data used in the search, supporting only one dataset at the time
- Output directory, in which all the temporary data and final integrated results will be created

Output:
- Directory containing the integrated result file with all the targets from the merge input file and a notfound file containing all the targets from empirical verified OT that does not match in a predicted in-silico target

Example call:
- Conda
    ```
    crisprme.py targets-integration --targets sg1617.bestMerge.txt --genome_version hg38 --guide sg1617.txt --gencode Gencode/gencode.protein_coding.bed --output .
    ```
- Docker
    ```
    docker run -v ${PWD}:/DATA -w /DATA -i i scancellieri/crisprme crisprme.py targets-integration --targets sg1617.bestMerge.txt --genome_version hg38 --guide sg1617.txt --gencode Gencode/gencode.protein_coding.bed --output .
    ```
    
**<a name="Web-Interface">3.3</a> CRISPRme Web-Interface function**  
This function starts the server to use the web-interface

Example call:
- Conda
    ```
    crisprme.py web-interface
    ```
- Docker
    ```
    docker run -v ${PWD}:/DATA -w /DATA -p 8080:8080 -i scancellieri/crisprme crisprme.py web-interface
    ```
