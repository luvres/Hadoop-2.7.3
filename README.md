## Hadoop 2.7.3 with CentOS 7
### · Pseudo distributed mode
### · PySpark with Jupyter Notebook
---

### Pull image latest (with CentOS 7)
```
docker pull izone/hadoop
```
#### Pull image with CentOS 6
```
docker pull izone/hadoop:2.7.3
```
#### Run pulled image
```
docker run --rm --name Hadoop -h hadoop \
	-p 8088:8088 \
	-p 8042:8042 \
	-ti izone/hadoop -test bash
```
#### Build image
```
git clone https://github.com/luvres/hadoop.git
cd hadoop
docker build -t hadoop .
```
#### Build image with CentOS 6
```
docker build -t hadoop:2.7.3 ./centos6/
```
### Run built image
```
docker run --rm --name Hadoop -h hadoop \
	-p 8088:8088 \
	-p 8042:8042 \
	-ti hadoop bash
```
### Hadoop Browser
```
http://localhost:8088
```
---
## Testing..

#### Create a Directory
```
hdfs dfs -mkdir /bigdata
```

#### List diretory
```
hadoop fs -ls /
```

#### Download a file csv
```
wget -c http://compras.dados.gov.br/contratos/v1/contratos.csv
```

#### Copy file to the HDFS directory created above
```
hadoop fs -copyFromLocal contratos.csv /bigdata
```

#### Read file
```
hadoop fs -cat /bigdata/contratos.csv
```
#### Test word count with mapreduce
```
hadoop jar /opt/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount /bigdata/contratos.csv /output
```

#### Read result
```
hdfs dfs -cat /output/*
```
---
## PySpark and Jupyter Notebook
```
mkdir $HOME/notebooks
```
### Pull image with Miniconda
```
docker run --rm --name Hadoop -h hadoop \
	-p 8088:8088 \
	-p 8042:8042 \
	-p 8888:8888 \
	-p 4040:4040 \
	-v $HOME/notebooks:/root/notebooks \
	-ti izone/hadoop:miniconda bash
```
### Pull image with Anaconda
```
docker run --rm --name Hadoop -h hadoop \
	-p 8088:8088 \
	-p 8042:8042 \
	-p 8888:8888 \
	-p 4040:4040 \
	-v $HOME/notebooks:/root/notebooks \
	-ti izone/hadoop:anaconda bash
```
### Browser access

#### Jupyter Notebook
```
http://localhost:8888
```
#### Spark management jobs
```
http://localhost:4040
```
### Build image
```
git clone https://github.com/luvres/hadoop.git
cd hadoop
```
#### With Miniconda
```
docker build -t hadoop:miniconda ./miniconda/
```
#### With Anaconda
```
docker build -t hadoop:anaconda ./anaconda/
```


