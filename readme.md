# Scripts
### Run 8u181-jdk with 512M 
docker run -it -m 512M openjdk:8u181-jdk

### MaxHeap space
java -XX:+PrintFlagsFinal -version | grep MaxHeap

### Run memory eater
javac MemoryEater.java
java MemoryEater

### limit the jdk to 1 cpu
docker run -it --cpus 1 openjdk:8u181-jdk

### Run the CPU count
java AvailableProcessors

### check the threads
java -XX:+PrintFlagsFinal -version | grep ParallelGCThreads

## Solution
### Run with 8u212-jdk and check the CPU
docker run -it --cpus 1 -m 1G openjdk:8u212-jdk
java -XX:+PrintFlagsFinal -version | grep MaxHeap

java AvailableProcessors

## For Oracle serverjre8 from the store
Starting with 8u131 JVM will apply the Docker --cpuset-cpus limit as number of cpu's the JVM sees in the container

-XX:ParallelGCThreads and -XX:CICompilerCount is given priority over --cpuset-cpus limit 

## Experimental support
Configure the max heapsize to match docker memeory limit use the following cmd line options
    -XX:+UnlockExperimentalVMOptions
    -XX:+UseCGroupMemoryLimitForHeap
 jvm uses the linux cgroup configuration which is what docker container uses for memory limit
 
### This can be turned 0ff with 
-XX:-UseContainerSupport
