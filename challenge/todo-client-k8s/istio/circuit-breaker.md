
```
[root@instance-1 istio-1.0.5]# kubectl exec -it $FORTIO_POD  -c fortio /usr/local/bin/fortio -- load -c 2 -qps 0 -n 20 -loglevel Warning http://todo-repo:8081/swagger-ui.html
10:47:40 I logger.go:97> Log level is now 3 Warning (was 2 Info)
Fortio 1.0.1 running at 0 queries per second, 2->2 procs, for 20 calls: http://todo-repo:8081/swagger-ui.html
Starting at max qps with 2 thread(s) [gomax 2] for exactly 20 calls (10 per thread + 0)
Ended after 888.639122ms : 20 calls. qps=22.506
Aggregated Function Time : count 20 avg 0.087049305 +/- 0.04978 min 0.038759684 max 0.22664897 sum 1.7409861
# range, mid point, percentile, count
>= 0.0387597 <= 0.04 , 0.0393798 , 5.00, 1
> 0.04 <= 0.045 , 0.0425 , 10.00, 1
> 0.045 <= 0.05 , 0.0475 , 25.00, 3
> 0.05 <= 0.06 , 0.055 , 45.00, 4
> 0.06 <= 0.07 , 0.065 , 55.00, 2
> 0.07 <= 0.08 , 0.075 , 65.00, 2
> 0.09 <= 0.1 , 0.095 , 70.00, 1
> 0.1 <= 0.12 , 0.11 , 75.00, 1
> 0.12 <= 0.14 , 0.13 , 85.00, 2
> 0.14 <= 0.16 , 0.15 , 90.00, 1
> 0.16 <= 0.18 , 0.17 , 95.00, 1
> 0.2 <= 0.226649 , 0.213324 , 100.00, 1
# target 50% 0.065
# target 75% 0.12
# target 90% 0.16
# target 99% 0.221319
# target 99.9% 0.226116
Sockets used: 2 (for perfect keepalive, would be 2)
Code 200 : 20 (100.0 %)
Response Header Sizes : count 20 avg 221.3 +/- 0.4583 min 221 max 222 sum 4426
Response Body/Total Sizes : count 20 avg 3539.3 +/- 0.4583 min 3539 max 3540 sum 70786
All done 20 calls (plus 0 warmup) 87.049 ms avg, 22.5 qps
[root@instance-1 istio-1.0.5]# kubectl exec -it $FORTIO_POD  -c fortio /usr/local/bin/fortio -- load -c 2 -qps 0 -n 20 -loglevel Warning http://todo-repo:8081/swagger-ui.html
10:49:32 I logger.go:97> Log level is now 3 Warning (was 2 Info)
Fortio 1.0.1 running at 0 queries per second, 2->2 procs, for 20 calls: http://todo-repo:8081/swagger-ui.html
Starting at max qps with 2 thread(s) [gomax 2] for exactly 20 calls (10 per thread + 0)
10:49:32 W http_client.go:604> Parsed non ok code 503 (HTTP/1.1 503)
Ended after 349.93745ms : 20 calls. qps=57.153
Aggregated Function Time : count 20 avg 0.03302465 +/- 0.03035 min 0.001208862 max 0.122511566 sum 0.660492996
# range, mid point, percentile, count
>= 0.00120886 <= 0.002 , 0.00160443 , 5.00, 1
> 0.014 <= 0.016 , 0.015 , 15.00, 2
> 0.016 <= 0.018 , 0.017 , 25.00, 2
> 0.018 <= 0.02 , 0.019 , 40.00, 3
> 0.02 <= 0.025 , 0.0225 , 60.00, 4
> 0.025 <= 0.03 , 0.0275 , 80.00, 4
> 0.035 <= 0.04 , 0.0375 , 85.00, 1
> 0.05 <= 0.06 , 0.055 , 90.00, 1
> 0.1 <= 0.12 , 0.11 , 95.00, 1
> 0.12 <= 0.122512 , 0.121256 , 100.00, 1
# target 50% 0.0225
# target 75% 0.02875
# target 90% 0.06
# target 99% 0.122009
# target 99.9% 0.122461
Sockets used: 3 (for perfect keepalive, would be 2)
Code 200 : 19 (95.0 %)
Code 503 : 1 (5.0 %)
Response Header Sizes : count 20 avg 210.05 +/- 48.19 min 0 max 222 sum 4201
Response Body/Total Sizes : count 20 avg 3373 +/- 724 min 217 max 3540 sum 67460
All done 20 calls (plus 0 warmup) 33.025 ms avg, 57.2 qps
```

