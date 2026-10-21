# AutoServ AI — Backend

Repositorio padre. Cada microservicio es un submódulo Git:

- `c-gateway` — API HTTP (NestJS)
- `ms-auth` — usuarios, roles y JWT
- `ms-core` — taller e inventario
- `ms-ia` — diagnóstico y predicción (Python)

El frontend está en [AutoServ_AI_Web](https://github.com/eliasDniel/AutoServ_AI_Web).

## Clonar

```bash
git clone --recurse-submodules https://github.com/eliasDniel/AutoServ_AI_Backend.git
```

Si ya lo clonaste sin los submódulos:

```bash
git submodule update --init --recursive
```
