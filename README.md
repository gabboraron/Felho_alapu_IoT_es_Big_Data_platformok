# Felho_alapu_IoT_es_Big_Data_platformok
követelmény: 
- 7. hét végig egy téma bejelentő

## ea1 - Big Data and Hadoop basics
> **Big Data**
> - massive volume of both structured, semi-structured and unstructured different type of data that has the potential to be mined for valuable information
> - data is so large, complex, and rapidly growing therefore, it is overly difficult to process using traditional databases and software techniques
> - Traditional sequential data processing algorithms are not sufficient to analyse this large volume of data. This phenomenon demands new strategies, techniques and tools

> **clouds?**
> - Cloud infrastructures are continuously emerging 
> - user-friendly way and on-demand solutions for complex problems

> **characteristics of Big Data - *"The 10 V’s"***
> - volume: size of data
> - velocity: the speed of data generation
> - variety: different types of data
> - veracity: data accuracy
> - value: useful data
> - validity: data quality
> - variability: dynamic evolving in data  structures
> - venue: distriuted heterogenous data from multiple platforms
> - vocabulary: data models
> - vagueness: confusion over big data and tools used

### volume
- 2.5 trillion Gb/day
- 6 billlion people
- companies data

### veriety 
- 150 exabyte in healthvcare in 2011
- 4 billion+ hours watched on YouTube/month
- 400 million tweet/day
- 30 billion post/day on facebook

### velocity
- 1 tb trade information /trading session
- ~100 sensor/car
- 18.9 billion network connection in 2016

**positive spiral**: *more users* generating *more data* leading to *better algorithms* creating *better user experience* resulting *more users*...

### veracity
- poor data quality costs the US 3.1 trillion USD/year 
- 27% of people is unsure of how much their data was inaccurate