### SUBIENDO PETICIONES CONCURRENTES A 3
```
[root@instance-1 istio-1.0.5]# kubectl exec -it $FORTIO_POD  -c fortio /usr/local/bin/fortio -- load -c 3 -qps 0 -n 20 -loglevel Warning http://todo-repo:8081/swagger-ui.html
11:00:20 I logger.go:97> Log level is now 3 Warning (was 2 Info)
Fortio 1.0.1 running at 0 queries per second, 2->2 procs, for 20 calls: http://todo-repo:8081/swagger-ui.html
Starting at max qps with 3 thread(s) [gomax 2] for exactly 20 calls (6 per thread + 2)
11:00:20 W http_client.go:604> Parsed non ok code 503 (HTTP/1.1 503)
11:00:20 W http_client.go:604> Parsed non ok code 503 (HTTP/1.1 503)
11:00:20 W http_client.go:604> Parsed non ok code 503 (HTTP/1.1 503)
11:00:20 W http_client.go:604> Parsed non ok code 503 (HTTP/1.1 503)
11:00:20 W http_client.go:604> Parsed non ok code 503 (HTTP/1.1 503)
11:00:20 W http_client.go:604> Parsed non ok code 503 (HTTP/1.1 503)
11:00:20 W http_client.go:604> Parsed non ok code 503 (HTTP/1.1 503)
Ended after 356.14267ms : 20 calls. qps=56.157
Aggregated Function Time : count 20 avg 0.042808971 +/- 0.06291 min 0.001432258 max 0.204666071 sum 0.856179428
# range, mid point, percentile, count
>= 0.00143226 <= 0.002 , 0.00171613 , 5.00, 1
> 0.002 <= 0.003 , 0.0025 , 10.00, 1
> 0.003 <= 0.004 , 0.0035 , 20.00, 2
> 0.004 <= 0.005 , 0.0045 , 25.00, 1
> 0.006 <= 0.007 , 0.0065 , 30.00, 1
> 0.008 <= 0.009 , 0.0085 , 35.00, 1
> 0.016 <= 0.018 , 0.017 , 40.00, 1
> 0.018 <= 0.02 , 0.019 , 45.00, 1
> 0.02 <= 0.025 , 0.0225 , 65.00, 4
> 0.025 <= 0.03 , 0.0275 , 75.00, 2
> 0.035 <= 0.04 , 0.0375 , 85.00, 2
> 0.16 <= 0.18 , 0.17 , 90.00, 1
> 0.18 <= 0.2 , 0.19 , 95.00, 1
> 0.2 <= 0.204666 , 0.202333 , 100.00, 1
# target 50% 0.02125
# target 75% 0.03
# target 90% 0.18
# target 99% 0.203733
# target 99.9% 0.204573
Sockets used: 9 (for perfect keepalive, would be 3)
Code 200 : 13 (65.0 %)
Code 503 : 7 (35.0 %)
Response Header Sizes : count 20 avg 143.8 +/- 105.5 min 0 max 222 sum 2876
Response Body/Total Sizes : count 20 avg 2376.45 +/- 1585 min 217 max 3540 sum 47529
All done 20 calls (plus 0 warmup) 42.809 ms avg, 56.2 qps
```


Aquí se pueden ver las estadísticas en el sidecar de istio:
```
[root@instance-1 istio-1.0.5]# kubectl exec -it $FORTIO_POD  -c istio-proxy  -- sh -c 'curl localhost:15000/stats' | grep todo-repo | grep pending
cluster.outbound|8081||todo-repo.default.svc.cluster.local.upstream_rq_pending_active: 0
cluster.outbound|8081||todo-repo.default.svc.cluster.local.upstream_rq_pending_failure_eject: 0
cluster.outbound|8081||todo-repo.default.svc.cluster.local.upstream_rq_pending_overflow: 31
cluster.outbound|8081||todo-repo.default.svc.cluster.local.upstream_rq_pending_total: 134
```
