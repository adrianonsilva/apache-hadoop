# Hadoop

- [1. Descrição](#link1)
- [2. Instalação](#link2)
- [3. Verificando a Instalação](#link3)
- [4. Links](#link4)

<a id="link1"></a>
## 1. Descrição

Hadoop é um framework de código aberto que permite processar e armazenar grandes quantidades de datasets (big data) em um ambiente distribuido através de clusters de computadores, usando o modelo de progração MapReduce.

- HDFS
Hadoop distributed file system (HDFS)</br>
Sistema de arquivos onde os datasets são armazenados (datanodes)</br>

- MapReduce
Camada de processamento de dados do Hadoop</br>

1) Map (lógica mais complexa a ser executada)
2) Reduce (coleta os resultados dos sub-job e produz o resultado final)

- YARN
É o framework de processamento do Hadoop, realiza o gerenciamento de recursos

- Funções

Name Node ou Master Node gerencia o sistema de arquivos e contêm o metadado de dos dados armazenados,
contendo os detalhes do número de blocos, localização dos dados e replicas.

Data Node ou Slave é onde os dados estão armazenados. Estão em constante cominicação com o Name Node.

<a id="link2"></a>
## 2. Instalação

A instalação a seguir será usado o Hadoop 2.6.4, em um cluster de 6 máquinas (1 master e 5 slaves)

- criação do usuário e grupo

#criar usuário e grupo</br>
sudo addgroup hadoop</br>
sudo adduser --ingroup hadoop hduser</br>

sudo adduser hduser hadoop</br>
sudo adduser hduser sudo</br>

- SSH and Key Generation</br>
SSH é necessário para sejam realizadas operações dentro do cluster (star, stop de serviços)</br>
As chaves são necessárias para que seja realizada a conexão sem precisar de digitação de senhas

su hduser</br>
ssh-keygen -t rsa -P "" -f ~/.ssh/id_rsa</br>
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys</br>
chmod 0600 ~/.ssh/authorized_keys</br>

#Generate ssh key</br>
ssh-keygen -t rsa -b 4096</br>
#Copy to other nodes</br>
ssh-copy-id [destino]</br>


![Screenshot](/images/hd07.jpg)

![Screenshot](/images/hd08.jpg)

![Screenshot](/images/hd09.jpg)

![Screenshot](/images/hd10.jpg)

![Screenshot](/images/hd12.jpg)

- Java

![Screenshot](/images/hd01.jpg)

![Screenshot](/images/hd02.jpg)

- Download do Hadoop</br>

wget https://archive.apache.org/dist/hadoop/core/hadoop-2.6.4/hadoop-2.6.4.tar.gz</br>

sudo tar -xzf hadoop-2.6.4.tar.gz</br>
sudo mv hadoop-2.6.4 /usr/local/hadoop</br>
sudo chown -R hduser /usr/local/hadoop</br>

![Screenshot](/images/hd03.jpg)

![Screenshot](/images/hd04.jpg)

- Variáveis de ambiente</br>
#editar o arquivo ~/.bashrc</br>

sudo nano ~/.bashrc</br>

#java</br>
export JAVA_HOME="/usr/lib/jvm/jdk-8-oracle-arm32-vfp-hflt/jre"</br>
export PATH=$PATH:$JAVA_HOME/bin</br>
export CLASSPATH=$JAVA_HOME/lib/*</br>

#hadoop</br>
export HADOOP_HOME=/usr/local/hadoop</br>
export HADOOP_INSTALL=/usr/local/hadoop</br>
export PATH=$PATH:$HADOOP_INSTALL/bin:$HADOOP_INSTALL/sbin</br>
export HADOOP_MAPRED_HOME=$HADOOP_HOME</br>
export HADOOP_COMMON_HOME=$HADOOP_HOME</br>
export HADOOP_HDFS_HOME=$HADOOP_HOME</br>
export YARN_HOME=$HADOOP_HOME</br>
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native</br>
export HADOOP_OPTS="-Djava.library.path"=$HADOOP_HOME/lib</br>
export CLASSPATH=$CLASSPATH:/usr/local/hadoop/lib/*</br>

source ~/.bashrc</br>

![Screenshot](/images/hd05.jpg)

![Screenshot](/images/hd06.jpg)

- Editar arquivos hostname, hosts, slaves</br>
sudo nano /etc/hostname</br>
sudo nano /etc/hosts</br>
sudo nano slaves</br>

- Configuração do Hadoop

#criação dos diretórios</br>
#master</br>
cd /usr/local/hadoop</br>
mkdir /usr/local/hadoop/hadoopdata</br>
mkdir /usr/local/hadoop/hadoopdata/hdfs</br>
mkdir /usr/local/hadoop/hadoopdata/hdfs/namenode</br>
mkdir /usr/local/hadoop/hadoopdata/hdfs/tmp</br>

#slaves</br>
cd /usr/local/hadoop</br>
mkdir /usr/local/hadoop/hadoopdata</br>
mkdir /usr/local/hadoop/hadoopdata/hdfs</br>
mkdir /usr/local/hadoop/hadoopdata/hdfs/datanode</br>
mkdir /usr/local/hadoop/hadoopdata/hdfs/tmp</br>

![Screenshot](/images/hd11.jpg)

#edição dos arquivos de configuração

#hadoop-env.sh</br>
sudo nano /usr/local/hadoop/etc/hadoop/hadoop-env.sh</br>

#hdfs-site.xml</br>
sudo nano /usr/local/hadoop/etc/hadoop/hdfs-site.xml</br>

#mapred-site.xml</br>
cd /usr/local/hadoop/etc/hadoop/</br>
cp mapred-site.xml.template mapred-site.xml</br>
sudo nano /usr/local/hadoop/etc/hadoop/mapred-site.xml</br>

#yarn-site.xml</br>
sudo nano /usr/local/hadoop/etc/hadoop/yarn-site.xml</br>

![Screenshot](/images/hd13.jpg)

![Screenshot](/images/hd14.jpg)

![Screenshot](/images/hd15.jpg)

![Screenshot](/images/hd16.jpg)

#formatar o nanonode</br>
cd $HADOOP_HOME/bin/</br>
hdfs namenode -format</br>

![Screenshot](/images/hd17.jpg)

<a id="link3"></a>
## 3. Verificando a Instalação

#verificando a versão instalada

hadoop version

![Screenshot](/images/hd17a.jpg)

#start hadoop

start-dfs.sh

![Screenshot](/images/hd18.jpg)

start-yarn.sh

![Screenshot](/images/hd19.jpg)

mr-jobhistory-daemon.sh start historyserver

![Screenshot](/images/hd20.jpg)

#verificando o status dos serviços

namenode

![Screenshot](/images/hd21.jpg)

datanode

![Screenshot](/images/hd22.jpg)

#interface web

Alem da linha de comando, podemos usar a interface web para verificação do ambiente

http://master:50070

![Screenshot](/images/hd23.jpg)

![Screenshot](/images/hd24.jpg)

![Screenshot](/images/hd25.jpg)

![Screenshot](/images/hd26.jpg)

![Screenshot](/images/hd27.jpg)

http://master:8088/

![Screenshot](/images/hd28.jpg)

![Screenshot](/images/hd29.jpg)

<a id="link4"></a>
## 4. Links

Apache</br>
https://hadoop.apache.org/

Comandos hdfs</br>
https://www.geeksforgeeks.org/hdfs-commands/

Calculadora de megabytes</br>
https://pt.calcuworld.com/calculadoras-informaticas/calculadora-de-megabytes/