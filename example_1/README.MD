# Mapreduce

1. From Azure portal copy cluster ssh [address].
    Grupy zasobów  -> "name of the group" (ex bigdata) -> enter to the "HDInsight cluster" -> Properties -> Copy Secure Shell (SSH).

2. From local shell copy example_1 to cluster:
```console
	$ ssh sshuser@[ssh_address] "mkdir -p /home/sshuser/example_1"
	$ scp -r  [git repo path]* sshuser@[ssh_address]:/home/sshuser/example_1
```
**where:**<br/>
* sshuser - is default name created by the Azure<br/>
* [ssh_address] - address from the first step.
* [git repo path] - local git repository -> C:/Users/vdi-student/hadoop/example_1/

3. Login to the cluster:
```console
    $ ssh sshuser@[ssh_address]
```
**where:**<br/>
* ssh_address - address from the first step.

4. From cluster shell copy data.txt to hdfs:
```console
    $ hdfs dfs -copyFromLocal /home/sshuser/example_1/data.txt /user/data.txt
```
**where:**<br/>
* sshuser - is default name created by the Azure<br/>

5. Run script:
```console
    $ hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files ./example_1/MRatingCount.py,./example_1/RRatingCount.py -mapper MRatingCount.py -reducer RRatingCount.py -input /user/data.txt -output /user/count
```

6. When the work is done check result:
```console
    $ hdfs dfs -text /user/count/part-00000
```
