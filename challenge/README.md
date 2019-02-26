# Challenge
Esta carpeta contiene los descriptores de despliegue de los microservicios utilizados para la poc

## Escenario 1 - http-errors - 500 (100%)
``` bash
# deploy app
./apps/scripts/deploy
# deploy scenario 01
./scenarios/01-http-errors/deploy-scenario
# populate scripts (allow time to service become alive)
./apps/scripts/startup
# clean up
./apps/scripts/cleanup
```

## Escenario 2 - delay
``` bash
# deploy scenario 02
./scenarios/02-delay/deploy-scenario
# creamos un todo en repo y accedemos por cliente y observamos delay de 3s 80% (inspect, network view)
# populate scripts
./apps/scripts/startup
# clean up
./apps/scripts/cleanup
```

## Escenario 3 - circuit breaker
``` bash
# deploy scenario 03
#n the DestinationRule settings, you specified maxConnections: 1 and http1MaxPendingRequests: 1. These rules indicate that if you exceed more than one connection and request concurrently, you should see some failures when the istio-proxy opens the circuit for further requests and connections.
./scenarios/03-circuit-breaker/deploy-scenario
# populate scripts
./apps/scripts/startup
# clean up
./apps/scripts/cleanup
```

## Escenario 4 - traffic shifting
``` bash
# deploy release and canary version with some weights (70/30)
./scenarios/04-traffic-shifting/deploy-scenario
# populate scripts (services must be healthy)
./apps/scripts/startup
# deploy release (100% v3)
./scenarios/04-traffic-shifting/deploy-release
# populate scripts (services must be healthy)
./apps/scripts/startup
# clean up
./apps/scripts/cleanup
```
