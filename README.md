EFK-Docker
==============

## Prerequisite

Install `Rancher Desktop`, which is an alternative to `Docker Desktop`.

1. Go to https://rancherdesktop.io/
2. Download the installer image for your OS.
3. Open Rancher and proceed installation.
4. Choose `dockerd(moby)` when you are asked container engine.

![choose dockerd(moby)](https://cdn-ak.f.st-hatena.com/images/fotolife/k/knqyf263/20220201/20220201220235.png)

Once everything is set, Rancher starts internal kubernetes. Just wait for a while until the state becomes running.
Even if you are not sure of kubernetes, no worry. Rancher takes care of necessary CLI tools as well.  It creates `~/.rd` and adds it to your PATH automatically under the hood.
What you need here is `docker` and `docker-compose`.

Let's start docker, and see what is happening on http://localhost:5601.

```console
$ docker-compose up 

Creating network "efk-docker_local" with driver "bridge"
Creating efk-docker_fluent-bit_1 ... done
Creating efk-docker_elasticsearch_1 ... done
Creating efk-docker_kibana_1        ... done
Attaching to efk-docker_fluent-bit_1, efk-docker_elasticsearch_1, efk-docker_kibana_1
fluent-bit_1     | Fluent Bit v1.8.11
fluent-bit_1     | * Copyright (C) 2019-2021 The Fluent Bit Authors
fluent-bit_1     | * Copyright (C) 2015-2018 Treasure Data
fluent-bit_1     | * Fluent Bit is a CNCF sub-project under the umbrella of Fluentd
fluent-bit_1     | * https://fluentbit.io
fluent-bit_1     | 
fluent-bit_1     | [2022/01/12 02:03:53] [ info] [engine] started (pid=1)
fluent-bit_1     | [2022/01/12 02:03:53] [ info] [storage] version=1.1.5, initializing...
fluent-bit_1     | [2022/01/12 02:03:53] [ info] [storage] in-memory
fluent-bit_1     | [2022/01/12 02:03:53] [ info] [storage] normal synchronization mode, checksum disabled, max_chunks_up=128
fluent-bit_1     | [2022/01/12 02:03:53] [ info] [cmetrics] version=0.2.2
fluent-bit_1     | [2022/01/12 02:03:53] [ info] [input:forward:forward.0] listening on 0.0.0.0:24224
fluent-bit_1     | [2022/01/12 02:03:53] [ info] [http_server] listen iface=0.0.0.0 tcp_port=2020
fluent-bit_1     | [2022/01/12 02:03:53] [ info] [sp] stream processor started
fluent-bit_1     | [2022/01/12 02:03:57] [ warn] [engine] failed to flush chunk '1-1641953034.259683819.flb', retry in 7 seconds: task_id=0, input=forward.0 > output=es.0 (out_id=0)
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:02Z","tags":["info","plugins-service"],"pid":8,"message":"Plugin \"visTypeXy\" is disabled."}
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:02Z","tags":["info","plugins-system"],"pid":8,"message":"Setting up [40] plugins: [usageCollection,telemetryCollectionManager,telemetry,kibanaUsageCollection,mapsLegacy,securityOss,newsfeed,kibanaLegacy,share,legacyExport,embeddable,expressions,data,home,console,apmOss,management,indexPatternManagement,advancedSettings,savedObjects,dashboard,visualizations,regionMap,visTypeMarkdown,visTypeTimelion,timelion,visTypeVega,tileMap,visTypeTable,inputControlVis,visualize,esUiShared,charts,visTypeMetric,visTypeVislib,visTypeTimeseries,visTypeTagcloud,discover,savedObjectsManagement,bfetch]"}
fluent-bit_1     | [2022/01/12 02:04:02] [ warn] [engine] failed to flush chunk '1-1641953042.466928965.flb', retry in 10 seconds: task_id=2, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:02] [ warn] [engine] failed to flush chunk '1-1641953037.924003187.flb', retry in 11 seconds: task_id=1, input=forward.0 > output=es.0 (out_id=0)
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:03Z","tags":["info","savedobjects-service"],"pid":8,"message":"Waiting until all Elasticsearch nodes are compatible with Kibana before starting saved objects migrations..."}
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:03Z","tags":["error","elasticsearch","data"],"pid":8,"message":"[ConnectionError]: connect ECONNREFUSED 192.168.160.3:9200"}
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:03Z","tags":["error","savedobjects-service"],"pid":8,"message":"Unable to retrieve version information from Elasticsearch nodes."}
fluent-bit_1     | [2022/01/12 02:04:04] [ warn] [engine] failed to flush chunk '1-1641953034.259683819.flb', retry in 17 seconds: task_id=0, input=forward.0 > output=es.0 (out_id=0)
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:05Z","tags":["error","elasticsearch","data"],"pid":8,"message":"[ConnectionError]: connect ECONNREFUSED 192.168.160.3:9200"}
fluent-bit_1     | [2022/01/12 02:04:07] [ warn] [engine] failed to flush chunk '1-1641953042.836743672.flb', retry in 11 seconds: task_id=3, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:07] [ warn] [engine] failed to flush chunk '1-1641953043.212595071.flb', retry in 6 seconds: task_id=4, input=forward.0 > output=es.0 (out_id=0)
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:08Z","tags":["error","elasticsearch","data"],"pid":8,"message":"[ConnectionError]: connect ECONNREFUSED 192.168.160.3:9200"}
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:10Z","tags":["error","elasticsearch","data"],"pid":8,"message":"[ConnectionError]: connect ECONNREFUSED 192.168.160.3:9200"}
fluent-bit_1     | [2022/01/12 02:04:12] [ warn] [engine] failed to flush chunk '1-1641953047.837115035.flb', retry in 6 seconds: task_id=5, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:12] [ warn] [engine] failed to flush chunk '1-1641953048.230386845.flb', retry in 8 seconds: task_id=6, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:12] [ warn] [engine] failed to flush chunk '1-1641953042.466928965.flb', retry in 13 seconds: task_id=2, input=forward.0 > output=es.0 (out_id=0)
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:13Z","tags":["error","elasticsearch","data"],"pid":8,"message":"[ConnectionError]: connect ECONNREFUSED 192.168.160.3:9200"}
fluent-bit_1     | [2022/01/12 02:04:13] [ warn] [engine] failed to flush chunk '1-1641953037.924003187.flb', retry in 13 seconds: task_id=1, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:13] [ warn] [engine] failed to flush chunk '1-1641953043.212595071.flb', retry in 7 seconds: task_id=4, input=forward.0 > output=es.0 (out_id=0)
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:15,051Z", "level": "INFO", "component": "o.e.n.Node", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "version[7.10.2], pid[7], build[oss/docker/747e1cc71def077253878a59143c1f785afa92b9/2021-01-13T00:42:12.435326Z], OS[Linux/5.10.0-9-amd64/amd64], JVM[AdoptOpenJDK/OpenJDK 64-Bit Server VM/15.0.1/15.0.1+9]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:15,054Z", "level": "INFO", "component": "o.e.n.Node", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "JVM home [/usr/share/elasticsearch/jdk], using bundled JDK [true]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:15,055Z", "level": "INFO", "component": "o.e.n.Node", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "JVM arguments [-Xshare:auto, -Des.networkaddress.cache.ttl=60, -Des.networkaddress.cache.negative.ttl=10, -XX:+AlwaysPreTouch, -Xss1m, -Djava.awt.headless=true, -Dfile.encoding=UTF-8, -Djna.nosys=true, -XX:-OmitStackTraceInFastThrow, -XX:+ShowCodeDetailsInExceptionMessages, -Dio.netty.noUnsafe=true, -Dio.netty.noKeySetOptimization=true, -Dio.netty.recycler.maxCapacityPerThread=0, -Dio.netty.allocator.numDirectArenas=0, -Dlog4j.shutdownHookEnabled=false, -Dlog4j2.disable.jmx=true, -Djava.locale.providers=SPI,COMPAT, -Xms1g, -Xmx1g, -XX:+UseG1GC, -XX:G1ReservePercent=25, -XX:InitiatingHeapOccupancyPercent=30, -Djava.io.tmpdir=/tmp/elasticsearch-9588261412037892243, -XX:+HeapDumpOnOutOfMemoryError, -XX:HeapDumpPath=data, -XX:ErrorFile=logs/hs_err_pid%p.log, -Xlog:gc*,gc+age=trace,safepoint:file=logs/gc.log:utctime,pid,tags:filecount=32,filesize=64m, -Des.cgroups.hierarchy.override=/, -XX:MaxDirectMemorySize=536870912, -Des.path.home=/usr/share/elasticsearch, -Des.path.conf=/usr/share/elasticsearch/config, -Des.distribution.flavor=oss, -Des.distribution.type=docker, -Des.bundled_jdk=true]" }
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:15Z","tags":["error","elasticsearch","data"],"pid":8,"message":"[ConnectionError]: connect ECONNREFUSED 192.168.160.3:9200"}
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,588Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [aggs-matrix-stats]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,589Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [analysis-common]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,589Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [geo]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,589Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [ingest-common]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,589Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [ingest-geoip]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,589Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [ingest-user-agent]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,590Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [kibana]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,590Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [lang-expression]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,591Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [lang-mustache]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,591Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [lang-painless]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,591Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [mapper-extras]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,592Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [parent-join]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,592Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [percolator]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,592Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [rank-eval]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,592Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [reindex]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,592Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [repository-url]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,593Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "loaded module [transport-netty4]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,593Z", "level": "INFO", "component": "o.e.p.PluginsService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "no plugins loaded" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,644Z", "level": "INFO", "component": "o.e.e.NodeEnvironment", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "using [1] data paths, mounts [[/usr/share/elasticsearch/data (/dev/sda1)]], net usable_space [47.2gb], net total_space [97.9gb], types [ext4]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,644Z", "level": "INFO", "component": "o.e.e.NodeEnvironment", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "heap size [1gb], compressed ordinary object pointers [true]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:16,730Z", "level": "INFO", "component": "o.e.n.Node", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "node name [0168d6d9c3a1], node ID [ZPX7GhmURk2HEgwne7ojYw], cluster name [docker-cluster], roles [master, remote_cluster_client, data, ingest]" }
fluent-bit_1     | [2022/01/12 02:04:17] [ warn] [engine] failed to flush chunk '1-1641953052.881605039.flb', retry in 8 seconds: task_id=7, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:17] [ warn] [engine] failed to flush chunk '1-1641953053.232821610.flb', retry in 9 seconds: task_id=8, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:17] [ warn] [engine] failed to flush chunk '1-1641953055.54999890.flb', retry in 10 seconds: task_id=9, input=forward.0 > output=es.0 (out_id=0)
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:18Z","tags":["error","elasticsearch","data"],"pid":8,"message":"[ConnectionError]: connect ECONNREFUSED 192.168.160.3:9200"}
fluent-bit_1     | [2022/01/12 02:04:18] [ warn] [engine] failed to flush chunk '1-1641953042.836743672.flb', retry in 6 seconds: task_id=3, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:18] [ warn] [engine] failed to flush chunk '1-1641953047.837115035.flb', retry in 10 seconds: task_id=5, input=forward.0 > output=es.0 (out_id=0)
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:20Z","tags":["error","elasticsearch","data"],"pid":8,"message":"[ConnectionError]: connect ECONNREFUSED 192.168.160.3:9200"}
fluent-bit_1     | [2022/01/12 02:04:20] [ warn] [engine] failed to flush chunk '1-1641953048.230386845.flb', retry in 17 seconds: task_id=6, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:20] [ warn] [engine] failed to flush chunk '1-1641953043.212595071.flb', retry in 24 seconds: task_id=4, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:21] [ warn] [engine] failed to flush chunk '1-1641953034.259683819.flb', retry in 14 seconds: task_id=0, input=forward.0 > output=es.0 (out_id=0)
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:22,370Z", "level": "INFO", "component": "o.e.t.NettyAllocator", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "creating NettyAllocator with the following configs: [name=unpooled, suggested_max_allocation_size=256kb, factors={es.unsafe.use_unpooled_allocator=null, g1gc_enabled=true, g1gc_region_size=1mb, heap_size=1gb}]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:22,469Z", "level": "INFO", "component": "o.e.d.DiscoveryModule", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "using discovery type [single-node] and seed hosts providers [settings]" }
fluent-bit_1     | [2022/01/12 02:04:22] [ warn] [engine] failed to flush chunk '1-1641953057.834343001.flb', retry in 11 seconds: task_id=10, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:22] [ warn] [engine] failed to flush chunk '1-1641953058.239782322.flb', retry in 6 seconds: task_id=11, input=forward.0 > output=es.0 (out_id=0)
fluent-bit_1     | [2022/01/12 02:04:22] [ warn] [engine] failed to flush chunk '1-1641953062.370803636.flb', retry in 11 seconds: task_id=12, input=forward.0 > output=es.0 (out_id=0)
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:22,934Z", "level": "WARN", "component": "o.e.g.DanglingIndicesState", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "gateway.auto_import_dangling_indices is disabled, dangling indices will not be automatically detected or imported and must be managed manually" }
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:23Z","tags":["error","elasticsearch","data"],"pid":8,"message":"[ConnectionError]: connect ECONNREFUSED 192.168.160.3:9200"}
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:23,311Z", "level": "INFO", "component": "o.e.n.Node", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "initialized" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:23,312Z", "level": "INFO", "component": "o.e.n.Node", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "starting ..." }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:23,591Z", "level": "INFO", "component": "o.e.t.TransportService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "publish_address {192.168.160.3:9300}, bound_addresses {0.0.0.0:9300}" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:24,038Z", "level": "WARN", "component": "o.e.b.BootstrapChecks", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:24,047Z", "level": "INFO", "component": "o.e.c.c.Coordinator", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "setting initial configuration to VotingConfiguration{ZPX7GhmURk2HEgwne7ojYw}" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:24,268Z", "level": "INFO", "component": "o.e.c.s.MasterService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "elected-as-master ([1] nodes joined)[{0168d6d9c3a1}{ZPX7GhmURk2HEgwne7ojYw}{Z9Cg3LlXQbqzSeGeB7nq-A}{192.168.160.3}{192.168.160.3:9300}{dimr} elect leader, _BECOME_MASTER_TASK_, _FINISH_ELECTION_], term: 1, version: 1, delta: master node changed {previous [], current [{0168d6d9c3a1}{ZPX7GhmURk2HEgwne7ojYw}{Z9Cg3LlXQbqzSeGeB7nq-A}{192.168.160.3}{192.168.160.3:9300}{dimr}]}" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:24,323Z", "level": "INFO", "component": "o.e.c.c.CoordinationState", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "cluster UUID set to [cd8ckYKZRgSppblpeUIgQg]" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:24,347Z", "level": "INFO", "component": "o.e.c.s.ClusterApplierService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "master node changed {previous [], current [{0168d6d9c3a1}{ZPX7GhmURk2HEgwne7ojYw}{Z9Cg3LlXQbqzSeGeB7nq-A}{192.168.160.3}{192.168.160.3:9300}{dimr}]}, term: 1, version: 1, reason: Publication{term=1, version=1}" }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:24,398Z", "level": "INFO", "component": "o.e.h.AbstractHttpServerTransport", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "publish_address {192.168.160.3:9200}, bound_addresses {0.0.0.0:9200}", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:24,398Z", "level": "INFO", "component": "o.e.n.Node", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "started", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:24,413Z", "level": "INFO", "component": "o.e.g.GatewayService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "recovered [0] indices into cluster_state", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
elasticsearch_1  | {"type": "deprecation", "timestamp": "2022-01-12T02:04:25,121Z", "level": "DEPRECATION", "component": "o.e.d.a.b.BulkRequestParser", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "[types removal] Specifying types in bulk requests is deprecated.", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:25,330Z", "level": "INFO", "component": "o.e.c.m.MetadataCreateIndexService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "[fluent-bit-2022.01.12] creating index, cause [auto(bulk api)], templates [], shards [1]/[1]", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:25Z","tags":["info","savedobjects-service"],"pid":8,"message":"Starting saved objects migrations"}
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:25,946Z", "level": "INFO", "component": "o.e.c.m.MetadataMappingService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "[fluent-bit-2022.01.12/CY2CvAGMTUia8hKozcpyNw] create_mapping [_doc]", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:25Z","tags":["info","savedobjects-service"],"pid":8,"message":"Creating index .kibana_1."}
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:26,013Z", "level": "INFO", "component": "o.e.c.m.MetadataCreateIndexService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "[.kibana_1] creating index, cause [api], templates [], shards [1]/[1]", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:26,015Z", "level": "INFO", "component": "o.e.c.r.a.AllocationService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "updating number_of_replicas to [0] for indices [.kibana_1]", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:26,105Z", "level": "INFO", "component": "o.e.c.m.MetadataMappingService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "[fluent-bit-2022.01.12/CY2CvAGMTUia8hKozcpyNw] update_mapping [_doc]", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:26Z","tags":["info","savedobjects-service"],"pid":8,"message":"Pointing alias .kibana to .kibana_1."}
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:26Z","tags":["info","savedobjects-service"],"pid":8,"message":"Finished in 310ms."}
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:26Z","tags":["info","plugins-system"],"pid":8,"message":"Starting [40] plugins: [usageCollection,telemetryCollectionManager,telemetry,kibanaUsageCollection,mapsLegacy,securityOss,newsfeed,kibanaLegacy,share,legacyExport,embeddable,expressions,data,home,console,apmOss,management,indexPatternManagement,advancedSettings,savedObjects,dashboard,visualizations,regionMap,visTypeMarkdown,visTypeTimelion,timelion,visTypeVega,tileMap,visTypeTable,inputControlVis,visualize,esUiShared,charts,visTypeMetric,visTypeVislib,visTypeTimeseries,visTypeTagcloud,discover,savedObjectsManagement,bfetch]"}
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:26Z","tags":["listening","info"],"pid":8,"message":"Server running at http://0:5601"}
kibana_1         | {"type":"log","@timestamp":"2022-01-12T02:04:27Z","tags":["info","http","server","Kibana"],"pid":8,"message":"http server running at http://0:5601"}
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:27,107Z", "level": "INFO", "component": "o.e.c.m.MetadataMappingService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "[.kibana_1/-fkG8S1rT8iPArijB-uPrg] update_mapping [_doc]", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:27,859Z", "level": "INFO", "component": "o.e.c.m.MetadataMappingService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "[fluent-bit-2022.01.12/CY2CvAGMTUia8hKozcpyNw] update_mapping [_doc]", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
elasticsearch_1  | {"type": "server", "timestamp": "2022-01-12T02:04:27,923Z", "level": "INFO", "component": "o.e.c.m.MetadataMappingService", "cluster.name": "docker-cluster", "node.name": "0168d6d9c3a1", "message": "[fluent-bit-2022.01.12/CY2CvAGMTUia8hKozcpyNw] update_mapping [_doc]", "cluster.uuid": "cd8ckYKZRgSppblpeUIgQg", "node.id": "ZPX7GhmURk2HEgwne7ojYw"  }
^CGracefully stopping... (press Ctrl+C again to force)
Stopping efk-docker_kibana_1        ... done
Stopping efk-docker_elasticsearch_1 ... done
Stopping efk-docker_fluent-bit_1    ... done
```
