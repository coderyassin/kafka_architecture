flowchart TB

    subgraph Cluster[Kafka Cluster]
        B1[Broker 1]
        B2[Broker 2]
        B3[Broker 3]
    end

    subgraph Topics
        T1[Topic A]
        T2[Topic B]
    end

    subgraph Partitions
        P0[Partition 0]
        P1[Partition 1]
        P2[Partition 2]
    end

    subgraph Replication[Leader & Followers]
        L0[Leader P0]
        F01[Follower P0]
        F02[Follower P0]
    end

    subgraph Metadata[ZooKeeper / KRaft]
        ZK[(Cluster Metadata)]
    end

    Producers --> T1
    Consumers --> T1

    T1 --> P0
    T1 --> P1
    T1 --> P2

    P0 --> B1
    P1 --> B2
    P2 --> B3

    L0 --> B1
    F01 --> B2
    F02 --> B3

    B1 --> ZK
    B2 --> ZK
    B3 --> ZK
