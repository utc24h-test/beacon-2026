# beacon-2026

Anclaje de emisiones del año.

Este es un repositorio de **anclaje**: guarda pruebas criptográficas con fecha, y todo su valor
depende de que **nada de lo que entra se modifique después**.

> 🇬🇧 In English: [`README.md`](README.md)

## Qué hay adentro

Cada turno deja dos archivos firmados:

```
emissions/AAAA/MM/DD/HHMM-commitment.jws   el compromiso, publicado ANTES de que el insumo exista
emissions/AAAA/MM/DD/HHMM-emission.jws     el resultado, publicado después
```

Cuando un turno no se puede completar, un `-failure.jws` ocupa el lugar del `-emission`. Dice por
qué, y revela la semilla para que cualquiera pueda calcular cuál habría sido el resultado.

## Cómo comprobar que esto solo agrega

No hace falta creernos. Preguntá:

```bash
# La rama está protegida — sin credenciales
curl -s https://api.github.com/repos/utc24h-test/beacon-2026/branches/main

# Nada se modificó después de publicado: solo agregados
git log --diff-filter=M --oneline -- emissions/
```

El segundo comando **tiene que no devolver nada**. Si devuelve algo, un archivo se tocó después de
firmado.

## Clonar en Windows

El `.gitattributes` de la raíz ya se ocupa. No cambies `core.autocrlf` y no conviertas los archivos:
los `.jws` se verifican **byte por byte**, y un solo final de línea convertido rompe la firma.

---

Creado por `provision/`, no a mano.
