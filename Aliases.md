# Aliases
textotexto

### Archivo `~/.bash_aliases`
```bash
#!/bin/bash
alias activate=". venv/bin/activate"
alias docker-staging="sudo docker compose -f docker-compose.staging.yml"
alias docker-staging-logs="while true; do docker-staging logs -f \$(docker-staging config --services | grep -v redis) ; clear; echo Contenedor abajo, esperando a que reviva...; sleep 5; done"
alias docker-logs="while true; do sudo docker compose logs -ft ; clear; echo Contenedor abajo, esperando a que reviva...; sleep 5; done"
```