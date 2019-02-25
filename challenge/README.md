# Challenge
Esta carpeta contiene los descriptores de despliegue de los microservicios utilizados para la poc

# Deploy services
``` bash
# deploy app
./apps/scripts/deploy
# populate scripts
./apps/scripts/startup
# clean up
./apps/scripts/cleanup
```

## Escenario 1 - http-errors - 404 aleatorio (50%)
``` bash
# deploy app
./apps/scripts/deploy
# deploy scenario 01
./scenarios/01-http-errors/deploy-scenario
# populate scripts
./apps/scripts/startup
# clean up
./apps/scripts/cleanup
```

## Escenario 2 - delay
``` bash
# deploy app
./apps/scripts/deploy
# deploy scenario 02
./scenarios/02-delay/deploy-scenario
# creamos un todo en repo y accedemos por cliente y observamos delay de 7s (inspect, network view)
# populate scripts
./apps/scripts/startup
# clean up
./apps/scripts/cleanup
```