**Google Modular Computing Environment**
- low-cost servers with directly attached disk storages
- Google hardware infrastructure consisted of hundreds of thousands of servers following modular approach
- note that no operating system or database platform available at the time could come close to operating across such a huge number of servers
- Google developed a hierarchical software stack with three major layers:
  - **Google File System (GFS)**: a distributed cluster file system that allows all of the disk capacities within the Google data center to be aggregated and accessed as one massive, distributed, redundant file system.
  - **[MapReduce](https://www.youtube.com/watch?v=FYkSPn5ppEIy)**: a distributed processing framework for parallelizing algorithms across large numbers of potentially unreliable servers and being capable of dealing with massive datasets. 
  - **BigTable**: a nonrelational database system that uses the GFS for storage. 

![Google software architecture map reduce big table  file system server](https://fulmanski.pl/tutorials/wp-content/data/images/dataprocessing/nosql/google_stack.jpg)

> #### MapReduce
> *provides general-purpose parallelization of data-intensive processing*
> 
> - **mapping phase**: data is split into smaller chunks that can be processed easier by separate threads—potentially running on separate machines
> - **a reduce phase**: it combines the output into the final result
> 
> *ex: word-count program*
> - *the program counts the occurrences of pet types in the given input files*
> – *by breaking the data into equal chunks in the map phase*
> – *then the data is shuffled into groups of pet types*
> – *finally, the reduce phase sums the occurrences that is fed into the output*
>
> ![word count example](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2016/11/MapReduce-Way-MapReduce-Tutorial-Edureka.png)
> 
> #### Multi-stage MapReduce
> multiple MapReduce phases might be also chained each after another to achieve more complex results
> - multiple input files to be merged in a given way
> - some complex iterative processing to perform a statistical or machine learning analysis
> 
> **more complex multi-stage MapReduce pipeline:**
> - a file containing information about visits to various product webpages is joined with
> - a file containing product details — to obtain the product category — and then joined again to
> - a file containing customer details, so as to determine the customer’s country
> - this joined data is then aggregated to provide a report of product categories, customer geographies, and page visits
> 
> *Equivalent SQL query:*
> ```SQL
> SELECT prod_category, Cust_country, SUM(visits)
> FROM products
> JOIN product_page_visits
> USING (prod_id)
> JOIN customers
> USING (cust_id)
> GROUP BY prod_category, Cust_country
> ```

### [Hadoop](https://hadoop.apache.org/): Open-Source Google Stack
- **An economical scalable storage model**. As data volumes increase, so does the cost of storing that data online. Because Hadoop can run on commodity hardware that in turn utilizes commodity disks, the price point per terabyte is lower than that of almost any other technology
- **Massive scalable IO capability**. Because Hadoop uses a large number of commodity devices, the aggregate IO and network capacity is higher than that provided by dedicated storage arrays in which smaller numbers of larger disks are provided by even smaller numbers of processors
  - adding new servers to Hadoop adds storage, IO, CPU, and network capacity all at once, whereas adding disks to a storage array might simply exacerbate a network or CPU bottleneck within the array
- **Reliability** Data in Hadoop is stored redundantly in multiple servers using HDFS (Hadoop File System) and can be distributed across multiple computer racks. Failure of a server does not result in a loss of data; in fact, a Hadoop job will continue even if a server fails — the processing simply switches to another server
- **A scalable processing model**: MapReduce represents a widely applicable and scalable distributed processing model. While MapReduce is not the most efficient implementation for all algorithms, it is capable of brute-forcing acceptable performance for almost all.
- **Schema on read**: Data can be loaded into Hadoop without having to be converted to a highly structured normalized format. This makes it easy for Hadoop to quickly ingest data from various forms. The imposition of structure can be delayed until the data is accessed; this is sometimes referred to as schema on read (in opposite to the schema on write mode of relational data warehouses)

> ***Survey questions***
> - Why is not the size of data the only factor that matters when we are speaking about Big Data? 
- What was the role of Google in the evolution of Big Data platforms?
- What are the 5 steps of MapReduce paradigm?
- Why Hadoop is a so scalable platform?

## gyak1
emodi.mark@uni-obuda.hu

**Követelmények:**
- zh: MS Teams szóbeli / írásbeli
- féléves feladat +/- 1
  - 11. héten zh pótlás **vagy** féléves feladat pótlás
- vizsga: megajánlott jegy a félévi teljesítmény alapján (4/5) vagy vizsga

## ea2: Database scaling and noSQL basics
### HBASE
- using Hadoop HDFS as its file system, HBase is able to create tables of truly massive size—way beyond the possible size for a system like MySQL, or even for Oracle
- In addition, the fault tolerance of HDFS provides automatic redundancy for HBase tables
- HBase tables vary significantly from relational tables:
  - in each cell — a column value for a particular row— there will usually be multiple versions of a data value. Each version of data within a cell is identified by a timestamp. This provides HBase tables with a sort of temporal “third dimension.”
  - HBase columns are more similar to the key values
#### SQL over Hadoop: HIVE
- Hive provides a catalog for the Hadoop system, as well as a SQL processing layer
- The Hive metadata service contains information about the structure of registered files in the HDFS file system
- Hive client or server (depending on the Hive configuration) accepts SQL-like commands: HQL

![Hive architecture hive client server map reduce yarn hdfs hive meta store](https://www.tutorialandexample.com/wp-content/uploads/2020/02/Apache-Hive-Architecture.png)

- Performance:
  - The predominant Hadoop vendor Cloudera has created an alternative proprietary SQL on the Hadoop framework called Impala 
  - others (including another major Hadoop vendor Hortonworks) have attempted to improve Hive’s performance through incremental changes and better integration with post- MapReduce frameworks such as YARN and Tez

#### MySQL – scaling up
- Memcached is an open-source utility that provides a distributed object cache
- Object-oriented languages could cache an object-oriented representation of database information across many servers
- reading from these servers rather than the database, the load on the database could be reduced
- Web developers took advantage of MySQL replication:
  - read: from any replica
  - write to master
##### Sharding
*a logical database to be partitioned across multiple physical servers*
- the largest tables are partitioned across multiple database servers
- Each partition is referred to as a `shard` 
  - This partitioning is based on a Key Value, such as a userID
  - When operating on a particular record, the application must determine which shard will contain the data and then send the SQL to the appropriate server
- **Application complexity**. It is up to the application code to route SQL requests to the correct shard
  - statically sharded database, this would be hard enough
  - massive websites are adding shards as they grow, which means that a dynamic routing layer must be implemented
- **Crippled SQL** it is not possible to issue a SQL statement that operates across shards
- **Loss of transactional integrity** ACID transactions against multiple shards are not possible — or at least not practical: *Two Phase Commit*
- **Operational complexity** Adding new shards requires a complex rebalancing of data. Changing the database schema also requires a rolling operation across all the shards, resulting in transitory inconsistencies in the schema

##### CAP Theorem
in a distributed database system, you can have at most only two of: 
- Consistency: every user of the database has an identical view of the data at any given instant.
- Availability: in the event of a node failure, the database remains operational
- Partition tolerance: the database can maintain operations in the event of the network’s failing between two segments of the distributed system

*if you want your system to be undisturbed by network partitions, you must sacrifice strict consistency between partitions.*

for social networks and certain e-commerce operations, this worldwide synchronous consistency is unnecessary

***Tunable Consistency*** Amazon Dynamo allows the application to choose the level of consistency applied to specific operations.:
- **N** is the number of copies of each data item that the database will maintain.
– **W** is the number of copies of the data item that must be writtenbefore the write can complete.
– **R** is the number of copies that the application will access when reading the data item.

*When W = N, Dynamo will always write every copy before returning control to the application. This is ACID*

- N > W > 1 i.e. more than one write must complete, but not all nodes need to be updated immediately
- W + R > N this ensures that the latest value will always be included in a read operation, even if it is mixed in with “older” values. 

> ***Survey questions***
> - What is the main mechanism behind HIVE?
> - Explain at least three of the drawbacks of sharding!
> - How would you set the NWR parameters in order to ensure that the value(s) of last write operation can be accessed during the upcoming read operations?

## gyak2
vm: https://ubuntu.com/download/server

- client: `docker build` `docker pull` `docker run`
- docker host: futtatja a daemon által létrehozott rendszerű konténert
- registry: daemonok beállítják az imaget

![docker](https://containerjournal.com/wp-content/uploads/2021/12/Docker-Architecture.png)

docker hub imagek: https://hub.docker.com/search?image_filter=official&type=image

![docker vs containers](https://images.contentstack.io/v3/assets/blt300387d93dabf50e/bltb6200bc085503718/5e1f209a63d1b6503160c6d5/containers-vs-virtual-machines.jpg)

***ha rootként privilegizált módban futtatjuk a usert akkor a kinti rendszerhez is hozzáfér => read only fájlhozzáférés megoldás lehet***

![docker fájlrendszere](https://docs.docker.com/storage/images/types-of-mounts-volume.png)


10.0.2.15/24
user 
Almafa123

10.0.2.15/24
10.0.2.0/24
10.0.2.2

# GY3
**Beadandóról** 
- dokumentáció 
- prezentáció

## Docker architecture 
Minden egyes változatás után új réteg a képfájlon 

Kötetek hosszú távú tárolásra jók 

Docker volume 

Portman Docker helyett mint freeware megoldás. 

## Elosztott működés 
> több erőforrás csoportba szervezve is képes kiadni a nekünk szükséges erőforrást 
>
> erre jó a Kubernetees vagy Docker swarm - > clusterek hozhatóak létre 
>
>. Swarmban a titkosítás könnyebb 

Nginx szolgáltatás  -> minden állomáson kiosztunk egy replikát; belső kommunikáció `tls`en zajlik. 
Managerek egymás közt leadert választanak, a leaderek leaderét a leaderek választják. 

Node balancerrel is rendelkeznek, node vagy cluster portot is megadhatunk. Let's encrypt szolgáltatása is használható. 

## NoSQL adatbázis 
- oszlop - idősoros adat
- gráf alapú - kapcsolatok 
- dokumentum tároló - mongo db

CAP tétel 
- rendelkezésre állás 
- konzisztencia
- partíció tolerálás

# Adattárolás
## NoSQL adatbázis
- skálázhatóság
- sok elérhető típusú adatbázis
- változatos adatstruktúrák
- objektum alapú adattárolás

![CAP tétel](https://blog.fps.hu/content/images/2017/04/cap-tetel.png)

```Shell
docker run --name some-cassandra --network some-network -d cassandra:3.11
docker exec -it some-cassandra bash
cqlsh -u cassandra
```

# monitorozás
## netdata
https://learn.netdata.cloud/docs
```
wget -O /tmp/netdata-kickstart.sh https://my-netdata.io/kickstart.sh && sh /tmp/netdata-kickstart.sh
```
alert manager:
https://medium.com/devops-dudes/prometheus-alerting-with-alertmanager-e1bbba8e6a8e

![](https://miro.medium.com/max/1120/1*wWz5vwHcBeTATvBFKGqRkA.png)

# felhő tárolás
- prometheus
- prometheus nem tárolásra lett kitalálva
- hosszútávú tárolási megoldások:
  - https://thanos.io/
  - https://github.com/VictoriaMetrics/VictoriaMetrics

`docker compose up` letölti az aktuális prometheus képfájlt

nincs processor specifikus információ szolgáltatás

https://grafana.com/

## opensource szoftware fejlesztés

style guide -> more readable,  docs can be generated from code, easier to maintain, easier to expand

version numbering: MAJOR.MINOR.PATCH
- MAJOR: inkompatibilis változások
- MINOR: funkcionalitásában változik, de visszafele kompatibilis
- PATCH: visszafelé kompatibilis verzió, bugok javítás

egyéb alverziósámok hozzzáadhatóak a fejlesztés követése érdekében

az első publikus elérhető verzió legyen 0.1.0

[angularjs commit guideline](https://gist.github.com/stephenparish/9941e89d80e2bc58a153)

### travis ci
- menetközben buildelni
- unit testeket végez menet küzben

### jenkins 
- magát a keretrendszert felépíteni
- self hosted
- integrációs vagy rendszerfelépíési testek
- release naplót tud készíteni
- hírt tud automatizálni

### gitlab bot
- lehet self hosted
- konténert tud létrehozni automatikusan

read the docs 
