Installtion for softwares for tanglab NGS docker.

usage:

```bash
# avoiding Permission issue
mkdir -p  /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/out
chmod 777 /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/out

docker run  -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/test_fq/:/fastq -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/out:/home/analyzer/project -v /Volumes/MacintoshHD/Users/hubq/Downloads/FileZilla/DataBase/mm10/:/home/analyzer/database_ChIP/mm10  -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/settings/:/settings/ --env ref=mm10 --env type=ChIP tanginstall:v1

docker run  -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/test_fq_RNA/:/fastq -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/outRNA:/home/analyzer/project -v /Volumes/MacintoshHD/Users/hubq/Downloads/FileZilla/DataBase/mm10/:/home/analyzer/database_RNA/mm10  -v /Users/hubq/Downloads/Project/tangEpiPipeline/tangEpiPipelineInstall/settings/:/settings/ --env ref=mm10 --env type=RNA tanginstall:v1
```

------

edit by shenweiyan:

ref 选择为 mm10，如果你的本地路径没有 mm10.fa，本 Docker 流程的第一步会：

首先，下载网上的 fasta 文件（[http://hgdownload.soe.ucsc.edu/goldenPath/mm10/bigZips/chromFa.tar.gz](http://hgdownload.soe.ucsc.edu/goldenPath/mm10/bigZips/chromFa.tar.gz)）。

然后，解压，再通过 cat 把 chr{1..22} X Y M 合并成 ${ref}.fa。
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

最后，建立 bwa 软件的 index。
