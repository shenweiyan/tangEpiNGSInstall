Installtion for softwares for tanglab NGS docker.

# Usage

- Basic Usage example 1: 
```bash
# avoiding Permission issue
mkdir -p  /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/out
chmod 777 /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/out

docker run  -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/test_fq/:/fastq -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/out:/home/analyzer/project -v /Volumes/MacintoshHD/Users/hubq/Downloads/FileZilla/DataBase/mm10/:/home/analyzer/database_ChIP/mm10  -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/settings/:/settings/ --env ref=mm10 --env type=ChIP tanginstall:v1

docker run  -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/test_fq_RNA/:/fastq -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/outRNA:/home/analyzer/project -v /Volumes/MacintoshHD/Users/hubq/Downloads/FileZilla/DataBase/mm10/:/home/analyzer/database_RNA/mm10  -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/settings/:/settings/ --env ref=mm10 --env type=RNA tanginstall:v1
```

- Basic Usage example 2: 
```
$ git clone https://github.com/shenweiyan/tangEpiNGSInstall.git
$ tree
.
└── tangEpiNGSInstall
    ├── Dockerfile
    ├── README.md
    ├── settings
    │   ├── run_chipseq.py
    │   ├── run_chipseq.sh
    │   ├── run_mRNA.py
    │   ├── run_mRNA.sh
    │   ├── scripts_chipseq.py
    │   └── scripts_mRNA.py
    ├── src
    │   └── run_sample.sh
    ├── test_fq
    │   ├── H3K4me3
    │   │   ├── test.1.fq.gz
    │   │   └── test.2.fq.gz
    │   ├── Input
    │   │   ├── test.1.fq.gz
    │   │   └── test.2.fq.gz
    │   └── sample.tab.xls
    └── test_fq_RNA
        ├── SampleA1
        │   ├── test.1.fastq.gz
        │   └── test.2.fastq.gz
        └── sample.tab.xls

8 directories, 17 files

$ mkdir -p results database_ChIP/mm10
$ chmod 777 results database_ChIP/mm10    # avoiding Permission issue
$ tree
.
├── database_ChIP
│   └── mm10
├── results
└── tangEpiNGSInstall
    ├── Dockerfile
    ├── README.md
    ├── settings
    │   ├── run_chipseq.py
    │   ├── run_chipseq.sh
    │   ├── run_mRNA.py
    │   ├── run_mRNA.sh
    │   ├── scripts_chipseq.py
    │   └── scripts_mRNA.py
    ├── src
    │   └── run_sample.sh
    ├── test_fq
    │   ├── H3K4me3
    │   │   ├── test.1.fq.gz
    │   │   └── test.2.fq.gz
    │   ├── Input
    │   │   ├── test.1.fq.gz
    │   │   └── test.2.fq.gz
    │   └── sample.tab.xls
    └── test_fq_RNA
        ├── SampleA1
        │   ├── test.1.fastq.gz
        │   └── test.2.fastq.gz
        └── sample.tab.xls

11 directories, 17 files

$ docker pull hubq/tanginstall:latest

$ docker run -v /data/docker/train/tangEpiNGSInstall/test_fq:/fastq -v /data/docker/train/results:/home/analyzer/project -v /data/docker/train/database_ChIP/mm10:/home/analyzer/database_ChIP/mm10 -v /data/docker/train/tangEpiNGSInstall/settings/:/settings/ --env ref=mm10 --env type=ChIP hubq/tanginstall:latest
INFO  @ 2021-06-10 03:29:48,154: Begin checking input files.
INFO  @ 2021-06-10 03:29:48,154: Input database files were all put in /home/analyzer/database_ChIP/mm10.
INFO  @ 2021-06-10 03:29:48,154: Input fasta /home/analyzer/database_ChIP/mm10/mm10.fa not find. Now download from UCSC
INFO  @ 2021-06-10 03:45:01,604: /home/analyzer/database_ChIP/mm10/mm10.fa generation done!
INFO  @ 2021-06-10 03:45:01,605: Fasta were not indexed.
INFO  @ 2021-06-10 03:45:02,105: Now build index using bwa.
INFO  @ 2021-06-10 03:48:20,683: Building index done!
INFO  @ 2021-06-10 03:48:20,683: Genome GTF file were not found.
INFO  @ 2021-06-10 03:48:21,184: Now download refGene file from UCSC.
INFO  @ 2021-06-10 05:03:38,768: Generate refGene done!
INFO  @ 2021-06-10 05:03:38,768: RepeatMask file were not found.
INFO  @ 2021-06-10 05:03:39,269: Now download rmsk file from UCSC.
INFO  @ 2021-06-10 05:06:03,592: Generate RepeatMask done!
Traceback (most recent call last):
  File "/home/analyzer/module/ChIP/run_chipseq.py", line 148, in <module>
    main()
  File "/home/analyzer/module/ChIP/run_chipseq.py", line 126, in main
    samp_peak.get_idr_stat()
  File "/home/analyzer/module/ChIP/frame/module02_call_peaks.py", line 244, in get_idr_stat
    mod_Stat.IDR_Stat()
  File "/home/analyzer/module/ChIP/frame/module00_StatInfo.py", line 113, in IDR_Stat
    f_idr_out   = open(file_idr_out,"w")
IOError: [Errno 2] No such file or directory: '/home/analyzer/project/ChIP_test/StatInfo/IDR_result./home/analyzer/project/ChIP_test/sample.tab.xls'
cp: cannot stat `03.2.Peak_mrg/*/*_treat_minus_control.sort.norm.bw': No such file or directory
cp: cannot stat `03.3.Peak_idr/*/*.conservative.regionPeak.gz*': No such file or directory
cp: cannot stat `StatInfo/*': No such file or directory
```
![docker-error](https://user-images.githubusercontent.com/26101369/121470941-79a3a080-c9f1-11eb-8fd7-2f199d2d5c16.jpg)

**注意：**

hubq/tanginstall:latest 的镜像如果运行过程中出现上面的错误，**请把 hubq/tanginstall:latest 镜像更换为 shenweiyan/tanginstall:latest，然后重新执行 docker run 命令！**

# 其他简要说明

ref 选择为 mm10，如果你的本地路径没有 mm10.fa，本 Docker 流程的第一步会：

1. 首先，下载网上的 fasta 文件（[http://hgdownload.soe.ucsc.edu/goldenPath/mm10/bigZips/chromFa.tar.gz](http://hgdownload.soe.ucsc.edu/goldenPath/mm10/bigZips/chromFa.tar.gz)）。

2. 然后，解压，再通过 cat 把 chr{1..22} X Y M 合并成 ${ref}.fa。
```
$ cat /home/analyzer/project/ChIP_test/scripts/sample.tab/db01.DownloadRef.sh
ref=$1
dir_database=/home/analyzer/database_ChIP/$ref
dir_path=/home/analyzer/module/ChIP

cd $dir_database

wget http://hgdownload.soe.ucsc.edu/goldenPath/${ref}/bigZips/chromFa.tar.gz

tar -zxvf $dir_database/chromFa.tar.gz

for i in {1..22} X Y M
do
    cat $dir_database/chr$i.fa
done  >$dir_database/${ref}.fa && rm $dir_database/chr*fa
```

3. 最后，建立 bwa 软件的 index。
```
/software/install_packages/bwa-0.7.5a/bwa index /home/analyzer/database_ChIP/mm10/mm10.fa
```
