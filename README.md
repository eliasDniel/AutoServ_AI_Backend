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

## Actualizar en otra PC (después de un pull)

```bash
git pull
git submodule update --init --recursive
```

Los archivos `.joblib` **no van en Git**. Antes de levantar Docker hay que dejar los modelos en disco.

### 1. Modelo de diagnóstico

Copia el archivo de tu compañera a esta ruta exacta:

```text
ms-ia/modelo/modelo_diagnostico_rf.joblib
```

### 2. Modelo de demanda

Genera el joblib con el script (necesitas Python con `scikit-learn` y `joblib`, por ejemplo el venv del proyecto de IA):

```bash
cd ms-ia
python scripts/entrenar_demanda.py
```

Eso crea:

```text
ms-ia/modelo/modelo_demanda.joblib
```

### 3. Levantar el backend

Desde la raíz de este repositorio, **después de cada pull** (y siempre que cambien los submódulos o el compose):

```bash
docker compose up --build
```

Sin los dos `.joblib` en `ms-ia/modelo/`, la imagen de `ms-ia` puede fallar al construir o arrancar sin predicción/diagnóstico.
