# Hadoop Ecosystem

Hadoop é um framework de código aberto, feito em Java.

Permite o processamento e armazenamento distribuído de grandes datasets. (falaremos do formato desses datasets depois)

Várias máquinas interligadas, formando um cluster, são responsáveis pelo armazenamento e processamento.

Graças ao processamento em paralelo é possível consumir grandes datasets e obter o resultado em um tempo muito menor do que um grande servidor levaria.

O hardware usado é chamado de commodity hardware. 
(importante, é um hardware barato (em relação a um high end) e fácil de se comprar) mas isso não significa de graça.

Podemos ter desde um cluster de raspberries até máquinas com 4 discos, 64GB memória e vários processadores

2 quad-/hex-/octo-core CPUs, running at least 2-2.5GHz
64-512GB of RAM
12 ou > (hard disks) 1 a 4TB hard disks in a JBOD (Just a Bunch Of Disks) configuration (não é Raid)
Gigabit Ethernet or 10 Gigabit Ethernet (the more storage density, the higher the network throughput needed)

- Arquitetura

As máquinas são divididas em Master e Slave

O Master é chamado de namenode
Os Slaves são chamado de datanote (onde os dados estão armazenados)

Os datasets são quebrados em blocos de 128 MB e espalhados pelos slaves em um fator de 3 (configurável)
isto é : cada bloco deve ter 3 cópias.

ex: 
1 dataset de 514 MB
4 Slaves

Slave 1
1 dataset de 514 MB teremos 4 blocos de 128MB  1 bloco de 2MB

espalhado em 4 Slaves de forma que se perder um ou dois Slaves, tenha cópias dos bloco em outros Slaves

- Componentes do Hadoop

HDFS
Hadoop distributed file system (HDFS)
Sistema de arquivos onde os datasets são armazenados (datanodes)

MapReduce
Camada de processamento de dados do Hadoop
Ele divide o Job (processo) em sub-jobs

Possui duas fazes:
1) Map (lógica mais complexa a ser executada)
2) Reduce (coleta os resultados dos sub-job e produz o resultado final)

YARN
É o framework de processamento do Hadoop
Gerenciamento de recursos
Permite vários engines de processamento como realk time streaming
Data science
Processamento batch 

Links

https://searchstorage.techtarget.com/definition/JBOD 
https://pt.calcuworld.com/calculadoras-informaticas/calculadora-de-megabytes/
http://www.edureka.co/blog/apache-hadoop-hdfs-architecture/?utm_source=quora&utm_medium=crosspost&utm_campaign=social-media-edureka-ab
