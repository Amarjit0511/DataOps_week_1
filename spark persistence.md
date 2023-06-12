# Spark Persistence

It is the ability of Spark to cache/persist data that in the memory or disk for improved performance. It is normally done to avoid the recomputation of data that is used across multiple iterations. 

Also Saprk provides different persistent levels to control how the RDDs are stored in the memory.

***The different types of persistence levels include***
1. MEMORY_ONLY
2. MEMORY_AND_DISK
3. MEMORY_ONLY_SER
4. MEMORY_AND_DISK_SER
5. DISK_ONLY
6. OFF_HEAP

#### MEMORY_ONLY
This is the default persistence level in Spark. Here the RDDs ar stored in deserialised manner as Java Objects in the JVM Heap memory (a dynamic memory).

#### MEMORY_AND_DISK
When the data is larger than the available memory, Spark tries to store as much data as possible in ***memory*** and the remaining is put in the disk.

#### MEMORY_ONLY_SER
It is similar to MEMORY_ONLY, just the difference is that it requires less memory because here the data is stored in a serialised manner in JVM Heap Memory.

#### MEMORY_AND_DISK_SER
It is similar to MEMORY_AND_DISK, just the difference is that it stores the data in MEMORY AND DISK both in a serialised manner. 

#### DISK_ONLY
This persistence level is used when the data is ***too large*** to be stored in the memory and the 
